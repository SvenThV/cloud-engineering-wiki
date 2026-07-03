# Maintenance Configurations

## Overview

A Maintenance Configuration defines when and how operating system updates are installed on virtual machines.

It specifies:

- Maintenance window
- Update classifications
- Reboot behavior
- Recurrence schedule
- Target resources

Maintenance Configurations can be assigned directly to virtual machines or automatically using Dynamic Scopes.

---

## Prerequisites

Before creating a Maintenance Configuration, ensure that:

- Azure Update Manager is available.
- The target virtual machines are onboarded.
- The required permissions are available.
- The virtual machines are configured for Azure Update Manager.

---

## Step 1 – Create a Maintenance Configuration

Navigate to:

**Azure Update Manager → Maintenance configurations → Create**

Configure the basic settings.

Example configuration:

| Setting | Value |
|---------|-------|
| Scope | Guest |
| Region | West Europe |
| Reboot setting | Reboot if required |

> **Note**
>
> The maintenance scope **Guest** is used for Azure Virtual Machines and Azure Arc-enabled servers.

![Create Maintenance Configuration](images/maintenance-configuration-create.png)

*Create a Maintenance Configuration*

---

## Step 2 – Configure the Schedule

Define the maintenance window.

Example:

| Setting | Value |
|---------|-------|
| Frequency | Monthly |
| Occurrence | Second Saturday |
| End Date | None |

The schedule defines when updates are allowed to be installed.

![Maintenance Schedule](images/maintenance-configuration-schedule.png)

*Configure the maintenance schedule*

---

## Step 3 – Configure Update Classifications

Select the operating system update categories that should be installed.

Examples include:

Windows

- Critical Updates
- Security Updates
- Update Rollups
- Feature Packs
- Service Packs
- Definition Updates
- Updates

Linux

- Security Updates
- Critical Updates
- Other Updates

Only the selected update classifications will be installed during the maintenance window.

![Update Classifications](images/maintenance-configuration-update-classifications.png)

*Configure update classifications*

---

## Step 4 – Configure Reboot Behavior

Azure Update Manager supports different reboot options.

Available options include:

- Never reboot
- Reboot if required
- Always reboot

The selected option controls how operating system updates are finalized after installation.

---

## Step 5 – Review and Create

Review the configuration and create the Maintenance Configuration.

After deployment, it becomes available for assignment to virtual machines or Dynamic Scopes.

---

## Verification

Open the created Maintenance Configuration.

Verify:

- Schedule
- Update classifications
- Reboot behavior
- Assigned resources
- Dynamic Scopes

![Maintenance Configuration Overview](images/maintenance-configuration-overview.png)

*Maintenance Configuration overview*
