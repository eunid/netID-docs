# Browser-based API

The following APIs rely on using a previously established authentication status, stored as a JWT within the users browser. It enables access to the Permission Center APIs as described below for eligible Partners (their respective CMPs).

## API flow examples

### Obtaining a privacy status

The following sequence illustrates the API calls initiated by a Partners CMP to establish a privacy status for an already authenticated user.

![Browser based API](../diagrams/out/seq_cmp_webapi.svg)

## Read APIs

### User identifier

If the ORIGIN is eligible, a publisher (TAPP) can retrieve the user’s identifier (TPID) via the following interface:

=== "Query"

    ``` shell
    https://READSERVICE.netid.de/identification/tpid?
      tapp_id=<TAPP_ID>
      Cookie: tpid_sec=<JWT_TOKEN>
      Origin: <ORIGIN>
    ```

=== "Response"

    ``` shell
    Access-Control-Allow-Origin: <ORIGIN>
    Access-Control-Allow-Credentials: true
    {
      "tpid": "<TPID>|null"
      "status": "OK|NO_TPID|TOKEN_ERROR|CONSENT_REQUIRED"
    }
    ```

#### Response Parameters

```tpid``` -  Users identifier. Only present if consent "Identification" is given, the `tpid` is known and status is "OK". Otherwise null.

| status | description | tpid |
| ----------- | ----------- | ----------- |
| OK | Call successful | x |
| NO_TPID | There was no tpid_sec cookie available. | - |
| TOKEN_ERROR | Token (JWT) in the cookie has expired or is invalid. | - |
| CONSENT_REQUIRED | Consent for passing on the TPID missing ("Identification"). | - |

### Privacy status

=== "Query"

    ```
    https://READSERVICE.netid.de/permissions/iab-permissions?
        tapp_id=<TAPP_ID>
        Cookie: tpid_sec=<JWT_TOKEN>
        Origin: <ORIGIN>
    ```
=== "Response"

    ```shell
    Access-Control-Allow-Origin: <ORIGIN>
    Access-Control-Allow-Credentials: true
    {
      "tpid": "<TPID>|null",
      "tc": "<TC string>|null",
      "status": "OK|NO_TPID|TOKEN_ERROR|CONSENT_REQUIRED"
    }
    ```

#### Response Parameters

```tpid``` -  Users identifier. Only present if consent "Identification" is given, the `tpid` is known and status is "OK". Otherwise null.

```tc``` - The TC string stored for this user for this publisher (TCF 2.0). Only with status "OK". Otherwise null. |

| status | description | tc | tpid |
| ----------- | ----------- | ----------- | ----------- |
| OK | Status successfully retrieved | x | x |
| NO_TPID | There was no tpid_sec cookie available. | - | - |
| TOKEN_ERROR | Token (JWT) in the cookie has expired or is invalid. | - | - |
| CONSENT_REQUIRED | Consent for passing on the TPID missing ("Identification"). | x | - |

## Write API

### Privacy status

=== "Query"

    ``` shell
    https://WRITESERVICE.netid.de/permissions/iab-permissions?
        tapp_id=<TAPP_ID>
        Cookie: tpid_sec=<JWT_TOKEN>
        Origin: <ORIGIN>
    {
      "identification": "true|false",
      "tc": "<TC string>"
    }
    ```

=== "Response"

    ``` shell
    Access-Control-Allow-Origin: <ORIGIN>
    Access-Control-Allow-Credentials: true
    {
      "tpid": "<TPID>|null",
      "status": "OK|NO_TPID|TOKEN_ERROR"
    }
    ```

Remarks:

- If permission "identification" has been given by the user, this must be signaled by passing ```identification: true```. For the avoidance of doubt, this of course requires the prior collection of this consent by the CMP.
- If only the TC string is to be updated and the permission "Identification" already exists, only the ```tc``` attribute can be passed. Both can also be written at the same time.
- In case of revocation of permission "Identification", one would pass only ```identification: false```.

#### Request Parameters

| parameter|description|
|---|---|
| identification | Boolean flag, indicating the status of the permission "Identification". <br>*Yes* = consent given <br> *No* = consent not given / revoked |
| tc | The TC String to be stored for this this user in relation to the netID Partner (TCF 2.0) |

#### Response Parameters

```tpid``` -  Users identifier. Only present if consent "Identification" is given, the `tpid` is known and status is "OK". Otherwise null.

| status | description |
| ----------- | ----------- |
| OK | Successfully stored |
| NO_TPID | There was no `tpid_sec` cookie available |
| TOKEN_ERROR | Token (JWT) in the cookie has expired or is invalid|
