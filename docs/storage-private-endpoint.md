# Storage Private Endpoint

Private Endpoint `PE-AZ104-Storage` was created for `kishorestorage1` in `snet-app`. The endpoint uses private IP `10.10.2.5` and the Private DNS zone `privatelink.blob.core.windows.net` linked to `VNet-AZ104-Enterprise`.

Validation from `VM-AZ104-App` confirmed DNS resolution to `10.10.2.5` and authenticated Blob access using the VM system-assigned managed identity with `Storage Blob Data Reader`.

Public network access remains enabled for controlled administrative access.
