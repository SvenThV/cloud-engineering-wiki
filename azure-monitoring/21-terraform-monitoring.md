# Terraform & Azure Monitoring

## Overview

Terraform enables monitoring resources to be deployed consistently, reproducibly, and automatically across Azure environments.

Instead of configuring monitoring manually in the Azure portal, Infrastructure as Code (IaC) ensures that monitoring is version-controlled, standardized, and repeatable.

Monitoring should be deployed alongside the infrastructure it protects.

---

# Why Use Terraform?

Deploying monitoring with Terraform provides several benefits.

- Consistent deployments
- Version-controlled configuration
- Repeatable environments
- Reduced manual effort
- Easier maintenance
- Automated deployments through CI/CD
- Standardized monitoring across environments

---

# Typical Architecture

```text
Terraform
     │
     ▼
Azure Resources
     │
     ├── Log Analytics Workspace
     ├── Diagnostic Settings
     ├── Action Groups
     ├── Alert Rules
     ├── Data Collection Rules
     └── Azure Monitor Agent
```

---

# Common Azure Monitor Resources

Terraform provides resources for deploying Azure Monitor components.

| Terraform Resource | Purpose |
|--------------------|---------|
| `azurerm_log_analytics_workspace` | Create a Log Analytics Workspace |
| `azurerm_monitor_action_group` | Create Action Groups |
| `azurerm_monitor_metric_alert` | Create Metric Alerts |
| `azurerm_monitor_scheduled_query_rules_alert_v2` | Create Log Alerts |
| `azurerm_monitor_activity_log_alert` | Create Activity Log Alerts |
| `azurerm_monitor_diagnostic_setting` | Configure Diagnostic Settings |
| `azurerm_monitor_data_collection_rule` | Create Data Collection Rules |
| `azurerm_monitor_data_collection_rule_association` | Associate DCRs with resources |

---

# Typical Deployment Flow

Monitoring resources are often deployed in the following order.

```text
Terraform Apply
        │
        ▼
Log Analytics Workspace
        │
        ▼
Action Groups
        │
        ▼
Diagnostic Settings
        │
        ▼
Data Collection Rules
        │
        ▼
Alert Rules
```

Deploying resources in this order helps satisfy dependencies and simplifies maintenance.

---

# Modular Design

A modular Terraform design improves reusability and maintainability.

Example structure:

```text
modules/
├── log-analytics-workspace/
├── action-group/
├── diagnostic-settings/
├── metric-alert/
├── log-alert/
├── activity-log-alert/
├── data-collection-rule/
└── monitor-baseline-alerts/
```

Each module should have a clear responsibility and expose configurable input variables.

---

# Environment-Specific Configuration

Avoid hardcoding values directly into modules.

Common configuration options include:

- Environment
- Resource names
- Alert thresholds
- Severity levels
- Action Groups
- Log retention
- Tags

This allows the same module to be reused across development, test, and production environments.

---

# Monitoring Landing Zones

Monitoring is typically deployed as part of an Azure Landing Zone.

Example:

```text
Landing Zone
│
├── Networking
├── Identity
├── Storage
├── Compute
└── Monitoring
     ├── Log Analytics Workspace
     ├── Action Groups
     ├── Diagnostic Settings
     ├── Alert Rules
     └── Data Collection Rules
```

Deploying monitoring together with the Landing Zone ensures that newly deployed resources are monitored from the beginning.

---

# CI/CD Integration

Terraform monitoring deployments are commonly automated using CI/CD pipelines.

Typical workflow:

```text
Git Repository
        │
        ▼
Pull Request
        │
        ▼
Terraform Plan
        │
        ▼
Review
        │
        ▼
Terraform Apply
        │
        ▼
Azure Monitor Resources
```

This ensures monitoring changes are reviewed before deployment.

---

# Monitoring Strategy

A common strategy includes:

| Component | Recommendation |
|-----------|----------------|
| Log Analytics Workspace | Centralized deployment |
| Diagnostic Settings | Enable for critical resources |
| Metric Alerts | Standardize thresholds |
| Log Alerts | Use KQL for advanced scenarios |
| Action Groups | Reuse across multiple alerts |
| Data Collection Rules | Share across similar workloads |
| Azure Monitor Agent | Deploy using Azure Policy |
| AMBA | Use as the monitoring baseline |

---

# Best Practices

- Deploy monitoring using Infrastructure as Code.
- Use reusable Terraform modules.
- Standardize alert rules across environments.
- Avoid hardcoded configuration values.
- Deploy monitoring together with infrastructure.
- Review monitoring costs regularly.
- Keep Terraform modules focused on a single responsibility.
- Use Microsoft-recommended baseline alerts where appropriate.
