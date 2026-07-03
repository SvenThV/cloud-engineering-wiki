# Basics

In this step, the basic settings for the Azure Update Manager maintenance configuration are defined. These settings determine which resources the configuration can be applied to, how required reboots are handled, and when the maintenance window is executed.

The following sections explain the most important configuration options.

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

In most environments, the same region as the remaining management resources is selected. The region of the maintenance configuration does **not** need to match the region of the virtual machines that will later be assigned to it.

---

## Maintenance Scope

The **Maintenance scope** defines which type of Azure resources can use this maintenance configuration.

For operating system patch management with Azure Update Manager, select:

**Guest (Azure VM, Arc-enabled VMs/servers)**

This scope supports:

- Azure Virtual Machines
- Azure Arc-enabled servers

Other maintenance scopes are intended for different Azure maintenance scenarios (for example host or platform maintenance) and are not used for operating system patching.

> **Note**
>
> This guide focuses on patch management for Azure Virtual Machines and Azure Arc-enabled servers using the **Guest** maintenance scope.

---

## Reboot Setting

The **Reboot setting** determines how Azure Update Manager handles system reboots after installing updates.

The following options are available:

### Reboot if required (Recommended)

Azure Update Manager automatically reboots the machine **only if an installed update requires a restart**.

This is the recommended setting for most environments, as unnecessary reboots are avoided while ensuring that updates requiring a restart are completed successfully.

### Never reboot

Updates are installed, but Azure Update Manager never performs an automatic restart.

If a reboot is required, it must be performed manually or by another automation process.

### Always reboot

The machine is restarted after every maintenance run, regardless of whether a reboot is required.

This option is rarely used and is generally not recommended unless specifically required by operational procedures.

---

## Schedule

The schedule defines **when** and **how often** the maintenance configuration is executed.

The following settings are configured:

- **Start time** – Date and time of the first maintenance window
- **Time zone** – Time zone used for the schedule
- **Maintenance window** – Duration of the maintenance window
- **Recurrence** – Defines how often the maintenance window repeats (for example weekly or monthly)

### Maintenance Window

The maintenance window should be large enough to allow Azure Update Manager to:

- Assess available updates
- Download required packages
- Install updates
- Perform a reboot (if required)
- Complete post-reboot update operations

For production environments, a maintenance window of several hours is commonly used. The exact duration depends on the operating system, the number of available updates, and the expected reboot time.

---

## Summary

For the examples used throughout this guide, the following configuration is used:

| Setting | Value |
|---------|-------|
| Maintenance scope | Guest (Azure VM, Arc-enabled VMs/servers) |
| Reboot setting | Reboot if required |
| Schedule | Weekly maintenance window |
