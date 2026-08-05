# Azure Files

## Overview

Azure Files is a fully managed file sharing service in Microsoft Azure that provides SMB and NFS file shares.

This section contains implementation guides and reference documentation for configuring Azure Files with **Active Directory Domain Services (AD DS)** authentication.

The documentation focuses on practical implementation from the perspective of an Azure Cloud Engineer.

---

# Documentation

| Article | Description |
|---------|-------------|
| [Azure Files Authentication using Active Directory Domain Services](azure-files-ad-ds-authentication.md) | Introduction, architecture and authentication concepts |
| [Azure Files AD DS Configuration](azure-files-ad-ds-configuration.md) | Configure Azure Files for Active Directory Domain Services authentication |
| [Share-Level Permissions](azure-files-share-level-permissions.md) | Configure Azure RBAC permissions for Azure File Shares |
| [NTFS Permissions](azure-files-ntfs-permissions.md) | Configure Windows NTFS permissions |
| [Mount Azure File Share](azure-files-mount-file-share.md) | Connect an Azure File Share to a Windows client |
| [Validation](azure-files-validation.md) | Verify the deployment and authentication |
| [Troubleshooting](azure-files-troubleshooting.md) | Diagnose and resolve common Azure Files issues |

---

# Authentication Methods

Azure Files supports multiple identity providers.

| Authentication Method | Typical Scenario |
|-----------------------|------------------|
| Active Directory Domain Services (AD DS) | Hybrid environments with on-premises Active Directory |
| Microsoft Entra Kerberos | Cloud-first environments |
| Microsoft Entra Domain Services | Managed domain services |

This documentation currently focuses on **Active Directory Domain Services (AD DS)**.

---

# Implementation Workflow

```text
Create Storage Account
        │
        ▼
Create Azure File Share
        │
        ▼
Configure AD DS Authentication
        │
        ▼
Join Storage Account to Active Directory
        │
        ▼
Configure Share-Level Permissions
        │
        ▼
Configure NTFS Permissions
        │
        ▼
Mount Azure File Share
        │
        ▼
Validate Deployment
        │
        ▼
Troubleshooting
```

---

# Prerequisites

- Azure Subscription
- Storage Account
- Azure File Share
- Active Directory Domain Services
- Domain-joined Windows client
- Azure PowerShell
- AzFilesHybrid
- Network connectivity to Azure Storage

---

# Related Azure Services

- Azure Storage Account
- Azure RBAC
- Microsoft Entra ID
- Active Directory Domain Services
- Azure Private Endpoint
- Azure DNS
- Azure VPN Gateway
