# Server-based API (backend integration)

Description of the backend integration of the netID Permission Center by the CMP (integration from the server side / backend of the CMP if available).

A netID Partner (TAPP) that sends a user through the Single Sign-On Flow and requests to manage his privacy status receives an access token (`token`) after the successful login. Based on this token access to the netID Permission Center is authorized enabling read/write access for that specific users privacy status.

!!! info  ""
    The server-based requests are secured using an access token.
    Calls of this type are blocked from the browser environments for security reasons (no Origin header is allowed!)

## Read APIs

### Accessing a user identifier

A CMP/netID Partner can retrieve the user's identifier (TPID) via the following interface:

=== "Query"
    ``` shell
    GET https://READSERVICE.netid.de/identification/tpid?
          token=<TOKEN>
    ```

=== "Response"
    ``` shell
    {
      "tpid": "<TPID>|null"
      "status": "OK|NO_TOKEN|TOKEN_ERROR|CONSENT_REQUIRED"
    }
    ```

#### Response Parameters

```tpid```- Users identifier. Only returned if consent for "Identification" is given and status "OK"

| status | description | tpid |
| ----------- | ----------- | ----------- |
| OK | Call successful | x |
| NO_TOKEN | No access token provided. | - |
| TOKEN_ERROR | Access token has expired or is invalid | - |
| CONSENT_REQUIRED | Consent for passing on the TPID missing ("Identification") | - |

### Privacy status

=== "Query"
    ``` shell
    GET https://READSERVICE.netid.de/permissions/iab-permissions?
          token=<TOKEN>
    ```
=== "Reponse"

    ``` shell
    {
      "tpid": "<TPID>|null",
      "tc": "<TC string>|null",
      "status": "OK|NO_TOKEN|TOKEN_ERROR|CONSENT_REQUIRED"
    }
    ```

#### Response Parameters

```tpid``` - Only present if consent "Identification" is given and status "OK"

```tc``` - The TC String stored for this user in relation to the netID Partner (TCF 2.0)

| status | description | tc | tpid |
| ----------- | ----------- | ----------- | ----------- |
| OK | TC String stored for this user | x | x |
| NO_TPID | No access token provided | - | - |
| TOKEN_ERROR | Access token has expired or is invalid | - | - |
| CONSENT_REQUIRED | Consent for passing on the `tpid` missing ("Identification"). In case there is a tc string stored this will still be returned anyway| x | - |

## Write APIs

### Privacy status

=== "Query"
    ``` shell
    https://WRITESERVICE.netid.de/permissions/iab-permissions?
          token=<TOKEN>
    {
      "identification": "true|false",
      "tc": "<TC string>"
    }
    ```

=== "Response"
    ``` shell
    {
      "tpid": "<TPID>|null",
      "status": "OK|NO_TOKEN|TOKEN_ERROR"
    }
    ```

Remarks:

- If permission "identification" has been given by the user, this must be signaled by passing "identification: true". For the avoidance of doubt, this of course requires the prior collection of this consent by the CMP.
- If only the TC string is to be updated and the permission "Identification" already exists, only the "tc" attribute can be passed. Both can also be written at the same time.
- In case of revocation of permission "Identification", would pass only "identification: false".

#### Request Parameters

|parameter|description|
|---|---|
| identification | Boolean flag, indicating the status of the permission "Identification". <br>**Yes** = Consent given <br> **No** = consent not given / revoked |
| tc | The TC String to be stored for this this user in relation to the netID Partner (TCF 2.0)  |

#### Reponse Parameters

```tpid```- Users identifier. Only returned if consent for "Identification" is given and status "OK"

| status | description |
| ----------- | ----------- |
| OK | Successfully stored |
| NO_TOKEN | No access token provided |
| TOKEN_ERROR | Access token has expired or is invalid |
