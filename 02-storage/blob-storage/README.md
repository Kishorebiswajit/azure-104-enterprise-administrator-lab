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

The final globally unique storage account name was not captured in the conversation, so this documentation refers to it by role rather than inventing a name.

## Storage account settings configured

| Area | Setting |
| --- | --- |
| Secure transfer | Required for REST API operations. |
| Anonymous container access | Disabled. |
| Storage account key access | Enabled for the lab. |
| Portal authorization preference | Default to Microsoft Entra authorization enabled. |
| Minimum TLS | TLS 1.2. |
| Hierarchical namespace | Disabled. |
| SFTP | Disabled. |
| NFS v3 | Disabled. |
| Access tier | Hot. |
| SMB encryption in transit | Enabled. |

## Blob container

The container `application-files` was created with private access:

```text
Storage account
    -> Blob service
        -> application-files
            -> uploaded test blob(s)
```

The lab tested uploading a small file to the private container after fixing storage firewall access.

## Real-world purpose

In a production application, Blob Storage is commonly used for:

- Application documents.
- Reports.
- Images and media.
- Export files.
- Logs and backups.
- User-uploaded content.

The key architectural idea is that important application data should not live only on a VM disk. The app tier can be replaced or scaled while files remain in centralized cloud storage.

## Diagram

See [`../../../assets/diagrams/storage-architecture.mmd`](../../../assets/diagrams/storage-architecture.mmd).
