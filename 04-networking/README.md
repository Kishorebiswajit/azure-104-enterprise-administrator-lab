# 04 - Networking

Labs for Azure virtual networking, secure traffic flow, load balancing, name resolution, and hybrid connectivity.

## Implemented lab

The current project includes:

- `VNet-AZ104-Enterprise`
- Three segmented subnets.
- NAT Gateway.
- Azure Bastion Developer SKU.
- Three subnet-level NSGs.
- Validated management-to-app SSH and web-to-app TCP/8080 paths.

See the [implemented VNet documentation](virtual-networks/README.md) and [NSG documentation](network-security-groups/README.md) for the current configuration and validation results.

## Folders

| Path | Purpose |
| --- | --- |
| `virtual-networks/` | VNet, subnet, peering, route table, and IP planning labs. |
| `network-security-groups/` | NSG rules, application security groups, and traffic validation. |
| `load-balancing/` | Load Balancer and Application Gateway exercises. |
| `private-dns/` | Private DNS zones, records, links, and name resolution tests. |
| `vpn-and-hybrid-connectivity/` | VPN gateway and hybrid network design notes. |
