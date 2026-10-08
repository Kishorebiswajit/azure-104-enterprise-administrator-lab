# Storage Lifecycle and Data Protection

This lab configured basic data protection settings for Blob Storage.

## Configured settings

| Setting | Lab configuration | Purpose |
| --- | --- | --- |
| Blob soft delete | Enabled, 7 days | Recover accidentally deleted blobs during the retention period. |
| Container soft delete | Enabled, 7 days | Recover accidentally deleted containers. |
| Blob versioning | **Disabled** | Not enabled in the final lab configuration. |
| Blob change feed | Disabled | Not required for the current lab. |
| Version-level immutability | Disabled | Not required for the current lab. |
| Azure Files soft delete | Enabled, 7 days | Recovery protection for file shares if used later. |

## Important distinction

Soft delete, versioning, and backup provide different recovery capabilities:

- Soft delete helps recover from accidental deletion.
- Blob versioning can help recover from accidental overwrites, but it is **not enabled in this lab**.
- Backup is a broader recovery strategy and has not yet been implemented.

## Future work

Possible next steps:

- Enable and test Blob versioning.
- Add lifecycle rules for moving old blobs to cool/cold tiers.
- Test blob soft-delete recovery.
- Add backup and recovery documentation after those steps are actually performed.
