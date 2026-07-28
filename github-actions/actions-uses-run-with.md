# Actions: uses, run and with

## Overview

GitHub Actions workflows consist of individual steps.

Each step typically uses one of two approaches:

- Execute an existing GitHub Action using `uses`
- Execute shell commands using `run`

Some Actions also accept additional parameters through `with`.

---

## The `uses` Keyword

The `uses` keyword executes an existing GitHub Action.

Actions are reusable building blocks published by GitHub or the community.

Example:

```yaml
- uses: actions/checkout@v4
```

Another example:

```yaml
- uses: hashicorp/setup-terraform@v3
```

Azure example:

```yaml
- uses: azure/login@v2
```

Typical use cases:

- Checkout the repository
- Install Terraform
- Authenticate to Azure
- Upload artifacts
- Download artifacts

---

## The `run` Keyword

The `run` keyword executes shell commands directly on the runner.

Example:

```yaml
- run: terraform validate
```

Multiple commands can be executed.

Example:

```yaml
- run: |
    terraform init
    terraform validate
    terraform plan
```

Typical use cases:

- Execute Terraform commands
- Run scripts
- Install software
- Execute tests

---

## The `with` Keyword

The `with` keyword passes input parameters to an Action.

It is only used together with `uses`.

Example:

```yaml
- uses: hashicorp/setup-terraform@v3
  with:
    terraform_version: 1.13.0
```

Azure example:

```yaml
- uses: azure/login@v2
  with:
    client-id: ${{ secrets.AZURE_CLIENT_ID }}
    tenant-id: ${{ secrets.AZURE_TENANT_ID }}
    subscription-id: ${{ secrets.AZURE_SUBSCRIPTION_ID }}
```

---

## Comparison

| Keyword | Purpose |
|----------|---------|
| `uses` | Executes an existing GitHub Action |
| `run` | Executes shell commands on the runner |
| `with` | Passes parameters to an Action |

---

## Complete Example

```yaml
steps:

  - uses: actions/checkout@v4

  - uses: hashicorp/setup-terraform@v3
    with:
      terraform_version: 1.13.0

  - run: terraform init

  - run: terraform validate
```

Execution order:

```text
Checkout Repository
        │
        ▼
Setup Terraform
        │
        ▼
Terraform Init
        │
        ▼
Terraform Validate
```

---

## Common GitHub Actions

The following Actions are commonly used.

| Action | Purpose |
|---------|---------|
| `actions/checkout` | Downloads the repository onto the runner |
| `hashicorp/setup-terraform` | Installs Terraform |
| `azure/login` | Authenticates to Azure |
| `actions/upload-artifact` | Uploads files for later jobs |
| `actions/download-artifact` | Downloads previously uploaded artifacts |

---

## Best Practices

- Prefer `uses` whenever a suitable Action already exists.
- Use `run` for custom commands and scripts.
- Use `with` only for Actions that support input parameters.
- Pin Action versions (for example `@v4` or `@v3`) instead of using floating versions.
- Keep shell commands short and easy to understand.
