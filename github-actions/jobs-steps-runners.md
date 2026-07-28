# Jobs, Steps and Runners

## Overview

Every GitHub Actions workflow consists of one or more **jobs**.

Each job is executed on its own **runner** and contains one or more **steps**.

Understanding the relationship between jobs, steps, and runners is essential when designing GitHub Actions workflows.

---

## Workflow Hierarchy

The following diagram illustrates the hierarchy of a GitHub Actions workflow.

```text
Workflow
│
├── Job
│     ├── Step
│     ├── Step
│     └── Step
│
└── Job
      ├── Step
      └── Step
```

---

## Jobs

A job is a collection of steps that run on the same runner.

Example:

```yaml
jobs:
  validate:
```

A workflow may contain:

- One job
- Multiple independent jobs
- Multiple dependent jobs

By default, jobs run in parallel.

---

## Job Example

```yaml
jobs:
  validate:
    runs-on: ubuntu-latest

    steps:
      - uses: actions/checkout@v4

      - run: terraform validate
```

In this example:

- The workflow contains one job.
- The job is named `validate`.
- It runs on an Ubuntu runner.
- It contains two steps.

---

## Steps

A step is a single task executed within a job.

Examples include:

- Checking out the repository
- Installing software
- Running a script
- Executing Terraform commands

Example:

```yaml
steps:
  - uses: actions/checkout@v4

  - run: terraform fmt -check

  - run: terraform validate
```

Steps always execute sequentially.

If one step fails, the remaining steps are skipped unless configured otherwise.

---

## Runner

A runner is the virtual machine that executes a job.

Each job receives a fresh runner.

Example:

```yaml
runs-on: ubuntu-latest
```

Supported GitHub-hosted runners include:

| Runner | Operating System |
|---------|------------------|
| `ubuntu-latest` | Linux |
| `windows-latest` | Windows |
| `macos-latest` | macOS |

GitHub automatically provisions and removes hosted runners after the job finishes.

---

## Fresh Runner for Every Job

Every job starts on a clean virtual machine.

For example:

```text
Job 1
↓
ubuntu-latest
↓
Runner is deleted

Job 2
↓
New ubuntu-latest runner
↓
Runner is deleted
```

No files are shared between jobs automatically.

To transfer files between jobs, use **Artifacts**.

---

## Multiple Jobs

A workflow can contain multiple jobs.

Example:

```yaml
jobs:

  format:
    runs-on: ubuntu-latest

  validate:
    runs-on: ubuntu-latest

  plan:
    runs-on: ubuntu-latest
```

Without dependencies, all three jobs run in parallel.

---

## Job Dependencies

Dependencies can be created using `needs`.

Example:

```yaml
jobs:

  format:
    runs-on: ubuntu-latest

  validate:
    needs: format
    runs-on: ubuntu-latest

  plan:
    needs: validate
    runs-on: ubuntu-latest
```

Execution order:

```text
Format
   │
   ▼
Validate
   │
   ▼
Plan
```

---

## Example Workflow

```yaml
jobs:

  validate:
    runs-on: ubuntu-latest

    steps:
      - uses: actions/checkout@v4

      - uses: hashicorp/setup-terraform@v3

      - run: terraform init

      - run: terraform validate
```

Execution flow:

```text
Workflow
    │
    ▼
Validate Job
    │
    ├── Checkout
    ├── Setup Terraform
    ├── Terraform Init
    └── Terraform Validate
```

---

## Best Practices

- Use meaningful job names.
- Keep jobs focused on a single purpose.
- Split large workflows into multiple jobs.
- Use `needs` only when a dependency exists.
- Remember that each job starts with a fresh runner.
- Keep steps small and easy to understand.
