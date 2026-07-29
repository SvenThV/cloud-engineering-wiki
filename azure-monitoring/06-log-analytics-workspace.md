# Log Analytics Workspace

## Overview

A Log Analytics Workspace (LAW) is the central repository for log data in Azure Monitor.

It stores monitoring data collected from Azure resources, virtual machines, applications, and other connected services. The data can be queried using Kusto Query Language (KQL), visualized in Workbooks, and used to create log-based alerts.

Many Azure Monitor features depend on a Log Analytics Workspace.

---

# Key Capabilities

A Log Analytics Workspace enables you to:

- Store monitoring data centrally
- Query logs using KQL
- Create log-based alerts
- Build interactive Workbooks
- Analyze historical data
- Investigate incidents
- Monitor multiple Azure subscriptions and resources

---

# Supported Data Sources

A Log Analytics Workspace can receive data from various Azure services.

| Data Source | Description |
|-------------|-------------|
| Resource Logs | Diagnostic logs from Azure resources |
| Activity Log | Subscription-level management events |
| Azure Monitor Agent | Operating system telemetry |
| Application Insights | Application telemetry |
| Microsoft Defender for Cloud | Security recommendations and alerts |
| Microsoft Sentinel | Security events and analytics |

---

# Architecture

```text
Azure Resources
        │
        ▼
Diagnostic Settings
        │
        ▼
Log Analytics Workspace
        │
 ┌──────┼───────────────┐
 ▼      ▼               ▼
KQL   Alert Rules   Workbooks
```

The Log Analytics Workspace acts as the central platform for storing and analyzing monitoring data.

---

# Data Organization

Monitoring data is stored in tables.

Each table contains a specific type of information.

Examples include:

| Table | Description |
|-------|-------------|
| AzureActivity | Azure Activity Log events |
| AzureDiagnostics | Resource diagnostic logs |
| Heartbeat | Availability information from Azure Monitor Agent |
| Perf | Performance counters |
| InsightsMetrics | Metrics collected by Azure Monitor Agent |

The available tables depend on the connected services and enabled monitoring configuration.

---

# Querying Data

Log data is queried using Kusto Query Language (KQL).

Example:

```kusto
AzureActivity
| sort by TimeGenerated desc
| take 10
```

KQL allows filtering, aggregation, joins, and advanced analysis of monitoring data.

---

# Retention

Each Log Analytics Workspace has a configurable data retention period.

Retention affects:

- Historical investigations
- Compliance requirements
- Storage costs

Longer retention periods increase storage requirements and may increase overall monitoring costs.

---

# Workspace Design

Organizations typically choose one of the following approaches.

| Design | Description |
|--------|-------------|
| Centralized | One workspace shared by multiple resources or subscriptions |
| Distributed | Multiple workspaces for different environments or business units |

A centralized design simplifies monitoring, while multiple workspaces may be required for regulatory, organizational, or geographic reasons.

---

# Common Use Cases

A Log Analytics Workspace is commonly used for:

- Centralized log collection
- Infrastructure monitoring
- Security investigations
- Performance analysis
- Log-based alerting
- Dashboard creation
- Compliance reporting

---

# Log Analytics Workspace vs Storage Account

| Log Analytics Workspace | Storage Account |
|--------------------------|-----------------|
| Optimized for analysis | Optimized for storage |
| Supports KQL | No query capabilities |
| Supports alerts | No native alerting |
| Used for monitoring | Used for archival |
| Interactive investigations | Long-term retention |

---

# Best Practices

- Use a centralized Log Analytics Workspace whenever possible.
- Connect related Azure resources to the same workspace.
- Review retention settings regularly.
- Monitor data ingestion and retention costs.
- Apply consistent naming conventions.
- Deploy workspaces using Infrastructure as Code.
