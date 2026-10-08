# Network Security Groups Implementation

This document records the NSGs used to segment the three-tier lab network.

## NSG inventory

| NSG | Associated subnet | Purpose |
| --- | --- | --- |
| `NSG-AZ104-Management` | `snet-management` | Management access |
| `NSG-AZ104-Workload` | `snet-workload` | Web tier ingress |
| `NSG-AZ104-App` | `snet-app` | Private app-tier access |

## Management NSG

`NSG-AZ104-Management` protects the management subnet.

SSH access was restricted to the approved administrative source used during the lab.

The management NSG was intentionally not redesigned during later troubleshooting once the required access was working.

## Workload NSG

`NSG-AZ104-Workload` allows the web tier's required HTTP/HTTPS traffic:

| Priority | Rule | Protocol | Port | Action |
| --- | --- | --- | --- | --- |
| 100 | HTTP | TCP | 80 | Allow |
| 110 | HTTPS | TCP | 443 | Allow |

The Web VM does not require public SSH for the application design.

## App NSG

`NSG-AZ104-App` enforces the application-tier traffic model:

| Priority | Source | Protocol | Port | Action | Purpose |
| --- | --- | --- | --- | --- | --- |
| 100 | `10.10.1.0/24` | TCP | 8080 | Allow | Web → App |
| 110 | `10.10.0.0/24` | TCP | 22 | Allow | Management → App |

## Validation

### Management → App

```text
Source: 10.10.0.0/24
Destination: 10.10.2.4
Port: 22
Result: Allowed
```

The management VM successfully connected to the app VM over private SSH.

### Web → App

```text
Source: 10.10.1.0/24
Destination: 10.10.2.4
Port: 8080
Result: Allowed
```

The application service was reachable over the intended application port.

### Web → App SSH

```text
Source: 10.10.1.0/24
Destination: 10.10.2.4
Port: 22
Result: Denied
```

This negative test confirms that the app tier does not expose SSH to the web tier.

## Security principle demonstrated

The NSG design follows least privilege:

- Allow only the ports required by each tier.
- Keep the app tier private.
- Separate management traffic from application traffic.
- Validate both positive and negative traffic paths.

## Future networking security work

- Application Security Groups.
- Azure Firewall.
- Private Link.
- Private DNS.
- Centralized network monitoring.
