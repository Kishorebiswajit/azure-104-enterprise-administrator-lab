# Blob Storage Implementation

This lab documents the Blob Storage work completed in the AZ-104 enterprise environment.

## Implemented resources

| Component | Value |
| --- | --- |
| Resource group | `RG-AZ104-Storage` |
| Region | Central India |
| Performance | Standard |
| Redundancy | LRS |
| Access tier | Hot |
| Blob container | `application-files` |
| Container access level | Private, no anonymous access |

The final globally unique storage account name was not captured in the project notes, so this documentation refers to it by role rather than inventing a name.

## Storage account settings configured

| Area | Setting |
| --- | --- |
| Secure transfer | Required |
| Anonymous container access | Disabled |
| Storage account key access | Enabled for the lab |
| Portal authorization preference | Microsoft Entra authorization enabled |
| Minimum TLS | TLS 1.2 |
| Hierarchical namespace | Disabled |
| SFTP | Disabled |
| NFS v3 | Disabled |
| Access tier | Hot |
| SMB encryption in transit | Enabled |

## Blob container

The container `application-files` was created with private access:

```text
Storage account
    -> Blob service
        -> application-files
            -> uploaded test blob(s)
```

The lab tested uploading a small file to the private container after correcting storage firewall access.

## Data protection state

Configured:

- Blob soft delete — 7 days.
- Container soft delete — 7 days.
- Azure Files soft delete — 7 days.

**Blob versioning is currently disabled.** Older project notes that said versioning was enabled were incorrect and have been corrected.

## Storage access validation

The lab validated Microsoft Entra data-plane access using `reader@Kishoree.onmicrosoft.com` with the `Storage Blob Data Reader` role.

| Operation | Result |
| --- | --- |
| View/download blobs | Allowed |
| Upload blobs | Denied |
| Delete blobs | Denied |

## Real-world purpose

Blob Storage can provide centralized storage for:

- Application documents.
- Reports.
- Images and media.
- Export files.
- Logs and backups.
- User-uploaded content.

The architectural goal is to keep important application data separate from VM-local disks so the application tier can be replaced or scaled independently.

## Diagram

See [`../../../assets/diagrams/storage-architecture.mmd`](../../../assets/diagrams/storage-architecture.mmd).
