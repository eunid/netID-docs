# Browser-based API (Client-Side Integration)

Description of the browser-based integration by the CMP.

## API flow examples

### Obtaining a privacy status

The following sequence illustrates the API calls initiated by a netID Partners CMP to establish a privacy status for an already authenticated user.

![Browser based API](../diagrams/out/seq_cmp_webapi.svg)

## Read APIs

### netID Identifier

If the `origin` is eligible, a publisher (TAPP) can access the user’s identifier (`tpid`) via the following interface:

#### Request

```http
GET https://einwilligungsspeicher.netid.de/netid-subject-identifiers?q.tapp_id.eq=<TAPP_ID> HTTP/1.1
Accept: application/vnd.netid.permission-center.netid-tpid-subject-v1+json
Cookie: tpid_sec=<JWT_TOKEN>
Origin: <ORIGIN>
```

#### Response

```http
HTTP/1.1 200 OK
Content-Type: application/vnd.netid.permission-center.netid-tpid-subject-v1+json
Access-Control-Allow-Origin: <ORIGIN>
Access-Control-Allow-Credentials: true

{
  "tpid": "<TPID>"
  "status_code": "OK"
}
```

#### Response properties 

`tpid` - users netID identifier. Only returned if consent "identification" is given, the `tpid` is known (i.e. user is already authenticated on the device) and status "OK". Otherwise null.

| status_code | meaning | tpid |
| ----------- | ----------- | ----------- |
| OK | Call successful | x |
| NO_TPID | No tpid_sec cookie in request available. | - |
| NO_TAPP_ID | Mandatory parameter `tapp_id` is missing. | - |
| TOKEN_ERROR | Token (JWT) in the cookie is expired or invalid. | - |
| TAPP_ERROR | TAPP `tapp_id` is invalid. | - |
| TPID_NOT_FOUND | Permissions for `tpid` not found. | - |
| TAPP_NOT_ALLOWED | TAPP `tapp_id` is not allowed. | - |
| TPID_EXISTENCE_ERROR | `tpid` ("identification") does not exist any more. | - |
| ID_CONSENT_REQUIRED | Consent for passing the `tpid` ("identification") was not given or was revoked by the user. | - |
<br>

#### Response behavior

| HTTP status code | meaning |
| ----------- | ----------- |
| 200 OK | - `tpid` of the netID user returned, if consent is given. |
| 400 BAD REQUEST | - Parameters are missing or invalid. |
| 403 FORBIDDEN | - Consent for passing the `tpid` ("identification") was not given or was revoked by the user. |
| 404 NOT FOUND | - Permissions for `tpid` not found. |
| 410 GONE | - `tpid` (account) does not exist any more. |
<br>
### Read privacy status

#### Request

```http
GET https://einwilligungsspeicher.netid.de/netid-permissions? HTTP/1.1
    q.tapp_id.eq=<TAPP_ID>
Accept: application/vnd.netid.permission-center.netid-permission-status-v1+json
Cookie: tpid_sec=<JWT_TOKEN>
Origin: <ORIGIN>
```

#### Response

```http
HTTP/1.1 200 OK
Content-Type: application/vnd.netid.permissions.iab-permissions-read-v1+json
Access-Control-Allow-Origin: <ORIGIN>
Access-Control-Allow-Credentials: true

{
  "tpid": "<TPID>"|null,
  "tc": "<TCSTRING>"|null,
  "datashare": "VALID"|"INVALID"|null,
  "status_code": "OK"
}
```

#### Response Properties 

| item | description |
|---|---|
| tpid | Users netID identifier (`tpid`). Only returned if consent "identification" is given, the `tpid` is known (i.e. user is already authenticated on the device) and status "OK". Otherwise null. |
| tc | TC string stored for this `tpid` for this respective netID Partner (TAPP). Only with status "OK". Otherwise null. |
| datashare | If consent "datashare" is given, value is 'VALID'. If consent "datashare" is revoked, value is 'INVALID'. Otherwise null. |
<br>

| status_code | meaning | tc | tpid |
| ----------- | ----------- | ----------- | ----------- |
| OK | Call successful <br> - In case the consent for passing the `tpid` is missing ("identification") `null` is returned, otherwise the `tpid`. Stored TC String is returned (might be `null`). In case the consent for "datashare" is missing, `null` is returned. | x (-)| x (-) |
| NO_TPID | No tpid_sec cookie in request available. | - | - |
| NO_TAPP_ID | Mandatory parameter `tapp_id` is missing. | - | - |
| TOKEN_ERROR | Token (JWT) in the cookie is expired or invalid. | - | - |
| TAPP_ERROR | `tapp_id` is invalid. | - | - |
| PERMISSIONS_NOT_FOUND | Permissions for `tpid` not found. | - | - |
| TAPP_NOT_ALLOWED | TAPP `tapp_id` is not allowed. | - | - |
| TPID_EXISTENCE_ERROR | `tpid` ("identification") does not exist any more. | - | - |
| ID_CONSENT_REQUIRED | Consent for passing the `tpid` ("identification") was revoked or declined by the user. | x | - |
<br>
#### Response behavior

| HTTP status code | meaning |
| ----------- | ----------- |
| 200 OK | - `tpid` of the netID user is returned, if consent of "identification" is given. In case the consent for passing the `tpid` is missing ("identification") `null` is returned. <br> - Stored TC String is returned (might be `null`). <br> - In case the consent for "datashare" is missing, `null` is returned. |
| 400 BAD REQUEST | - Missing authentication/no tpid_sec cookie available. <br> - Provided token (JWT) in the tpid_sec cookie is expired or invalid. |
| 403 FORBIDDEN | - Missing parameters (`tapp_id`, `origin`). <br> - requesting TAPP isn't active. |
| 404 NOT FOUND | - Permissions for `tpid` not found. |
| 410 GONE | `tpid` (account) does not exist any more. |
<br>
## Write API

### Write privacy status

#### Request

```http
POST https://einwilligen.netid.de/netid-permissions?q.tapp_id.eq=<TAPP_ID> HTTP/1.1
Content-Type: application/vnd.netid.permission-center.netid-permissions-v1+json
Accept: application/vnd.netid.permission-center.netid-tpid-subject-status-v1+json
Cookie: tpid_sec=<JWT_TOKEN>
Origin: <ORIGIN>

{
  "identification": "true|false",
  "tc": "<TC string>"
}
```

#### Response

```http
HTTP/1.1 201 Created
Location: https://einwilligungsspeicher.netid.de/netid-permissions?q.tapp_id.eq=<TAPP_ID>
Access-Control-Allow-Origin: <ORIGIN>
Access-Control-Allow-Credentials: true

{
  "tpid": "<TPID>|null",
  "status_code": "OK"
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

`tpid` - Users netID identifier. Only passed, if consent "identification" is given, the `tpid` is known and status is "OK". Otherwise null.

| status_code | meaning |
| ----------- | ----------- |
| OK | Call successful |
| NO_TPID | No tpid_sec cookie in request available. |
| NO_TAPP_ID | Mandatory parameter `tapp_id` is missing. |
| TAPP_NOT_ALLOWED | TAPP `tapp_id` is not allowed. |
| TPID_EXISTENCE_ERROR | `tpid` ("identification") does not exist any more. |
| ID_CONSENT_REQUIRED | Consent for passing the `tpid` ("identification") was revoked or declined by the user. |
| NO_REQUEST_BODY | Required request body is missing. | 
| JSON_PARSE_ERROR | Invalid JSON body, parse error. | 
| NO_PERMISSIONS | Parameters are missing. At least one permission must be set. | 
| PERMISSION_PARAMETERS_ERROR | Syntactic or semantic error in a permission. Name ("identification", "tc") or value unknown.  | 
<br>
#### Response behavior

| HTTP status code | meaning |
| ----------- | ----------- |
| 201 CREATED | Call successful |
| 400 BAD REQUEST | - Missing authentication/no tpid_sec cookie available. <br> - Provided token (JWT) in the tpid_sec cookie is expired or invalid. |
| 403 FORBIDDEN | - Missing parameters (`tapp_id`, `origin`). <br> - Requesting TAPP isn't active. |
| 410 GONE | `tpid` (account) does not exist any more. |
