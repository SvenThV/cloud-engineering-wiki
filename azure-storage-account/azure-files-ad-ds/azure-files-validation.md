# Validate the Azure Files Deployment

## Overview

After configuring Azure Files with Active Directory Domain Services (AD DS) authentication, the deployment should be validated to ensure that all components are working correctly.

Validation should include Azure configuration, Active Directory integration, authentication, permissions, and file access.

---

# Validation Checklist

Verify the following:

- Storage Account created successfully
- Azure File Share exists
- AD DS authentication enabled
- Storage Account joined to Active Directory
- Share-Level Permissions assigned
- NTFS permissions configured
- Azure File Share successfully mounted
- Kerberos authentication working
- File operations successful

---

# Verify the Storage Account

In the Azure portal, navigate to:

Storage Account

↓

File shares

↓

Identity-based access

Verify that:

- Active Directory Domain Services is enabled
- Configuration status is successful

---

# Verify Active Directory Integration

Open **Active Directory Users and Computers**.

Navigate to the Organizational Unit used during the deployment.

Verify that the Storage Account computer object exists.

Example:

```text
OU=Servers
│
├── DC01
├── FILE01
└── AZUREFILES01
```

---

# Verify Share-Level Permissions

Open the Azure portal.

Navigate to:

Storage Account

↓

File Share

↓

Access Control (IAM)

Verify that the required Azure RBAC roles have been assigned.

---

# Verify NTFS Permissions

Open the mounted Azure File Share.

↓

Right-click the folder.

↓

Properties

↓

Security

Verify that the expected Active Directory users or groups have the required permissions.

---

# Verify the Network Drive

Open Windows Explorer.

Confirm that:

- the mapped drive is visible
- folders can be opened
- files can be created
- files can be modified
- files can be deleted

---

# Verify Kerberos Authentication

Open Command Prompt.

Display the current Kerberos tickets.

```cmd
klist
```

Verify that a Kerberos ticket for the Azure File Share is present.

---

# Verify Network Connectivity

Test SMB connectivity.

```powershell
Test-NetConnection `
    stfilesdemo001.file.core.windows.net `
    -Port 445
```

Expected result:

```text
TcpTestSucceeded : True
```

---

# Verify DNS Resolution

Confirm that the Storage Account name resolves correctly.

```powershell
Resolve-DnsName stfilesdemo001.file.core.windows.net
```

---

# Functional Test

Perform the following operations.

- Create a folder.
- Create a file.
- Edit the file.
- Rename the file.
- Delete the file.

If all operations succeed, both Share-Level Permissions and NTFS permissions have been configured correctly.

---

# Validation Summary

| Validation | Status |
|------------|--------|
| Storage Account | ✅ |
| Azure File Share | ✅ |
| AD DS Authentication | ✅ |
| Computer Object | ✅ |
| Azure RBAC | ✅ |
| NTFS Permissions | ✅ |
| Kerberos Authentication | ✅ |
| SMB Connectivity | ✅ |
| File Operations | ✅ |

---

# Best Practices

- Validate every configuration step before proceeding.
- Test with a standard user account instead of an administrator.
- Verify both Azure RBAC and NTFS permissions.
- Test Kerberos authentication explicitly.
- Document the validation results for future reference.
