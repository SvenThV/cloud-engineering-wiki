# Azure Files Troubleshooting

## Overview

This article describes common issues that may occur when configuring Azure Files with Active Directory Domain Services (AD DS) authentication.

The troubleshooting steps are ordered from basic connectivity checks to Active Directory validation and authentication diagnostics.

---

# Troubleshooting Workflow

Use the following order when troubleshooting Azure Files.

```text
Network Connectivity
        │
        ▼
DNS Resolution
        │
        ▼
Storage Account Configuration
        │
        ▼
AD DS Authentication
        │
        ▼
Share-Level Permissions
        │
        ▼
NTFS Permissions
        │
        ▼
Kerberos Authentication
        │
        ▼
Client Validation
```

---

# Storage Account Configuration

Verify the following:

- Storage Account exists
- Azure File Share exists
- Identity-based authentication is enabled
- Active Directory Domain Services is configured

Azure Portal

↓

Storage Account

↓

File shares

↓

Identity-based access

---

# Verify Network Connectivity

Azure Files requires SMB over TCP Port **445**.

Run:

```powershell
Test-NetConnection `
    <storage-account>.file.core.windows.net `
    -Port 445
```

Expected result:

```text
TcpTestSucceeded : True
```

If the test fails:

- Firewall blocks SMB
- ISP blocks Port 445
- VPN not connected
- Private Endpoint configuration incorrect

---

# Verify DNS Resolution

Check DNS.

```powershell
Resolve-DnsName <storage-account>.file.core.windows.net
```

If using Private Endpoints, verify that the Storage Account resolves to the private IP address.

---

# Verify Active Directory Integration

Open:

Active Directory Users and Computers

Verify that:

- the Storage Account computer object exists
- the object is enabled
- the object is located in the correct Organizational Unit

---

# Validate Azure Files Authentication

Run:

```powershell
Debug-AzStorageAccountAuth `
    -ResourceGroupName "rg-storage" `
    -StorageAccountName "stfilesdemo001"
```

The validation checks:

- Active Directory object
- Kerberos configuration
- SPNs
- Azure Storage configuration
- Encryption settings

Resolve all reported issues before continuing.

---

# Verify Share-Level Permissions

Open:

Storage Account

↓

File Share

↓

Access Control (IAM)

Verify that:

- the user or group has been assigned
- the correct Azure RBAC role is used
- the role assignment has propagated

---

# Verify NTFS Permissions

Open the mounted Azure File Share.

↓

Properties

↓

Security

Verify:

- User or group exists
- Correct NTFS permissions
- Inheritance configuration

---

# Verify Kerberos Authentication

Display the Kerberos tickets.

```cmd
klist
```

If no ticket exists:

- User is not authenticated
- Storage Account not joined correctly
- SPN missing
- Kerberos configuration incorrect

---

# Verify SMB Sessions

Display existing SMB connections.

```powershell
Get-SmbConnection
```

Disconnect stale connections.

```cmd
net use * /delete
```

Reconnect the Azure File Share afterwards.

---

# Verify User Identity

Display the current user.

```cmd
whoami
```

Display group memberships.

```cmd
whoami /groups
```

Confirm that the expected Active Directory groups are present.

---

# Common Error Messages

| Error | Possible Cause | Resolution |
|--------|----------------|------------|
| Access Denied | Missing Share-Level Permission | Verify Azure RBAC |
| Access Denied | Missing NTFS Permission | Verify NTFS ACLs |
| System error 53 | Network path not found | Verify DNS and Port 445 |
| System error 67 | File Share not found | Verify UNC path |
| System error 86 | Authentication failed | Verify Kerberos configuration |
| System error 1326 | Invalid credentials | Verify Active Directory account |
| Network path not found | DNS resolution failed | Verify DNS configuration |
| Logon failure | Kerberos authentication failed | Verify Storage Account integration |

---

# Useful Commands

Check Azure authentication.

```powershell
Connect-AzAccount
```

Check the current subscription.

```powershell
Get-AzContext
```

Display Storage Account information.

```powershell
Get-AzStorageAccount
```

Display Kerberos tickets.

```cmd
klist
```

Display SMB connections.

```powershell
Get-SmbConnection
```

Test SMB connectivity.

```powershell
Test-NetConnection `
    <storage-account>.file.core.windows.net `
    -Port 445
```

Resolve DNS.

```powershell
Resolve-DnsName `
    <storage-account>.file.core.windows.net
```

Display the current user.

```cmd
whoami
```

Display Active Directory group memberships.

```cmd
whoami /groups
```

---

# Best Practices

- Validate every deployment step before continuing.
- Test using a standard user account.
- Assign Azure RBAC permissions to groups instead of users.
- Apply the principle of least privilege.
- Verify both Azure RBAC and NTFS permissions.
- Test Kerberos authentication after the initial deployment.
- Document all configuration changes.
- Keep AzFilesHybrid up to date.
