# Log Analytics Workspace

The lab uses `LAW-AZ104-Enterprise` as the central workspace for Linux VM monitoring data.

## Workspace details

| Setting | Value |
| --- | --- |
| Workspace name | `LAW-AZ104-Enterprise` |
| Resource group | `RG-AZ104-Network` |
| Region | `centralindia` |
| Resource ID | `/subscriptions/9e7bf3ca-eee3-4fae-a459-3f0b6c583d38/resourceGroups/RG-AZ104-Network/providers/Microsoft.OperationalInsights/workspaces/LAW-AZ104-Enterprise` |
| Workspace ID observed | `9a641fd7-82a8-4fce-94ae-a62f815b27b1` |

## Connected data collection

The workspace receives Linux performance and syslog data through:

```text
Azure Monitor Agent
    -> DCR-AZ104-Linux
    -> LAW-AZ104-Enterprise
```

## Why this matters

Log Analytics provides a centralized place to query operational data instead of checking each VM individually. In enterprise operations, this supports troubleshooting, alerting, reporting, and incident investigation.
