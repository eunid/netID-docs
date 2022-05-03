# Data export

Using this API netID Partners can retrieve the status (privacy status) with respect to netID Permissions and TC strings of end users. This allows server based synchronization for netID Partners clean-up / update their server-side storage - e.g. purging data in case of withdrawal of consent.

By specifying a *changed_since* parameter deltas w.r.t. that point in time can be requested to allow for batched updates.

## netID Permissions

Allows a individual netID Partner to retrieve the status with respect to netID Permissions (omitting TC information).

=== "Query with Sync-ID in response"

    ``` shell
    GET https://einwilligungsuebersicht.netid.de/netid-permissions/?q.tapp_id.eq=<TAPP_ID>&q.date.ge=<DATE> HTTP/1.1
    Accept: application/vnd.netid.permission-center.netid-permission-export-audit.list-v1+json
    Authorization: Basic <base64(username:password)>
    ```

=== "Response with Sync-ID"

    ``` shell
    200 OK
    Content-Type: application/vnd.netid.permission-center.netid-permission-export-audit.list-v1+json 

    { 
    "tapp_netid_permissions_export_audit":[
      {
        "sync_id":"<SYNC_ID>",
        "type":"IDCONSENT",
        "status":"VALID",
        "changed_at":"<TIMESTAMP>"
      },
       {
         "sync_id":"<SYNC_ID>",
         "type": "DATASHARE",
         "status" : "VALID",
         "changed_at" : "<TIMESTAMP>"  
       },
      {
        "sync_id":"<SYNC_ID>",
        "type":"IAB_TC_STRING",
        "value":"<TC_STRING>",
        "changed_at":"<TIMESTAMP>"
      }]}

    ```
    
> **Note**: If the Sync-ID is not needed, please use accept header with the following media type. Response contains `TPID` instead. <br>
    ```
    Application/vnd.netid.permission-center.netid-permission-export.list-v1+json
    ```

### Response behavior

| HTTP status code | meaning |
| ----------- | ----------- |
| 200 OK | Call successful. Permissions of the TAPP are returned. | 
| 400 BAD REQUEST | Missing or invalid parameter (q.tapp_id.eq, q.date.ge). |
| 401 UNAUTHORIZED | Failed authentication. No (valid) authentication provided. |
| 403 FORBIDDEN | Requesting TAPP isn't active or allowed. Requesting API user hasn't the right role. |

## Complete Privacy Status

Allows netID Partners to retrieve the status with respect to netID Permissions as well as TC information. In case multiple statuses are managed via the same integration (*cmp_id*), the API allows to query for specific partner IDs or multiple.

=== "Query with Sync-ID in response"

    ``` shell
    GET https://einwilligungsuebersicht.netid.de/netid-permissions?
      &q.cmp_id.eq=<CMP_ID>
      &q.tapp_id.in=<tapp_id_1>,...,<tapp_id_n>
      &q.date.ge=<DATE>
    Accept: application/vnd.netid.permission-center.tapp-netid-permissions-export-audit.list-v1+json
    Authorization: Basic <b64(USERNAME:PASSWORD)>
    ```

=== "Response with Sync-ID"

    ``` shell
    200 OK
    Content-Type: application/vnd.netid.permission-center.tapp-netid-permissions-export-audit.list-v1+json

    {
    "cmp_netid_permissions_export_audit": [
    {
      "tapp_id":"<TAPP_ID_X>",
      "tapp_netid_permissions_export_audit": [
        {
          "sync_id":"<SYNC_ID>",
          "type":"IDCONSENT",
          "status":"VALID",
          "changed_at":"<TIMESTAMP>"
        },
        {
          "sync_id":"<SYNC_ID>",
          "type":"IAB_TC_STRING",
          "value":"<TC_STRING>",
          "changed_at":"<TIMESTAMP>"
        }
      ]
    },
    {
      "tapp_id":"<TAPP_ID_Y>",
      "tapp_netid_permissions_export_audit":[        
        {
          "sync_id":"<SYNC_ID>",
          "type":"IDCONSENT",
          "status":"VALID",
          "changed_at":"<TIMESTAMP>"
         },
        {
          "sync_id":"<SYNC_ID>",
          "type":"IAB_TC_STRING",
          "value":"<TC_STRING>",
          "changed_at":"<TIMESTAMP>"
        }
      ]}]}

    ```
> **Note**: If the Sync-ID is not needed, please use accept header with the following media type. Response contains `TPID` instead. <br>
    ```
    Application/vnd.netid.permission-center.tapp-netid-permissions-export.list-v1+json
    ```

### Response behavior

| HTTP status code | meaning |
| ----------- | ----------- |
| 200 OK | Call successful. Permissions of the TAPP’s of the CMP are returned. | 
| 400 BAD REQUEST | Missing or invalid parameter (q.tapp_id.in, q.cmp_id.eq, q.date.ge). | 
| 401 UNAUTHORIZED | Failed authentication. No (valid) authentication provided | 
| 403 FORBIDDEN | Requesting CMP isn't active or allowed. Requesting API user hasn't the right role. |
