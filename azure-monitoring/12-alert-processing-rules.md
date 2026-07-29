# Alert Processing Rules

## Overview

Alert Processing Rules allow you to modify how alerts are handled after they have been triggered.

Unlike Alert Rules, they do not detect conditions or generate alerts. Instead, they control the processing of existing alerts by suppressing notifications or assigning different Action Groups.

This helps reduce unnecessary notifications and provides greater flexibility in alert management.

---

# How Alert Processing Rules Work

```text
Azure Resource
        │
        ▼
Alert Rule
        │
        ▼
      Alert
        │
        ▼
Alert Processing Rule
        │
 ┌──────┴──────────────┐
 ▼                     ▼
Suppress          Action Group
Notifications     Override
```

---

# Typical Actions

Alert Processing Rules support the following actions:

| Action | Description |
|--------|-------------|
| Suppress Notifications | Prevent notifications from being sent |
| Apply Action Group | Assign one or more Action Groups to matching alerts |

The alert itself is still created and remains visible in Azure Monitor.

---

# Filtering Options

Processing Rules can be applied to specific alerts based on various criteria.

| Filter | Example |
|--------|---------|
| Subscription | Production Subscription |
| Resource Group | RG-Production |
| Resource Type | Virtual Machine |
| Resource | VM-01 |
| Severity | Sev 0, Sev 1 |
| Alert Rule | High CPU Alert |
| Monitor Service | Azure Monitor |

Multiple filters can be combined to create targeted processing rules.

---

# Scheduling

Alert Processing Rules can be active only during specific time periods.

Common scheduling scenarios include:

- Planned maintenance windows
- Business hours
- Weekends
- Public holidays
- Overnight maintenance

This prevents unnecessary notifications during expected maintenance activities.

---

# Common Use Cases

Alert Processing Rules are commonly used for:

- Suppressing alerts during maintenance windows
- Redirecting alerts to different support teams
- Applying different Action Groups outside business hours
- Reducing alert noise
- Implementing operational schedules

---

# Alert Rules vs Alert Processing Rules

| Alert Rules | Alert Processing Rules |
|-------------|------------------------|
| Detect monitoring conditions | Modify alert handling |
| Generate alerts | Do not generate alerts |
| Evaluate metrics, logs, or events | Process existing alerts |
| Define alert logic | Define notification behavior |

Both features complement each other but serve different purposes.

---

# Example

Example maintenance scenario:

```text
Saturday 22:00
        │
Scheduled Maintenance
        │
        ▼
Alert Triggered
        │
        ▼
Alert Processing Rule
        │
        ▼
Notification Suppressed
```

The alert is still recorded in Azure Monitor, but no notification is sent.

---

# Best Practices

- Use Alert Processing Rules for planned maintenance instead of disabling Alert Rules.
- Suppress notifications only when necessary.
- Keep maintenance schedules up to date.
- Reuse Action Groups for consistent notification handling.
- Regularly review Processing Rules to ensure they remain relevant.
