# Azure Monitor

## Overview

Azure Monitor is Microsoft's cloud-native monitoring platform for collecting, analyzing, visualizing, and acting on telemetry data from Azure resources, virtual machines, applications, and external systems.

It provides a centralized platform for monitoring the health, performance, availability, and operational state of cloud environments.

Azure Monitor is not a single service but a collection of monitoring components that work together.

---

# Objectives

Azure Monitor helps answer questions such as:

- Is a resource healthy?
- Is an application available?
- Has performance degraded?
- What changed recently?
- Why did an alert occur?
- Which resources require attention?

---

# Azure Monitor Components

Azure Monitor consists of multiple integrated services.

| Component | Purpose |
|----------|---------|
| Platform Metrics | Near real-time performance metrics |
| Activity Log | Subscription-level management events |
| Resource Logs | Resource-specific diagnostic logs |
| Log Analytics Workspace | Central storage for log data |
| KQL | Query language for log analysis |
| Alert Rules | Detect operational conditions |
| Action Groups | Send notifications or trigger automation |
| Workbooks | Interactive dashboards |
| Application Insights | Application performance monitoring |
| Service Health | Azure platform incidents |
| Resource Health | Health of individual Azure resources |

---

# Monitoring Data

Azure Monitor collects two primary types of monitoring data.

| Type | Description |
|------|-------------|
| Metrics | Numeric values collected at regular intervals |
| Logs | Detailed event and diagnostic information |

Both data types complement each other.

Metrics are optimized for real-time monitoring, while logs provide detailed diagnostic information.

---

# Typical Architecture

```text
Azure Resources
        │
        ▼
Azure Monitor
        │
 ┌──────┼─────────────┐
 ▼      ▼             ▼
Metrics Logs      Activity Log
 │       │
 └───┬───┘
     ▼
Log Analytics Workspace
     │
 ┌───┼────────────┐
 ▼   ▼            ▼
KQL Alerts   Workbooks
```

---

# Typical Use Cases

Azure Monitor is commonly used for:

- Infrastructure monitoring
- Application monitoring
- Performance analysis
- Availability monitoring
- Troubleshooting
- Alerting
- Capacity planning
- Operational dashboards

---

# Benefits

Using Azure Monitor provides several advantages.

- Centralized monitoring platform
- Near real-time metrics
- Powerful log analysis with KQL
- Flexible alerting
- Integrated visualization
- Automation through Action Groups
- Native integration with Azure services

---

# Azure Monitor vs Azure Portal Metrics

A common misconception is that Azure Monitor is only the Metrics blade in the Azure portal.

In reality, Azure Monitor includes much more than metrics.

```text
Azure Monitor

├── Metrics
├── Logs
├── Activity Log
├── Alerts
├── Workbooks
├── Application Insights
├── Service Health
├── Resource Health
└── Action Groups
```

---

# Best Practices

- Use Azure Monitor as the central monitoring platform.
- Combine metrics and logs for effective troubleshooting.
- Store diagnostic logs in a Log Analytics Workspace.
- Standardize monitoring across subscriptions.
- Deploy monitoring resources using Infrastructure as Code whenever possible.
