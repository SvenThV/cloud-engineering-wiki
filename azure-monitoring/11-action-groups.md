# Action Groups

## Overview

Action Groups define what happens after an Azure Monitor alert is triggered.

Instead of configuring notification actions for every alert individually, multiple alert rules can reuse the same Action Group. This simplifies management and ensures consistent alert handling across the environment.

---

# How Action Groups Work

```text
Azure Resource
        │
        ▼
Alert Rule
        │
Condition Met
        │
        ▼
Action Group
        │
 ┌──────┼──────────────┬──────────────┐
 ▼      ▼              ▼              ▼
Email  SMS         Webhook     Azure Function
                                    │
                                    ▼
                             Automated Response
```

---

# Supported Actions

Action Groups support multiple notification and automation actions.

| Action | Description |
|--------|-------------|
| Email | Send an email notification |
| SMS | Send a text message |
| Push Notification | Notify through the Azure mobile app |
| Voice Call | Automated phone call |
| Webhook | Send an HTTP request to an external service |
| Azure Function | Execute serverless code |
| Logic App | Start a workflow |
| Automation Runbook | Execute an Azure Automation runbook |
| Event Hub | Forward alert events for further processing |

The available actions may vary depending on the Azure region and subscription.

---

# Notification vs Automation

Action Groups support both notifications and automated responses.

| Notification | Automation |
|--------------|------------|
| Email | Azure Function |
| SMS | Logic App |
| Push Notification | Automation Runbook |
| Voice Call | Webhook |
| | Event Hub |

Notifications inform administrators, while automation can immediately perform remediation tasks.

---

# Reusability

One Action Group can be associated with multiple alert rules.

```text
                Alert Rule A
                     │
                Alert Rule B
                     │
                Alert Rule C
                     │
                     ▼
               Action Group
                     │
      ┌──────────────┴──────────────┐
      ▼                             ▼
    Email                   Azure Function
```

This reduces duplication and simplifies maintenance.

---

# Common Use Cases

Action Groups are commonly used for:

- Sending alert notifications
- Creating IT service tickets
- Triggering automated remediation
- Integrating with third-party monitoring tools
- Starting incident response workflows

---

# Example

Example Action Group configuration.

| Setting | Value |
|---------|-------|
| Name | Production Notifications |
| Email | operations@company.com |
| Webhook | Incident Management System |
| Azure Function | Restart failed service |

---

# Best Practices

- Create reusable Action Groups for common notification scenarios.
- Separate production and non-production notifications.
- Combine notifications with automated remediation where appropriate.
- Keep contact information up to date.
- Test Action Groups regularly to verify successful delivery.
- Use descriptive naming conventions to simplify administration.
