# Data export

Using this API netID Partners can retrieve the privacy status with respect to netID Permissions and the TC string of end users. This allows server based synchronization for netID Partners clean-up / update their server-side storage - e.g. purging data in case of withdrawal of consent.

!!! info  "Sync-ID"
    In case the [Sync-ID](../#custom-privacy-settings) should be included in the API responses (if preconditions are met), the APIs must be called with the respective accept header.

     Without Synch-ID: `application/vnd.netid.permission-center.netid-user-status-v1+json` <br>
     With Synch-ID: `application/vnd.netid.permission-center.netid-user-status-audit-v1+json`

## Privacy status

Allows an individual netID Partner to retrieve the privacy statuses from the permission center.

**Parameters**

| name  | function  | description |
| -----------  | ----------- | ----------- |
| q.tapp_id.eq | Parameter - authentication | Client for which status should be retrieved, provided during setup |
| Authorization | Header - authentication | basic auth credentials,  provided during setup |
| q.date.ge | Parameter - timeframe | only statuses which have been changed since this date are returned (for delta updates)|
| Accept  | Header - content type | determines the expected response, two options are available to define an expected response with Sync-ID or alternatively with netID Identifier |

=== "Query (incl. Sync-ID)"

    ``` shell
    HTTP/1.1
    GET https://einwilligungsuebersicht.netid.de/netid-permissions/?
      q.tapp_id.eq=<TAPP_ID>
      &q.date.ge=<DATE>
    Accept: application/vnd.netid.permission-center.netid-permission-export-audit.list-v1+json
    Authorization: Basic <base64(username:password)>
    ```

=== "Response (incl. Sync-ID)"

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

### Response behavior

| HTTP status code | meaning |
| ----------- | ----------- |
| 200 OK | Call successful. Permissions of the TAPP are returned. | 
| 400 BAD REQUEST | Missing or invalid parameter (q.tapp_id.eq, q.date.ge). |
| 401 UNAUTHORIZED | Failed authentication. No (valid) authentication provided. |
| 403 FORBIDDEN | Requesting TAPP isn't active or allowed. Requesting API user hasn't the right role. |

## Complete Privacy Status

Allows netID Partners to retrieve the privacy statuses from the permission center for multiple clients `tapp_id`. In case multiple statuses are managed via the same integration (*cmp_id*), the API allows to query for specific partner IDs or multiple.

**Parameters**

| name  | function  | description |
| -----------  | ----------- | ----------- |
| q.cmp_id.eq | Parameter - authentication | cmp-id associated for named `tapp_id`s |
| q.tapp_id.eq | Parameter - authentication | List of tapp_ids to return a status for - provided during setup |
| Authorization | Header - authentication | basic auth credential,  provided during setup |
| q.date.ge | Parameter - timeframe | only statuses which have been changed since are returned (for delta updates)|
| Accept  | Header - content type | determines the expected response, two options are available to define an expected response with Sync-ID or alternatively with netID Identifier |

=== "Query (incl. Sync-ID)"

    ``` shell
    GET https://einwilligungsuebersicht.netid.de/netid-permissions?
      &q.cmp_id.eq=<CMP_ID>
      &q.tapp_id.in=<tapp_id_1>,...,<tapp_id_n>
      &q.date.ge=<DATE>
    Accept: application/vnd.netid.permission-center.tapp-netid-permissions-export-audit.list-v1+json
    Authorization: Basic <b64(USERNAME:PASSWORD)>
    ```

=== "Response (incl. Sync-ID)"

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

### Response behavior

| HTTP status code | meaning |
| ----------- | ----------- |
| 200 OK | Call successful. Permissions of the TAPP’s of the CMP are returned. | 
| 400 BAD REQUEST | Missing or invalid parameter (q.tapp_id.in, q.cmp_id.eq, q.date.ge). | 
| 401 UNAUTHORIZED | Failed authentication. No (valid) authentication provided | 
| 403 FORBIDDEN | Requesting CMP isn't active or allowed. Requesting API user hasn't the right role. |
