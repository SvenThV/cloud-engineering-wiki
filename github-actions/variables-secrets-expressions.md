# Variables, Secrets and Expressions

## Overview

GitHub Actions provides several mechanisms for passing values to workflows.

The most common options are:

- Environment Variables (`env`)
- Secrets (`secrets`)
- Expressions (`${{ }}`)

Choosing the correct option improves security, readability, and maintainability.

---

## Environment Variables (`env`)

Environment variables store configuration values that are **not sensitive**.

Typical examples include:

- Azure region
- Environment name
- Terraform version
- Resource names

Example:

```yaml
env:
  LOCATION: westeurope
  ENVIRONMENT: dev
```

Variables can be defined at different levels:

- Workflow
- Job
- Step

Example:

```yaml
env:
  LOCATION: westeurope

jobs:
  validate:
    runs-on: ubuntu-latest

    steps:
      - run: echo $LOCATION
```

---

## Secrets

Secrets store confidential information.

Typical examples include:

- Client Secrets
- API Keys
- Access Tokens
- Personal Access Tokens (PAT)

Example:

```yaml
${{ secrets.AZURE_CLIENT_SECRET }}
```

Secrets are managed through:

```text
Repository
→ Settings
→ Secrets and variables
→ Actions
```

GitHub automatically masks secret values in workflow logs.

> **Important**
>
> Never store passwords, connection strings, or API keys directly in a workflow file.

---

## Expressions

Expressions allow dynamic values to be evaluated during workflow execution.

Syntax:

```yaml
${{ ... }}
```

Examples:

```yaml
${{ github.actor }}

${{ github.ref }}

${{ github.ref_name }}

${{ env.LOCATION }}

${{ secrets.AZURE_CLIENT_SECRET }}
```

Expressions can access information from:

- GitHub
- Environment variables
- Secrets
- Workflow context
- Previous jobs and steps

---

## Common Contexts

Frequently used GitHub contexts include:

| Expression | Description |
|------------|-------------|
| `${{ github.actor }}` | User who triggered the workflow |
| `${{ github.ref }}` | Full Git reference |
| `${{ github.ref_name }}` | Branch or tag name |
| `${{ github.repository }}` | Repository name |
| `${{ github.sha }}` | Commit SHA |

---

## Using Variables

Example:

```yaml
env:
  LOCATION: westeurope

steps:
  - run: echo $LOCATION
```

---

## Using Secrets

Example:

```yaml
steps:
  - run: echo "Deploying..."

    env:
      CLIENT_SECRET: ${{ secrets.AZURE_CLIENT_SECRET }}
```

Secrets should only be exposed when required.

---

## Combining Variables and Expressions

Example:

```yaml
env:
  LOCATION: westeurope

steps:
  - run: echo "Deploying to ${{ env.LOCATION }}"
```

---

## Variables vs Secrets

| Environment Variables | Secrets |
|------------------------|---------|
| Not confidential | Confidential |
| Visible in workflow files | Stored securely by GitHub |
| Suitable for configuration | Suitable for credentials |
| Can be printed | Automatically masked in logs |

---

## Best Practices

- Store configuration values in `env`.
- Store sensitive values in `Secrets`.
- Never hard-code credentials.
- Use expressions instead of duplicated values.
- Keep secret names descriptive and consistent.
- Remove unused secrets regularly.
