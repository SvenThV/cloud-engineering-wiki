# Azure File Sync

## Overview

Azure File Sync is a Microsoft Azure service that extends on-premises Windows File Servers with cloud capabilities.

Instead of replacing an existing File Server, Azure File Sync synchronizes one or more Windows Servers with an Azure File Share. Existing SMB shares, NTFS permissions and user workflows can remain unchanged while the Azure File Share becomes the central copy of the data.

This section documents the practical implementation of Azure File Sync from an Azure Cloud Engineer's perspective.

---

# Documentation

| Article | Description |
|---------|-------------|
| [Overview](01-overview.md) | Introduction, architecture and core concepts |
| [Configuration](02-configuration.md) | Step-by-step deployment and configuration |
| [Troubleshooting](03-troubleshooting.md) | Common issues and resolutions |

---

# Architecture

```text
                    Azure
+----------------------------------------------+

          Storage Sync Service
                    │
                    │
          Azure File Share
                    ▲
                    │
             Azure File Sync
                 Synchronization
                    │
                    ▼

+----------------------------------------------+
                 On-premises

         Windows File Server
      Azure File Sync Agent
                    │
                    ▼
           Local File System
```

---

# Core Components

Azure File Sync consists of several components.

| Component | Description |
|-----------|-------------|
| Storage Sync Service | Central management resource |
| Sync Group | Connects Azure Files with Windows Servers |
| Cloud Endpoint | Azure File Share participating in synchronization |
| Server Endpoint | Local folder synchronized with Azure Files |
| Azure File Sync Agent | Synchronization agent installed on Windows Server |

---

# Typical Use Cases

Azure File Sync is commonly used for:

- Hybrid file server environments
- Centralized file storage
- Branch office synchronization
- File server migration
- Cloud Tiering
- Disaster recovery

---

# Prerequisites

Before deploying Azure File Sync, the following resources should already exist:

- Azure Subscription
- Storage Account
- Azure File Share
- Windows Server
- Network connectivity between Azure and the Windows Server

---

# Related Azure Services

- Azure Storage Account
- Azure Files
- Azure Backup
- Azure Monitor
