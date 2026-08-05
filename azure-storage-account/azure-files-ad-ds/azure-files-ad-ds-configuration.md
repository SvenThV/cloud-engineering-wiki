# Enable Active Directory Authentication

After creating the Storage Account and Azure File Share, identity-based authentication must be enabled.

Azure Files supports three identity providers:

- Active Directory Domain Services (AD DS)
- Microsoft Entra Kerberos
- Microsoft Entra Domain Services

This guide uses **Active Directory Domain Services (AD DS)**.

---

# What Happens During This Step?

Enabling AD DS authentication establishes a trust relationship between the Azure Storage Account and the on-premises Active Directory.

Unlike a traditional Windows File Server, Azure Files cannot join the domain itself. Instead, Azure creates an Active Directory computer or service account that represents the Storage Account.

During authentication:

- the client requests a Kerberos ticket from the Domain Controller
- the Domain Controller validates the user's identity
- Azure Files validates the Kerberos ticket against the Active Directory object
- access is granted if both Azure RBAC and NTFS permissions allow it

---

# Azure Portal

Navigate to:

Storage Account

↓

**File shares**

↓

**Identity-based access**

↓

Select

**Active Directory Domain Services**

The page should initially show:

```

Identity-based access

Not configured

```

Select **Configure**.

At this point Azure only prepares the Storage Account.

The actual Active Directory integration is completed later using AzFilesHybrid.

> Screenshot:
>
> Identity-based access configuration

---

# Why AzFilesHybrid Is Required

Azure cannot automatically create the required objects inside your on-premises Active Directory.

Microsoft provides the **AzFilesHybrid** PowerShell module to automate this process.

AzFilesHybrid performs tasks such as:

- Creating the Active Directory computer account
- Registering the required Service Principal Names (SPNs)
- Configuring Kerberos settings
- Updating the Storage Account authentication configuration
- Validating the deployment

Without AzFilesHybrid, Azure Files cannot authenticate users against Active Directory.

---

# Install AzFilesHybrid

Download the latest release from Microsoft's GitHub repository.

Extract the archive to a local directory.

Open an elevated PowerShell session.

Import the module.

```powershell
Import-Module AzFilesHybrid
```

Verify that the module has been loaded.

```powershell
Get-Module AzFilesHybrid
```

---

# Authenticate to Azure

Sign in to Azure.

```powershell
Connect-AzAccount
```

If multiple subscriptions exist:

```powershell
Get-AzSubscription
```

Select the correct subscription.

```powershell
Set-AzContext -Subscription "<Subscription Name>"
```

---

# Join the Storage Account to Active Directory

The following cmdlet creates the Active Directory object and configures Azure Files for Kerberos authentication.

```powershell
Join-AzStorageAccount `
    -ResourceGroupName "rg-storage" `
    -StorageAccountName "stfilesdemo001" `
    -SamAccountName "AZUREFILES01" `
    -DomainAccountType ComputerAccount `
    -OrganizationalUnitDistinguishedName "OU=Servers,DC=contoso,DC=local"
```

Depending on your environment, additional parameters may be required.

The cmdlet performs most of the required Active Directory configuration automatically.

---

# What Does Join-AzStorageAccount Do?

The cmdlet performs several operations automatically.

- Creates an Active Directory computer account
- Registers the required SPNs
- Generates a Kerberos secret
- Stores the secret securely
- Configures the Storage Account for AD DS authentication
- Validates the Active Directory configuration

This replaces a large number of manual configuration steps.

---

# Verify the Configuration

Microsoft provides a validation cmdlet.

```powershell
Debug-AzStorageAccountAuth `
    -StorageAccountName "stfilesdemo001" `
    -ResourceGroupName "rg-storage"
```

The command checks:

- Active Directory object
- Kerberos configuration
- SPNs
- Storage Account settings
- Authentication status

Resolve any reported issues before continuing.

---

# Verify the Computer Object

Open **Active Directory Users and Computers**.

Navigate to the Organizational Unit specified during the deployment.

Verify that the Storage Account object has been created successfully.

Example:

```text
OU=Servers
│
├── DC01
├── FILE01
└── AZUREFILES01
```

If the object exists and the validation command completes successfully, the Active Directory integration is complete.

The next step is configuring Share-Level Permissions using Azure RBAC.
