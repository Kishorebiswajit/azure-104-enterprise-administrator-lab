# Troubleshooting

This section records issues encountered and resolved during the AZ-104 enterprise administrator lab.

## Storage firewall blocked Blob access

### Symptom

The private Blob container returned a 403-style authorization/network error after the storage account was restricted to selected networks and IP addresses.

### Cause

The lab client was not allowed by the storage firewall.

### Resolution

The approved public client IP used by the lab was added to the storage firewall. The actual IP is intentionally omitted from this public repository.

### Lesson

Authentication and network authorization are separate. A user can have correct Azure permissions but still be blocked by storage firewall rules.

## Blob upload appeared to work for a read-only user

### Symptom

`reader@Kishoree.onmicrosoft.com` appeared able to upload to Blob Storage even though the account had only `Storage Blob Data Reader`.

### Cause

The portal was using storage account access key authentication instead of Microsoft Entra user authentication.

### Resolution

The test was repeated using Microsoft Entra user authentication. Read/download succeeded while upload and delete were denied.

### Lesson

Always confirm the authentication method when testing storage RBAC.

## Web VM had no outbound internet access

### Symptom

Package installation/update commands from `VM-AZ104-Web` initially timed out.

### Cause

The workload subnet had outbound access disabled without a NAT Gateway providing explicit outbound connectivity.

### Resolution

A NAT Gateway was deployed and associated with the workload subnet. Package installation and Nginx maintenance then worked.

### Lesson

When subnet default outbound access is disabled, provide an explicit outbound path such as NAT Gateway.

## App VM was initially exposed by a public IP

### Symptom

The app VM temporarily had a public IP during early configuration.

### Resolution

The public IP was detached/deleted. The app tier now uses private addressing only, with private management access through the VNet/Bastion path.

### Lesson

Application tiers that do not require direct internet ingress should not retain unnecessary public IP exposure.

## SSH private-key permissions on Windows

### Symptom

Windows SSH rejected the VM private key because the key file permissions were too broad.

### Resolution

The private-key file ACL was restricted to the required Windows user before retrying SSH.

### Lesson

OpenSSH private keys must be protected with appropriate filesystem permissions.

## Bastion Developer SKU one-session behavior

### Symptom

Opening another Bastion Developer connection disconnected the previous VM session.

### Cause

Bastion Developer uses shared infrastructure and supports one active VM connection at a time.

### Resolution

The behavior was treated as a SKU limitation rather than a VM/network failure. Private SSH was also used for management-to-app administration.

### Lesson

Know the capabilities and limitations of the Bastion SKU selected for a lab.

## Data Collection Rule creation syntax

### Symptom

The Azure CLI failed to parse the `--destinations` argument while creating `DCR-AZ104-Linux`.

### Resolution

A JSON definition file was used to create the Data Collection Rule.

### Lesson

When structured Azure CLI arguments fail, a JSON definition can be a reliable alternative.

## DCR association listing error

### Symptom

Listing DCR associations returned a CLI extension error about a missing `resourceUri`.

### Resolution

The association was verified using the resource-specific command instead of the broader list command.

### Lesson

A CLI extension error does not necessarily mean the Azure resource failed. Verify the resource directly before changing working infrastructure.

## Action Group email receiver syntax

### Symptom

Updating the Action Group with a raw `emailReceivers` structure failed because the request content was missing `emailAddress`.

### Resolution

The email receiver was added using the CLI-supported `--add-action email` syntax.

### Lesson

Use the CLI-supported helper syntax for Action Group receivers when direct object updates fail.
