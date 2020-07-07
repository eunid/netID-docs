# Server-based API (backend integration)

Description of the backend integration of the netID Permission Center by the CMP (integration from the server side / backend of the CMP if available).

A netID Partner (TAPP) that sends a user through the Single Sign-On Flow can requests an access token (`token`) provided after the successful login, based on which a user can be authenticated at the netID Permission Center to enable read/write access for that specific users privacy status.

!!! info  ""
    The server-based requests are secured via the access token.
    Calls of this type are blocked from the browser environments for security reasons (no Origin header is allowed!)

## Read APIs

### netID Identifier

A CMP/netID Partner can retrieve the user's netID Identifier via the following interface:

=== "Query"

    ``` shell
    GET https://einwilligungsspeicher.netid.de/identification/tpid?
        token=<TOKEN>
    Accept: application/vnd.netid.identification.tpid-read-v1+json
    ```

=== "Response"

    ``` shell
    200 OK
    Content-Type: application/vnd.netid.identification.tpid-read-v1+json

    {
      "tpid": "<TPID>|null"
      "status": "OK|NO_TOKEN|TOKEN_ERROR|CONSENT_REQUIRED"
    }
    ```

#### Response properties

`tpid` - Users netID Identifier. Only present if consent "Identification" is given, the `tpid` is known and status is "OK". Otherwise null.

| status | meaning | tpid |
| ----------- | ----------- | ----------- |
| OK | Call successful | x |
| NO_TOKEN | No access token was passed. | - |
| TOKEN_ERROR | Access token is expired or invalid. | - |
| CONSENT_REQUIRED | Consent for passing on the TPID is missing ("identification"). | - |

#### Response behavior

| status code | meaning |
| ----------- | ----------- |
| 200 OK | `TPID` of the netID user returned |
| 400 BAD REQUEST | missing access token, or access token expired / invalid |
| 403 FORBIDDEN | requesting TAPP isn't active or consent for 'identification' isn't granted |
| 404 NOT FOUND | TPID in access token does not exist |
| 410 GONE | TPID in access token isn't active |

### Read privacy status

=== "Query"

    ``` shell
    GET https://einwilligungsspeicher.netid.de/permissions/iab-permissions?
        token=<TOKEN>
    Accept: application/vnd.netid.permissions.iab-permission-read-v1+json
    ```

=== "Response"

    ``` shell
    200 OK
    Content-Type: application/vnd.netid.permissions.iab-permission-read-v1+json

    {
      "tpid": "<TPID>|null",
      "tc": "<TC string>|null",
      "status": "OK|NO_TOKEN|TOKEN_ERROR|CONSENT_REQUIRED"
    }
    ```
  
#### Response properties

| |Description|
|---|---|
| tpid | Users netID identifier (`tpid`). Only if consent "identification" is given and status "OK". Otherwise null. |
| tc | The TC String which should be stored for  this user in relation to the netID Partner (TCF 2.0) Only with status "OK". Otherwise null. |

| status | significance | tc | tpid |
| ----------- | ----------- | ----------- | ----------- |
| OK | Call successfull - tc information (if present) and TPID returned | x | x |
| NO_TPID | No access token was passed. | - | - |
| TOKEN_ERROR | Access token is expired or invalid. | - | - |
| CONSENT_REQUIRED | Consent for passing on the TPID is missing ("identification"). | x | - |

#### Response behavior

| status code | meaning |
| ----------- | ----------- |
| 201 OK | Call successful |
| 400 BAD REQUEST | missing access token, or access token is expired / invalid |
| 403 FORBIDDEN | requesting TAPP isn't active  |
| 404 NOT FOUND | TPID in access token is not active or TC String is not available |
| 410 GONE | TPID in access token isn't active |

## Write APIs

### Write privacy status

=== "Query"

    ``` shell
    POST https://einwilligen.netid.de/permissions/iab-permissions?
        token=<TOKEN>
    Content-Type: application/vnd.netid.permissions.iab-permission-write-v1+json

    {
      "identification": "true|false",
      "tc": "<TC string>"
    }
    ```

=== "Response"

    ``` shell
    201 CREATED

    {
      "tpid": "<TPID>|null",
      "status": "OK|NO_TOKEN|TOKEN_ERROR"
    }
    ```

!!! info "Remarks"
    - If consent for "identification" has been given by the user, this must be signaled by passing "identification: true". For the avoidance of doubt, this of course requires the prior collection of this consent by the CMP.
    - If only the TC string is to be updated and the consent for "identification" already exists, only the "tc" attribute can be passed. Both can also be written at the same time.
    - In case of revocation the consent for "identification", only "identification: false" is passed.

#### Request properties

| |Description|
|---|---|
| identification | Boolean flag, indicating the status of the permission "Identification". <br>*true* = consent is given <br> *false* = consent is not given or revoked |
| tc | TC String which should be stored for this user in relation to the netID Partner (TCF 2.0) |

#### Response properties

`tpid` - Users netID Identifier. Only present if consent "Identification" is given, the `tpid` is known and status is "OK". Otherwise null.

| status | meaning |
| ----------- | ----------- |
| OK | TC String/consent for "identification" was stored. |
| NO_TOKEN | No access token was transferred. |
| TOKEN_ERROR | Access token is expired or invalid. |

#### Response behavior

| status code | meaning |
| ----------- | ----------- |
| 201 CREATED | - TPID of the netID user is returned, if consent for "identification" is granted <br> - TC String is returned |
| 400 BAD REQUEST | missing access token, or access token expired / invalid |
| 403 FORBIDDEN | requesting TAPP isn't active  |
| 410 GONE | TPID in access token isn't active |
