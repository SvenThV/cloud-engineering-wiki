# Platform Metrics

## Overview

Platform Metrics are numeric measurements automatically collected by Azure for supported resources.

They provide near real-time information about the performance, utilization, and health of Azure resources without requiring additional configuration.

Unlike logs, metrics are lightweight, aggregated, and optimized for monitoring and alerting.

---

# Characteristics

Platform Metrics have the following characteristics:

- Automatically collected by Azure
- Near real-time data
- Numeric values only
- Low latency
- Optimized for dashboards and alerts
- Short-term retention (depending on metric type)

---

# Typical Metrics

The available metrics depend on the Azure resource.

Examples include:

| Resource | Typical Metrics |
|----------|-----------------|
| Virtual Machine | CPU Percentage, Network In/Out, Disk IOPS |
| Storage Account | Transactions, Availability, Egress, Ingress |
| App Service | Requests, Response Time, CPU Time |
| Azure SQL Database | DTU Percentage, CPU Percentage, Connections |
| Application Gateway | Throughput, Failed Requests |
| Key Vault | Service API Hits, Availability |

---

# Metric Aggregations

Metrics can be aggregated in different ways.

| Aggregation | Description |
|-------------|-------------|
| Average | Average value during the selected period |
| Minimum | Lowest recorded value |
| Maximum | Highest recorded value |
| Total | Sum of all values |
| Count | Number of collected samples |

The available aggregations depend on the selected metric.

---

# Metrics Explorer

The Metrics Explorer is the primary tool for visualizing platform metrics.

It allows you to:

- Select resources
- Choose metrics
- Change the aggregation
- Configure the time range
- Split metrics by dimensions
- Pin charts to dashboards

---

# Dimensions

Some metrics support dimensions.

Dimensions allow filtering or splitting a metric into multiple data series.

Example:

```text
Metric:
Requests

Dimension:
HTTP Status Code

Results:
200
301
404
500
```

This makes it easier to identify specific trends or issues.

---

# Typical Use Cases

Platform Metrics are commonly used for:

- CPU monitoring
- Memory utilization (supported services)
- Storage performance
- Network throughput
- Request rate monitoring
- Capacity planning
- Metric-based alerting

---

# Metrics vs Logs

Platform Metrics and Logs serve different purposes.

| Platform Metrics | Logs |
|------------------|------|
| Numeric values | Detailed events |
| Near real-time | Event-based |
| Low storage requirements | Larger data volume |
| Optimized for dashboards | Optimized for investigation |
| Used for Metric Alerts | Queried using KQL |

---

# Example

A Virtual Machine reports the following CPU utilization.

```text
Time        CPU

10:00       18%
10:01       22%
10:02       31%
10:03       75%
10:04       84%
```

A Metric Alert can be configured to trigger if the average CPU usage exceeds a defined threshold.

---

# Best Practices

- Use metrics for operational monitoring.
- Use Metric Alerts whenever possible.
- Monitor long-term trends using aggregations.
- Combine metrics with logs for troubleshooting.
- Monitor only meaningful metrics to avoid unnecessary alerts.
