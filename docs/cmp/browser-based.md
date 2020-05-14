# Browser-based API (Webbrowser Integration)

Description of the browser-based integration by the CMP 

##  API flow examples

### Obtaining a privacy status

The following sequence illustrates the API calls initiated by a netID Partners CMP to establish a privacy status for an already authenticated user. 

![Browser based API](../diagrams/out/seq_cmp_webapi.svg)

## Read APIs

### netID identifier

If the `origin` is eligible, a publisher (TAPP) can access the user’s identifier (TPID) via the following interface:

``` shell
GET https://einwilligungsspeicher.netid.de/identification/tpid?tapp_id=<TAPP_ID>
Accept: application/vnd.netid.identification.tpid-read-v1+json
Cookie: tpid_sec=<JWT_TOKEN>
Origin: <ORIGIN>
```

``` shell
200 OK
Content-Type: application/vnd.netid.identification.tpid-read-v1+json
Access-Control-Allow-Origin: <ORIGIN>
Access-Control-Allow-Credentials: true

{
  "tpid": "<TPID>|null"
  "status": "OK|NO_TPID|TOKEN_ERROR|CONSENT_REQUIRED"
}
```

**JSON Properties**

| |Description|
|---|---|
| tpid | Users netID identifier (`TPID`). Only if consent "identification" is given, the `TPID` is passed and status "OK". Otherwise null. |

| status | meaning | tpid |
| ----------- | ----------- | ----------- |
| OK | Call successful | x |
| NO_TPID | There was no tpid_sec cookie available. | - |
| TOKEN_ERROR | Token (JWT) in the cookie is expired or  invalid. | - |
| CONSENT_REQUIRED | Consent for passing on the TPID is missing ("identification"). | - |

**Response behaviour**

| status code | meaning |
| ----------- | ----------- |
| 200 OK | - TPID of the netID user is delivered | 
| 400 BAD REQUEST | - missing authentication/no tpid_sec cookie <br> - token (JWT) in the tpid_sec cookie is expired or invalid | 
| 403 FORBIDDEN | - missing parameters (`tapp_id`, `origin`) <br> - requesting TAPP isn't active \ - consent for 'identification' isn't granted |
| 404 NOT FOUND | - TPID in tpid_sec cookie does not exist |
| 410 GONE | - TPID in tpid_sec cookie isn't active |

### Read consent status (privacy status)

``` shell
GET https://einwilligungsspeicher.netid.de/permissions/iab-permissions?tapp_id=<TAPP_ID>
Accept: application/vnd.netid.permissions.iab-permissions-read-v1+json
Cookie: tpid_sec=<JWT_TOKEN>
Origin: <ORIGIN>
```

``` shell
200 OK
Content-Type: application/vnd.netid.permissions.iab-permissions-read-v1+json
Access-Control-Allow-Origin: <ORIGIN>
Access-Control-Allow-Credentials: true

{
  "tpid": "<TPID>|null",
  "tc": "<TC string>|null",
  "status": "OK|NO_TPID|TOKEN_ERROR|CONSENT_REQUIRED"
}
```

**JSON Properties**

| |Description|
|---|---|
| tpid | Users identifier (`tpid`). If consent "identification" is given, the `tpid` does exist and status "OK". Otherwise null. |
| tc | The TC string stored for this `tpid` for this publisher (TCF 2.0). Only with status "OK". Otherwise null. |

| status | meaning | tc | pid |
| ----------- | ----------- | ----------- | ----------- |
| OK | Call successful | x | x |
| NO_TPID | There was no tpid_sec cookie available. | - | - |
| TOKEN_ERROR | Token (JWT) in the tpid_sec cookie is expired or invalid. | - | - |
| CONSENT_REQUIRED | Consent for passing on the TPID missing ("identification"). | x | - |

**Response behaviour**

| status code | meaning |
| ----------- | ----------- |
| 200 OK | - TPID of the netID user is delivered, if consent of "identification" is given <br> - TC String is delivered | 
| 400 BAD REQUEST | - missing authentication/no tpid_sec cookie <br> - token (JWT) in the tpid_sec cookie is expired or invalid | 
| 403 FORBIDDEN | - missing parameters (`tapp_id`, `origin`) <br> - requesting TAPP isn't active |
| 404 NOT FOUND | - TPID in tpid_sec cookie does not exist <br> - consent of "identification" is not granted and TC String is not available <br> - TC String is not available |
| 410 GONE | TPID in tpid_sec cookie isn't active |

## Write API

### Write consent status (privacy status)

``` shell
POST https://einwilligen.netid.de/permissions/iab-permissions?tapp_id=<TAPP_ID>
Content-Type: application/vnd.netid.permissions.iab-permission-write-v1+json
Cookie: tpid_sec=<JWT_TOKEN>
Origin: <ORIGIN>

{
  "identification": "true|false",
  "tc": "<TC string>"
}
```

``` shell
201 CREATED
Location: https://einwilligen.netid.de/permissions/iab-permissions?tapp_id=<TAPP_ID>
Access-Control-Allow-Origin: <ORIGIN>
Access-Control-Allow-Credentials: true

{
  "tpid": "<TPID>|null",
  "status": "OK|NO_TPID|TOKEN_ERROR"
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
| identification | Boolean flag, indicating the status of the consent "identification". <br> *true* = Consent is given <br> *false* = consent is not given or revoked |
| tc | TC String which should be stored for this user in relation to the netID Partner (TCF 2.0) |

**response**

| |Description|
|---|---|
| tpid | Users netID identifier (`tpid`). Only passed if consent "identification" is given, the `tpid` does exist and status "OK". Otherwise null.|

| status | meaning |
| ----------- | ----------- |
| OK | TC String/consent for "identifcation" was stored. |
| NO_TPID | There was no `tpid_sec` cookie available. |
| TOKEN_ERROR | Token (JWT) in the cookie has expired or is invalid. |

**Response behaviour**

| status code | meaning |
| ----------- | ----------- |
| 201 CREATED | - Call sucessfull | 
| 400 BAD REQUEST | - missing authentication/no tpid_sec cookie <br> - token (JWT) in the tpid_sec cookie is expired or invalid | 
| 403 FORBIDDEN | - missing parameters (`tapp_id`, `origin`) <br> - requesting TAPP isn't active |
| 410 GONE | TPID in tpid_sec cookie isn't active |