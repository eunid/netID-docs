# Data export

Using this API netID Partners can retrieve the status (privacy status) with respect to netID Permissions and TC strings of end users. This allows server based synchronization for netID Partners clean-up / update their server-side storage - e.g. purging data in case of withdrawal of consent.

By specifying a *changed_since* parameter deltas w.r.t. that point in time can be requested to allow for batched updates.

## netID Permissions

Allows a individual netID Partner to retrieve the status with respect to netID Permissions (omitting TC information).

=== "Query"

    ``` shell
    GET https://einwilligungsuebersicht.netid.de/netid-permissions/?q.tapp_id.eq=<TAPP_ID>&q.date.ge=<DATE>
    Accept: application/vnd.netid.permission-center.permission-export.list-v1+json
    Authorization: Basic <b64(USERNAME:PASSWORD)>
    ```

=== "Response"

    ``` shell
    200 OK
    Content-Type: application/vnd.netid.permission-center.permission-export.list-v1+json

    {
      "content": 
      [
        {
          "tpid": "<tpid>",
          "type": "IDCONSENT",
          "status": "VALID",
          "changed_at": "<timestamp>"
        },
        {
          "tpid": "<tpid>",
          "type": "DATASHARE",
          "status": "INVALID",
          "changed_at": "<timestamp>"
        },
        {
          "tpid": "<tpid>",
          "tc": "<tc-string>",
          "changed_at": "<timestamp>"
        }
      ]
    }
    ```

### Response behavior

| HTTP status code | meaning |
| ----------- | ----------- |
| 200 OK | - Status of consent "identification" (IDCONSENT) and "datashare" is returned. <br> - Stored TC String is returned. | 
| 400 BAD REQUEST | Missing or invalid parameter (`tapp_id`, `date`). |
| 401 UNAUTHORIZED | Failed authentication. No (valid) authentication provided. |
| 403 FORBIDDEN | Requesting TAPP isn't active or allowed. Requesting API User hasn't the right role. |

## Complete Privacy Status

Allows netID Partners to retrieve the status with respect to netID Permissions as well as TC information. In case multiple statuses are managed via the same integration (*cmp_id*), the API allows to query for specific partner IDs or multiple.

=== "Query"

    ``` shell
    GET https://einwilligungsuebersicht.netid.de/netid-permissions?
      &q.cmp_id.eq=<CMP_ID>
      &q.tapp_id.in=<tapp_id_1>,...,<tapp_id_n>
      &q.date.ge=<DATE>
    Accept: application/vnd.netid.permission-center.tapp-permissions-export.list-v1+json
    Authorization: Basic <b64(USERNAME:PASSWORD)>
    ```

=== "Response"

    ``` shell
    200 OK
    Content-Type: application/vnd.netid.permission-center.tapp-permissions-export.list-v1+json

    {
      "content":
        [
          {
            "tapp_id":"<tapp_id_1>",
            "content":
              [
                {
                  "tpid":"<tpid>",
                  "type":"IDCONSENT",
                  "status":"VALID",
                  "changed_at":"<timestamp>"
                },
                {
                  "tpid":"<tpid>",
                  "type":"DATASHARE",
                  "status":"INVALID",
                  "changed_at":"<timestamp>"
                },
                {
                  "tpid":"<tpid>",
                  "tc":"<tc-string>",
                  "changed_at":"<timestamp>"
                }
              ]
          },
          {
            "tapp_id":"<tapp_id_2>",
            "content":
              [
                {
                  "tpid":"<tpid>",
                  "type":"IDCONSENT",
                  "status":"VALID",
                  "changed_at":"<timestamp>"
                },
                {
                  "tpid":"<tpid>",
                  "tc":"<tc-string>",
                  "changed_at":"<timestamp>"
                }
            ]
          }
      ]
    }
    ```

### Response behavior

| HTTP status code | meaning |
| ----------- | ----------- |
| 200 OK | - status of consent "identification" (IDCONSENT) and "datashare" is returned. <br> - Stored TC String is returned. | 
| 400 BAD REQUEST | Missing or invalid parameter (`tapp_id`, `date`) | 
| 401 UNAUTHORIZED | Failed authentication. No (valid) authentication provided | 
| 403 FORBIDDEN | Requesting TAPP isn't active or allowed. Requesting API User hasn't the right role. |