# AZ-104 Enterprise Administrator Lab

Hands-on Azure Administrator lab aligned with AZ-104 objectives and enterprise administration workflows.

This repository documents the Azure environment built during the lab so far: enterprise-style resource organization, a three-tier VM architecture, least-privilege RBAC, Azure Monitor/Log Analytics, CPU alerting, and secure Blob Storage access testing.

## Current lab milestone

The current completed milestone covers:

- Resource group separation for network, compute, and storage workloads.
- `VNet-AZ104-Enterprise` in `RG-AZ104-Network` with three subnets for management, web, and app tiers.
- Three Linux VMs in `RG-AZ104-COMPUTE`:
  - `VM-AZ104-Management`
  - `VM-AZ104-Web`
  - `VM-AZ104-App`
- NSG-based segmentation, NAT Gateway, and Bastion as part of the network foundation.
- Private tier-to-tier communication between the web and app tiers.
- Public IP removal from the app VM.
- Nginx web tier and Python app tier configured as part of the workload.
- Least-privilege RBAC validation for VM operator, network admin, reader, and owner access patterns.
- Azure Monitor Agent installed on all three VMs.
- `LAW-AZ104-Enterprise` Log Analytics workspace.
- `DCR-AZ104-Linux` Data Collection Rule collecting Linux performance and syslog streams.
- DCR associations for management, web, and app VMs.
- `AG-AZ104-Alerts` action group with email notification.
- CPU metric alerts for all three VMs.
- Storage account in `RG-AZ104-Storage` with private Blob container `application-files`.
- Storage firewall/network access testing.
- Blob soft delete, container soft delete, and blob versioning enabled.
- Storage Blob Data Reader access validated for `reader@Kishoree.onmicrosoft.com`.

## Architecture diagrams

Diagram source files are stored in [`assets/diagrams`](assets/diagrams):

- [`enterprise-architecture.mmd`](assets/diagrams/enterprise-architecture.mmd)
- [`network-topology.mmd`](assets/diagrams/network-topology.mmd)
- [`rbac-access-model.mmd`](assets/diagrams/rbac-access-model.mmd)
- [`monitoring-architecture.mmd`](assets/diagrams/monitoring-architecture.mmd)
- [`storage-architecture.mmd`](assets/diagrams/storage-architecture.mmd)

These are Mermaid diagrams so they can be rendered directly by GitHub and reused in documentation.

## Key documentation

- [Architecture overview](docs/architecture/README.md)
- [Enterprise foundation scenario](07-end-to-end-scenarios/enterprise-foundation/README.md)
- [RBAC implementation](01-identity-and-governance/rbac/README.md)
- [Monitoring implementation](05-monitoring-and-maintenance/azure-monitor/README.md)
- [Blob Storage implementation](02-storage/blob-storage/README.md)
- [Storage security notes](02-storage/security/README.md)
- [Storage lifecycle and data protection](02-storage/lifecycle-management/README.md)
- [Troubleshooting notes](docs/troubleshooting/README.md)

## Repository structure

| Path | Purpose |
| --- | --- |
| `00-setup/` | Subscription, tooling, naming, and environment readiness tasks. |
| `01-identity-and-governance/` | Microsoft Entra ID, RBAC, Azure Policy, locks, and tags. |
| `02-storage/` | Storage accounts, Blob Storage, Azure Files, security, and lifecycle management. |
| `03-compute/` | Virtual machines, scale sets, App Service, and container-based workloads. |
| `04-networking/` | Virtual networks, NSGs, load balancing, DNS, and hybrid connectivity. |
| `05-monitoring-and-maintenance/` | Azure Monitor, Log Analytics, backup, recovery, and update operations. |
| `06-automation-and-iac/` | ARM, Bicep, Terraform, PowerShell, and Azure CLI automation assets. |
| `07-end-to-end-scenarios/` | Integrated enterprise scenarios that combine multiple AZ-104 domains. |
| `assets/` | Diagrams and screenshots used by lab guides and evidence packs. |
| `docs/` | Architecture notes, operational runbooks, and troubleshooting references. |
| `scripts/` | Reusable helper scripts for lab deployment and validation. |
| `templates/` | Lab guide, checklist, and naming templates for new exercises. |
| `evidence/` | Completion records, assessment notes, and cost reports. |

## Suggested workflow

1. Complete `00-setup` before starting domain labs.
2. Copy `templates/lab-guide/LAB_TEMPLATE.md` into the relevant module folder for each new exercise.
3. Capture screenshots and command output in `evidence/` as each lab is completed.
4. Keep infrastructure code in `06-automation-and-iac/` and link it from the matching lab guide.
5. Record clean-up steps for every deployed resource to control Azure spend.

## Not yet implemented

The following topics were discussed as future lab items but are not documented as completed resources yet:

- Storage private endpoint and Private DNS.
- SAS-based temporary Blob access.
- Backup and restore testing.
- Azure Policy, locks, and tagging enforcement.
- Infrastructure as Code conversion.
