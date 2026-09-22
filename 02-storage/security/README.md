# Storage Security

This lab focused on secure Blob Storage access using private containers, storage networking, and Microsoft Entra/RBAC validation.

## Network access

The storage account was configured with:

```text
Public network access: Enabled
Scope: Selected virtual networks and IP addresses
Routing: Microsoft network routing
```

The intended allowed Azure network paths were:

- Management subnet.
- App subnet.

The web subnet was not required for storage access in the current design.

## Firewall troubleshooting

When the storage firewall blocked the user's computer, Azure returned a 403-style authorization/network error and identified the public client IP:

```text
152.57.125.49
```

The local private Wi-Fi IP was:

```text
10.33.83.77
```

The lab confirmed that the storage firewall needs the public IP seen by Azure, not the private LAN address behind NAT.

## Authentication methods

Two authentication paths were observed during testing:

| Method | Effect |
| --- | --- |
| Storage account access key | Broad storage access; not a valid test of reader RBAC permissions. |
| Microsoft Entra user account | Correct method for validating Azure RBAC data-plane permissions. |

The final RBAC test used:

```text
Authentication method: Microsoft Entra user account
```

## Data-plane RBAC

`reader@Kishoree.onmicrosoft.com` was assigned `Storage Blob Data Reader` at the storage account.

Expected behavior:

| Operation | Result |
| --- | --- |
| View/download blobs | Allowed. |
| Upload blobs | Denied. |
| Delete blobs | Denied. |

This proved the difference between read-only blob data access and contributor-level write access.

## Not yet implemented

- Private endpoint.
- Private DNS zone for storage.
- SAS token access.
- Disabling storage account key access.

These should be added only after they are configured and verified in Azure.
