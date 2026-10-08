# AZ-104 Enterprise Administrator Lab

Hands-on Azure Administrator lab aligned with AZ-104 objectives and enterprise administration workflows.

This repository documents the Azure environment actually built and validated during the lab: enterprise resource organization, a three-tier Linux VM architecture, NSG segmentation, NAT Gateway, Bastion, least-privilege RBAC, Azure Monitor/Log Analytics, CPU alerting, and secure Blob Storage access testing.

## Current lab milestone

The completed implementation currently covers:

- Separate resource groups for network, compute, storage, and operations.
- `VNet-AZ104-Enterprise` in `RG-AZ104-Network` with:
  - `snet-management` — `10.10.0.0/24`
  - `snet-workload` — `10.10.1.0/24`
  - `snet-app` — `10.10.2.0/24`
- Three Ubuntu Linux VMs in `RG-AZ104-COMPUTE`:
  - `VM-AZ104-Management` — `10.10.0.4`
  - `VM-AZ104-Web` — `10.10.1.4`
  - `VM-AZ104-App` — `10.10.2.4`
- NSG-based segmentation for management, workload, and app traffic.
- NAT Gateway for outbound connectivity from the workload subnet.
- Azure Bastion Developer SKU for private VM administration.
- Web tier running Nginx on TCP/80.
- App tier running a Python HTTP service on TCP/8080 under systemd.
- Private Web → App TCP/8080 communication.
- App VM public IP removed; app tier is private.
- Management → App SSH validation through the private network.
- Least-privilege RBAC validation for VM operator, network admin, reader, and owner access patterns.
- Azure Monitor Agent installed on all three VMs.
- `LAW-AZ104-Enterprise` Log Analytics workspace.
- `DCR-AZ104-Linux` collecting `Microsoft-Perf` and `Microsoft-Syslog`.
- DCR associations for management, web, and app VMs.
- `AG-AZ104-Alerts` action group with email notification.
- CPU alerts for all three VMs with an average CPU threshold above 80%.
- Storage account in `RG-AZ104-Storage` with private Blob container `application-files`.
- Storage firewall/network access testing.
- Blob soft delete, container soft delete, and Azure Files soft delete configured for 7 days.
- Microsoft Entra/RBAC validation for `Storage Blob Data Reader`.

> **Documentation correction:** Blob versioning was checked during the lab and was **not enabled**. Any older documentation claiming otherwise has been corrected.

## Architecture diagrams

Diagram source files are stored in [`assets/diagrams`](assets/diagrams):

- [`enterprise-architecture.mmd`](assets/diagrams/enterprise-architecture.mmd)
- [`network-topology.mmd`](assets/diagrams/network-topology.mmd)
- [`rbac-access-model.mmd`](assets/diagrams/rbac-access-model.mmd)
- [`monitoring-architecture.mmd`](assets/diagrams/monitoring-architecture.mmd)
- [`storage-architecture.mmd`](assets/diagrams/storage-architecture.mmd)

## Key documentation

- [Current implementation state](docs/current-state.md)
- [Architecture overview](docs/architecture/README.md)
- [Enterprise foundation scenario](07-end-to-end-scenarios/enterprise-foundation/README.md)
- [VM implementation](03-compute/virtual-machines/README.md)
- [Virtual networking implementation](04-networking/virtual-networks/README.md)
- [NSG implementation and validation](04-networking/network-security-groups/README.md)
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

## Not yet implemented

The following remain future milestones and are not represented as completed Azure resources:

- Storage private endpoint and Private DNS.
- SAS-based temporary Blob access.
- Backup and restore testing.
- Azure Policy, locks, and tagging enforcement.
- Infrastructure as Code conversion.
- Additional load balancing and hybrid connectivity scenarios.
