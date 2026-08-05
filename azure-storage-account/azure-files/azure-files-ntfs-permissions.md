# Configure NTFS Permissions

## Overview

After Share-Level Permissions have been assigned using Azure RBAC, access to individual files and folders is controlled by NTFS permissions.

Azure Files supports the same NTFS permission model as traditional Windows file servers.

NTFS permissions provide fine-grained access control for files and folders and are evaluated after Share-Level Permissions.

---

# Permission Evaluation

Azure Files evaluates permissions in the following order.

```text
User
 │
 ▼
Authentication (Kerberos)
 │
 ▼
Share-Level Permission (Azure RBAC)
 │
 ▼
NTFS Permissions
 │
 ▼
Effective Access
```

Both Share-Level Permissions and NTFS permissions must allow access.

---

# Share-Level Permissions vs NTFS Permissions

| Share-Level Permissions | NTFS Permissions |
|--------------------------|------------------|
| Configured in Azure | Configured in Windows |
| Azure RBAC | Windows ACLs |
| Controls access to the file share | Controls access to files and folders |
| Assigned to users or groups | Assigned to users or groups |
| Evaluated first | Evaluated second |

---

# Configure NTFS Permissions

After the Azure File Share has been mounted, NTFS permissions can be configured using standard Windows tools.

Typical methods include:

- File Explorer
- Computer Management
- PowerShell
- icacls

In many enterprise environments, configuring NTFS permissions is performed by the Windows or Active Directory administration team.

---

# Configure Permissions using File Explorer

Open the mounted Azure File Share.

Right-click the folder.

↓

Properties

↓

Security

↓

Edit

↓

Add the required users or Active Directory groups.

Assign the appropriate permissions.

> Screenshot:
>
> NTFS Security Settings

---

# Configure Permissions using PowerShell

Grant Modify permissions.

```powershell
icacls "Z:\Projects" `
    /grant "CONTOSO\Developers:(OI)(CI)(M)"
```

Grant Read permissions.

```powershell
icacls "Z:\Projects" `
    /grant "CONTOSO\Auditors:(OI)(CI)(RX)"
```

Remove permissions.

```powershell
icacls "Z:\Projects" `
    /remove "CONTOSO\TestUser"
```

Display the current ACL.

```powershell
icacls "Z:\Projects"
```

---

# Best Practices

- Assign permissions to Active Directory groups instead of individual users.
- Follow the principle of least privilege.
- Avoid assigning Full Control unless required.
- Use inherited permissions whenever possible.
- Separate administrative and user permissions.

---

# Common Permission Levels

| Permission | Typical Use Case |
|------------|------------------|
| Read | Read-only access |
| Modify | Read, create, edit and delete files |
| Full Control | Administrative access |

For most business users, **Modify** permissions are sufficient.

---

# Verify Effective Access

After assigning permissions:

- Sign in as the target user.
- Mount the Azure File Share.
- Create a test file.
- Modify the file.
- Delete the file.
- Verify that restricted folders remain inaccessible.

---

# Common Issues

| Problem | Possible Cause |
|----------|----------------|
| Access Denied | Missing Share-Level Permission |
| Access Denied | Missing NTFS Permission |
| Read works, Write fails | NTFS permission is Read only |
| Folder visible but cannot open | Missing NTFS permission on the folder |
| Permission changes not applied | Existing SMB session still active |

If permission changes are not immediately reflected, disconnect the mapped drive and reconnect it.
