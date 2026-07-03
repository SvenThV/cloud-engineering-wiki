# Azure Update Manager

## Overview

Azure Update Manager is an Azure service for centrally managing operating system updates for Azure Virtual Machines, Azure Arc-enabled servers, and virtual machine scale sets.

It enables administrators to:

- Assess missing updates
- Schedule recurring maintenance windows
- Install updates automatically
- Monitor update compliance
- Review update history

---

## Supported resources

- Azure Virtual Machines
- Azure Arc-enabled Servers
- Virtual Machine Scale Sets

---

## Core components

- Maintenance Configurations
- Customer Managed Schedules
- Dynamic Scopes
- Azure Policies
- AutomaticByPlatform
- Monitoring & Reporting

---

## Typical workflow

1. Configure the VM for AutomaticByPlatform.
2. Create a Maintenance Configuration.
3. Define the maintenance schedule.
4. Select the update classifications.
5. Configure Dynamic Scopes.
6. Assign VMs automatically using tags.
7. Monitor compliance and update history.
