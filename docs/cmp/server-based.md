# Server-based API (backend integration)

Description of the backend integration of the netID Permission Center by the CMP (integration from the server side / backend of the CMP if available).

A netID Partner (TAPP) that sends a user through the Single Sign-On Flow can requests an access token (`token`) provided after the successful login, based on which a user can be authenticated at the netID Permission Center to enable read/write access for that specific users privacy status.

!!! info  ""
    The server-based requests are secured via the access token.
    Calls of this type are blocked from the browser environments for security reasons (no Origin header is allowed!)

## Read APIs

### Read privacy status

#### Request with Sync-ID in response

```http
GET https://einwilligungsspeicher.netid.de/netid-user-status HTTP/1.1
Accept: application/vnd.netid.permission-center.netid-user-status-audit-v1+json
Authorization: Bearer <Access Token>
```

#### Response with Sync-ID

```http
HTTP/1.1 200 OK
Content-Type: application/vnd.netid.permission-center.netid-user-status-audit-v1+json

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

> **Note**: If the Sync-ID is not needed, please use accept header with the following media type: <br>
    ```
    Application/vnd.netid.permission-center.netid-user-status-v1+json
    ```

#### Response Properties

| item | description |
|---|---|
| tpid | Users netID identifier (`tpid`). Only returned if consent "idconsent" is VALID, the `tpid` is known (i.e. user is already authenticated on the device) and status "PERMISSIONS_FOUND". Otherwise null. |
| sync_id | Parnter specific sync-id of the netID user. Only returned if any "netid_privacy_settings" are available. |
| IDCONSENT | If consent "IDCONSENT" is given, value is 'VALID' and users netID identifier (`tpid`) is returned. If consent "IDCONSENT" is revoked, value is 'INVALID'. Otherwise null. |
| DATASHARE | If consent "DATASHARE" is given, value is 'VALID'. If consent "datashare" is revoked, value is 'INVALID'. Otherwise null. |
| IAB_TC_STRING | TC string stored for this `tpid` for this respective netID Partner (TAPP). |

#### Response behavior

| HTTP status_code | status_code | meaning |
| ----------- | ----------- | ----------- |
| 200 OK | PERMISSIONS_FOUND | Call successful. Permissions of the netID user are returned. |
| 200 OK | PERMISSIONS_NOT_FOUND | Call sucessful. netID user is identified. User has no permissions. No subject_identifier is returned.  |
| 400 BAD REQUEST | NO_TOKEN | No bearer token in request available. User could not be identified as netID user. |
| 400 BAD REQUEST | TOKEN_ERROR | Token in bearer token is expired or invalid. |
| 403 FORBIDDEN | TAPP_NOT_ALLOWED | TAPP `tapp_id` is not allowed. |
| 410 GONE | TPID_EXISTENCE_ERROR | Account does not exist anymore. |

## Write APIs

### Write privacy status

#### Request with Sync-ID in response

```http
POST https://einwilligen.netid.de/netid-permissions HTTP/1.1
Content-Type: application/vnd.netid.permission-center.netid-permissions-v2+json
Accept: application/vnd.netid.permission-center.netid-subject-status-audit-v1+json 
Authorization: Bearer <Access Token>
{
  "idconsent": "VALID",
  "iab_tc_string": "CO3P7LWO3P7LWCnAAAENAwCgAAAAAAAAAAAAAAAAAAAA.YAAAAAAAAAA"
}
```

#### Response with Sync-ID

```http
HTTP/1.1 201 Created
Location: https://einwilligungsspeicher.netid.de/netid-permissions

{
  "subject_identifiers": {
     "tpid": "6dG7h0ziSu_tCjL75i5tHURKnYNgazllX1JBOpYLu4U",
     "sync_id": "examplesyncid"
  }
}
```

> **Note**: If the Sync-ID is not needed, please use accept header with the following media type: <br>
    ```
    Application/vnd.netid.permission-center.netid-user-status-v1+json
    ```

#### Request properties

|item|description|
|---|---|
| IDCONSENT | Is indicating the status of the consent "IDCONSENT". VALID = Consent is given. INVALID = Consent is revoked. |
| IAB_TC_STRING | TC String which should be stored/updated for this netID user for this respective netID partner (TAPP). |

#### Response properties

| item | description |
|---|---|
| tpid | Users netID identifier (`tpid`). Only returned if consent "idconsent" is VALID, the `tpid` is known (i.e. user is already authenticated on the device) and status "PERMISSIONS_FOUND". Otherwise null. |
| sync_id | Parnter specific sync-id of the netID user. Only returned if any "netid_privacy_settings" are available. |

#### Response behavior

| HTTP status code | status_code | meaning |
| ----------- | ----------- | ----------- |
| 201 CREATED |  | Call successful |
| 400 BAD REQUEST | NO_TOKEN | No bearer token in request available. |
| 400 BAD REQUEST | TOKEN_ERROR | Token in bearer token is expired or invalid. |
| 400 BAD REQUEST | NO_PERMISSIONS | Parameters are missing. At least one permission must be set. |
| 400 BAD REQUEST | JSON_PARSE_ERROR | Invalid JSON body, parse error. |
| 400 BAD REQUEST | NO_REQUEST_BODY | Required request body is missing. |
| 403 FORBIDDEN | | Missing parameters in request/Requesting TAPP isn't active. |
| 410 GONE | TPID_EXISTENCE_ERROR | Account does not exist anymore. |

