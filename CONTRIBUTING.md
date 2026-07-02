# Contributing Guide

## Purpose

This document explains how changes should be made across the Kubernetes Platform project.

Even though this is currently a portfolio project, it is written as if it belongs to a real internal Platform Engineering team. The goal is to keep changes organized, reviewable, documented, and safe.

## Project Approach

This project follows a GitHub-first approach.

That means all architecture, documentation, Terraform code, Ansible playbooks, Kubernetes manifests, Helm charts, GitHub Actions, automation scripts, and runbooks should be created and reviewed before anything is executed.

During the current phase:

```text
Do not deploy.
Do not execute Terraform.
Do not run Ansible.
Do not install Kubernetes.
Do not apply Kubernetes manifests.
Do not sync Argo CD.
Do not run operational scripts against real systems.
```

The current focus is repository creation, documentation, code structure, and review readiness.

## Contribution Goals

Every contribution should improve at least one of the following:

* Clarity
* Reliability
* Security
* Automation
* Observability
* Maintainability
* Documentation quality
* Operational readiness
* Disaster recovery readiness
* Platform consistency

## Repository Standards

Before contributing to any repository, follow the standards defined in:

```text
PROJECT-STANDARDS.md
```

All repositories should use consistent naming, folder structure, documentation style, and review expectations.

## Branching Standard

Use descriptive branch names.

Recommended branch prefixes:

```text
feature/  - New repository content or platform feature
docs/     - Documentation changes
fix/      - Corrections or bug fixes
chore/    - Maintenance updates
refactor/ - Structure changes without behavior changes
```

Examples:

```text
docs/add-architecture-overview
feature/create-terraform-network-module
feature/add-ansible-bootstrap-roles
docs/add-kubernetes-upgrade-runbook
fix/correct-repository-map
chore/add-github-templates
```

Avoid unclear branch names:

```text
update
changes
fix
new
final
test
```

## Commit Message Standard

Use short, clear commit messages.

Good examples:

```text
Add platform architecture document
Add project roadmap
Create repository map
Document GitOps promotion model
Add Terraform network module structure
Create Ansible bootstrap role layout
Add Kubernetes namespace standards
```

Avoid unclear commit messages:

```text
done
update
changes
fix
stuff
final
new commit
```

## Pull Request Standard

Every pull request should clearly explain the change.

A good pull request should include:

* What changed
* Why it changed
* What files were added or updated
* Whether execution is required
* Any risks
* Any follow-up tasks
* Validation or review notes

During the design phase, most pull requests should say:

```text
Execution required: No
Deployment performed: No
```

## Pull Request Checklist

Before opening or merging a pull request, check the following:

```text
[ ] The change has a clear purpose.
[ ] The files are in the correct repository.
[ ] The folder names follow the project standards.
[ ] The documentation is clear.
[ ] No secrets are included.
[ ] No real credentials are included.
[ ] No deployment was performed.
[ ] No destructive commands were added without explanation.
[ ] Rollback or recovery notes are included where needed.
[ ] The change fits the GitHub-first project strategy.
```

## Documentation Contributions

Documentation should be clear enough for someone seeing the project for the first time.

Good documentation should explain:

* What this component does
* Why it exists
* Where it fits in the platform
* How it will be used later
* What assumptions are being made
* What risks exist
* How to troubleshoot problems
* How to roll back changes when applicable

Avoid documentation that only lists commands without context.

## Code Contributions

Code should be written for readability and safe review.

This applies to:

* Terraform
* Ansible
* Kubernetes YAML
* Helm charts
* GitHub Actions
* Bash scripts
* Python scripts

Code should avoid hardcoded secrets, unclear names, and destructive behavior.

## Terraform Contribution Rules

Terraform changes should follow these rules:

* Use reusable modules where appropriate
* Keep environment-specific values outside modules
* Use clear variable names
* Add descriptions to variables
* Add outputs where useful
* Keep `dev`, `staging`, and `prod` separated
* Do not run `terraform apply` during the design phase

Preferred module files:

```text
main.tf
variables.tf
outputs.tf
README.md
```

## Ansible Contribution Rules

Ansible changes should follow these rules:

* Use roles for reusable logic
* Use inventories for environment separation
* Use readable task names
* Use variables instead of hardcoded values
* Document required privileges
* Keep playbooks focused
* Do not run playbooks during the design phase

## Kubernetes Contribution Rules

Kubernetes manifest changes should follow these rules:

* Use clear resource names
* Avoid using the `default` namespace for platform workloads
* Add consistent labels
* Add resource requests and limits where appropriate
* Keep environment-specific configuration separate
* Document what each manifest does
* Do not apply manifests during the design phase

Recommended labels:

```yaml
app.kubernetes.io/part-of: kubernetes-platform
app.kubernetes.io/managed-by: gitops
```

## Helm Contribution Rules

Helm chart changes should follow these rules:

* Use standard Helm chart structure
* Keep templates readable
* Use values files for environment differences
* Avoid hardcoded secrets
* Document chart values
* Include example values where useful
* Make releases rollback-friendly

## GitHub Actions Contribution Rules

GitHub Actions should be used for validation and review support.

Allowed during the design phase:

* Markdown validation
* YAML validation
* Terraform formatting checks
* Terraform validation
* Ansible syntax checks
* Shell script checks
* Python linting
* Security scanning

Avoid during the current phase:

* Automatic infrastructure deployment
* Automatic Kubernetes deployment
* Automatic Argo CD sync to a real cluster
* Automatic production changes

## Script Contribution Rules

Scripts should be safe, clear, and documented.

Bash scripts should usually start with:

```bash
#!/usr/bin/env bash
set -euo pipefail
```

Scripts should include:

* Purpose
* Usage
* Required inputs
* Safety notes
* Dry-run option where useful
* Clear error messages

Python scripts should include:

* Clear function names
* Argument parsing
* Input validation
* Error handling
* Logging where useful
* Usage documentation

## Secrets Policy

Never commit secrets.

Do not commit:

```text
Passwords
Private keys
API tokens
Cloud credentials
Kubeconfig files with real credentials
SSH private keys
Database credentials
Personal access tokens
```

Use placeholders instead:

```text
REPLACE_ME
example-token
example-password
your-domain.example.com
```

## Issue Standard

Issues should be used to track work clearly.

Each issue should include:

* Goal
* Scope
* Deliverables
* Acceptance criteria
* Related repository
* Related roadmap phase

Example issue titles:

```text
Create Terraform network module structure
Add Ansible role for Kubernetes prerequisites
Create Argo CD app-of-apps layout
Document Prometheus alerting strategy
Create backup and restore runbook
```

## Review Standard

Before a change is considered complete, review it for:

* Correct repository ownership
* Consistent naming
* Clear documentation
* No secrets
* Safe commands
* Rollback awareness
* Security impact
* Operational impact
* Future execution readiness

## Current Project Rule

The most important rule during the current phase is:

```text
Create first.
Document first.
Review first.
Execute later.
```

## Summary

Contributions to this project should make the Kubernetes Platform more complete, professional, secure, maintainable, and operationally realistic.

The project should always look like a serious Platform Engineering effort, not a quick lab or disconnected tutorial.
