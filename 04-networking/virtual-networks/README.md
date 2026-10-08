# Virtual Network Implementation

This document records the Azure networking foundation actually implemented for the AZ-104 enterprise administrator lab.

## VNet

| Property | Value |
| --- | --- |
| VNet | `VNet-AZ104-Enterprise` |
| Resource group | `RG-AZ104-Network` |
| Region | Central India |
| Address space | `10.10.0.0/16` |

## Subnet design

| Subnet | Address range | Purpose |
| --- | --- | --- |
| `snet-management` | `10.10.0.0/24` | Management VM |
| `snet-workload` | `10.10.1.0/24` | Web VM / workload tier |
| `snet-app` | `10.10.2.0/24` | Private application tier |

The subnet structure separates administrative, web, and application traffic into distinct network segments.

## VM placement

```text
VNet-AZ104-Enterprise
|
+-- snet-management 10.10.0.0/24
|     +-- VM-AZ104-Management 10.10.0.4
|
+-- snet-workload 10.10.1.0/24
|     +-- VM-AZ104-Web 10.10.1.4
|
+-- snet-app 10.10.2.0/24
      +-- VM-AZ104-App 10.10.2.4
```

## NAT Gateway

A NAT Gateway was deployed for the workload subnet.

### Why it was required

The workload subnet had default outbound access disabled. The Web VM initially could not reach Ubuntu package repositories.

### Resolution

The NAT Gateway provided explicit outbound internet connectivity for the workload subnet.

After NAT deployment, package operations and Nginx maintenance completed successfully.

## Azure Bastion

Azure Bastion was deployed in `RG-AZ104-Network`:

- Name: `VNet-AZ104-Enterprise-bastion`
- SKU: Developer
- Region: Central India
- Provisioning state: Succeeded

Bastion provides browser-based administration without requiring a public IP on the target VM.

The Developer SKU limitation of one active VM connection at a time was observed during the lab.

## Final network security model

The network is intentionally tiered:

```text
Management
    |
    | SSH 22
    v
App

Web
    |
    | TCP 8080
    v
App
```

The app tier is private and does not have a public IP.

## Validation

The following network tests were completed:

- VNet and subnet configuration verified.
- Management → App TCP/22 succeeded.
- Web → App TCP/8080 succeeded.
- Web → App TCP/22 failed as intended.
- Web VM outbound connectivity was restored through NAT Gateway.
- App VM public IP was removed.

## Future networking work

Not yet implemented:

- VNet peering.
- Azure Load Balancer.
- Application Gateway.
- Private DNS.
- VPN Gateway / hybrid connectivity.
- Storage private endpoint.
