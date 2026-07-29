# Azure Monitor Agent (AMA)

## Overview

The Azure Monitor Agent (AMA) is Microsoft's current agent for collecting monitoring data from virtual machines and Arc-enabled servers.

It replaces the legacy Log Analytics Agent (MMA) and Dependency Agent for most monitoring scenarios.

The Azure Monitor Agent collects operating system telemetry and sends it to Azure Monitor based on one or more Data Collection Rules (DCRs).

---

# Why Is an Agent Required?

Azure can automatically collect platform-level information such as CPU utilization or resource availability.

However, Azure cannot access data inside the operating system without an agent.

Examples include:

- Windows Event Logs
- Linux Syslog
- Performance Counters
- Custom log files

The Azure Monitor Agent enables Azure Monitor to collect this guest operating system data.

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
        ▼
Log Analytics Workspace
        │
        ▼
KQL • Alerts • Workbooks
```

---

# Supported Environments

Azure Monitor Agent supports multiple environments.

| Environment | Supported |
|-------------|-----------|
| Azure Virtual Machines | Yes |
| Azure Virtual Machine Scale Sets | Yes |
| Azure Arc-enabled Servers | Yes |
| Windows Server | Yes |
| Linux | Yes |

---

# Collected Data

The Azure Monitor Agent can collect various types of operating system telemetry.

| Data Type | Example |
|-----------|---------|
| Windows Event Logs | Application, Security, System |
| Linux Syslog | Authentication, Kernel, Daemon |
| Performance Counters | CPU, Memory, Disk, Network |
| Custom Logs | Application log files |

The exact data collected is defined by one or more Data Collection Rules.

---

# Deployment

The Azure Monitor Agent can be installed in several ways.

- Azure Portal
- Azure Policy
- Azure Virtual Machine Extensions
- Azure CLI
- PowerShell
- ARM Templates
- Terraform

For production environments, Azure Policy is commonly used to ensure the agent is deployed consistently across virtual machines.

---

# Azure Monitor Agent vs Log Analytics Agent

| Azure Monitor Agent | Log Analytics Agent (MMA) |
|----------------------|---------------------------|
| Current Microsoft agent | Legacy agent |
| Uses Data Collection Rules | Workspace-based configuration |
| More flexible configuration | Limited configuration options |
| Recommended for new deployments | Deprecated for new deployments |
| Supports modern Azure Monitor features | Legacy monitoring scenarios |

---

# Relationship with Data Collection Rules

The Azure Monitor Agent does not define what data should be collected.

Instead, it receives its configuration from one or more Data Collection Rules.

```text
Azure Monitor Agent
          │
          ▼
Data Collection Rule
          │
          ├── Windows Event Logs
          ├── Linux Syslog
          ├── Performance Counters
          └── Destination
```

This separation allows multiple virtual machines to share the same monitoring configuration.

---

# Common Use Cases

The Azure Monitor Agent is commonly used for:

- Operating system monitoring
- Performance monitoring
- Security monitoring
- Compliance reporting
- Centralized log collection
- Virtual machine troubleshooting

---

# Best Practices

- Use Azure Monitor Agent for all new deployments.
- Manage agent deployment with Azure Policy whenever possible.
- Configure data collection using Data Collection Rules.
- Collect only the telemetry required for monitoring and compliance.
- Review ingestion costs regularly, especially when collecting large volumes of event logs.
