# OIDC Authentication

## Overview

OpenID Connect (OIDC) is the recommended authentication method for GitHub Actions when deploying resources to Microsoft Azure.

Instead of storing a long-lived client secret in GitHub, OIDC uses short-lived access tokens issued during workflow execution.

This approach improves security by eliminating the need to manage client secrets.

---

## Why Use OIDC?

Traditional authentication requires a Service Principal and a client secret.

```text
GitHub
    │
Client Secret
    │
    ▼
Azure
```

With OIDC, GitHub requests a temporary identity token, which Azure validates before issuing an access token.

```text
GitHub Actions
      │
OIDC Identity Token
      │
      ▼
Microsoft Entra ID
      │
Temporary Access Token
      │
      ▼
Azure Resources
```

---

## Benefits

Compared to client secrets, OIDC provides several advantages.

- No client secret stored in GitHub
- Temporary access tokens
- Reduced secret management
- Improved security
- Recommended by Microsoft

---

## Requirements

Before using OIDC, the following components must be configured:

- Microsoft Entra ID Application
- Federated Credential
- GitHub Repository
- Azure Login Action

---

## Workflow Permissions

To allow GitHub to request an identity token, the workflow must include the following permission:

```yaml
permissions:
  id-token: write
  contents: read
```

Without this permission, Azure authentication using OIDC will fail.

---

## Azure Login

Authentication is performed using the Azure Login Action.

Example:

```yaml
- uses: azure/login@v2
  with:
    client-id: ${{ secrets.AZURE_CLIENT_ID }}
    tenant-id: ${{ secrets.AZURE_TENANT_ID }}
    subscription-id: ${{ secrets.AZURE_SUBSCRIPTION_ID }}
```

Unlike traditional authentication, no client secret is required.

---

## Authentication Flow

```text
GitHub Actions
        │
        ▼
Request OIDC Token
        │
        ▼
Microsoft Entra ID
        │
        ▼
Issue Temporary Access Token
        │
        ▼
Azure Login
        │
        ▼
Azure Resources
```

---

## OIDC vs Client Secret

| OIDC | Client Secret |
|------|---------------|
| No client secret required | Client secret required |
| Temporary access tokens | Long-lived credentials |
| Recommended by Microsoft | Legacy approach |
| Reduced secret management | Secret rotation required |
| Higher security | Higher risk if secret is compromised |

---

## Common Errors

### Azure Login fails

Possible causes:

- Missing `id-token: write`
- Incorrect Federated Credential
- Incorrect Client ID
- Incorrect Tenant ID
- Incorrect Subscription ID

---

### No Federated Credential found

Verify that:

- The GitHub repository matches the configured repository.
- The GitHub branch matches the configured branch.
- The correct Microsoft Entra ID Application is used.

---

## Best Practices

- Prefer OIDC over client secrets.
- Grant only the required Azure permissions.
- Use separate Service Principals for different environments.
- Store only non-sensitive IDs as GitHub Secrets.
- Use GitHub Environments for production deployments.
