# Data export

Using this API netID Partners can retrieve the current status (privacy status) with respect to netID Permissions and TC strings of end users. This allows server based synchronization in case a netID partner maintains its users privacy status also persistently in his own backend infrastructure and not only locally on end users devices.

By specifying a *changed_since* parameter deltas w.r.t. that point in time can be requested to allow for batched updates.

## netID Permissions

Allows a individual netID Partner to retrieve the status with respect to netID Permissions (omitting TC information).

=== "Query"

    ``` shell
    GET https://einwilligungsuebersicht.netid.de/permissions/iab-permissions?
      &tapp_id=<TAPP_ID>
      &changed_since=<DATE>
    Accept: application/vnd.netid.permissions.tapp-iab-permission-export.list-v1+json
    Authorization: Basic <b64(USERNAME:PASSWORD)>
    ```

=== "Response"

    ``` shell
    200 OK
    Content-Type: application/vnd.netid.permissions.tapp-iab-permission-export.list-v1+json

    {
      [
        {
          "tpid": "<tpid>",
          "type": "IDCONSENT",
          "status": "VALID",
          "changed_at": "<timestamp>"
        }
      ]
    }
    ```

### Response behavior

| status code | meaning |
| ----------- | ----------- |
| 200 OK | Call successful |
| 400 BAD REQUEST | Missing parameter `changed_since` |
| 401 UNAUTHORIZED | No (valid) authentication provided |
| 403 FORBIDDEN | Missing parameters (`tapp_id`) and/or requesting TAPP isn't active |

## Complete Privacy Status

Allows netID Partners to retrieve the status with respect to netID Permissions as well as TC information. In case multiple statuses are managed via the same integration (*cmp_id*), the API allows to query for specific partner IDs or multiple.

=== "Query"

    ``` shell
    GET https://einwilligungsuebersicht.netid.de/permissions/iab-permissions?
      &cmp_id=<CMP_ID>
      &tapp_ids=<tapp_id_1,...,<tapp_id_n>
      &changed_since=<DATE>
    Accept: application/vnd.netid.permissions.tapp-iab-permission-export.list-v1+json
    Authorization: Basic <b64(USERNAME:PASSWORD)>
    ```

=== "Response"

    ``` shell
    200 OK
    Content-Type: application/vnd.netid.permissions.tapp-iab-permission-export.list-v1+json

    {
      "tapp_permissons":
        [
          {
            "tapp_id":"<tapp_id_1>",
            "permissions":
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
          },
          {
            "tapp_id":"<tapp_id_2>",
            "permissions":
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

| status code | meaning |
| ----------- | ----------- |
| 200 OK | Call successful |
| 400 BAD REQUEST | Missing parameter `changed_since` |
| 401 UNAUTHORIZED | No (valid )authentication provided |
| 403 FORBIDDEN | Missing parameters (`cmp_id`), (`tapp_id`) <br> - requesting TAPP isn't active |