# Workflow Events

## Overview

Workflow events determine when a GitHub Actions workflow is executed.

Events are configured in the `on` section of a workflow.

A workflow can react to one or multiple events.

Example:

```yaml
on:
  push:
```

---

## Common Events

The following events are commonly used in GitHub Actions.

| Event | Description |
|--------|-------------|
| `push` | Triggered when commits are pushed to a repository |
| `pull_request` | Triggered when a pull request is opened, updated, or merged |
| `workflow_dispatch` | Allows manual execution of a workflow |
| `schedule` | Executes a workflow based on a cron schedule |

---

## Push

The `push` event starts a workflow whenever commits are pushed to a repository.

Example:

```yaml
on:
  push:
```

To limit execution to a specific branch:

```yaml
on:
  push:
    branches:
      - main
```

Typical use cases:

- Run CI pipelines
- Validate Terraform code
- Execute automated tests

---

## Pull Request

The `pull_request` event starts a workflow whenever a pull request is created or updated.

Example:

```yaml
on:
  pull_request:
```

Restrict execution to specific branches:

```yaml
on:
  pull_request:
    branches:
      - main
```

Typical use cases:

- Validate changes before merging
- Run tests
- Perform code quality checks

---

## Workflow Dispatch

The `workflow_dispatch` event allows a workflow to be started manually from the GitHub Actions page.

Example:

```yaml
on:
  workflow_dispatch:
```

Typical use cases:

- Manual Terraform plan
- Manual deployments
- Testing workflows

---

## Schedule

The `schedule` event executes workflows automatically based on a cron expression.

Example:

```yaml
on:
  schedule:
    - cron: '0 2 * * *'
```

This example runs the workflow every day at **02:00 UTC**.

Typical use cases:

- Nightly builds
- Scheduled backups
- Dependency updates
- Maintenance tasks

---

## Multiple Events

A workflow can listen to multiple events.

Example:

```yaml
on:
  push:
    branches:
      - main

  pull_request:
    branches:
      - main

  workflow_dispatch:
```

The workflow starts when **any** configured event occurs.

---

## Event Filters

Many events support additional filters.

Example:

```yaml
on:
  push:
    branches:
      - main
      - develop
```

You can also exclude branches.

Example:

```yaml
on:
  push:
    branches-ignore:
      - experimental
```

---

## Best Practices

- Use `push` for Continuous Integration.
- Use `pull_request` to validate changes before merging.
- Use `workflow_dispatch` for manual operations.
- Use `schedule` only for recurring tasks.
- Limit workflows to the required branches whenever possible.
