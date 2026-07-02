# Repository Map

## Purpose

This document provides a focused map of all repositories in the Kubernetes Platform project.

The main `REPOSITORIES.md` file explains repository ownership in detail. This document is a simpler navigation guide that helps someone quickly understand where each part of the platform lives.

## GitHub Organization

The master repository is:

```text
abdurrehmansyed/kubernetes-platform
```

All related platform repositories should follow the same owner namespace:

```text
abdurrehmansyed/<repository-name>
```

## Repository Naming Pattern

All implementation repositories use the `kp-` prefix.

```text
kp = Kubernetes Platform
```

Example:

```text
kp-terraform-infra
kp-ansible-bootstrap
kp-k8s-platform
```

The master repository is named:

```text
kubernetes-platform
```

## Repository Overview

| Repository             | Category       | Purpose                                            |
| ---------------------- | -------------- | -------------------------------------------------- |
| `kubernetes-platform`  | Master         | Main project entry point                           |
| `kp-terraform-infra`   | Infrastructure | Terraform infrastructure code                      |
| `kp-ansible-bootstrap` | Bootstrap      | Server preparation using Ansible                   |
| `kp-k8s-platform`      | Kubernetes     | Core Kubernetes platform configuration             |
| `kp-gitops`            | GitOps         | Argo CD and desired-state delivery                 |
| `kp-applications`      | Applications   | Sample applications and deployment examples        |
| `kp-observability`     | Observability  | Metrics, logs, dashboards, alerts, and SLOs        |
| `kp-security`          | Security       | RBAC, Pod Security, Network Policies, and scanning |
| `kp-ops-automation`    | Operations     | Python and Bash operational automation             |
| `kp-runbooks`          | Operations     | Human-readable operational runbooks                |
| `kp-disaster-recovery` | Recovery       | Backup, restore, RPO, RTO, and DR testing          |
| `kp-design-docs`       | Design         | ADRs, trade-offs, and architecture decisions       |

## Master Repository

### Repository

```text
kubernetes-platform
```

### Purpose

This repository is the main entry point for the entire platform.

It contains:

* Project vision
* High-level architecture
* Roadmap
* Repository list
* Project standards
* Documentation standards
* Initial ADRs
* Navigation to all platform repositories

### This Repository Answers

```text
What is this project, and how does everything fit together?
```

## Infrastructure Repository

### Repository

```text
kp-terraform-infra
```

### Purpose

This repository contains Terraform code for infrastructure provisioning.

It contains:

* Network modules
* Compute modules
* Storage modules
* Firewall or access rule modules
* Environment folders
* Variables
* Outputs
* Remote state design

### This Repository Answers

```text
Where will the Kubernetes platform run?
```

## Bootstrap Repository

### Repository

```text
kp-ansible-bootstrap
```

### Purpose

This repository contains Ansible automation for preparing servers before Kubernetes installation.

It contains:

* Inventories
* Roles
* Playbooks
* OS preparation
* User setup
* SSH hardening
* Kubernetes prerequisites
* Validation tasks

### This Repository Answers

```text
Are the servers ready for Kubernetes?
```

## Kubernetes Platform Repository

### Repository

```text
kp-k8s-platform
```

### Purpose

This repository contains the core Kubernetes platform configuration.

It contains:

* K3s bootstrap structure
* Cluster configuration
* Namespace standards
* Ingress configuration
* Storage configuration
* Certificate management
* Upgrade procedures
* Rollback procedures
* Day-2 operations

### This Repository Answers

```text
How is the Kubernetes platform built and operated?
```

## GitOps Repository

### Repository

```text
kp-gitops
```

### Purpose

This repository contains the GitOps structure for Argo CD.

It contains:

* Argo CD configuration
* App-of-apps pattern
* Argo CD projects
* Argo CD applications
* Environment sync policies
* Promotion workflow

### This Repository Answers

```text
How do platform and application changes reach Kubernetes?
```

## Applications Repository

### Repository

```text
kp-applications
```

### Purpose

This repository contains sample applications and deployment examples.

It contains:

* Sample apps
* Dockerfiles
* Helm charts
* Kubernetes manifests
* Environment values
* CI/CD examples
* Rollback examples

### This Repository Answers

```text
How should applications be packaged and deployed on the platform?
```

## Observability Repository

### Repository

```text
kp-observability
```

### Purpose

This repository contains observability configuration.

It contains:

* Prometheus configuration
* Grafana dashboards
* Loki configuration
* Alertmanager configuration
* Alert rules
* Recording rules
* SLOs
* Observability runbooks

### This Repository Answers

```text
How do we understand platform and application health?
```

## Security Repository

### Repository

```text
kp-security
```

### Purpose

This repository contains platform security controls.

It contains:

* RBAC
* Pod Security standards
* Network Policies
* Secrets strategy
* Image scanning workflows
* Compliance checklists
* Security runbooks

### This Repository Answers

```text
How is the platform protected?
```

## Operations Automation Repository

### Repository

```text
kp-ops-automation
```

### Purpose

This repository contains automation scripts for operational tasks.

It contains:

* Health check scripts
* Maintenance scripts
* Upgrade pre-checks
* Upgrade post-checks
* Backup helpers
* Restore helpers
* Certificate checks
* Reporting scripts

### This Repository Answers

```text
How do we make routine operations safer and repeatable?
```

## Runbooks Repository

### Repository

```text
kp-runbooks
```

### Purpose

This repository contains human-readable operational procedures.

It contains:

* Incident response runbooks
* Troubleshooting guides
* Upgrade procedures
* Rollback procedures
* Alert response guides
* Maintenance checklists
* Escalation examples

### This Repository Answers

```text
What should an engineer do during an issue?
```

## Disaster Recovery Repository

### Repository

```text
kp-disaster-recovery
```

### Purpose

This repository contains disaster recovery planning.

It contains:

* Backup strategy
* Restore procedures
* RPO definitions
* RTO definitions
* Failure scenarios
* DR test plans
* Recovery checklists

### This Repository Answers

```text
How do we recover from serious failures?
```

## Design Documentation Repository

### Repository

```text
kp-design-docs
```

### Purpose

This repository contains deeper design documentation and decision records.

It contains:

* Architecture Decision Records
* Networking design
* Storage design
* Scaling design
* Reliability design
* Air-gapped design
* Failure scenario analysis
* Trade-off analysis

### This Repository Answers

```text
Why was the platform designed this way?
```

## Repository Dependency Flow

The main build order is:

```text
kubernetes-platform
        ↓
kp-terraform-infra
        ↓
kp-ansible-bootstrap
        ↓
kp-k8s-platform
        ↓
kp-gitops
        ↓
kp-applications
```

Supporting repositories connect across the platform:

```text
kp-observability
kp-security
kp-ops-automation
kp-runbooks
kp-disaster-recovery
kp-design-docs
```

## Simple Navigation Guide

Use this guide when deciding where a file belongs.

| If you are creating...        | Put it in...           |
| ----------------------------- | ---------------------- |
| Project overview              | `kubernetes-platform`  |
| Architecture roadmap          | `kubernetes-platform`  |
| Terraform module              | `kp-terraform-infra`   |
| Terraform environment config  | `kp-terraform-infra`   |
| Ansible role                  | `kp-ansible-bootstrap` |
| Ansible inventory             | `kp-ansible-bootstrap` |
| K3s bootstrap config          | `kp-k8s-platform`      |
| Kubernetes namespace manifest | `kp-k8s-platform`      |
| Ingress controller config     | `kp-k8s-platform`      |
| Argo CD application           | `kp-gitops`            |
| App-of-apps config            | `kp-gitops`            |
| Sample app source code        | `kp-applications`      |
| Helm chart for sample app     | `kp-applications`      |
| Prometheus rule               | `kp-observability`     |
| Grafana dashboard             | `kp-observability`     |
| Loki config                   | `kp-observability`     |
| RBAC manifest                 | `kp-security`          |
| Network Policy                | `kp-security`          |
| Image scanning workflow       | `kp-security`          |
| Bash health check script      | `kp-ops-automation`    |
| Python reporting script       | `kp-ops-automation`    |
| Incident runbook              | `kp-runbooks`          |
| Troubleshooting procedure     | `kp-runbooks`          |
| Backup strategy               | `kp-disaster-recovery` |
| Restore procedure             | `kp-disaster-recovery` |
| ADR                           | `kp-design-docs`       |
| Trade-off analysis            | `kp-design-docs`       |

## GitHub-First Rule

All repositories should be created and populated before execution.

During the current phase:

```text
Do not deploy.
Do not run Terraform.
Do not run Ansible.
Do not install Kubernetes.
Do not apply manifests.
Do not sync Argo CD.
```

The purpose of this repository map is to keep the platform organized before implementation and execution begin.

## Summary

The Kubernetes Platform project is split into multiple repositories so each part of the platform has clear ownership.

This structure makes the project easier to understand, review, maintain, and expand.
