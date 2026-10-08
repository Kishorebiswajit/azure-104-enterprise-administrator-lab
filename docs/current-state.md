# AZ-104 Lab — Current State

This document is the source-of-truth summary of the implementation completed during the current lab milestone.

## Completed

| Domain | Status | Evidence / implementation |
| --- | --- | --- |
| Resource organization | Completed | Network, compute, and storage resource groups |
| VNet | Completed | `VNet-AZ104-Enterprise`, `10.10.0.0/16` |
| Subnets | Completed | Management, workload, app |
| NSGs | Completed | Management, workload, app segmentation |
| NAT Gateway | Completed | Workload subnet outbound connectivity |
| Bastion | Completed | Developer SKU |
| Linux VMs | Completed | Management, Web, App |
| Nginx | Completed | Web VM |
| Python application | Completed | App VM, TCP/8080 |
| Private app tier | Completed | App VM has no public IP |
| Tier-to-tier validation | Completed | Web → App 8080; Management → App 22 |
| RBAC | Completed | VM operator, network admin, reader, owner patterns |
| Azure Monitor Agent | Completed | Installed on all three VMs |
| DCR | Completed | Performance + syslog to Log Analytics |
| Log Analytics | Completed | `LAW-AZ104-Enterprise` |
| CPU alerts | Completed | Three VM alerts, CPU >80%, severity 2 |
| Storage | Completed | Private `application-files` container |
| Storage firewall | Completed | Network access tested |
| Storage data-plane RBAC | Completed | Reader read/download allowed; upload/delete denied with Entra auth |
| Storage soft delete | Completed | Blob/container/Azure Files, 7 days |
| Blob versioning | **Not completed** | Remains disabled |
| Troubleshooting documentation | Completed | Storage, NAT, SSH, Bastion, DCR, Action Group |

## Network address plan

```text
VNet-AZ104-Enterprise
10.10.0.0/16

snet-management
10.10.0.0/24
VM-AZ104-Management
10.10.0.4

snet-workload
10.10.1.0/24
VM-AZ104-Web
10.10.1.4

snet-app
10.10.2.0/24
VM-AZ104-App
10.10.2.4
```

## Monitoring chain

```text
Linux VMs
   |
Azure Monitor Agent
   |
DCR-AZ104-Linux
   |
LAW-AZ104-Enterprise
   |
CPU alerts
   |
AG-AZ104-Alerts
   |
Email notification
```

## Storage security state

The current storage design uses:

- Private Blob container.
- Selected network/IP access.
- Secure transfer.
- TLS 1.2 minimum.
- Microsoft Entra data-plane validation.
- Storage Blob Data Reader for the reader identity.
- 7-day soft-delete settings.

Not yet implemented:

- Private endpoint.
- Private DNS.
- SAS.
- Backup/restore.
- Disabling account-key access.

## Important public-repository hygiene

The repository documentation intentionally does not publish:

- Actual client public IP addresses.
- Private keys.
- Passwords.
- Access tokens.
- Storage account keys.
- Other credentials.

## Next milestones

1. Storage private endpoint + Private DNS.
2. SAS access testing.
3. Backup/restore.
4. Azure Policy and resource locks.
5. Infrastructure as Code with Bicep.
6. Additional load-balancing and hybrid-network labs.
