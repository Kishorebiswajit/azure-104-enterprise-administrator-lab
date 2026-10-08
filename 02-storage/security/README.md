# Storage Security

This lab focused on secure Blob Storage access using private containers, storage networking, and Microsoft Entra/RBAC validation.

## Network access

The storage account was configured with:

```text
Public network access: Enabled
Scope: Selected virtual networks and IP addresses
Routing: Microsoft network routing
```

The lab used selected Azure network paths and an approved client public IP for testing. The exact selected network/IP list is intentionally not reproduced here because it was not captured as a stable project artifact.

> Security note: real client public IP addresses are intentionally omitted from this public repository.

## Firewall troubleshooting

When the storage firewall blocked the lab client, Azure returned a 403-style authorization/network error.

The important finding was that Azure Storage evaluates the **public client IP visible to the service**, not the client's private LAN address behind NAT.

The public repository therefore does not contain the actual client IP used during testing.

## Authentication methods

Two authentication paths were observed during testing:

| Method | Effect |
| --- | --- |
| Storage account access key | Broad storage access; not a valid test of reader RBAC permissions. |
| Microsoft Entra user account | Correct method for validating Azure RBAC data-plane permissions. |

The final RBAC test used Microsoft Entra user authentication.

## Data-plane RBAC

`reader@Kishoree.onmicrosoft.com` was assigned `Storage Blob Data Reader` at the storage account.

Expected and validated behavior:

| Operation | Result |
| --- | --- |
| View/download blobs | Allowed |
| Upload blobs | Denied |
| Delete blobs | Denied |

This proved the difference between read-only blob data access and contributor-level write access.

## Not yet implemented

- Private endpoint.
- Private DNS zone for storage.
- SAS token access.
- Disabling storage account key access.

These should be added only after they are configured and verified in Azure.
