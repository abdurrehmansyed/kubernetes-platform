# Architecture Overview

## Purpose

This document provides a focused architecture overview for the Kubernetes Platform project.

The main `ARCHITECTURE.md` file explains the complete platform architecture at a high level. This document provides a simpler overview of how the major layers fit together and how the project should be understood before implementation begins.

## Project Context

The Kubernetes Platform project is designed as a production-style platform engineering project.

The platform is being built using a GitHub-first approach:

```text
Design first.
Create all repositories first.
Create all files first.
Document everything first.
Execute later.
```

No deployment is performed during the current phase.

## Platform Layers

The platform is organized into the following layers:

```text
1. Infrastructure Layer
2. Server Bootstrap Layer
3. Kubernetes Platform Layer
4. GitOps Layer
5. Application Layer
6. Observability Layer
7. Security Layer
8. Operations Automation Layer
9. Disaster Recovery Layer
10. Documentation and Runbook Layer
```

Each layer has its own responsibility and its own repository.

## Layer 1 - Infrastructure

Repository:

```text
kp-terraform-infra
```

Purpose:

The infrastructure layer defines the base resources needed before Kubernetes can be installed.

This includes:

* Networks
* Compute resources
* Storage prerequisites
* Firewall or access rules
* Environment-specific infrastructure
* Terraform modules
* Outputs for later automation

This layer answers the question:

```text
Where will Kubernetes run?
```

## Layer 2 - Server Bootstrap

Repository:

```text
kp-ansible-bootstrap
```

Purpose:

The server bootstrap layer prepares Linux servers before Kubernetes installation.

This includes:

* Operating system preparation
* Package installation
* User setup
* SSH hardening
* Kernel parameters
* Firewall preparation
* Kubernetes prerequisites
* Container runtime preparation if needed

This layer answers the question:

```text
Are the servers ready for Kubernetes?
```

## Layer 3 - Kubernetes Platform

Repository:

```text
kp-k8s-platform
```

Purpose:

The Kubernetes platform layer defines the base Kubernetes cluster and core platform components.

This includes:

* K3s bootstrap structure
* Cluster configuration
* Namespaces
* Ingress controller
* Storage configuration
* cert-manager
* Platform policies
* Upgrade and rollback procedures
* Day-2 operational procedures

This layer answers the question:

```text
How is the Kubernetes platform built and operated?
```

## Layer 4 - GitOps

Repository:

```text
kp-gitops
```

Purpose:

The GitOps layer defines how changes are delivered to Kubernetes using Git as the source of truth.

This includes:

* Argo CD configuration
* App-of-apps structure
* Argo CD projects
* Application definitions
* Environment-specific sync policies
* Promotion flow between dev, staging, and prod

This layer answers the question:

```text
How do changes reach the cluster safely and consistently?
```

## Layer 5 - Applications

Repository:

```text
kp-applications
```

Purpose:

The application layer demonstrates how workloads are packaged and deployed onto the platform.

This includes:

* Sample applications
* Dockerfiles
* Helm charts
* Kubernetes manifests
* Environment values
* CI/CD examples
* Rollback examples

This layer answers the question:

```text
How do applications run on this platform?
```

## Layer 6 - Observability

Repository:

```text
kp-observability
```

Purpose:

The observability layer helps engineers understand platform and application health.

This includes:

* Prometheus
* Grafana
* Loki
* Alertmanager
* Metrics
* Logs
* Dashboards
* Alerts
* SLOs
* Observability runbooks

This layer answers the question:

```text
How do we know what is happening in the platform?
```

## Layer 7 - Security

Repository:

```text
kp-security
```

Purpose:

The security layer defines controls that protect the platform and workloads.

This includes:

* RBAC
* Pod Security standards
* Network Policies
* Secrets strategy
* Image scanning
* Compliance checklists
* Security runbooks

This layer answers the question:

```text
How is the platform protected?
```

## Layer 8 - Operations Automation

Repository:

```text
kp-ops-automation
```

Purpose:

The operations automation layer reduces manual work and makes common tasks safer.

This includes:

* Health check scripts
* Upgrade pre-checks
* Upgrade post-checks
* Backup helpers
* Restore helpers
* Certificate checks
* Maintenance scripts
* Reporting scripts

This layer answers the question:

```text
How do we automate routine and high-risk operational tasks?
```

## Layer 9 - Disaster Recovery

Repository:

```text
kp-disaster-recovery
```

Purpose:

The disaster recovery layer defines how the platform should recover from failures.

This includes:

* Backup strategy
* Restore procedures
* Recovery Point Objectives
* Recovery Time Objectives
* Failure scenarios
* DR test plans
* Recovery checklists

This layer answers the question:

```text
How do we recover when something fails badly?
```

## Layer 10 - Documentation and Runbooks

Repositories:

```text
kp-runbooks
kp-design-docs
kubernetes-platform
```

Purpose:

The documentation and runbook layer explains how the platform works, why decisions were made, and how operators should respond to problems.

This includes:

* Architecture documents
* ADRs
* Trade-off analysis
* Troubleshooting guides
* Incident response runbooks
* Upgrade runbooks
* Rollback runbooks
* Maintenance procedures

This layer answers the question:

```text
How can someone understand, operate, and improve the platform?
```

## End-to-End Flow

The full platform flow is:

```text
Terraform creates infrastructure
        ↓
Ansible prepares servers
        ↓
K3s creates the Kubernetes cluster
        ↓
Platform components are installed
        ↓
Argo CD manages desired state
        ↓
Applications are deployed
        ↓
Observability monitors health
        ↓
Security controls enforce boundaries
        ↓
Automation supports operations
        ↓
Runbooks guide incident response
        ↓
Disaster recovery validates resilience
```

## Environment Model

The platform is designed around three environments:

```text
dev
staging
prod
```

### dev

Used for early testing and platform changes.

### staging

Used for production-like validation.

### prod

Used as the stable production-style environment.

## Design Direction

The initial platform may be implemented using virtual machines, but the architecture should support future expansion toward bare metal or private infrastructure.

The larger design direction includes:

* Multiple Kubernetes clusters
* Separate control plane and worker nodes
* Management network
* Application network
* Storage network
* Local registry
* Offline or air-gapped support
* Backup and restore infrastructure
* Disaster recovery testing

## Current Phase

The current phase is documentation and repository creation.

During this phase:

```text
Do not run Terraform.
Do not run Ansible.
Do not install Kubernetes.
Do not apply Kubernetes manifests.
Do not install Argo CD.
Do not deploy applications.
```

The goal is to create a complete and professional GitHub structure before execution.

## Summary

This architecture overview explains how the Kubernetes Platform is organized into layers.

Each layer has a clear responsibility, and each repository exists to support one part of the platform. Together, these layers form a complete production-style Kubernetes platform that is repeatable, observable, secure, automated, documented, and ready for future execution.
