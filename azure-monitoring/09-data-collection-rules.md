# Data Collection Rules (DCR)

## Overview

Data Collection Rules (DCRs) define what monitoring data is collected by the Azure Monitor Agent, how it is processed, and where it is sent.

They provide a centralized and reusable configuration model that separates data collection from the virtual machines themselves.

Instead of configuring each server individually, a single Data Collection Rule can be assigned to multiple resources.

---

# Purpose

A Data Collection Rule defines:

- Which data should be collected
- Which resources should collect the data
- Where the collected data should be sent

This makes monitoring easier to standardize and maintain across large environments.

---

# Architecture

```text
Virtual Machine
        │
        ▼
Azure Monitor Agent
        │
        ▼
Data Collection Rule
        │
        ├── Data Sources
        ├── Data Collection
        └── Destinations
                │
                ▼
      Log Analytics Workspace
```

---

# Main Components

A Data Collection Rule consists of three main parts.

| Component | Description |
|----------|-------------|
| Data Sources | Define which data should be collected |
| Data Flows | Specify how collected data is processed |
| Destinations | Define where the collected data is sent |

---

# Supported Data Sources

Depending on the operating system, a Data Collection Rule can collect various types of telemetry.

| Data Source | Example |
|-------------|---------|
| Windows Event Logs | Application, Security, System |
| Linux Syslog | Authentication, Kernel, Daemon |
| Performance Counters | CPU, Memory, Disk, Network |
| Custom Logs | Application log files |

---

# Destinations

A Data Collection Rule can send collected data to one or more destinations.

Common destinations include:

| Destination | Purpose |
|-------------|---------|
| Log Analytics Workspace | Log analysis and monitoring |
| Azure Monitor Metrics | Store selected performance counters as metrics |

The available destinations depend on the selected data source.

---

# Assigning a Data Collection Rule

A Data Collection Rule must be associated with one or more resources before data collection begins.

Supported resources include:

- Azure Virtual Machines
- Virtual Machine Scale Sets
- Azure Arc-enabled Servers

A single Data Collection Rule can be assigned to many resources.

---

# Example

Example configuration:

| Setting | Value |
|---------|-------|
| Target | Azure Virtual Machines |
| Data Source | Windows Event Logs |
| Events | Application, System |
| Performance Counters | CPU, Memory |
| Destination | Log Analytics Workspace |

---

# Data Collection Rules vs Diagnostic Settings

Although both are part of Azure Monitor, they serve different purposes.

| Data Collection Rules | Diagnostic Settings |
|-----------------------|---------------------|
| Collect guest operating system data | Export Azure platform data |
| Used with Azure Monitor Agent | Used directly by Azure resources |
| Configure Windows and Linux telemetry | Configure Resource Logs and Platform Metrics |
| Assigned to virtual machines | Configured per Azure resource |

---

# Common Use Cases

Data Collection Rules are commonly used for:

- Operating system monitoring
- Performance monitoring
- Security event collection
- Standardized monitoring configurations
- Large-scale virtual machine deployments
- Azure Arc monitoring

---

# Best Practices

- Create reusable Data Collection Rules for similar workloads.
- Assign a single rule to multiple resources whenever possible.
- Collect only the required telemetry to reduce monitoring costs.
- Use descriptive naming conventions for Data Collection Rules.
- Manage Data Collection Rules using Infrastructure as Code.
- Regularly review collected data and update rules as requirements change.
