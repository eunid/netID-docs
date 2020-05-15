# Server-based API (backend integration)

Description of the backend integration of the netID Permission Center by the CMP (integration from the server side / backend of the CMP if available).

A netID Partner (TAPP) that sends a user through the Single Sign-On Flow and requests the authentication token (`token`) after the successful login, based on which a user can be authenticated at the netID Permission Center to enable read/write access for that specific users privacy status.



!!! info  ""
    The server-based requests are secured via the authentication token.
    Calls of this type are blocked from the browser environments for security reasons (no Origin header is allowed!)

## Read APIs

### netID Identifier

A CMP can retrieve the user's netID identifier (TPID) via the following interface:

``` shell
GET https://einwilligungsspeicher.netid.de/identification/tpid?token=<TOKEN>
Accept: application/vnd.netid.identification.tpid-read-v1+json
```

``` shell
200 OK
Content-Type: application/vnd.netid.identification.tpid-read-v1+json

{
  "tpid": "<TPID>|null"
  "status": "OK|NO_TOKEN|TOKEN_ERROR|CONSENT_REQUIRED"
}
```

**JSON Properties**

| |Description|
|---|---|
| tpid | Users netID identifier (`tpid`). Only if consent "identification" is given, the `tpid` is passed and status "OK". Otherwise null. |

| status | meaning | tpid |
| ----------- | ----------- | ----------- |
| OK | call successful | x |
| NO_TOKEN | No authentication token was passed. | - |
| TOKEN_ERROR | Authentication token is expired or invalid. | - |
| CONSENT_REQUIRED | Consent for passing on the TPID is missing ("identification"). | - |

**Response behaviour**

| status code | meaning |
| ----------- | ----------- |
| 200 OK | - TPID of the netID user is delivered | 
| 400 BAD REQUEST | - missing authentication token <br> - authentication token is expired or invalid | 
| 403 FORBIDDEN | - requesting TAPP isn't active <br> - consent for 'identification' isn't granted |
| 404 NOT FOUND | - TPID in authentication token does not exist |
| 410 GONE | - TPID in authentication token isn't active |

### Read consent status (privacy status)

``` shell
GET https://einwilligungsspeicher.netid.de/permissions/iab-permissions?token=<TOKEN>
Accept: application/vnd.netid.permissions.iab-permission-read-v1+json
```

``` shell
200 OK
Content-Type: application/vnd.netid.permissions.iab-permission-read-v1+json

{
  "tpid": "<TPID>|null",
  "tc": "<TC string>|null",
  "status": "OK|NO_TOKEN|TOKEN_ERROR|CONSENT_REQUIRED"
}
```

**JSON Properties**

| |Description|
|---|---|
| tpid | Users netID identifier (`tpid`). Only if consent "identification" is given, the `tpid` is passed and status "OK". Otherwise null. |
| tc | The TC String which should be stored for  this user in relation to the netID Partner (TCF 2.0) Only with status "OK". Otherwise null. |

| status | significance | tc | tpid |
| ----------- | ----------- | ----------- | ----------- |
| OK | TC String stored for this `tpid`. | x | x |
| NO_TPID | No authentication token was passed. | - | - |
| TOKEN_ERROR | Authentication token is expired or invalid. | - | - |
| CONSENT_REQUIRED | Consent for passing on the TPID is missing ("identification"). | x | - |

**Response behaviour**

| status code | meaning |
| ----------- | ----------- |
| 201 CREATED | - call successful | 
| 400 BAD REQUEST | - missing authentication token <br> - authentication token is expired or invalid | 
| 403 FORBIDDEN | - requesting TAPP isn't active  |
| 404 NOT FOUND | - TPID in authentication token is not active <br> - TC String is not available |
| 410 GONE | - TPID in authentication token isn't active |

## Write APIs
### Write consent status (privacy status)

``` shell
POST https://einwilligen.netid.de/permissions/iab-permissions?token=<TOKEN>
Content-Type: application/vnd.netid.permissions.iab-permission-write-v1+json

{
  "identification": "true|false",
  "tc": "<TC string>"
}
```

``` shell
201 CREATED
Location: https://einwilligungsspeicher.netid.de/permissions/iab-permissions?token=<TOKEN>

{
  "tpid": "<TPID>|null",
  "status": "OK|NO_TOKEN|TOKEN_ERROR"
}
```

Notes:

- If consent for "identification" has been given by the user, this must be signaled by passing "identification: true". For the avoidance of doubt, this of course requires the prior collection of this consent by the CMP.
- If only the TC string is to be updated and the consent for "identification" already exists, only the "tc" attribute can be passed. Both can also be written at the same time.
- In case of revocation the consent for "identification", only "identification: false" is passed.

**JSON Properties**

**request**

| |Description|
|---|---|
| identification | Boolean flag, indicating the status of the permission "Identification". <br>*true* = consent is given <br> *false* = consent is not given or revoked |
| tc | TC String which should be stored for this user in relation to the netID Partner (TCF 2.0) |

**response**

| |Description|
|---|---|
| tpid | Users netID identifier (`tpid`). Only passed if consent "identification" is given, the `tpid` does exist and status "OK". Otherwise null.|

| status | meaning |
| ----------- | ----------- |
| OK | TC String/consent for "identifcation" was stored. |
| NO_TOKEN | No authentication token was transferred. |
| TOKEN_ERROR | Authentication token is expired or invalid. |

**Response behaviour**

| status code | meaning |
| ----------- | ----------- |
| 200 OK | - TPID of the netID user is delivered, if consent for "identification" is granted <br> - TC String is delivered | 
| 400 BAD REQUEST | - missing authentication token <br> - authentication token is expired or invalid | 
| 403 FORBIDDEN | - requesting TAPP isn't active  |
| 410 GONE | - TPID in authentication token isn't active |
