# Create a Maintenance Configuration

## Overview

A Maintenance Configuration defines when and how Azure Update Manager installs operating system updates.

It specifies:

- Maintenance scope
- Maintenance schedule
- Update classifications
- Reboot behavior
- Target resources

---

## Prerequisites

Before creating a Maintenance Configuration, ensure that:

- Azure Update Manager is enabled.
- The target virtual machines are onboarded.
- The required permissions are available.

---

## Step 1 – Create a Maintenance Configuration

Navigate to:

**Azure Update Manager → Maintenance configurations → Create**

Configure the basic settings.

![Create Maintenance Configuration](images/maintenance-configuration-create.png)

*Create a Maintenance Configuration*

### Basic Settings

| Setting | Description |
|---------|-------------|
| Subscription | Azure subscription in which the Maintenance Configuration is created. |
| Resource Group | Resource group that stores the Maintenance Configuration. |
| Configuration name | Unique name of the Maintenance Configuration. |
| Region | Azure region where the Maintenance Configuration is deployed. |

---

## Maintenance Scope

The **Maintenance scope** determines which Azure resources can be managed by the Maintenance Configuration.

![Maintenance Scope](images/maintenance-scope-options.png)

*Available maintenance scopes*

### Guest

Updates the operating system of:

- Azure Virtual Machines
- Azure Arc-enabled Servers

Supports:

- Windows Updates
- Linux package updates
- Custom update classifications

> **Recommended for operating system patching of Azure VMs and Arc-enabled servers.**

### Host

Used for Azure Dedicated Hosts and isolated infrastructure.

Azure performs platform maintenance on the physical host infrastructure rather than the guest operating system.

Typical scenarios:

- Azure Dedicated Hosts
- Isolated Virtual Machine Scale Sets

### OS Image (VMSS)

Updates the operating system image of a Virtual Machine Scale Set.

Used when managing image-based updates for VMSS instances.

### Resource

Used for Azure platform resources that support Maintenance Configurations.

Examples include:

- Virtual Network Gateways
- Network Security Gateways (when supported)
- other Azure platform resources

---

## Reboot Setting

The reboot setting controls how Azure Update Manager handles system restarts after installing updates.

![Reboot Settings](images/maintenance-reboot-settings.png)

*Available reboot options*

### Always reboot

Always restarts the operating system after update installation.

Use when:

- maintenance windows are dedicated to patching
- a restart is always acceptable

---

### Reboot if required

The operating system is restarted only if an installed update requires it.

This is the recommended option for most production environments.

---

### Never reboot

Azure Update Manager never initiates a restart.

Use when:

- reboots are controlled by another process
- applications require manual validation before restarting

> **Important:** Some updates are not fully applied until the operating system has been restarted.

---

## Schedule

The maintenance schedule defines when updates are allowed to be installed.

Available options include:

- One-time schedule
- Hourly
- Daily
- Weekly
- Monthly

Depending on the selected frequency, additional settings become available, for example:

- Start time
- Time zone
- Maintenance window duration
- Day of week
- Week of month
- End date

Example:

| Setting | Value |
|---------|-------|
| Frequency | Monthly |
| Occurrence | Second Saturday |
| Start time | 00:00 |
| Duration | 3 hours 55 minutes |
| End date | None |

---

## Next Step

After configuring the basic settings, continue with:

- Resources
- Dynamic Scopes
- Update Classifications
- Events
- Tags

These topics are covered in separate articles.
