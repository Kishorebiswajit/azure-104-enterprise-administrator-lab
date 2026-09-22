# Enterprise Foundation Scenario

This scenario combines the AZ-104 domains already completed in the lab: networking, compute, RBAC, monitoring, and storage.

## Business scenario

The environment represents a small enterprise application foundation:

- A management tier for administration access.
- A web tier running Nginx.
- An app tier running a Python application service.
- Centralized Blob Storage for application files.
- Monitoring and alerts for operational visibility.
- RBAC separation between compute, network, read-only, and owner responsibilities.

## Implemented architecture

| Layer | Implemented configuration |
| --- | --- |
| Network | `VNet-AZ104-Enterprise` in `RG-AZ104-Network`, address space `10.10.0.0/16`, with management, web, and app subnets. |
| Secure access | Bastion and NSG segmentation were included in the network foundation. |
| Outbound connectivity | NAT Gateway included in the network foundation. |
| Compute | `VM-AZ104-Management`, `VM-AZ104-Web`, and `VM-AZ104-App` in `RG-AZ104-COMPUTE`. |
| Workload | Nginx on the web tier and a Python app running with systemd on the app tier. |
| Storage | Private Blob container `application-files` in a storage account under `RG-AZ104-Storage`. |
| Monitoring | AMA, DCR, Log Analytics, Action Group, and CPU alerts for all three VMs. |
| RBAC | Least-privilege testing for VM operator, network admin, reader, and owner roles. |

## Validation completed

- The three VMs were listed and confirmed in `RG-AZ104-COMPUTE`.
- `VNet-AZ104-Enterprise` was confirmed in `RG-AZ104-Network`.
- The VM operator role could access compute resources but was denied network resource access.
- Azure Monitor Agent was installed successfully on all three VMs.
- DCR associations were created for management, web, and app VMs.
- CPU alerts were created and verified as enabled.
- Blob upload to `application-files` was tested.
- Storage firewall behavior was tested and corrected by allowing the public client IP.
- Reader blob access was tested using Microsoft Entra authorization instead of storage access key authentication.

## Diagram

See [`../../assets/diagrams/enterprise-architecture.mmd`](../../assets/diagrams/enterprise-architecture.mmd).
