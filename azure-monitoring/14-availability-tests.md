# Availability Tests

## Overview

Availability Tests continuously monitor the availability and responsiveness of an application by sending requests from multiple Azure locations.

They help detect outages, increased response times, expired certificates, and other issues before they impact users.

Availability Tests are part of Application Insights.

---

# How Availability Tests Work

```text
Azure Test Locations
        │
        ▼
HTTP/HTTPS Request
        │
        ▼
Application Endpoint
        │
        ▼
Application Insights
        │
        ├── Availability Results
        ├── Response Time
        ├── Success Rate
        └── Alerts
```

---

# Test Types

Azure supports different types of Availability Tests.

| Test Type | Description |
|-----------|-------------|
| Standard Test | Sends HTTP or HTTPS requests from multiple Azure regions |
| Custom Test | Executes custom test logic using Azure Monitor |
| TrackAvailability API | Allows applications to report custom availability results |

---

# What Is Monitored?

Availability Tests collect information such as:

- Response status
- Response time
- DNS resolution
- SSL/TLS certificate validation
- Endpoint availability
- Redirect behavior

---

# Test Configuration

A typical Availability Test includes the following settings.

| Setting | Description |
|---------|-------------|
| URL | Endpoint to monitor |
| Test Frequency | Interval between requests |
| Test Locations | Azure regions performing the test |
| Success Criteria | Expected HTTP status code or response |
| Timeout | Maximum allowed response time |

---

# Test Locations

Availability Tests can be executed from multiple Azure regions around the world.

Using multiple locations helps distinguish between:

- Regional outages
- Network connectivity issues
- Global application failures

Testing from different locations also reduces the risk of false positives caused by temporary regional network issues.

---

# Success Criteria

A test is considered successful when the configured validation criteria are met.

Typical criteria include:

- HTTP 200 response
- Maximum response time
- Expected response content
- Valid SSL/TLS certificate

If one or more checks fail, the test is marked as unsuccessful.

---

# Alert Integration

Availability Tests can trigger Azure Monitor Alerts.

Common alert scenarios include:

- Website unavailable
- Response time exceeds threshold
- Multiple test locations report failures
- Certificate validation fails

The alert can trigger an Action Group to notify administrators or start automated remediation.

---

# Common Use Cases

Availability Tests are commonly used for:

- Public websites
- REST APIs
- Web applications
- Customer portals
- Internal business applications
- Critical service endpoints

---

# Best Practices

- Monitor all business-critical applications.
- Configure multiple Azure test locations.
- Use realistic success criteria.
- Create alerts for failed availability tests.
- Regularly review response time trends.
- Combine Availability Tests with Application Insights telemetry for comprehensive monitoring.
