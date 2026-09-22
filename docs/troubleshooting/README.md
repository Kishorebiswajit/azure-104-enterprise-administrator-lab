# Troubleshooting

This section records issues encountered and resolved during the AZ-104 enterprise administrator lab.

## Storage firewall blocked Blob access

### Symptom

The private Blob container returned a 403-style authorization/network error after the storage account was restricted to selected networks and IP addresses.

### Cause

The user's local machine was not allowed by the storage firewall.

Azure identified the public client IP as:

```text
152.57.125.49
```

The local machine's private Wi-Fi IP was:

```text
10.33.83.77
```

### Resolution

The public IP seen by Azure was added to the storage firewall. The private LAN IP was not used because Azure Storage cannot see that address across the public internet.

### Lesson

Authentication and network authorization are separate. A user can have correct Azure permissions but still be blocked by storage firewall rules.

## Blob upload appeared to work for a read-only user

### Symptom

`reader@Kishoree.onmicrosoft.com` appeared able to upload to Blob Storage even though the account had only `Storage Blob Data Reader`.

### Cause

The portal was using storage account access key authentication for the blob operation instead of Microsoft Entra user authentication.

### Resolution

The test was repeated using:

```text
Authentication method: Microsoft Entra user account
```

With Entra authorization, the reader role correctly allowed read access and denied upload/write access.

### Lesson

Always confirm the authentication method when testing storage RBAC. Access key authentication is not a valid proof of Entra/RBAC permissions.

## Data Collection Rule creation syntax

### Symptom

The Azure CLI failed to parse the `--destinations` argument while creating `DCR-AZ104-Linux`.

### Resolution

A JSON definition method was used for the Data Collection Rule instead of relying on the direct argument format.

### Lesson

Azure CLI syntax can vary by version and extension. When a structured argument fails, a JSON definition file can be more reliable.

## DCR association listing error

### Symptom

Listing DCR associations returned an extension error about a missing `resourceUri`.

### Resolution

The association was verified using the resource-specific command instead of the broader list command.

### Lesson

An Azure CLI extension error does not always mean the Azure resource failed. Verify using another resource-specific query before changing working infrastructure.

## Action Group email receiver syntax

### Symptom

Updating the action group with a raw `emailReceivers` structure failed because the request content was missing `emailAddress`.

### Resolution

The email receiver was added using:

```text
az monitor action-group update --add-action email ...
```

### Lesson

Use the CLI-supported action helper syntax for Action Group receivers when direct object updates fail.
