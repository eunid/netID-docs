# System Health Status

The public netID endpoint for the system health is: https://status.netid.de


=== "Example Status Response"
    ```json
    {
        "updatedAt": "2020-07-15T12:15:25.655496Z",
        "status": "DEGRADED",                     // "overall" state, a  aggregation of usecase states
        "details": {                              // optional details - additional information about subsystems.
            "broker": { "status": "OK" },
            "op-ni": { "status": "SEVERE" },
            "op-webde": { "status": "OK" },
            "op-gmx": { "status": "OK" },
            "op-7pass": { "status": "OK" },
            "permissionservice": { "status": "OK" }
        },
        "usecases": {                                     // optional usecases
            "sso-login": { "status": "DEGRADED" }
        }
    }
    ```

| status | color | meaning |
| ----------- | ----------- | ----------- |
| OK | green | No reported issues and request are completed normally. |
| DEGRADED | yellow | Some noncritical issues with the subsystem/usecase. |
| SEVERE | red | A definitive proof of an outage has been found. |
