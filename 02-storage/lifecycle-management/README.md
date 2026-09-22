# Storage Lifecycle and Data Protection

This lab configured basic data protection settings for Blob Storage.

## Configured settings

| Setting | Lab configuration | Purpose |
| --- | --- | --- |
| Blob soft delete | Enabled, 7 days | Recover accidentally deleted blobs during the retention period. |
| Container soft delete | Enabled, 7 days | Recover accidentally deleted containers. |
| Blob versioning | Enabled | Recover previous versions after overwrite or modification. |
| Blob change feed | Disabled | Not required for the current lab. |
| Version-level immutability | Disabled | Not required for the current lab. |
| Azure Files soft delete | Enabled, 7 days | Recovery protection for file shares if used later. |

## Important distinction

Soft delete and versioning are not the same as a full backup strategy:

- Soft delete helps recover from accidental deletion.
- Versioning helps recover from accidental overwrites.
- Backup is a broader recovery strategy and has not yet been implemented in this lab.

## Future work

Possible next steps:

- Add lifecycle rules for moving old blobs to cool/cold tiers.
- Test blob version restore.
- Test soft-delete recovery.
- Add backup and recovery documentation after those steps are actually performed.
