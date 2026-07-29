# Azure Monitor Baseline Alerts (AMBA)

## Overview

Azure Monitor Baseline Alerts (AMBA) is a Microsoft-maintained collection of recommended Azure Monitor alert rules.

It provides standardized monitoring for many Azure services by deploying predefined alert rules based on Microsoft's operational best practices.

AMBA helps organizations implement consistent monitoring across Azure environments without creating every alert manually.

---

# Why Use AMBA?

Building alert rules from scratch for every Azure resource can be time-consuming and may lead to inconsistent monitoring.

AMBA provides:

- Standardized alert rules
- Microsoft-recommended thresholds
- Broad Azure service coverage
- Infrastructure as Code support
- Consistent monitoring across environments

---

# How AMBA Works

```text
Azure Resources
        │
        ▼
Azure Monitor Baseline Alerts
        │
        ▼
Alert Rules
        │
        ▼
Action Groups
        │
        ▼
Notifications / Automation
```

---

# Supported Services

AMBA supports a wide range of Azure services.

Examples include:

- Virtual Machines
- App Service
- Storage Accounts
- Azure SQL Database
- Key Vault
- Virtual Networks
- Load Balancer
- Application Gateway
- Azure Firewall
- Log Analytics Workspace
- Kubernetes (AKS)

Microsoft regularly expands the list of supported services.

---

# Deployment Options

AMBA can be deployed using Infrastructure as Code.

Common deployment methods include:

| Method | Description |
|--------|-------------|
| ARM Templates | Microsoft-provided deployment templates |
| Bicep | Native Azure deployment language |
| Terraform | Community-supported implementations and custom modules |
| Azure Policy | Deploy monitoring at scale |

Infrastructure as Code enables consistent monitoring across environments.

---

# Alert Categories

AMBA includes different types of alerts depending on the resource.

Examples include:

| Category | Example |
|----------|---------|
| Availability | Resource unavailable |
| Performance | High CPU utilization |
| Capacity | Low storage space |
| Networking | Failed connections |
| Platform | Resource health events |

The available alerts depend on the Azure service.

---

# Customization

AMBA serves as a baseline and can be adapted to organizational requirements.

Typical customizations include:

- Alert thresholds
- Severity levels
- Evaluation frequency
- Action Groups
- Resource scope

This allows organizations to maintain consistent monitoring while accommodating workload-specific requirements.

---

# Benefits

Using AMBA provides several advantages.

- Faster monitoring deployment
- Consistent alert configuration
- Reduced implementation effort
- Alignment with Microsoft recommendations
- Easier maintenance of monitoring standards

---

# Considerations

Although AMBA provides a strong baseline, it is not intended to replace workload-specific monitoring.

Additional alert rules may still be required for:

- Business applications
- Custom services
- Security requirements
- Compliance requirements
- Organization-specific operational processes

AMBA should be considered a starting point rather than a complete monitoring solution.

---

# Best Practices

- Use AMBA as the foundation for Azure monitoring.
- Review the deployed alert rules before moving to production.
- Adjust thresholds to match workload characteristics.
- Reuse standardized Action Groups across environments.
- Deploy AMBA using Infrastructure as Code.
- Supplement AMBA with workload-specific alerts where necessary.
