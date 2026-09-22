# RBAC Implementation

This lab validates least-privilege access control using Azure RBAC.

## Implemented users and access patterns

| Identity | Intended role pattern | Scope tested | Result |
| --- | --- | --- | --- |
| `KishoreJena@Kishoree.onmicrosoft.com` | Owner | Subscription/lab resources | Full administrative access. |
| `vm-operator@Kishoree.onmicrosoft.com` | Virtual Machine Contributor | `RG-AZ104-COMPUTE` | Could list compute resources. |
| `vm-operator@Kishoree.onmicrosoft.com` | No network role | `RG-AZ104-Network` | Denied access to VNet resources. |
| Network admin account | Network administration role pattern | Network resources | Network access validated in the lab. |
| `reader@Kishoree.onmicrosoft.com` | Reader | Subscription/resource visibility | Read access validated. |
| `reader@Kishoree.onmicrosoft.com` | Storage Blob Data Reader | Storage account | Blob read access validated; write/upload denied when using Entra authorization. |

## Management plane vs data plane

The storage RBAC portion of the lab demonstrated an important Azure distinction:

| Permission type | Example role | Controls |
| --- | --- | --- |
| Management plane | Reader | Visibility of Azure resources and configuration. |
| Data plane | Storage Blob Data Reader | Access to the actual blob data inside the storage account. |

The lab proved that the Azure `Reader` role alone is not the same as `Storage Blob Data Reader`.

## VM operator test

When signed in as `vm-operator@Kishoree.onmicrosoft.com`, compute access worked:

```text
VM-AZ104-App
VM-AZ104-Management
VM-AZ104-Web
```

The same account was denied when trying to list virtual networks in `RG-AZ104-Network`:

```text
AuthorizationFailed
Microsoft.Network/virtualNetworks/read
```

That confirms the VM operator role was scoped to compute responsibilities and did not grant unnecessary network access.

## Storage reader test

The `reader@Kishoree.onmicrosoft.com` account was assigned:

- `Reader` inherited at subscription level.
- `Storage Blob Data Reader` at the storage account.

Expected and validated behavior:

| Operation | Expected result |
| --- | --- |
| View storage resource | Allowed. |
| View/download blob data | Allowed with Microsoft Entra user authentication. |
| Upload blob data | Denied with Microsoft Entra user authentication. |
| Delete blob data | Denied. |

## Troubleshooting lesson

During testing, blob upload initially appeared to work for the reader account because Azure Portal was using storage access key authentication instead of Microsoft Entra user authentication.

The corrected test used:

```text
Authentication method: Microsoft Entra user account
```

This is an important real-world troubleshooting lesson: storage access keys can bypass the intended data-plane RBAC test, so administrators must confirm which authentication method the portal or tool is using.

## Diagram

See [`../../../assets/diagrams/rbac-access-model.mmd`](../../../assets/diagrams/rbac-access-model.mmd).
