# Terraform CI Example

## Overview

Terraform is commonly used together with GitHub Actions to automatically validate Infrastructure as Code (IaC).

A typical Continuous Integration (CI) workflow performs the following tasks:

- Checkout the repository
- Install Terraform
- Check formatting
- Initialize Terraform
- Validate the configuration
- Generate an execution plan (optional)

---

## Typical Workflow

```text
Developer
    │
    │ git push
    ▼
GitHub Actions
    │
    ├── Checkout Repository
    ├── Setup Terraform
    ├── Terraform Format Check
    ├── Terraform Init
    ├── Terraform Validate
    └── Terraform Plan (optional)
```

---

## Example Workflow

```yaml
name: Terraform CI

on:
  push:
    branches:
      - main

jobs:
  validate:

    runs-on: ubuntu-latest

    defaults:
      run:
        working-directory: infra

    permissions:
      id-token: write
      contents: read

    steps:

      - name: Checkout Repository
        uses: actions/checkout@v4

      - name: Setup Terraform
        uses: hashicorp/setup-terraform@v3
        with:
          terraform_version: 1.13.0

      - name: Terraform Format Check
        run: terraform fmt -check

      - name: Terraform Init
        run: terraform init

      - name: Terraform Validate
        run: terraform validate
```

---

## Workflow Explanation

| Step | Purpose |
|------|---------|
| Checkout Repository | Downloads the repository to the runner |
| Setup Terraform | Installs the required Terraform version |
| Terraform Format Check | Verifies formatting (`terraform fmt -check`) |
| Terraform Init | Downloads providers and initializes Terraform |
| Terraform Validate | Validates the Terraform configuration |

---

## Adding Terraform Plan

To generate an execution plan, add an additional step.

```yaml
- name: Terraform Plan
  run: terraform plan
```

Terraform Plan usually requires Azure authentication.

A common approach is to authenticate using OIDC before executing the plan.

---

## Working Directory

If the Terraform configuration is stored inside a subdirectory, specify the working directory.

Example:

```yaml
defaults:
  run:
    working-directory: infra
```

Without this configuration, Terraform searches for `.tf` files in the repository root.

---

## Common Errors

### No configuration files

Cause:

Terraform configuration files are located in a different directory.

Solution:

```yaml
defaults:
  run:
    working-directory: infra
```

---

### Please run az login

Cause:

Azure authentication is missing.

Solution:

Authenticate before executing Terraform.

Example:

```yaml
- uses: azure/login@v2
```

---

### Duplicate provider configuration

Cause:

The same Terraform provider is configured multiple times.

Solution:

Keep only one provider configuration for each provider.

---

## Best Practices

- Keep CI and CD workflows separate.
- Use descriptive step names.
- Pin Action versions (for example `@v4` or `@v3`).
- Validate Terraform before generating a plan.
- Use OIDC for Azure authentication.
- Store Terraform code in a dedicated directory (for example `infra/`).
- Keep workflows small and easy to maintain.
