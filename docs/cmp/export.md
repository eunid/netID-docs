# Data export

Using this API netID Partners can request the consent status (privacy status) of the netID Permissions and TC strings of users unrelated to a specific context, via the specification of changed_since deltas can also be requested.

## netID Permissions

Allows a netID Partner to retrieve the status with respect to netID Permissions (omitting TC information). This API can be called unrelated to the CMP.

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

| status code | meaning |
| ----------- | ----------- |
| 200 OK | Call successful | 
| 400 BAD REQUEST | Missing parameter `changed_since` | 
| 401 UNAUTHORIZED | No (valid) authentication provided | 
| 403 FORBIDDEN | Missing parameters (`tapp_id`) and/or requesting TAPP isn't active |

## Complete Privacy Status

Allows a netID Partners CMP to retrieve the status with respect to netID Permissions (omitting TC information) as well as TC information.

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