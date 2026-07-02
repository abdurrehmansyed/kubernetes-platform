# ADR-0002: Use Free and Open-Source Technology Stack

## Status

Accepted

## Date

2026-07-02

## Context

The Kubernetes Platform project is intended to demonstrate how a production-style platform can be designed, automated, secured, operated, and documented from scratch.

The platform should be realistic, but it should not depend on paid cloud services, commercial tools, or company-specific products by default.

The goal is to make the project accessible, repeatable, and portfolio-friendly. Anyone reviewing the project should be able to understand the architecture and, later, deploy the platform using commonly available open-source technologies.

The platform needs tools for:

* Infrastructure as Code
* Server configuration
* Kubernetes bootstrap
* Package management
* GitOps
* Ingress
* Certificate management
* Observability
* Logging
* Alerting
* Security
* Automation
* Disaster recovery
* Documentation

## Decision

The Kubernetes Platform project will use a free and open-source first technology stack.

The core stack will include:

```text
Linux Ubuntu
Git
GitHub
GitHub Actions
Terraform
Ansible
K3s
Helm
Argo CD
NGINX Ingress Controller
cert-manager
Prometheus
Grafana
Loki
Alertmanager
Harbor or local container registry
Bash
Python
```

Paid services and commercial tools will not be required for the default project implementation.

## Selected Technology Areas

### Operating System

Selected technology:

```text
Ubuntu Linux
```

Reason:

Ubuntu is widely used, well documented, beginner-friendly, and commonly supported by Kubernetes tooling.

### Version Control

Selected technologies:

```text
Git
GitHub
```

Reason:

Git and GitHub provide version control, collaboration, pull requests, issue tracking, documentation hosting, and GitHub Actions workflows.

### CI/CD and Validation

Selected technology:

```text
GitHub Actions
```

Reason:

GitHub Actions is available directly inside GitHub and can be used for validation workflows such as Markdown checks, Terraform formatting, YAML checks, shell script checks, Python checks, and security scanning.

During the design phase, GitHub Actions will be used for validation only, not deployment.

### Infrastructure as Code

Selected technology:

```text
Terraform
```

Reason:

Terraform is widely used for Infrastructure as Code and supports reusable modules, environment separation, variables, outputs, and reviewable infrastructure changes.

### Server Bootstrap

Selected technology:

```text
Ansible
```

Reason:

Ansible is simple, agentless, and commonly used for Linux server preparation, package installation, hardening, and Kubernetes prerequisites.

### Kubernetes Distribution

Selected technology:

```text
K3s
```

Reason:

K3s is lightweight, CNCF-certified, easier to run in small environments, and suitable for virtual machines, labs, edge environments, and private infrastructure.

It allows the project to demonstrate production-style Kubernetes operations without requiring a large cloud environment.

### Package Management

Selected technology:

```text
Helm
```

Reason:

Helm is the standard package manager for Kubernetes and is commonly used to deploy platform components and applications.

### GitOps

Selected technology:

```text
Argo CD
```

Reason:

Argo CD is widely used for GitOps-based Kubernetes delivery. It provides desired-state management, sync visibility, rollback support, and environment-based application promotion.

### Ingress

Selected technology:

```text
NGINX Ingress Controller
```

Reason:

NGINX Ingress Controller is widely adopted, well documented, and suitable for demonstrating ingress routing in a Kubernetes platform.

### Certificate Management

Selected technology:

```text
cert-manager
```

Reason:

cert-manager automates certificate issuance and renewal in Kubernetes. It is commonly used with ingress controllers and supports production-style TLS management.

### Metrics

Selected technology:

```text
Prometheus
```

Reason:

Prometheus is a widely used open-source monitoring system for Kubernetes metrics and alert rules.

### Dashboards

Selected technology:

```text
Grafana
```

Reason:

Grafana is commonly used with Prometheus and Loki to visualize metrics, logs, and platform health.

### Logging

Selected technology:

```text
Loki
```

Reason:

Loki integrates well with Grafana and provides a lightweight log aggregation option for Kubernetes environments.

### Alerting

Selected technology:

```text
Alertmanager
```

Reason:

Alertmanager works with Prometheus to route, group, silence, and manage alerts.

### Container Registry

Selected technologies:

```text
Harbor
Local registry
```

Reason:

Harbor provides a strong open-source registry option with security and scanning features. A local registry can also be used for smaller or air-gapped environments.

### Automation

Selected technologies:

```text
Bash
Python
```

Reason:

Bash is useful for simple operational tasks and shell-based automation. Python is useful for more structured automation, reporting, validation, and operational tooling.

## Consequences

### Positive Consequences

Using a free and open-source stack provides:

* Lower cost
* Easier access
* Better portfolio reproducibility
* No dependency on paid cloud accounts
* Strong learning value
* Broad industry relevance
* Easier local or private infrastructure deployment
* Better support for air-gapped planning
* Clear demonstration of platform engineering fundamentals

### Negative Consequences

Using only free and open-source tools also has trade-offs:

* Some managed-service convenience is not available
* More components must be configured manually
* More operational responsibility remains with the platform owner
* High availability and scaling require careful design
* Some enterprise features may require additional setup
* Integration between tools must be documented clearly

These trade-offs are acceptable because the project goal is to demonstrate how a platform is built and operated, not how to consume a fully managed platform.

## Alternatives Considered

### Alternative 1: Use Managed Cloud Services

Examples:

```text
Amazon EKS
Azure AKS
Google GKE
Cloud Load Balancers
Managed Prometheus
Managed Grafana
Managed Container Registry
```

Advantages:

* Faster deployment
* Less operational burden
* Built-in integrations
* Managed upgrades
* Better production support

Disadvantages:

* Requires cloud accounts
* May create costs
* Can hide important platform engineering details
* Makes the project cloud-specific
* Less suitable for bare metal or private infrastructure simulation

This option was rejected for the default implementation because the project should remain free, portable, and focused on building the platform from scratch.

### Alternative 2: Use Commercial Platform Tools

Examples:

```text
Rancher commercial support
Datadog
Splunk
New Relic
Aqua Security
Prisma Cloud
HashiCorp enterprise products
```

Advantages:

* Enterprise features
* Strong support options
* Mature integrations
* Rich dashboards and workflows

Disadvantages:

* May require licenses
* May not be reproducible by reviewers
* Can reduce focus on core platform design
* May not fit the free and open-source project goal

This option was rejected for the default implementation.

### Alternative 3: Open-Source First Stack

This is the selected option.

Advantages:

* Free to use
* Easy to document
* Good for portfolio demonstration
* Works with private infrastructure
* Supports learning and transparency
* Shows how components fit together
* Avoids vendor lock-in

Disadvantages:

* Requires more configuration
* Requires more operational documentation
* Requires careful integration work

This option was selected because it best supports the project vision.

## GitHub-First Impact

Because this project follows a GitHub-first approach, the open-source stack will be documented and coded before anything is installed.

During the current phase:

```text
Do not install K3s.
Do not install Argo CD.
Do not install Prometheus.
Do not install Grafana.
Do not install Loki.
Do not install cert-manager.
Do not install Harbor.
Do not run Terraform apply.
Do not run Ansible playbooks.
```

All files will be created first, reviewed, and executed later.

## Future Review

This decision may be reviewed if:

* A selected tool becomes unsuitable
* A better open-source tool becomes more appropriate
* The platform requirements change
* Air-gapped support requires a different approach
* Security requirements require additional tooling
* Execution later shows operational issues with a selected component

## Related Documents

* `README.md`
* `ARCHITECTURE.md`
* `ROADMAP.md`
* `REPOSITORIES.md`
* `PROJECT-STANDARDS.md`
* `docs/architecture/overview.md`
* `docs/standards/documentation-standards.md`

## Summary

The Kubernetes Platform project will use a free and open-source first technology stack.

This decision keeps the platform accessible, reproducible, cost-effective, and focused on real platform engineering fundamentals. It also supports the long-term goal of building a production-style Kubernetes platform that can run on virtual machines, bare metal, private infrastructure, or air-gapped environments.
