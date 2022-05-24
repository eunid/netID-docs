# Browser-based API 

Description of the browser-based integration.

## API flow examples

### Retrieving a users privacy status

The following sequence illustrates the API calls initiated by a netID Partners CMP to establish a privacy status for an already authenticated user.

![Browser based API](../diagrams/out/seq_cmp_webapi.svg)

## Read APIs

!!! info  "Sync-ID"
    In case the [Sync-ID](../#custom-privacy-settings) should be included in the API responses (if preconditions are met), the APIs must be called with the respective accept header.

     Without Sync-ID: ``application/vnd.netid.permission-center.netid-user-status-v1+json`` <br>
     With Sync-ID: ``application/vnd.netid.permission-center.netid-user-status-audit-v1+json``

### Read privacy status

#### Request (incl. Sync-ID)

```http
GET https://einwilligungsspeicher.netid.de/netid-user-status?q.tapp_id.eq=<TAPP_ID> HTTP/1.1
Accept: application/vnd.netid.permission-center.netid-user-status-audit-v1+json
Cookie: tpid_sec=<JWT_TOKEN>
Origin: <ORIGIN>
```

#### Response (incl. Sync-ID)

```http
HTTP/1.1 200 OK
Content-Type: application/vnd.netid.permission-center.netid-user-status-audit-v1+json
Access-Control-Allow-Origin: <ORIGIN>
Access-Control-Allow-Credentials: true

{
  "status_code": "PERMISSIONS_FOUND",
  "subject_identifiers": {
    "tpid": "<TPID>"|null,
    "sync_id": "<SYNC_ID>"
  },
  "netid_privacy_settings": [
    {
      "type": "IDCONSENT",
      "status": "VALID"|"INVALID",
      "changed_at": "<TIMESTAMP>"
    },
    {
      "type": "DATASHARE",
      "status": "VALID"|"INVALID",
      "changed_at": "<TIMESTAMP>" 
    },
    {
      "type": "IAB_TC_STRING",
      "value": "<TCSTRING>",
      "changed_at": "<TIMESTAMP>"
    }
  ]
}

```

#### Response Properties

| item | description |
|---|---|
| tpid | Users netID identifier (`tpid`). Only returned if consent "idconsent" is VALID, the `tpid` is known (i.e. user is already authenticated on the device) and status "PERMISSIONS_FOUND". Otherwise null. |
| sync_id | Partner specific Sync-ID of the netID user. Only returned if any "netid_privacy_settings" are present in the permission center at the time of the API call|
| IDCONSENT | If consent "IDCONSENT" is given, value is 'VALID' and users netID identifier (`tpid`) is returned. If consent "IDCONSENT" is revoked, value is 'INVALID'. Otherwise null. |
| IAB_TC_STRING | TC string stored for this `tpid` for this respective netID Partner (TAPP). |

#### Response behavior

| HTTP status_code | status_code | meaning |
| ----------- | ----------- | ----------- |
| 200 OK | PERMISSIONS_FOUND | Call successful. Permissions found and returned. |
| 200 OK | PERMISSIONS_NOT_FOUND | Call successful. netID user is authenticated. No permission (privacy status) found for the given `tapp_id`. No subject_identifiers returned.  |
| 400 BAD REQUEST | NO_TPID | No tpid_sec cookie in request available. No authenticated netID user. |
| 400 BAD REQUEST | TOKEN_ERROR | Token in cookie is expired or invalid. |
| 403 FORBIDDEN | TAPP_NOT_ALLOWED | TAPP `tapp_id` is not allowed, e.g. origin not eligible. |
| 410 GONE | TPID_EXISTENCE_ERROR | Account does not exist anymore. |

## Write API

!!! info  "Synch-ID"
    In case the [Synch-ID](../#custom-privacy-settings) should be included in the API responses (if preconditions are met), the APIs must be called with the respective accept header.

     Without Synch-ID: ``application/vnd.netid.permission-center.netid-user-status-v1+json`` <br>
     With Synch-ID: ``application/vnd.netid.permission-center.netid-user-status-audit-v1+json``

### Write privacy status

#### Request (incl. Sync-ID)

```http
POST https://einwilligen.netid.de/netid-permissions?q.tapp_id.eq=<TAPP_ID> HTTP/1.1
Accept: application/vnd.netid.permission-center.netid-subject-status-audit-v1+json
Cookie: tpid_sec=<JWT_TOKEN>
Origin: <ORIGIN>

{
  "idconsent": "VALID"|"INVALID",
  "iab_tc_string": "<TCSTRING>"
}
```

#### Response (incl. Sync-ID)

```http
HTTP/1.1 201 Created
Location: https://einwilligungsspeicher.netid.de/netid-user-status?q.tapp_id.eq=<TAPP_ID>
Access-Control-Allow-Origin: <ORIGIN>
Access-Control-Allow-Credentials: true
 
{
  "subject_identifiers": {
     "tpid": "<TPID>"|null,
     "sync_id": "<SYNC_ID>"
  }
}

```

#### Request properties

|item|description|
|---|---|
| IDCONSENT | Is indicating the status of the consent "IDCONSENT". VALID = Consent is given. INVALID = Consent is revoked|
| IAB_TC_STRING | TC String which should be stored/updated for this netID user for this respective netID partner (TAPP)|

#### Response properties

| item | description |
|---|---|
| tpid | Users netID identifier (`tpid`). Only returned if consent "idconsent" is VALID, the `tpid` is known (i.e. user is already authenticated on the device) and status "PERMISSIONS_FOUND". Otherwise null. |
| sync_id | Partner specific sync-id of the netID user. |

#### Response behavior

| HTTP status code | status_code | meaning |
| ----------- | ----------- | ----------- |
| 201 CREATED |  | Call successful |
| 400 BAD REQUEST | NO_TPID | No tpid_sec cookie in request available. |
| 400 BAD REQUEST | TOKEN_ERROR | Token in cookie is expired or invalid. |
| 400 BAD REQUEST | NO_PERMISSIONS | Parameters are missing. At least one permission must be set. |
| 400 BAD REQUEST | JSON_PARSE_ERROR | Invalid JSON body, parse error. |
| 400 BAD REQUEST | NO_REQUEST_BODY | Required request body is missing. |
| 403 FORBIDDEN | TAPP_NOT_ALLOWED | Missing parameters in request/Requesting TAPP isn't active/Origin not eligible |
| 410 GONE | TPID_EXISTENCE_ERROR | Account does not exist anymore. |
