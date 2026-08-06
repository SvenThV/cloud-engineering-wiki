# Azure File Sync Troubleshooting

## Overview

This article describes common issues that may occur when deploying and operating Azure File Sync.

The troubleshooting steps are based on practical deployment experience.

---

# Server Registration Fails

The Windows Server cannot be registered with the Storage Sync Service.

## Possible Causes

- Incorrect Azure account
- Missing Azure permissions
- Internet connectivity issues
- Azure File Sync Agent not installed correctly

## Resolution

Verify:

- Azure sign-in
- Subscription
- Resource Group
- Storage Sync Service
- Network connectivity

Restart the Server Registration wizard if necessary.

---

# Server Does Not Appear in Azure

The registration completed successfully, but the server does not appear under **Registered servers**.

## Resolution

- Refresh the Azure portal.
- Verify that the correct Storage Sync Service was selected.
- Wait a few minutes for synchronization.

---

# Synchronization Does Not Start

Files are not synchronized between the Windows Server and Azure Files.

## Verify

- Server Endpoint exists.
- Cloud Endpoint exists.
- Storage Sync Service is healthy.
- Azure File Sync Agent is running.

Also verify that the Sync Group reports a healthy status.

---

# Synchronization Is Delayed

Azure File Sync is not a real-time synchronization service.

Small synchronization delays are normal.

Wait several minutes before troubleshooting further.

---

# Storage Account Name Already Exists

Storage Account names must be globally unique across Microsoft Azure.

If the selected name is already in use, choose another unique name.

---

# Resource Group Cannot Be Deleted

A Resource Group may remain in the **Deleting** state for several minutes.

Verify that no dependent resources still exist.

Refresh the Azure portal after a few minutes.

---

# Internet Explorer Enhanced Security Configuration

On Windows Server, Internet Explorer Enhanced Security Configuration may prevent downloading the Azure File Sync Agent.

Possible solutions:

- Use Microsoft Edge.
- Temporarily disable IE Enhanced Security Configuration.
- Download the installer on another computer.

---

# Verify Synchronization

A healthy deployment should meet the following conditions.

- Storage Sync Service status: Healthy
- Registered Server: Online
- Sync Group: Healthy
- Upload to cloud completed
- Download to server completed

![Sync Group Health](images/azure-file-sync-sync-group.png)

---

# Verify Local Synchronization

Create a test file inside the synchronized folder.

Example:

```text
C:\FileSync\Test.txt
```

Verify that the file appears in the Azure File Share.

![Local Folder](images/azure-file-sync-local-folder.png)

↓

![Azure File Share](images/azure-file-sync-file-share.png)

---

# Best Practices

- Verify synchronization after every configuration change.
- Register servers using an Azure account with sufficient permissions.
- Use descriptive names for Sync Groups and Server Endpoints.
- Monitor the health status of the Storage Sync Service regularly.
- Test synchronization before using Azure File Sync in production.
