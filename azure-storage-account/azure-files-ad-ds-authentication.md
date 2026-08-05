# Azure Files Authentication using Active Directory Domain Services (AD DS)

## Overview

Azure Files provides fully managed SMB file shares that can be accessed from Windows, Linux, and macOS.

To preserve existing user identities and NTFS permissions, Azure Files supports identity-based authentication. In hybrid environments, authentication is commonly performed using an on-premises Active Directory Domain Services (AD DS) deployment.

With this approach, users authenticate using their existing Active Directory accounts without requiring storage account keys or SAS tokens.

This guide describes how to configure Azure Files with Active Directory Domain Services authentication from the perspective of an Azure Cloud Engineer.

---

# Architecture

```text
                Active Directory Domain Services
                ┌───────────────────────────────┐
                │                               │
                │  Domain Controller            │
                │  Kerberos Authentication      │
                │                               │
                └──────────────┬────────────────┘
                               │
                               │
                               ▼
                 Azure Storage Account
          (Identity-based Authentication)
                               │
                               ▼
                     Azure File Share (SMB)
                               │
                               ▼
                     Windows Domain Client
```

---

# Authentication Options

Azure Files currently supports three identity providers.

| Authentication Method | Typical Scenario |
|-----------------------|------------------|
| Active Directory Domain Services (AD DS) | Hybrid environments with an on-premises Active Directory |
| Microsoft Entra Kerberos | Cloud-first environments using Microsoft Entra ID |
| Microsoft Entra Domain Services | Organizations using managed domain services |

This guide focuses on **Active Directory Domain Services (AD DS)**.

---

# How Authentication Works

Unlike traditional SMB shares that reside directly on a Windows file server, Azure Files stores the data inside an Azure Storage Account.

The authentication process still relies on Kerberos provided by the on-premises Active Directory.

The simplified authentication flow is shown below.

```text
User
 │
 │ Logon using AD credentials
 ▼
Windows Client
 │
 │ Kerberos Ticket Request
 ▼
Domain Controller
 │
 │ Kerberos Ticket
 ▼
Azure File Share
 │
 ▼
Access Granted
```

Azure Storage validates the Kerberos ticket against the Active Directory object that represents the storage account.

---

# Permission Model

Azure Files uses two independent permission layers.

```text
Azure RBAC
(Share-Level Permission)
            │
            ▼
Windows NTFS Permissions
(File & Folder Permissions)
            │
            ▼
Effective Access
```

Both permission layers must allow access before a user can open files or folders.

Microsoft recommends assigning Azure RBAC permissions at the share level and using NTFS permissions for granular access control. :contentReference[oaicite:0]{index=0}

---

# Prerequisites

Before configuring Azure Files with AD DS authentication, ensure the following requirements are met.

## Azure

- Azure Subscription
- Resource Group
- Storage Account (StorageV2)
- Standard File Share (SMB)
- TCP Port 445 reachable
- Appropriate Azure RBAC permissions

## On-Premises

- Active Directory Domain Services
- Domain Controller
- Domain-joined Windows client
- Domain Administrator privileges
- Network connectivity between Azure and the domain controller

---

# Required Components

The solution consists of the following components.

| Component | Purpose |
|----------|---------|
| Storage Account | Hosts the Azure File Share |
| Azure File Share | Stores user files |
| Active Directory Domain Services | Provides Kerberos authentication |
| AzFilesHybrid | Joins the storage account to Active Directory |
| Azure RBAC | Controls share-level access |
| NTFS ACLs | Controls file and folder permissions |

---

# Deployment Workflow

The complete implementation typically follows these steps.

```text
Create Storage Account
        │
        ▼
Create Azure File Share
        │
        ▼
Enable AD DS Authentication
        │
        ▼
Join Storage Account to Active Directory
        │
        ▼
Assign Share-Level Permissions
        │
        ▼
Configure NTFS Permissions
        │
        ▼
Map Azure File Share
        │
        ▼
Validate Access
```

---

# Create the Storage Account

Create a General Purpose v2 Storage Account.

Recommended configuration:

| Setting | Value |
|----------|-------|
| Performance | Standard |
| Redundancy | LRS (Lab) |
| Storage Type | StorageV2 |
| Large File Shares | Optional |
| Secure Transfer | Enabled |

PowerShell example:

```powershell
New-AzStorageAccount `
    -ResourceGroupName "rg-storage" `
    -Name "stfilesdemo001" `
    -Location "Germany West Central" `
    -SkuName Standard_LRS `
    -Kind StorageV2
```

---

# Create the Azure File Share

Create a new SMB file share inside the Storage Account.

Portal:

Storage Account

↓

Data Storage

↓

Classic File Shares

↓

+ File Share

Example PowerShell:

```powershell
$ctx = (Get-AzStorageAccount `
    -ResourceGroupName "rg-storage" `
    -Name "stfilesdemo001").Context

New-AzStorageShare `
    -Context $ctx `
    -Name "documents" `
    -QuotaGiB 1024
```

At this point, the Azure File Share exists but still authenticates using storage account credentials.

The next step is enabling Active Directory authentication.
