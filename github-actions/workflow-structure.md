# Workflow Structure

## Overview

A GitHub Actions workflow is defined in a YAML file that describes the automation process.

Each workflow specifies:

- When it should run
- Which jobs should be executed
- Which steps each job performs
- Which runner executes the workflow

Every workflow is stored inside the repository.

---

## Workflow Location

Workflow files must be placed in the following directory:

```text
.github/workflows/
```

Example:

```text
my-repository/
│
├── .github/
│   └── workflows/
│       ├── terraform-ci.yml
│       ├── deploy.yml
│       └── nightly-build.yml
│
├── infra/
└── README.md
```

GitHub automatically detects all workflow files stored in this directory.

---

## Basic Workflow Structure

A minimal workflow consists of the following sections:

```yaml
name: Terraform CI

on:
  push:

jobs:
  validate:
    runs-on: ubuntu-latest

    steps:
      - uses: actions/checkout@v4
```

---

## Main Components

Every workflow is built from the following components.

| Component | Purpose |
|----------|---------|
| `name` | Display name of the workflow |
| `on` | Defines which event starts the workflow |
| `jobs` | Collection of jobs executed by the workflow |
| `runs-on` | Defines the runner operating system |
| `steps` | Individual tasks executed within a job |

---

## Workflow Name

The workflow name is displayed in the GitHub Actions overview.

Example:

```yaml
name: Terraform CI
```

Example in GitHub:

```text
Terraform CI
```

Choose short and descriptive workflow names.

---

## Events

The `on` section defines when the workflow starts.

Example:

```yaml
on:
  push:
```

A workflow can also react to multiple events.

Example:

```yaml
on:
  push:
  pull_request:
  workflow_dispatch:
```

The supported events are explained in a separate article.

---

## Jobs

A workflow contains one or more jobs.

Example:

```yaml
jobs:
  validate:
```

Each job:

- runs independently
- executes on its own runner
- contains one or more steps

Multiple jobs run in parallel unless dependencies are configured.

---

## Runner

Each job requires a runner.

Example:

```yaml
runs-on: ubuntu-latest
```

Common runner images include:

| Runner | Operating System |
|---------|------------------|
| `ubuntu-latest` | Linux |
| `windows-latest` | Windows |
| `macos-latest` | macOS |

Every job starts with a fresh runner.

---

## Steps

A job consists of one or more steps.

Example:

```yaml
steps:
  - uses: actions/checkout@v4

  - run: terraform validate
```

Steps are executed sequentially.

If one step fails, the job stops by default.

---

## Complete Example

```yaml
name: Terraform CI

on:
  push:
    branches:
      - main

jobs:
  validate:
    runs-on: ubuntu-latest

    steps:
      - uses: actions/checkout@v4

      - uses: hashicorp/setup-terraform@v3

      - run: terraform init

      - run: terraform validate
```

This workflow:

1. Starts when code is pushed to the `main` branch.
2. Creates a Linux runner.
3. Downloads the repository.
4. Installs Terraform.
5. Initializes the Terraform working directory.
6. Validates the Terraform configuration.

---

## Best Practices

- Use meaningful workflow names.
- Keep workflows small and focused.
- Split large workflows into multiple jobs.
- Store workflow files only in `.github/workflows/`.
- Use descriptive job names.
- Prefer reusable Actions instead of long shell scripts.
