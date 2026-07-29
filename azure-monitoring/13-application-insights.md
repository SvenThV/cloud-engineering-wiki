# Application Insights

## Overview

Application Insights is Azure's Application Performance Monitoring (APM) service.

It helps developers and operations teams monitor the availability, performance, and usage of applications. In addition to infrastructure monitoring, Application Insights provides detailed insights into application behavior, request processing, dependencies, exceptions, and user interactions.

Application Insights integrates with Azure Monitor and stores its telemetry in a Log Analytics Workspace when using workspace-based mode.

---

# What Can Be Monitored?

Application Insights collects application telemetry such as:

- Incoming requests
- Response times
- Failed requests
- Exceptions
- Dependencies
- Availability tests
- User sessions
- Custom events
- Custom metrics

---

# Architecture

```text
Application
      │
      ▼
Application Insights SDK
      │
      ▼
Application Insights
      │
      ▼
Log Analytics Workspace
      │
 ┌────┼──────────────┐
 ▼    ▼              ▼
KQL Alerts      Workbooks
```

---

# Data Collection

Telemetry can be collected automatically or manually.

| Collection Method | Description |
|-------------------|-------------|
| Automatic Instrumentation | Minimal configuration for supported platforms |
| Application SDK | Integrated into the application code |
| OpenTelemetry | Vendor-neutral telemetry collection |

The supported options depend on the application platform and hosting environment.

---

# Common Telemetry

| Telemetry Type | Description |
|----------------|-------------|
| Requests | Incoming client requests |
| Dependencies | Outbound calls to databases or APIs |
| Exceptions | Application errors and unhandled exceptions |
| Traces | Diagnostic log messages |
| Availability | Results from availability tests |
| Custom Events | User-defined application events |
| Custom Metrics | User-defined performance metrics |

---

# Key Features

Application Insights provides several built-in monitoring capabilities.

| Feature | Purpose |
|---------|---------|
| Live Metrics | View real-time application performance |
| Failures | Analyze failed requests and exceptions |
| Performance | Identify slow operations |
| Application Map | Visualize application dependencies |
| Availability | Monitor endpoint availability |
| Logs | Query telemetry using KQL |

---

# Application Map

The Application Map provides a visual representation of application components and their dependencies.

It helps identify:

- Backend services
- External API calls
- Database connections
- Failed dependencies
- Performance bottlenecks

---

# Live Metrics

Live Metrics provides near real-time monitoring without waiting for log ingestion.

Typical metrics include:

- Request rate
- Response time
- Failed requests
- CPU usage
- Memory usage

Live Metrics is particularly useful during deployments or incident investigations.

---

# Performance Monitoring

Application Insights automatically measures request performance.

Examples include:

- Average response time
- Slowest requests
- Request duration trends
- Dependency duration
- Server response times

This helps identify performance bottlenecks before they impact users.

---

# Exception Monitoring

Exceptions are automatically collected and categorized.

Typical information includes:

- Exception type
- Error message
- Stack trace
- Request details
- Timestamp
- Affected operation

This simplifies troubleshooting and root cause analysis.

---

# Distributed Tracing

Application Insights supports distributed tracing across multiple services.

Example:

```text
Web Application
       │
       ▼
API Service
       │
       ▼
Database
```

A single user request can be traced across all application components, making it easier to diagnose failures and performance issues.

---

# Typical Use Cases

Application Insights is commonly used for:

- Application performance monitoring
- Error analysis
- Root cause analysis
- Dependency monitoring
- Availability monitoring
- Performance optimization
- Application troubleshooting

---

# Best Practices

- Use workspace-based Application Insights for new deployments.
- Enable distributed tracing for multi-service applications.
- Monitor failed requests and exceptions proactively.
- Configure Availability Tests for critical applications.
- Use KQL to investigate application telemetry.
- Combine Application Insights with Azure Monitor Alerts for proactive monitoring.
