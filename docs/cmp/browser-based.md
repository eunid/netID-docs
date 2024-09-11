# Browser-based API 

Description of the browser-based integration.

## API flow examples

### Retrieving a users privacy status

The following sequence illustrates the API calls initiated by a netID Partners CMP to establish a privacy status for an already authenticated user.

![Browser based API](../diagrams/out/seq_cmp_webapi.svg)

## Read APIs

The list of identifiers returned is controlled via the query parameter q.identifier:
- Only identifiers requested with parameter q.identifier will be returned
- `sync_id` is only returned, if permissions for the user are found
- `tpid` and `etpid` are only returned if the user has a valid IDConsent permission. Otherwise they are null
- [`etpid`](#encrypted-tpid-etpid) is the users encrypted identifier (encrypted `tpid`, netID adtechpass). Key for encryption of the `etpid` is changing every 24 hrs 

### Read privacy status

#### Request

```http
GET https://einwilligungsspeicher.netid.de/netid-user-status?q.tapp_id.eq=<TAPP_ID>&q.identifier.in=TPID,SYNC_ID,ETPID HTTP/1.1
Accept: application/vnd.netid.permission-center.netid-user-status-v2+json
Cookie: tpid_sec=<JWT_TOKEN>
Origin: <ORIGIN>
```

#### Response

```http
HTTP/1.1 200 OK
Content-Type: application/vnd.netid.permission-center.netid-user-status-v2+json
Access-Control-Allow-Origin: <ORIGIN>
Access-Control-Allow-Credentials: true

{
  "status_code": "PERMISSIONS_FOUND",
  "subject_identifiers": {
    "tpid": "<TPID>"|null,
    "sync_id": "<SYNC_ID>"|null,
    "etpid": "<ETPID>"|null
  },
  "netid_privacy_settings": {
    "idconsent": {
      "changed_at": "<TIMESTAMP>",
      "status": "VALID"|"INVALID"
    },
    "iab_tcstring": {
      "changed_at": "<TIMESTAMP>", 
      "value": "<TCSTRING>"
    }
  }
}

```

#### Response Properties

| item | description |
|---|---|
| tpid | Users netID identifier (`tpid`). Only returned if requested (q.identifier.in=TPID), consent "idconsent" is VALID, the `tpid` is known (i.e. user is already authenticated on the device) and status "PERMISSIONS_FOUND". Otherwise null. |
| sync_id | Partner specific Sync-ID of the netID user. Only returned if requested (q.identifier.in=SYNC_ID), any "netid_privacy_settings" are present in the permission center at the time of the API call. Might be null in case of a server error. |
| etpid | Users encrypted identifier (encrypted `tpid`, netID adtechpass). Only returned if requested (q.identifier.in=ETPID), consent "idconsent" is VALID, the `tpid` is known (i.e. user is already authenticated on the device) and status "PERMISSIONS_FOUND". Otherwise null. |
| idconsent | If consent "idconsent" is given, value is 'VALID' and users netID identifier (`tpid`) is returned. If consent "IDCONSENT" is revoked, value is 'INVALID'. Otherwise property won't be returned. |
| iab_tcstring | TC string stored for this `tpid` for this respective netID Partner (TAPP). |

#### Response behavior

| HTTP status_code | status_code | meaning |
| ----------- | ----------- | ----------- |
| 200 OK | PERMISSIONS_FOUND | Call successful. Permissions found and returned. |
| 200 OK | PERMISSIONS_NOT_FOUND | Call successful. netID user is authenticated. No permission (privacy status) found for the given `tapp_id`. All requested identifiers are set to null. netID privacy settings are empty. |
| 400 BAD REQUEST | NO_TPID | No tpid_sec cookie in request available. No authenticated netID user. |
| 400 BAD REQUEST | NO_TAPP_ID | No `tapp_id` in request available. |
| 400 BAD REQUEST | TOKEN_ERROR | Token in cookie is expired or invalid. |
| 400 BAD REQUEST | TAPP_ERROR | `tapp_id` is invalid. |
| 403 FORBIDDEN | TAPP_NOT_ALLOWED | `tapp_id` is not allowed, e.g. origin not eligible. |
| 410 GONE | TPID_EXISTENCE_ERROR | Account does not exist anymore. |

## Write API

The list of identifiers returned is controlled via the query parameter q.identifier:
- Only identifiers requested with parameter q.identifier will be returned
- `sync_id` is only returned, if permissions for the user are found
- `tpid` and `etpid` are only returned if the user has a valid IDConsent permission. Otherwise they are null
- [`etpid`](#encrypted-tpid-etpid) is the users encrypted identifier (encrypted `tpid`, netID adtechpass). Key for encryption of the `etpid` is changing every 24 hrs 

### Write privacy status

#### Request

```http
POST https://einwilligen.netid.de/netid-permissions?q.tapp_id.eq=<TAPP_ID>&q.identifier.in=TPID,SYNC_ID,ETPID  HTTP/1.1
Content-Type: application/vnd.netid.permission-center.netid-permissions-v2+json
Accept: application/vnd.netid.permission-center.netid-subject-status-v2+json
Cookie: tpid_sec=<JWT_TOKEN>
Origin: <ORIGIN>

{
  "idconsent": "VALID"|"INVALID",
  "iab_tc_string": "<TCSTRING>"
}
```

#### Response

```http
HTTP/1.1 201 Created
Access-Control-Allow-Origin: <ORIGIN>
Access-Control-Allow-Credentials: true
 
{
  "subject_identifiers": {
     "tpid": "<TPID>"|null,
     "sync_id": "<SYNC_ID>"|null,
     "etpid": "<ETPID>|null
  }
}

```

#### Request properties

|item|description|
|---|---|
| idconsent | Consent "idconsent" to store for this `tpid` for this respective netID Partner. VALID = Consent is given. INVALID = Consent is revoked. Optional. |
| iab_tc_string | TC String which should be stored/updated for this netID user for this respective netID partner (TAPP). Optional. |
_minProperties: 1_

#### Response properties

| item | description |
|---|---|
| tpid | Users netID identifier (`tpid`). Only returned if requested (q.identifier.in=TPID), consent "idconsent" is VALID, the `tpid` is known (i.e. user is already authenticated on the device) and status "PERMISSIONS_FOUND". Otherwise null. |
| sync_id | Partner specific sync-id of the netID user. Only returned if requested, any "netid privacy settings" are present in the permission center at the time of the API call. |
| etpid | Users encrypted identifier (encrypted `tpid`, netID adtechpass). Only returned if requested, consent "idconsent" is VALID, the `tpid`is known (i.e. user is already authenticated on the device) and status "PERMISSIONS_FOUND". Otherwise null.  |

#### Response behavior

| HTTP status code | status_code | meaning |
| ----------- | ----------- | ----------- |
| 201 CREATED |  | Call successful |
| 400 BAD REQUEST | NO_TPID | No tpid_sec cookie in request available. |
| 400 BAD REQUEST | TOKEN_ERROR | Token in cookie is expired or invalid. |
| 400 BAD REQUEST | NO_PERMISSIONS | Parameters are missing. At least one permission must be set. |
| 400 BAD REQUEST | JSON_PARSE_ERROR | Invalid JSON body, parse error. |
| 400 BAD REQUEST | NO_REQUEST_BODY | Required request body is missing. |
| 400 BAD REQUEST | PERMISSION_PARAMETERS_ERROR | Syntactic or semantic error in a permission (e.g. invalid TC String)  |
| 403 FORBIDDEN | TAPP_NOT_ALLOWED | Missing parameters in request/Requesting TAPP isn't active/Origin not eligible |
| 410 GONE | TPID_EXISTENCE_ERROR | Account does not exist anymore. |
_On a CORS error 403 is returned._

## Encrypted tpid (`etpid`)
The netID identifier (`tpid`) is used as the base for he encrypted tpid (`etpid`), which is valid for a maximum of 24 hours (nonce). netID partners who work with the `etpid` must therefore request a new `etpid` at least every 24 hours. By introducing encryption, netID partners have the ability to transmit a volatile and encrypted ID in the bidstream for marketing purposes to prevent data leakage. In the first step, the `etpid` can only be used sensibly in combination with Utiq, as the cooperation between Utiq and netID can ensure that the `etpid` is passed into the bidstream in a standardized way via the Utiq PreBid Adapter. Adtech players can only decrypt the `etpid` and use it as a stable online identifier if they have implemented Utiq's decryption API. In order to be able to use the `etpid` via Utiq PreBid Adapter for programmatic marketing, the following requirements must be met:
- Utiq PreBid Adapter must be implemented 
- `etpid` must be stored in the following way in the local storage: 
  - “localStorage.setItem(”netid_utiq_adtechpass”, ID-VALUE);”

