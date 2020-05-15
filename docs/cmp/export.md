# Data export

Via this API netID Partners get the ability to request the consent status (privacy status) of the netID permissions and TC strings of users unrelated to a specific context, via the specification of changed_since deltas can also be requested. There is an HTTP service with a REST API for this service.

## TAPP Request

``` shell
GET https://einwilligungsuebersicht/permissions/iab-permissions?tapp_id=<TAPP_ID>&changed_since=<DATE>
Accept: application/vnd.netid.permissions.tapp-iab-permission-export.list-v1+json
Authorization: Basic <b64(USERNAME:PASSWORD)>
```

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

**Response behaviour**

| status code | meaning |
| ----------- | ----------- |
| 200 OK | - call successful | 
| 400 BAD REQUEST | - missing parameter `changed_since` | 
| 401 UNAUTHORIZED | - no authentification | 
| 403 FORBIDDEN | - missing parameters (`cmp_id`) <br> - requesting TAPP isn't active |

## CMP Request

``` shell
GET https://einwilligungsuebersicht/permissions/iab-permissions?cmp_id=<CMP_ID>&tapp_ids=<tapp_id_1,...,<tapp_id_n>&changed_since=<DATE>
Accept: application/vnd.netid.permissions.tapp-iab-permission-export.list-v1+json
Authorization: Basic <b64(USERNAME:PASSWORD)>
```

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

**Response behaviour**

| status code | meaning |
| ----------- | ----------- |
| 200 OK | - call successful | 
| 400 BAD REQUEST | - missing parameter `changed_since` | 
| 401 UNAUTHORIZED | - no authentification | 
| 403 FORBIDDEN | - missing parameters (`cmp_id`) <br> - requesting TAPP isn't active |