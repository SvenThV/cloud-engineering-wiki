# Diagnostic Settings

## Overview

Diagnostic Settings determine which monitoring data is collected from Azure resources and where it is sent.

They are the primary mechanism for exporting Resource Logs, Platform Metrics, and Activity Logs to external destinations for long-term storage, analysis, and monitoring.

Without Diagnostic Settings, most Resource Logs are not collected.

---

# Supported Destinations

Diagnostic Settings can send monitoring data to one or more destinations simultaneously.

| Destination | Purpose |
|-------------|---------|
| Log Analytics Workspace | Centralized log storage and analysis using KQL |
| Storage Account | Long-term retention and archival |
| Event Hub | Stream monitoring data to external systems |

A single Diagnostic Setting can send data to multiple destinations at the same time.

---

# Supported Data Types

Depending on the Azure resource, Diagnostic Settings can export:

- Resource Logs
- Platform Metrics
- Activity Logs (configured at the subscription level)

The available log categories differ between Azure services.

---

# How Diagnostic Settings Work

```text
Azure Resource
        │
        ▼
Diagnostic Settings
        │
 ┌──────┼───────────────┐
 ▼      ▼               ▼
Log Analytics     Storage Account     Event Hub
 Workspace
```

Diagnostic Settings act as the routing layer between Azure resources and monitoring destinations.

---

# Configuration Process

A typical configuration consists of the following steps:

1. Open the Azure resource.
2. Navigate to **Diagnostic Settings**.
3. Create a new Diagnostic Setting.
4. Select the required log categories.
5. Select the destination.
6. Save the configuration.

After the configuration is complete, Azure starts forwarding the selected monitoring data.

---

# Example

Example configuration for an Azure Storage Account:

| Setting | Value |
|---------|-------|
| Resource | Storage Account |
| Logs | Read, Write, Delete |
| Metrics | Transaction Metrics |
| Destination | Log Analytics Workspace |

---

# Choosing the Right Destination

Each destination serves a different purpose.

| Destination | Typical Use Case |
|-------------|------------------|
| Log Analytics Workspace | Monitoring, alerting, troubleshooting |
| Storage Account | Compliance, long-term retention, backup |
| Event Hub | SIEM integration, external analytics platforms |

Many production environments use a combination of multiple destinations.

---

# Important Considerations

- Diagnostic Settings are configured individually for each resource.
- Available log categories differ between Azure services.
- Not every resource supports Platform Metrics export.
- Multiple Diagnostic Settings can be configured for a single resource.
- Sending large amounts of log data may increase Azure Monitor costs.

---

# Common Use Cases

Diagnostic Settings are commonly used to:

- Centralize monitoring data
- Enable KQL queries
- Create log-based alerts
- Meet compliance requirements
- Archive monitoring data
- Forward logs to external SIEM platforms

---

# Diagnostic Settings vs Data Collection Rules

Although both are related to Azure Monitor, they serve different purposes.

| Diagnostic Settings | Data Collection Rules |
|---------------------|-----------------------|
| Configure data export | Configure agent-based data collection |
| Resource-level configuration | Azure Monitor Agent configuration |
| Export Resource Logs and Metrics | Collect operating system telemetry |
| No agent required | Azure Monitor Agent required |

---

# Best Practices

- Send production logs to a centralized Log Analytics Workspace.
- Enable only the required log categories.
- Review log ingestion costs regularly.
- Use consistent naming conventions for Diagnostic Settings.
- Standardize Diagnostic Settings across environments using Infrastructure as Code.
- Archive compliance-relevant logs in a Storage Account when required.
