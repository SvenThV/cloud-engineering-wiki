# Workbooks

## Overview

Azure Monitor Workbooks provide interactive dashboards for visualizing and analyzing monitoring data.

They combine metrics, log queries, charts, tables, and text into customizable reports, making it easier to monitor infrastructure, troubleshoot issues, and share operational insights.

Workbooks integrate with Azure Monitor, Log Analytics, Application Insights, Microsoft Sentinel, and other Azure services.

---

# How Workbooks Work

```text
Azure Resources
        │
        ▼
Azure Monitor
        │
 ┌──────┼───────────────┐
 ▼      ▼               ▼
Metrics Logs      Application Insights
        │
        ▼
     Workbook
        │
 ┌──────┼──────────────┐
 ▼      ▼              ▼
Charts Tables      Visualizations
```

---

# Workbook Components

A Workbook can contain multiple visualization elements.

| Component | Description |
|-----------|-------------|
| Text | Documentation and explanations |
| Parameters | User-selectable filters |
| Metrics | Azure Monitor metrics |
| Log Queries | Results from KQL queries |
| Tables | Tabular data |
| Charts | Line, bar, pie, and other charts |
| Grids | Interactive data views |
| Links | Navigation to Azure resources |

---

# Data Sources

Workbooks can display data from multiple Azure services.

| Data Source | Example |
|-------------|---------|
| Azure Monitor Metrics | CPU utilization |
| Log Analytics Workspace | KQL query results |
| Application Insights | Requests and exceptions |
| Azure Resource Graph | Resource inventory |
| Microsoft Sentinel | Security incidents |

A single Workbook can combine data from multiple sources.

---

# Parameters

Parameters allow users to customize the displayed data without modifying the Workbook.

Common parameters include:

- Subscription
- Resource Group
- Resource
- Region
- Time Range
- Environment

Parameters make Workbooks reusable across different environments.

---

# Visualizations

Workbooks support multiple visualization types.

| Visualization | Typical Use Case |
|---------------|------------------|
| Line Chart | Performance trends |
| Bar Chart | Category comparison |
| Pie Chart | Distribution analysis |
| Table | Detailed information |
| Grid | Interactive exploration |
| Metric Tile | Key performance indicators |

Selecting the appropriate visualization improves readability and helps identify trends more quickly.

---

# Common Use Cases

Workbooks are commonly used for:

- Infrastructure dashboards
- Application monitoring
- Operational reporting
- Performance analysis
- Capacity planning
- Security monitoring
- Executive dashboards

---

# Workbook vs Azure Dashboard

| Workbook | Azure Dashboard |
|-----------|-----------------|
| Interactive | Static dashboard |
| Supports KQL | Limited querying capabilities |
| Rich visualizations | Basic widgets |
| Highly customizable | Simpler configuration |
| Best for analysis | Best for operational overview |

---

# Sharing Workbooks

Workbooks can be shared with other users through Azure role-based access control (RBAC).

Organizations often create standardized Workbooks for:

- Operations teams
- Platform teams
- Security teams
- Management reporting

---

# Best Practices

- Create reusable Workbooks with parameters.
- Use descriptive titles and section headings.
- Combine metrics and logs for comprehensive insights.
- Keep dashboards focused on a specific purpose.
- Reuse common Workbook templates across environments.
- Review Workbook performance when querying large datasets.
