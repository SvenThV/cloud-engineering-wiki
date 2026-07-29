# Alert Rules

## Overview

Alert Rules automatically detect conditions that require attention and notify administrators or trigger automated actions.

They continuously evaluate monitoring data and generate alerts when predefined conditions are met.

Azure Monitor supports multiple alert types depending on the monitored data source.

---

# Alert Workflow

```text
Azure Resource
        │
        ▼
Metrics / Logs / Events
        │
        ▼
Alert Rule
        │
Condition Met?
        │
   Yes ▼
      Alert
        │
        ▼
Action Group
        │
        ├── Email
        ├── SMS
        ├── Webhook
        ├── Azure Function
        ├── Logic App
        └── Automation Runbook
```

---

# Alert Types

Azure Monitor supports several alert types.

| Alert Type | Data Source | Typical Use Case |
|------------|-------------|------------------|
| Metric Alert | Platform Metrics | CPU usage, response time, storage capacity |
| Log Alert | Log Analytics Workspace | Failed logins, application errors, custom queries |
| Activity Log Alert | Activity Log | Resource deletion, role assignments, policy changes |
| Smart Detection Alert | Application Insights | Performance anomalies and application issues |

---

# Alert Components

Every alert rule consists of several components.

| Component | Description |
|-----------|-------------|
| Scope | Resource or resources being monitored |
| Condition | Defines when an alert should trigger |
| Evaluation | Frequency at which Azure evaluates the condition |
| Action Group | Defines what happens after the alert is triggered |
| Alert Details | Name, severity, and description |

---

# Severity Levels

Azure Monitor uses severity levels to classify alerts.

| Severity | Description |
|----------|-------------|
| Sev 0 | Critical service outage requiring immediate action |
| Sev 1 | High-impact issue |
| Sev 2 | Significant issue requiring prompt investigation |
| Sev 3 | Medium-priority issue |
| Sev 4 | Informational alert |

Severity levels help prioritize operational response.

---

# Metric Alerts

Metric Alerts evaluate numeric metrics collected by Azure Monitor.

Example:

| Metric | Condition |
|---------|-----------|
| CPU Percentage | Greater than 80% |
| Response Time | Greater than 2 seconds |
| Storage Capacity | Greater than 90% |

Metric Alerts provide near real-time detection with low latency.

---

# Log Alerts

Log Alerts evaluate KQL queries against data stored in a Log Analytics Workspace.

Example:

```kusto
AzureActivity
| where ActivityStatusValue == "Failed"
```

If the query returns matching results, the alert is triggered.

Log Alerts are suitable for detecting complex conditions that cannot be expressed using metrics alone.

---

# Activity Log Alerts

Activity Log Alerts monitor management events within an Azure subscription.

Typical examples include:

- Resource deleted
- Resource created
- New role assignment
- Policy modification
- Subscription changes

These alerts are event-based and do not require a Log Analytics Workspace.

---

# Evaluation Frequency

Alert rules evaluate conditions at regular intervals.

Common evaluation frequencies include:

- Every minute
- Every 5 minutes
- Every 15 minutes
- Every hour

The available intervals depend on the alert type.

---

# Common Use Cases

Alert Rules are commonly used for:

- High CPU utilization
- Failed deployments
- Resource deletions
- Storage capacity monitoring
- Application failures
- Security event detection
- Availability monitoring

---

# Best Practices

- Define meaningful thresholds based on operational requirements.
- Use appropriate severity levels.
- Avoid unnecessary alerts to reduce alert fatigue.
- Test alert rules before deploying them to production.
- Reuse Action Groups across multiple alert rules.
- Regularly review and adjust alert thresholds as workloads change.
