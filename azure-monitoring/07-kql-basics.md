# Kusto Query Language (KQL)

## Overview

Kusto Query Language (KQL) is the query language used by Azure Monitor to analyze data stored in a Log Analytics Workspace.

It enables you to search, filter, aggregate, and visualize monitoring data from Azure resources, virtual machines, applications, and other connected services.

KQL is the foundation for log analysis, troubleshooting, dashboards, and log-based alerts.

---

# Query Structure

A KQL query consists of one or more operators connected by the pipe (`|`) operator.

```kusto
TableName
| Operator1
| Operator2
| Operator3
```

Each operator processes the output of the previous step.

---

# Selecting a Table

Every query starts with a table.

Example:

```kusto
AzureActivity
| take 10
```

This query returns the first 10 records from the `AzureActivity` table.

---

# Common Operators

| Operator | Purpose |
|----------|---------|
| where | Filter rows |
| project | Select specific columns |
| sort by | Sort results |
| summarize | Aggregate data |
| extend | Create calculated columns |
| distinct | Return unique values |
| count | Count records |
| take | Return a limited number of rows |

---

# Filtering Data

Use the `where` operator to filter records.

Example:

```kusto
AzureActivity
| where OperationNameValue contains "Delete"
```

---

# Selecting Columns

Use the `project` operator to display only the required columns.

```kusto
AzureActivity
| project TimeGenerated, ResourceGroup, OperationNameValue
```

---

# Sorting Results

Sort records by a column.

```kusto
AzureActivity
| sort by TimeGenerated desc
```

---

# Counting Records

Count matching records.

```kusto
AzureActivity
| count
```

---

# Aggregating Data

Use `summarize` to calculate aggregated values.

```kusto
AzureActivity
| summarize count() by OperationNameValue
```

Example output:

| Operation | Count |
|----------|------:|
| Create | 18 |
| Delete | 4 |
| Update | 52 |

---

# Time Filtering

Most monitoring queries filter by time.

Example:

```kusto
AzureActivity
| where TimeGenerated > ago(24h)
```

Other examples:

- `ago(1h)`
- `ago(7d)`
- `ago(30d)`

---

# Combining Operators

Operators can be chained together.

```kusto
AzureActivity
| where TimeGenerated > ago(24h)
| where ActivityStatusValue == "Succeeded"
| project TimeGenerated, ResourceGroup, OperationNameValue
| sort by TimeGenerated desc
```

---

# Common Tables

| Table | Description |
|-------|-------------|
| AzureActivity | Activity Log |
| AzureDiagnostics | Resource Logs |
| Heartbeat | Azure Monitor Agent heartbeat |
| Perf | Performance counters |
| InsightsMetrics | Metrics collected by Azure Monitor Agent |

The available tables depend on the connected Azure resources and monitoring configuration.

---

# Typical Use Cases

KQL is commonly used for:

- Troubleshooting incidents
- Investigating failed deployments
- Finding failed requests
- Monitoring resource health
- Creating log-based alerts
- Building Workbooks
- Security investigations

---

# Best Practices

- Always filter by time using `TimeGenerated`.
- Start with a small result set using `take`.
- Use `project` to return only the required columns.
- Use `summarize` for aggregated reporting.
- Build complex queries incrementally.
- Test queries before using them in alert rules or dashboards.
