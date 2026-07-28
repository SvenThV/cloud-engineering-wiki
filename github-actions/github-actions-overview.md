# GitHub Actions

## Overview

GitHub Actions is GitHub's built-in automation platform for implementing Continuous Integration (CI) and Continuous Delivery/Deployment (CD) workflows.

Workflows are defined as YAML files and executed automatically in response to repository events, such as pushing code, creating a pull request, or manually triggering a workflow.

GitHub Actions can be used to automate software development tasks including:

- Building applications
- Running tests
- Validating Infrastructure as Code (IaC)
- Deploying applications
- Publishing artifacts
- Automating repetitive tasks

---

# Continuous Integration (CI)

Continuous Integration (CI) is the practice of automatically validating code changes whenever developers push commits to a repository.

The primary goal is to detect issues as early as possible and ensure that changes can be safely integrated into the main branch.

Typical CI tasks include:

- Code formatting
- Static code analysis
- Dependency installation
- Build validation
- Unit testing
- Terraform validation

---

# Continuous Delivery (CD)

Continuous Delivery extends CI by automatically preparing software for deployment.

Deployment packages, artifacts, or infrastructure plans are generated automatically, while the actual deployment is typically approved manually.

Typical CD tasks include:

- Building deployment packages
- Creating Terraform execution plans
- Publishing build artifacts
- Preparing production deployments

---

# Continuous Deployment

Continuous Deployment goes one step further by automatically deploying validated changes to the target environment without requiring manual approval.

This approach is commonly used for development or testing environments where rapid feedback is important.

Typical deployment targets include:

- Azure App Service
- Azure Container Apps
- Azure Kubernetes Service (AKS)
- Virtual Machines
- Static Web Apps

---

# Typical CI/CD Workflow

A typical GitHub Actions workflow follows these steps:

```text
Developer
    │
    │ git push
    ▼
GitHub Repository
    │
    ▼
GitHub Actions Workflow
    │
    ├── Checkout Repository
    ├── Setup Environment
    ├── Validate Code
    ├── Run Tests
    ├── Build / Package
    └── Deploy (optional)
```

---

# Core Components

GitHub Actions consists of several core components.

| Component | Description |
|----------|-------------|
| Workflow | YAML file defining the automation process |
| Event | Determines when a workflow starts |
| Job | A collection of steps executed on a runner |
| Step | A single task executed within a job |
| Runner | Virtual machine that executes a workflow |
| Action | Reusable automation component |

Each component is explained in detail in the following articles.

---

# Common Use Cases

GitHub Actions is commonly used for:

- Infrastructure as Code validation
- Terraform CI pipelines
- Application testing
- Container image builds
- Security scanning
- Automated deployments
- Scheduled maintenance tasks
- Release automation

---

# Benefits

Using GitHub Actions provides several advantages:

- Native GitHub integration
- YAML-based workflow definitions
- Hosted Linux, Windows, and macOS runners
- Large marketplace of reusable Actions
- Built-in support for Secrets and Environments
- Easy integration with cloud providers such as Microsoft Azure
