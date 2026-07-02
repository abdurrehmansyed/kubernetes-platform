# Security Policy

## Purpose

This document defines the security expectations for the Kubernetes Platform project.

Security is treated as a core platform requirement, not as a final step. Every repository in this project should be designed with secure defaults, clear access boundaries, reviewable changes, and no hardcoded secrets.

This project currently follows a GitHub-first approach. All security-related documentation, policies, manifests, workflows, scripts, and runbooks will be created and reviewed before anything is deployed or executed.

## Security Philosophy

The Kubernetes Platform should be designed so that security is built into the system from the beginning.

The project follows these security principles:

* Use least privilege wherever possible.
* Do not commit secrets to GitHub.
* Keep infrastructure and platform changes reviewable.
* Use version control for security policies.
* Separate environments clearly.
* Document access requirements.
* Document risks and rollback procedures.
* Validate changes before execution.
* Treat security as part of daily operations.
* Make security controls understandable and maintainable.

## Current Project Status

Current status:

```text
Design and repository creation phase
```

No infrastructure has been provisioned yet.

No Kubernetes cluster has been installed yet.

No security policy has been applied to a real environment yet.

All security files created during this phase are intended for review and later execution.

## Supported Repositories

This security policy applies to all repositories in the Kubernetes Platform project:

```text
kubernetes-platform
kp-terraform-infra
kp-ansible-bootstrap
kp-k8s-platform
kp-gitops
kp-applications
kp-observability
kp-security
kp-ops-automation
kp-runbooks
kp-disaster-recovery
kp-design-docs
```

## Reporting Security Issues

If a security issue is found in this project, it should be documented and reviewed before changes are made.

Examples of security issues include:

* Exposed secrets
* Hardcoded passwords
* Insecure Kubernetes manifests
* Overly permissive RBAC
* Missing network restrictions
* Unsafe GitHub Actions workflows
* Scripts with destructive defaults
* Missing authentication or authorization assumptions
* Weak TLS or certificate handling
* Sensitive information in documentation

## Secret Handling Policy

Secrets must never be committed to GitHub.

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
TLS private keys
Production IP allowlists containing sensitive details
Internal-only credentials
```

Use placeholders instead:

```text
REPLACE_ME
example-token
example-password
your-domain.example.com
example-api-key
example-private-key
```

## Example Safe Placeholder

Use this style in documentation and examples:

```yaml
apiVersion: v1
kind: Secret
metadata:
  name: example-secret
  namespace: example
type: Opaque
stringData:
  username: REPLACE_ME
  password: REPLACE_ME
```

This is acceptable because it does not contain real credentials.

## Environment Separation

The standard environments are:

```text
dev
staging
prod
```

Security boundaries should be designed separately for each environment.

Production should be treated as the most restricted environment.

Development can be more flexible, but it should still avoid unsafe defaults.

## Access Control Standards

Access should follow least privilege.

This applies to:

* GitHub repository access
* Terraform permissions
* Ansible SSH access
* Kubernetes RBAC
* Argo CD access
* Registry access
* Observability dashboards
* Backup and restore permissions
* Automation scripts

Users and service accounts should receive only the permissions required to perform their tasks.

## Kubernetes Security Standards

Kubernetes security controls should include:

* Namespace isolation
* RBAC
* Pod Security standards
* Network Policies
* Resource requests and limits
* Secure ingress configuration
* TLS certificate management
* Secrets management strategy
* Image scanning
* Audit-friendly labels and annotations

Platform workloads should not run in the `default` namespace unless there is a documented reason.

## RBAC Standards

RBAC should be explicit and minimal.

Avoid broad permissions such as:

```yaml
verbs:
  - "*"
resources:
  - "*"
```

Avoid cluster-wide permissions unless they are required and documented.

Every Role, ClusterRole, RoleBinding, and ClusterRoleBinding should have a clear purpose.

## Pod Security Standards

Workloads should avoid privileged settings unless required and documented.

Avoid:

```yaml
securityContext:
  privileged: true
```

Preferred controls include:

* Run as non-root where possible
* Drop unnecessary Linux capabilities
* Avoid privilege escalation
* Use read-only root filesystem where practical
* Set resource requests and limits
* Use trusted images

## Network Policy Standards

Network Policies should be used to reduce unnecessary communication between workloads.

The long-term goal is to move toward explicit network access instead of allowing all traffic by default.

Network Policies should document:

* Source namespace
* Destination namespace
* Allowed ports
* Allowed protocols
* Reason for the access

## Container Image Security

Container images should come from trusted sources.

Security goals include:

* Use official or trusted base images
* Pin image versions where practical
* Avoid unnecessary packages
* Scan images for vulnerabilities
* Avoid running containers as root when possible
* Document image sources
* Support local registry or Harbor workflows later

## GitHub Actions Security

GitHub Actions should be used carefully.

During the design phase, workflows should focus on validation only.

Allowed workflow types:

* Markdown checks
* YAML validation
* Terraform format checks
* Terraform validation
* Ansible syntax checks
* Shell script linting
* Python linting
* Security scanning

Avoid during the current phase:

* Automatic production deployment
* Automatic Terraform apply
* Automatic Kubernetes apply
* Automatic Argo CD sync to a real cluster
* Workflows that require production secrets

## Terraform Security Standards

Terraform code should avoid hardcoded secrets and sensitive values.

Terraform should use:

* Variables for configurable values
* Sensitive flags where appropriate
* Clear separation between environments
* Least-privilege infrastructure design
* Reviewable modules
* Documented assumptions

Do not run this during the current phase:

```bash
terraform apply
```

## Ansible Security Standards

Ansible should avoid hardcoded credentials.

Ansible should use:

* Variables
* Inventory separation
* Clear privilege escalation documentation
* Secure SSH assumptions
* Idempotent tasks
* Hardening roles
* Validation playbooks

Do not run this during the current phase:

```bash
ansible-playbook
```

## Script Security Standards

Scripts should be safe by default.

Bash scripts should usually start with:

```bash
#!/usr/bin/env bash
set -euo pipefail
```

Scripts should include:

* Purpose
* Usage
* Input validation
* Safe defaults
* Clear error messages
* Dry-run mode where useful
* No hardcoded secrets
* No destructive action without documentation

Python scripts should include:

* Argument parsing
* Input validation
* Error handling
* Logging
* Clear function names
* Safe defaults

## Documentation Security

Documentation should not expose sensitive information.

Do not include:

* Real credentials
* Private IPs from sensitive environments unless they are fictional examples
* Real customer names
* Internal hostnames from real companies
* Real production screenshots with sensitive data
* Private diagrams from actual employers

Use fictional examples instead.

## Vulnerability Management

The platform should eventually include vulnerability scanning for:

* Container images
* Kubernetes manifests
* Terraform code
* GitHub Actions
* Python dependencies
* Bash scripts where applicable

Planned tools may include:

* Trivy
* Checkov
* kube-score
* kube-linter
* shellcheck
* pip-audit

These tools should be introduced in validation workflows before execution.

## Backup and Recovery Security

Backup and restore processes should protect sensitive data.

Security considerations include:

* Encrypt backups where possible
* Restrict backup access
* Document restore permissions
* Avoid exposing secrets in backup logs
* Test restore procedures safely
* Separate backup storage permissions from normal workload permissions

## Air-Gapped Security

The platform will eventually support air-gapped or offline environments.

Security considerations include:

* Trusted image sources
* Offline image scanning
* Local registry access control
* Offline package verification
* Restricted network paths
* Controlled transfer of artifacts
* Documented upgrade procedures

## Security Review Checklist

Before execution, review each repository for:

```text
[ ] No real secrets are committed.
[ ] No private keys are committed.
[ ] No real kubeconfig files are committed.
[ ] No real cloud credentials are committed.
[ ] Placeholder values are clearly marked.
[ ] RBAC follows least privilege.
[ ] Network Policies are documented.
[ ] Scripts have safe defaults.
[ ] GitHub Actions do not deploy automatically.
[ ] Terraform does not contain hardcoded sensitive values.
[ ] Ansible does not contain hardcoded credentials.
[ ] Kubernetes manifests avoid unsafe defaults.
[ ] Security assumptions are documented.
[ ] Rollback or recovery steps exist where needed.
```

## Current Security Rule

The most important rule during the current phase is:

```text
Design security first.
Document security first.
Review security first.
Apply security later.
```

## Summary

Security is part of the Kubernetes Platform from the beginning.

Every repository should be written with secure defaults, no hardcoded secrets, clear access boundaries, reviewable changes, and operational documentation. The platform should be safe to understand, safe to review, and later safe to execute.
