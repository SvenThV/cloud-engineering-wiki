# Common Errors

## Overview

This page summarizes common GitHub Actions and Terraform CI errors together with their typical causes and solutions.

---

## No configuration files

### Error

```text
No configuration files
```

### Cause

Terraform could not find any `.tf` files.

This usually happens when the Terraform configuration is stored in a subdirectory instead of the repository root.

### Solution

Specify the working directory.

Example:

```yaml
defaults:
  run:
    working-directory: infra
```

---

## Terraform command not found

### Error

```text
terraform: command not found
```

### Cause

Terraform has not been installed on the runner.

### Solution

Install Terraform before executing any Terraform commands.

Example:

```yaml
- uses: hashicorp/setup-terraform@v3
```

---

## Repository files not found

### Error

```text
No such file or directory
```

or

```text
Terraform configuration not found
```

### Cause

The repository was not checked out.

Without checkout, the runner does not contain any repository files.

### Solution

Add the Checkout Action.

Example:

```yaml
- uses: actions/checkout@v4
```

---

## Please run az login

### Error

```text
Please run az login
```

### Cause

Terraform tries to authenticate with Azure, but no Azure login has been performed.

### Solution

Authenticate before executing Terraform.

Example:

```yaml
- uses: azure/login@v2
```

---

## Authentication failed

### Error

Azure authentication fails.

### Possible Causes

- Incorrect Client ID
- Incorrect Tenant ID
- Incorrect Subscription ID
- Missing permissions
- Invalid Federated Credential

### Solution

Verify:

- Azure Login configuration
- GitHub Secrets
- Microsoft Entra ID configuration

---

## Duplicate provider configuration

### Error

```text
Duplicate provider configuration
```

### Cause

The same Terraform provider has been declared multiple times.

### Solution

Keep only one provider configuration for each provider.

---

## Workflow not triggered

### Cause

The configured event does not match the current action.

Examples:

- Wrong branch
- Wrong event
- Workflow file stored in the wrong directory

### Solution

Verify:

- `on`
- Branch filters
- `.github/workflows/`

---

## Secret not found

### Error

```text
Secret not found
```

### Cause

The referenced secret does not exist.

Example:

```yaml
${{ secrets.AZURE_CLIENT_SECRET }}
```

### Solution

Verify that the secret exists under:

```text
Repository
→ Settings
→ Secrets and variables
→ Actions
```

---

## Invalid YAML syntax

### Error

The workflow cannot be parsed.

### Cause

Invalid YAML formatting.

Common examples:

- Incorrect indentation
- Missing colon (`:`)
- Invalid list syntax

### Solution

Validate the YAML file and check the indentation.

---

## Permission denied

### Cause

The workflow identity does not have sufficient Azure permissions.

### Solution

Verify:

- Azure Role Assignment
- Federated Credential
- Subscription scope

---

## Runner timeout

### Cause

The workflow exceeds the maximum execution time.

### Solution

- Optimize the workflow.
- Split long-running jobs.
- Cache dependencies whenever possible.

---

## Best Practices

- Read the complete error message.
- Review the workflow logs step by step.
- Verify the YAML syntax first.
- Check Azure authentication before troubleshooting Terraform.
- Test Terraform locally before pushing changes.
- Keep workflows simple and easy to debug.
