---

# Configure Share-Level Permissions

After the Storage Account has been successfully joined to Active Directory, users still cannot access the Azure File Share.

Before NTFS permissions are evaluated, Azure Files first checks the **Share-Level Permissions**.

These permissions are configured using **Azure Role-Based Access Control (Azure RBAC)**.

Only after the share-level permission check succeeds are NTFS permissions evaluated.

```text
User
 │
 ▼
Share-Level Permissions (Azure RBAC)
 │
 ▼
NTFS Permissions
 │
 ▼
Access Granted
```

---

# Built-in Azure RBAC Roles

Azure provides several built-in roles for Azure Files.

| Role | Description |
|------|-------------|
| Storage File Data SMB Share Reader | Read-only access |
| Storage File Data SMB Share Contributor | Read, write and delete files |
| Storage File Data SMB Share Elevated Contributor | Read, write, delete and modify NTFS ACLs |
| Storage File Data SMB Share Privileged Contributor | Administrative access that can override existing ACLs |
| Storage File Data SMB Share Privileged Reader | Read access that can bypass existing ACLs |

For most user scenarios, **Storage File Data SMB Share Contributor** is the recommended role.

---

# Share-Level Permissions vs NTFS Permissions

A common misconception is that Azure RBAC replaces NTFS permissions.

This is **not** the case.

Azure Files uses two independent authorization layers.

| Layer | Managed In |
|--------|------------|
| Share-Level Permissions | Azure RBAC |
| File & Folder Permissions | NTFS ACLs |

Both layers must allow access.

Example:

```text
Azure RBAC
Contributor
        │
        ▼
NTFS
No Access
        │
        ▼
Access Denied
```

Likewise, granting NTFS permissions alone is not sufficient if no Share-Level Permission has been assigned.

---

# Assign Permissions in the Azure Portal

Navigate to:

Storage Account

↓

**File shares**

↓

Select the file share

↓

**Access Control (IAM)**

↓

**Add**

↓

**Add role assignment**

Choose one of the Azure Files SMB roles.

Select the Microsoft Entra user or group.

Save the assignment.

> Screenshot:
>
> Add role assignment

---

# Assign Permissions using PowerShell

Assign the **Storage File Data SMB Share Contributor** role.

```powershell
$scope = "/subscriptions/<subscription-id>/resourceGroups/<resource-group>/providers/Microsoft.Storage/storageAccounts/stfilesdemo001/fileServices/default/fileshares/documents"

New-AzRoleAssignment `
    -ObjectId "<ObjectId>" `
    -RoleDefinitionName "Storage File Data SMB Share Contributor" `
    -Scope $scope
```

The **ObjectId** refers to the Microsoft Entra ID object representing the user or group.

---

# Assign Permissions to Groups

Whenever possible, assign permissions to Active Directory groups instead of individual users.

Advantages:

- Easier administration
- Centralized permission management
- Reduced number of Azure RBAC assignments
- Better scalability

Microsoft also recommends assigning permissions to groups rather than individual accounts whenever possible.

---

# Default Share-Level Permissions

Instead of assigning Azure RBAC roles to individual users or groups, Azure also supports a **Default Share-Level Permission**.

This grants the same share-level access to **all authenticated users**.

Typical scenarios include:

- Identities are not synchronized to Microsoft Entra ID.
- Computer accounts require access.
- Legacy Active Directory environments.
- Cross-tenant synchronization scenarios.

For most enterprise environments, assigning Azure RBAC roles to specific users or groups is the recommended approach.

---

# Verify Share-Level Permissions

After assigning permissions:

1. Open the Storage Account.
2. Navigate to the File Share.
3. Open **Access Control (IAM)**.
4. Verify the role assignment.
5. Wait several minutes for Azure RBAC propagation.

Permission changes usually become effective within approximately 30 minutes, although propagation can sometimes take longer. :contentReference[oaicite:0]{index=0}

---

# Best Practices

- Assign permissions to groups instead of individual users.
- Apply the principle of least privilege.
- Avoid assigning privileged roles unless required.
- Use Azure RBAC only for Share-Level Permissions.
- Manage file and folder permissions using NTFS ACLs.
- Regularly review Azure RBAC assignments.
