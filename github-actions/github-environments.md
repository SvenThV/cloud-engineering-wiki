# GitHub Environments

## Overview

GitHub Environments provide an additional security layer for deployment workflows.

An environment represents a deployment target such as:

- Development
- Test
- Production

Each environment can have its own configuration, secrets, and approval requirements.

---

## Why Use Environments?

Environments help protect deployment workflows by allowing different settings for different stages.

Typical use cases include:

- Deployment approvals
- Environment-specific secrets
- Deployment protection rules
- Production safeguards

---

## Creating an Environment

Environments can be created in:

```text
Repository
→ Settings
→ Environments
```

Example:

```text
Development

Test

Production
```

---

## Using an Environment

An environment is assigned at the job level.

Example:

```yaml
jobs:

  deploy:
    runs-on: ubuntu-latest

    environment:
      name: Production
```

When the workflow reaches this job, GitHub applies the configured protection rules.

---

## Required Reviewers

One or more reviewers can be required before a deployment starts.

Example:

```text
Production

↓

Reviewer Approval

↓

Deployment
```

This helps prevent accidental deployments to production.

---

## Environment Secrets

Each environment can store its own secrets.

Example:

```text
Development

AZURE_SUBSCRIPTION_ID

↓

Production

AZURE_SUBSCRIPTION_ID
```

Although the secret names are identical, the values can differ.

This makes it easy to deploy the same workflow to multiple environments.

---

## Deployment Protection Rules

GitHub supports several protection mechanisms.

Examples include:

- Required reviewers
- Wait timers
- Deployment branch restrictions

These rules are configured per environment.

---

## Example Workflow

```yaml
jobs:

  deploy:

    runs-on: ubuntu-latest

    environment:
      name: Production

    steps:

      - uses: actions/checkout@v4

      - run: echo "Deploying..."
```

If approval is required, the workflow pauses until the deployment is approved.

---

## Typical Environment Structure

```text
Development
│
├── Environment Secrets
└── Automatic Deployment

Test
│
├── Environment Secrets
└── Optional Approval

Production
│
├── Environment Secrets
├── Required Reviewers
└── Protected Deployment
```

---

## Repository Secrets vs Environment Secrets

| Repository Secrets | Environment Secrets |
|--------------------|---------------------|
| Available to all workflows | Available only within the selected environment |
| Shared across all environments | Environment-specific |
| Suitable for common values | Suitable for deployment-specific credentials |

---

## Best Practices

- Create separate environments for Development, Test, and Production.
- Store production credentials as Environment Secrets.
- Require approvals before production deployments.
- Use meaningful environment names.
- Keep deployment protection rules simple and consistent.
