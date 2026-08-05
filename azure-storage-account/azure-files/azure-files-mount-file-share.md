# Mount the Azure File Share

## Overview

After the Storage Account has been integrated with Active Directory and the required permissions have been assigned, the Azure File Share can be mounted on a Windows client.

Users authenticate using their Active Directory credentials. No Storage Account Key or Shared Access Signature (SAS) is required.

---

# Prerequisites

Before mounting the Azure File Share, verify the following:

- Active Directory authentication has been configured.
- The user has the required Share-Level Permissions.
- NTFS permissions have been assigned.
- The client is joined to the Active Directory domain.
- Network connectivity to the Storage Account is available.
- TCP Port **445** is reachable.

---

# Determine the UNC Path

The Azure File Share is accessed using its UNC path.

```text
\\<storage-account-name>.file.core.windows.net\<share-name>
```

Example:

```text
\\stfilesdemo001.file.core.windows.net\documents
```

---

# Mount Using File Explorer

Open **File Explorer**.

↓

Right-click **This PC**

↓

**Map network drive**

↓

Choose a drive letter.

↓

Enter the UNC path.

Example:

```text
\\stfilesdemo001.file.core.windows.net\documents
```

Enable:

- Reconnect at sign-in

Select **Finish**.

Windows automatically uses the current Active Directory credentials.

> Screenshot:
>
> Map Network Drive

---

# Mount Using Command Prompt

The Azure File Share can also be mapped using the **net use** command.

```cmd
net use Z: \\stfilesdemo001.file.core.windows.net\documents
```

To make the mapping persistent:

```cmd
net use Z: \\stfilesdemo001.file.core.windows.net\documents /persistent:yes
```

---

# Mount Using PowerShell

PowerShell provides an alternative method.

```powershell
New-PSDrive `
    -Name "Z" `
    -PSProvider FileSystem `
    -Root "\\stfilesdemo001.file.core.windows.net\documents" `
    -Persist
```

The mapped drive appears in Windows Explorer like any other network drive.

---

# Verify the Connection

After mounting the file share:

- Open the mapped drive.
- Create a new folder.
- Create a test file.
- Modify the file.
- Delete the file.
- Verify access to existing folders.

If all operations succeed, both Share-Level Permissions and NTFS permissions have been configured correctly.

---

# Verify Kerberos Authentication

To verify that Kerberos authentication is being used, display the current Kerberos tickets.

```cmd
klist
```

The output should contain a ticket for the Azure File Share service.

---

# Disconnect the File Share

To remove the mapped drive:

Command Prompt:

```cmd
net use Z: /delete
```

PowerShell:

```powershell
Remove-PSDrive -Name Z
```

---

# Common Issues

| Problem | Possible Cause |
|----------|----------------|
| Access Denied | Missing Share-Level Permission |
| Access Denied | Missing NTFS Permission |
| Network path not found | Incorrect UNC path |
| System error 53 | Network connectivity or DNS issue |
| System error 67 | File Share does not exist |
| System error 86 | Authentication failed |
| System error 1326 | Invalid credentials |
| Port 445 unavailable | Firewall or ISP blocks SMB traffic |

---

# Best Practices

- Always use identity-based authentication instead of Storage Account Keys.
- Map drives using the DNS name of the Storage Account.
- Use persistent mappings only when appropriate.
- Verify Kerberos authentication after the initial configuration.
- Disconnect and reconnect the drive after permission changes if necessary.
