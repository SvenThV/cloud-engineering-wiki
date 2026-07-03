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

# Resources

The **Resources** tab allows virtual machines to be assigned directly to the maintenance configuration.

![Resources](images/maintenance-configuration-resources.png)

*Assign resources to the maintenance configuration*

## Direct Resource Assignment

Virtual machines can be added manually by selecting **Add resources**.

Azure Update Manager supports assigning:

- Azure Virtual Machines
- Azure Arc-enabled servers
- Other supported resource types depending on the selected maintenance scope

Once assigned, the selected resources will use this maintenance configuration during the configured maintenance window.

---

## When to use Direct Assignments

Direct resource assignments are suitable for:

- Small environments
- Test environments
- Individual virtual machines
- Temporary maintenance configurations

Since each virtual machine must be assigned manually, administration becomes increasingly complex as the environment grows.

---

## Dynamic Scopes (Recommended)

For larger environments, Microsoft recommends using **Dynamic Scopes** instead of manually assigning resources.

Dynamic Scopes automatically assign maintenance configurations based on resource properties such as:

- Subscription
- Resource Group
- Location
- Operating System
- Resource Type
- Tags

This allows newly created virtual machines to be assigned automatically without modifying the maintenance configuration.

> **Best Practice**
>
> Use direct resource assignments only for small or temporary environments. For production environments, Dynamic Scopes provide a more scalable and easier to maintain solution.

> **Note**
>
> Dynamic Scopes are configured in the next step of the maintenance configuration wizard.

# Dynamic Scopes

A **Dynamic Scope** automatically assigns virtual machines to a maintenance configuration based on predefined filter criteria.

Instead of manually assigning individual virtual machines, Azure Update Manager evaluates the configured filters whenever a maintenance window starts and automatically includes all matching resources.

This significantly reduces administrative effort and ensures that newly deployed virtual machines are automatically included without modifying the maintenance configuration.

![Dynamic Scopes](images/maintenance-configuration-dynamic-scopes.png)

*Maintenance Configuration – Dynamic Scopes*

---

## Create a Dynamic Scope

Select **Add a dynamic scope** to create a new assignment.

A dynamic scope always requires at least one Azure subscription. Additional filters can then be applied to limit the scope.

![Create Dynamic Scope](images/dynamic-scope-create.png)

*Create a Dynamic Scope*

---

## Available Filter Options

Dynamic Scopes support multiple filter criteria that can be combined.

![Dynamic Scope Filters](images/dynamic-scope-filters.png)

*Available Dynamic Scope filter options*

| Filter | Description | Typical Use Case |
|---------|-------------|------------------|
| Resource Groups | Includes only resources from selected resource groups. | Separate production and test environments. |
| Resource Types | Limits the scope to specific Azure resource types. | Target only Azure Virtual Machines. |
| Locations | Includes resources from selected Azure regions. | Regional maintenance windows. |
| OS Types | Filters Windows or Linux systems. | Separate maintenance schedules for Windows and Linux. |
| Tags | Assigns resources based on Azure tags. | Patch rings, application owners, business units or environments. |

Multiple filters can be combined to create highly granular maintenance scopes.

---

## Using Tags

Azure tags are commonly used to control maintenance assignments.

Typical examples include:

| Tag | Example Values |
|-----|----------------|
| Environment | Production, Test, Development |
| PatchRing | Ring1, Ring2 |
| SecurityUpdates | withRESTART, withoutRESTART |
| FeatureUpdates | Ring1, Ring2 |

This approach allows maintenance configurations to be assigned automatically based on the role or lifecycle of a virtual machine.

---

## Preview

Before saving the Dynamic Scope, Azure displays a preview of all matching resources.

This allows administrators to verify that the configured filters return the expected virtual machines before the maintenance configuration is applied.

---

> **Best Practice**
>
> For production environments, Microsoft recommends using Dynamic Scopes instead of manually assigning resources. Tag-based assignments are easier to maintain, scale automatically as new virtual machines are deployed, and reduce ongoing administrative effort.

# Updates

The **Updates** tab defines which operating system updates Azure Update Manager installs during the configured maintenance window.

Updates can be selected by **classification** or by explicitly including or excluding individual Windows Knowledge Base (KB) updates or Linux packages.

![Maintenance Configuration - Updates](images/maintenance-configuration-updates.png)

*Maintenance Configuration – Updates*

---

## Update Classifications

Azure Update Manager groups operating system updates into different classifications.

Select **Include update classification** to choose which update categories should be installed.

![Update Classifications](images/maintenance-configuration-update-classifications.png)

*Select update classifications*

### Windows Update Classifications

| Classification | Description | Recommendation |
|---------------|-------------|----------------|
| Critical updates | Updates that address critical, non-security issues affecting system stability or reliability. | Recommended |
| Security updates | Updates that address known security vulnerabilities. | Strongly recommended |
| Update rollups | Collections of multiple updates bundled into a single package. | Recommended in most environments |
| Feature packs | Introduces new Windows features and functionality. | Evaluate before deployment |
| Service packs | Large collections of updates and fixes for older Windows versions. Rarely used on modern Windows Server versions. | Only if applicable |
| Definition updates | Updates for Microsoft Defender and other security definitions. | Recommended |
| Tools | Additional Microsoft tools that are distributed through Windows Update. | Usually not required |
| Updates | General updates that do not belong to another classification. | Evaluate depending on the environment |

### Linux Update Classifications

| Classification | Description | Recommendation |
|---------------|-------------|----------------|
| Security and critical updates | Security fixes and critical operating system updates. | Strongly recommended |
| Other updates | All remaining package updates. | Evaluate depending on maintenance strategy |

---

## Recommended Configuration

For production environments, Microsoft generally recommends installing security-related updates regularly.

A common configuration includes:

### Windows

- Critical updates
- Security updates
- Definition updates

### Linux

- Security and critical updates

Feature updates or feature packs are often deployed separately after validation to reduce operational risk.

---

## Include KB ID / Package

Specific Windows KB updates or Linux packages can be explicitly included.

Examples:

Windows

- KB5035857
- KB5036892

Linux

- openssh
- kernel
- nginx

This option is useful when:

- deploying a specific security fix,
- validating a newly released update,
- installing an update outside the regular maintenance cycle.

---

## Exclude KB ID / Package

Specific Windows KB updates or Linux packages can also be excluded from installation.

This is useful when:

- an update is known to cause compatibility issues,
- an application vendor has not yet approved a specific update,
- a temporary workaround is required until Microsoft releases a corrected version.

Excluded updates are skipped even if they belong to a selected update classification.

> **Best Practice**
>
> Use **Include** and **Exclude KB ID / Package** only for exceptional situations. In most environments, update deployment should be managed through update classifications rather than individual KBs or packages, as this reduces administrative effort and simplifies long-term maintenance.

# Events

The **Events** tab allows Azure Update Manager to publish events before and after a maintenance window.

These events can be consumed by Azure Event Grid and used to trigger automated workflows, notifications, or operational tasks.

![Maintenance Configuration - Events](images/maintenance-configuration-events.png)

*Maintenance Configuration – Events*

---

## Event Subscriptions

Select **Add Event subscription** to create an Event Grid subscription for the maintenance configuration.

An event subscription forwards Azure Update Manager events to a supported destination, such as:

- Azure Functions
- Azure Logic Apps
- Azure Automation
- Azure Event Hubs
- Azure Service Bus
- Webhooks
- Azure Storage Queues

This enables automated actions before or after a maintenance window without manual intervention.

---

## Supported Event Types

Azure Update Manager publishes two event types:

### Pre-maintenance

Triggered before the maintenance window starts.

Typical use cases include:

- Notify administrators about upcoming maintenance
- Stop business applications gracefully
- Disable monitoring alerts
- Drain Azure Virtual Desktop session hosts
- Create snapshots or backups before patching

> **Note**
>
> Microsoft recommends scheduling pre-maintenance actions at least **40 minutes** before the maintenance window begins to ensure there is sufficient time for execution.

---

### Post-maintenance

Triggered after the maintenance run has completed.

Typical use cases include:

- Send completion notifications
- Re-enable monitoring alerts
- Start previously stopped services
- Execute validation or health checks
- Trigger follow-up automation

---

## Typical Architecture

A common implementation is:

```text
Azure Update Manager
        │
        ▼
Azure Event Grid
        │
        ├── Azure Function
        ├── Logic App
        ├── Automation Runbook
        └── Webhook
```

This approach enables event-driven automation without requiring manual interaction.

---

> **Best Practice**
>
> Event subscriptions are optional and are primarily intended for environments that require automated operational workflows before or after patch installation. For smaller environments, Maintenance Configurations can be used without configuring event subscriptions.
