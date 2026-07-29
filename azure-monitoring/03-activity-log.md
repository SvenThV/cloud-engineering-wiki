# Activity Log

## Overview

The Activity Log records management events that occur at the Azure subscription level.

It provides visibility into operations performed on Azure resources, including resource creation, deletion, configuration changes, service health events, and administrative actions.

Unlike Resource Logs, the Activity Log is automatically available for every Azure subscription.

---

# What Does the Activity Log Capture?

The Activity Log records events related to the Azure Resource Manager (ARM) control plane.

Typical events include:

- Resource creation
- Resource deletion
- Resource updates
- Start and stop operations
- Role assignments (RBAC)
- Policy evaluations
- Subscription events
- Service Health events
- Resource Health events

---

# Activity Log Categories

The Activity Log is organized into several categories.

| Category | Description |
|----------|-------------|
| Administrative | Resource management operations performed through Azure Resource Manager |
| Service Health | Azure platform incidents, maintenance, and advisories |
| Resource Health | Health status changes of individual resources |
| Alert | Activity Log Alert events |
| Policy | Azure Policy evaluations and compliance events |
| Recommendation | Azure Advisor recommendations |
| Security | Security-related events (when available) |
| Autoscale | Autoscale operations |

---

# Control Plane vs Data Plane

The Activity Log records **control plane** operations only.

```text
Control Plane
-------------
Create VM
Delete Storage Account
Assign RBAC Role
Modify Network Security Group

↓

Recorded in Activity Log

---------------------------------------

Data Plane
----------
Read Blob
Upload File
Download Document
Query Database

↓

NOT recorded in Activity Log
```

Data plane operations are typically captured through Resource Logs when diagnostic settings are enabled.

---

# Common Use Cases

The Activity Log is commonly used to answer questions such as:

- Who deleted a resource?
- When was a Virtual Machine restarted?
- Who modified a Network Security Group?
- When was a Key Vault created?
- Which deployment failed?
- Why is a resource unavailable?

---

# Filtering the Activity Log

The Azure portal allows filtering by:

- Subscription
- Time range
- Resource Group
- Resource
- Event category
- Resource type
- Operation
- Severity

Filtering makes it easier to locate specific management events.

---

# Activity Log Retention

The Activity Log is retained automatically by Azure for a limited period.

For long-term retention or advanced analysis, configure a Diagnostic Setting to send Activity Log data to one or more destinations:

- Log Analytics Workspace
- Storage Account
- Event Hub

---

# Activity Log Alerts

Activity Log Alerts can notify administrators when specific management events occur.

Typical examples include:

- Resource deleted
- New role assignment
- Subscription changes
- Policy modifications
- Resource creation

Unlike Metric Alerts, Activity Log Alerts are event-based.

---

# Activity Log vs Resource Logs

Although both contain monitoring data, they serve different purposes.

| Activity Log | Resource Logs |
|--------------|---------------|
| Subscription-level | Resource-level |
| Automatically available | Must be enabled using Diagnostic Settings |
| Records management operations | Records resource-specific events |
| Control plane | Mostly data plane and service diagnostics |
| Limited retention | Configurable retention depending on destination |

---

# Best Practices

- Regularly review the Activity Log for administrative changes.
- Configure Diagnostic Settings for long-term retention.
- Create Activity Log Alerts for critical management events.
- Monitor role assignments and resource deletions.
- Use the Activity Log together with Resource Logs during troubleshooting.
