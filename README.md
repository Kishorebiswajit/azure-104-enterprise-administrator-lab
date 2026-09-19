# AZ-104 Enterprise Administrator Lab

Hands-on Azure Administrator lab aligned with AZ-104 objectives and enterprise administration workflows.

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
