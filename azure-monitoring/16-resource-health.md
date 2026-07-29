# Resource Health

## Overview

Resource Health provides information about the health and availability of individual Azure resources.

It helps determine whether an issue originates from the Azure platform or from the resource's own configuration. Resource Health can significantly reduce troubleshooting time by identifying platform-related problems.

Unlike Service Health, Resource Health focuses on individual resources rather than Azure services or regions.

---

# Resource Health Information

Resource Health reports the current health status of supported Azure resources.

Typical information includes:

- Current availability status
- Health history
- Platform-related issues
- Planned maintenance events
- Recovery recommendations

---

# Health Status

Each supported resource has one of several health states.

| Status | Description |
|--------|-------------|
| Available | The resource is operating normally. |
| Unavailable | Azure has detected a platform-related issue affecting the resource. |
| Unknown | Azure cannot determine the current health state. |
| Degraded | The resource is operational but experiencing reduced performance or functionality. |

The available status values may vary depending on the resource type.

---

# How Resource Health Works

```text
Azure Resource
        │
        ▼
Resource Health
        │
        ├── Current Status
        ├── Health History
        ├── Platform Events
        └── Recovery Guidance
```

---

# Health History

Resource Health maintains a history of health events.

This allows administrators to determine:

- When an issue started
- When the resource recovered
- How long the outage lasted
- Whether similar incidents occurred previously

Health history is useful during post-incident analysis.

---

# Supported Resources

Resource Health supports many Azure resource types, including:

- Virtual Machines
- Virtual Machine Scale Sets
- App Services
- Azure SQL Database
- Storage Accounts
- Network resources

Support varies by Azure service.

---

# Common Use Cases

Resource Health is commonly used for:

- Troubleshooting resource outages
- Identifying Azure platform issues
- Verifying service recovery
- Incident analysis
- Determining whether escalation to Microsoft is required

---

# Alert Integration

Resource Health events can trigger Azure Monitor Activity Log Alerts.

Typical alert scenarios include:

- Resource becomes unavailable
- Resource recovers after an outage
- Planned maintenance affects a resource

Alerts can notify administrators or trigger automated workflows through Action Groups.

---

# Resource Health vs Service Health

| Resource Health | Service Health |
|-----------------|----------------|
| Individual resource | Azure service or region |
| Resource-specific availability | Platform-wide incidents |
| Current health status | Service incidents and advisories |
| Health history | Maintenance and outage notifications |

---

# Best Practices

- Monitor Resource Health for all production workloads.
- Configure alerts for critical resources.
- Review health history after incidents.
- Use Resource Health together with Activity Logs and Resource Logs during troubleshooting.
- Combine Resource Health with Service Health to distinguish between platform and resource-specific issues.
