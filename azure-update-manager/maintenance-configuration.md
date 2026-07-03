# Basics

In this step, the basic settings for the Azure Update Manager maintenance configuration are defined. These settings determine which resources the configuration can be applied to, how required reboots are handled, and when the maintenance window is executed.

The following sections explain the most important configuration options.

![Create Maintenance Configuration](images/maintenance-configuration-basics.png)

*Azure Update Manager – Basics*

---

## Configuration Name

Choose a meaningful and descriptive name for the maintenance configuration.

If multiple maintenance configurations are used (for example for different deployment rings), a consistent naming convention improves readability and administration.

Example:

- `mc-patch-pilot`
- `mc-patch-test`
- `mc-patch-production`

---

## Region

The maintenance configuration is stored as an Azure resource and therefore requires an Azure region.

In most environments, the same region as the remaining management resources is selected.

---

## Maintenance Scope

The **Maintenance scope** defines which type of Azure resources can use this maintenance configuration.

For operating system patch management with Azure Update Manager, select:

**Guest (Azure VM, Arc-enabled VMs/servers)**

This scope supports:

- Azure Virtual Machines
- Azure Arc-enabled servers

Other maintenance scopes are intended for different Azure maintenance scenarios:

| Scope | Typical Use Case |
|--------|------------------|
| Guest | Operating system patching of Azure VMs and Arc-enabled servers |
| Host | Azure Dedicated Hosts and isolated infrastructure |
| OS Image (VMSS) | Updating Virtual Machine Scale Set images |
| Resource | Azure platform resources supporting Maintenance Configurations |

> **Best Practice**
>
> For standard Windows and Linux virtual machines, use the **Guest** maintenance scope.

---

## Reboot Setting

The **Reboot setting** determines how Azure Update Manager handles required restarts after update installation.

Available options:

### Reboot if required (Recommended)

Only reboots the machine when required by an installed update.

Recommended for most production environments.

### Never reboot

No automatic restart is performed.

Suitable when reboots are controlled manually or by another automation process.

### Always reboot

The machine is restarted after every maintenance run.

Typically only used in dedicated maintenance environments.

---

## Schedule

The schedule defines **when** Azure Update Manager is allowed to install updates.

Click **Edit schedule** to configure the maintenance window.

![Configure Maintenance Schedule](images/maintenance-configuration-schedule.png)

*Maintenance schedule configuration*

The following options can be configured:

- Start date and time
- Time zone
- Maintenance window duration
- Recurrence (Daily, Weekly or Monthly)
- Optional end date

### Maintenance Window

The maintenance window should be long enough to:

- Assess available updates
- Download update packages
- Install updates
- Reboot the operating system (if required)
- Complete post-reboot update operations

For production environments, maintenance windows between two and four hours are commonly used.

### Recurrence

Azure Update Manager supports recurring maintenance windows.

Typical options include:

- Daily
- Weekly
- Monthly

The appropriate schedule depends on the organization's patch management strategy.
