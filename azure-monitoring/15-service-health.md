# Service Health

## Overview

Azure Service Health provides personalized information about the health of Azure services and regions used by your subscriptions.

It helps identify platform issues that may affect your Azure resources, allowing administrators to quickly determine whether an incident is caused by Azure or by their own environment.

Unlike Resource Health, Service Health focuses on Azure platform services rather than individual resources.

---

# Service Health Information

Service Health provides information about:

- Service issues
- Planned maintenance
- Health advisories
- Security advisories
- Resource-specific notifications

The information is filtered based on the subscriptions and regions you use.

---

# Service Health Categories

| Category | Description |
|----------|-------------|
| Service Issues | Active Azure incidents affecting services |
| Planned Maintenance | Scheduled maintenance performed by Microsoft |
| Health Advisories | Recommendations and known platform issues |
| Security Advisories | Security-related notifications and guidance |

---

# How Service Health Works

```text
Azure Platform
        │
        ▼
Azure Service Health
        │
        ├── Service Issues
        ├── Planned Maintenance
        ├── Health Advisories
        └── Security Advisories
                │
                ▼
        Azure Administrators
```

---

# Typical Information

A Service Health event may include:

- Affected Azure service
- Affected region
- Current status
- Incident start time
- Estimated resolution time
- Microsoft updates
- Recommended actions

---

# Alert Integration

Service Health events can trigger Azure Monitor Activity Log Alerts.

Typical alert scenarios include:

- New service incident
- Planned maintenance notification
- Health advisory
- Security advisory

Notifications can be delivered through Action Groups.

---

# Common Use Cases

Service Health is commonly used for:

- Monitoring Azure platform incidents
- Tracking planned maintenance
- Receiving regional outage notifications
- Operational awareness
- Incident management

---

# Service Health vs Resource Health

| Service Health | Resource Health |
|---------------|-----------------|
| Azure platform services | Individual Azure resources |
| Subscription and region scope | Resource scope |
| Microsoft-managed events | Resource-specific availability |
| Planned maintenance and incidents | Resource status and outage history |

---

# Best Practices

- Configure alerts for critical Service Health events.
- Monitor the Azure regions hosting production workloads.
- Review planned maintenance notifications regularly.
- Subscribe only to relevant services and regions.
- Use Service Health together with Resource Health for complete operational visibility.
