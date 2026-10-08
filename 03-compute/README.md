# 03 - Compute

Labs for deploying, configuring, securing, scaling, and maintaining Azure compute workloads.

## Implemented lab

The current project includes a three-tier Linux VM implementation:

- `VM-AZ104-Management`
- `VM-AZ104-Web`
- `VM-AZ104-App`

See the [implemented VM documentation](virtual-machines/README.md) for the actual VM inventory, Nginx web tier, Python app service, private addressing, systemd configuration, and validation results.

## Folders

| Path | Purpose |
| --- | --- |
| `virtual-machines/` | VM deployment, disks, extensions, availability, and access. |
| `vm-scale-sets/` | Scale set deployment, autoscale, upgrade policy, and monitoring. |
| `app-service/` | App Service plans, deployment slots, configuration, and scaling. |
| `containers/` | Container instances and operational container scenarios. |
