# Server-based API (backend integration)

Description of the backend integration of the netID Permission Center by the CMP (integration from the server side / backend of the CMP if available).

A netID Partner (TAPP) that sends a user through the Single Sign-On Flow can requests an access token (`token`) provided after the successful login, based on which a user can be authenticated at the netID Permission Center to enable read/write access for that specific users privacy status.

!!! info  ""
    The server-based requests are secured via the access token.
    Calls of this type are blocked from the browser environments for security reasons (no Origin header is allowed!)

## Read APIs

### netID Identifier

A CMP/netID Partner can retrieve the user's netID Identifier via the following interface:

#### Request

```http
GET https://einwilligungsspeicher.netid.de/netid-subject-identifiers HTTP/1.1
Accept: application/vnd.netid.permission-center.netid-tpid-subject-v1+json
Authorization: Bearer <Access Token>
```

#### Response

```http
HTTP/1.1 200 OK
Content-Type: application/vnd.netid.permission-center.netid-tpid-subject-v1+json

{
  "tpid": "<TPID>",
  "status_code": "OK"
}
```

#### Response properties

`tpid` - Users netID identifier. Only returned if consent "identification" is given, the `tpid` is known (i.e. user is already authenticated on the device) and status "OK". Otherwise null.

| status_code | meaning | tpid |
| ----------- | ----------- | ----------- |
| OK | Call successful | x |
| NO_TPID | No `tpid` in request available. | - |
| TOKEN_ERROR | Access token was expired or invalid. | - |
| NO_TOKEN | No access token was passed. | - |
| TPID_NOT_FOUND | Permissions for `tpid` not found. | - |
| TAPP_NOT_ALLOWED | TAPP `tapp_id` is not allowed. | - |
| TPID_EXISTENCE_ERROR | Account does not exist anymore. | - |
| ID_CONSENT_REQUIRED | Consent for passing the `tpid` ("identification") was not given or was revoked by the user. | -

#### Response behavior

| HTTP status code | meaning |
| ----------- | ----------- |
| 200 OK | `tpid` of the netID user returned. |
| 400 BAD REQUEST | Missing access token, or access token expired / invalid. |
| 403 FORBIDDEN | Requesting TAPP isn't active or consent for "identification" isn't granted. |
| 404 NOT FOUND | `tpid` in access token does not exist. |
| 410 GONE | Account does not exist anymore. |

### Read privacy status

#### Request

```http
GET https://einwilligungsspeicher.netid.de/netid-permissions HTTP/1.1
Accept: application/vnd.netid.permission-center.netid-permission-status-v1+json
Authorization: Bearer <Access Token>
```

#### Response

```http
HTTP/1.1 200 OK
Content-Type: application/vnd.netid.permission-center.netid-permission-status-v1+json

{
  "tpid": "<TPID>"|null,
  "tc": "<TCSTRING>"|null,
  "datashare": "VALID"|"INVALID"|null,
  "status_code": "OK"
}
```
  
#### Response properties

| item |description|
|---|---|
| tpid | Users identifier (`tpid`). Only returned if consent "identification" is given, the `tpid` is known (i.e. user is already authenticated on the device) and status "OK". Otherwise null. |
| tc | TC string stored for this `tpid` for this respective netID partner (TAPP). Only with status "OK". Otherwise null. |
| datashare | If consent "datashare" is given, value is 'VALID'. If consent "datashare" is revoked, value is 'INVALID'. Otherwise null. |
<br>

| status_code | meaning | tpid |
| ----------- | ----------- | ----------- |
| OK | Call successful | x |
| NO_TPID | No `tpid` in request available. | - |
| TOKEN_ERROR | Access token was expired or invalid. | - |
| NO_TOKEN | No access token was passed. | - |
| PERMISSIONS_NOT_FOUND | Permissions for `tpid` not found. | - |
| TAPP_NOT_ALLOWED | TAPP `tapp_id` is not allowed. | - |
| TPID_EXISTENCE_ERROR | Account does not exist anymore. | - |
| ID_CONSENT_REQUIRED | Consent for passing the `tpid` ("identification") was not given or was revoked by the user | - |

#### Response behavior

| HTTP status code | meaning |
| ----------- | ----------- |
| 200 OK | Call successful |
| 400 BAD REQUEST | Missing parameter. |
| 403 FORBIDDEN | Requesting TAPP isn't active.  |
| 404 NOT FOUND | Permissions for `tpid` not found. |
| 410 GONE | Account does not exist anymore. |

## Write APIs

### Write privacy status

#### Request

```http
POST https://einwilligen.netid.de/netid-permissions HTTP/1.1
Content-Type: application/vnd.netid.permission-center.netid-permissions-v1+json
Accept: application/vnd.netid.permission-center.netid-tpid-subject-status-v1+json
Authorization: Bearer <Access Token>
{
  "identification": true|false,
  "tc": "<TC string>"
}
```

#### Response

```http
HTTP/1.1 201 Created

{
  "tpid": "<TPID>|null",
  "status": "OK"
}
```

!!! info "Remarks"
    - There must be at least one permission ("identification", "tc"). Permissions are optional. If a permission should not be written, the JSON property is missing. 
    - If consent for "identification" has been given by the user, this must be signaled by passing "identification: true". For the avoidance of doubt, this of course requires the prior collection of this consent by the CMP.
    - If only the TC string is to be updated and the consent for "identification" already exists, only the "tc" attribute can be passed. All two can also be written at the same time.
    - In case of revocation the consent for "identification", "identification: false" is passed.
<br>
#### Request properties

|item|description|
|---|---|
| identification | Boolean flag, indicating the status of the consent "identification". <br> *true* = Consent is given <br> *false* = consent is not given or revoked |
| tc | TC String which should be stored/updated for this user in relation to the netID Partner (TCF 2.0) |
<br>

#### Response properties

`tpid` - Users netID Identifier. Only present if consent "identification" is given, the `tpid` is known and status is "OK". Otherwise null.

| status_code | meaning |
| ----------- | ----------- |
| OK | Call successful 
| NO_TPID | No `tpid` in request available. |
| NO_TAPP_ID | Mandatory parameter `tapp_id` is missing. |
| TAPP_NOT_ALLOWED | TAPP `tapp_id` is not allowed. |
| TPID_EXISTENCE_ERROR | Account does not exist anymore. |
| ID_CONSENT_REQUIRED | Consent for passing the `tpid` ("identification") was revoked or declined by the user. |
| NO_REQUEST_BODY | Required request body is missing. | 
| JSON_PARSE_ERROR | Invalid JSON body, parse error. | 
| NO_PERMISSIONS | Parameters are missing. At least one permission must be set. | 
| PERMISSION_PARAMETERS_ERROR | Syntactic or semantic error in a permission. Name ("identification", "tc") or value unknown.  | 

#### Response behavior

| HTTP status code | meaning |
| ----------- | ----------- |
| 201 CREATED | Call successful |
| 400 BAD REQUEST | - Missing authentication.  <br> - Provided token access cookie is expired or invalid. No access token passed. |
| 403 FORBIDDEN | - Missing parameters (`tapp_id`, `origin`) <br> - Requesting TAPP isn't active. |
| 410 GONE | Account does not exist anymore. |
