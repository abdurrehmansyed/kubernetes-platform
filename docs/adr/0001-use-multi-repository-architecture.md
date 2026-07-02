# ADR-0001: Use Multi-Repository Architecture

## Status

Accepted

## Date

2026-07-02

## Context

The Kubernetes Platform project is designed to simulate how a Platform Engineering team would build, document, secure, automate, operate, and maintain a production-style Kubernetes platform.

The platform includes many different areas:

* Infrastructure as Code
* Server bootstrap automation
* Kubernetes platform configuration
* GitOps
* Application deployment
* Observability
* Security
* Operations automation
* Runbooks
* Disaster recovery
* Architecture documentation

One option would be to keep everything in a single repository. This would make the project easier to start, but over time the repository could become large, confusing, and harder to navigate.

A production-style platform usually has different ownership areas. Infrastructure code, Kubernetes configuration, GitOps, security, observability, automation, and runbooks often change at different speeds and may be owned by different teams or roles.

Because this project is intended to demonstrate realistic platform engineering practices, the repository structure should reflect clear ownership and separation of concerns.

## Decision

The Kubernetes Platform project will use a multi-repository architecture.

The master repository will be:

```text id="4g26sy"
kubernetes-platform
```

Implementation and supporting repositories will use the `kp-` prefix:

```text id="5my12t"
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

Each repository will have a clear responsibility.

The master repository will provide the overall context, architecture, roadmap, standards, and navigation.

## Repository Responsibilities

### kubernetes-platform

Owns:

* Project overview
* High-level architecture
* Roadmap
* Repository map
* Project standards
* Documentation standards
* Initial ADRs
* Navigation

### kp-terraform-infra

Owns:

* Terraform modules
* Environment infrastructure
* Network definitions
* Compute definitions
* Storage prerequisites
* Remote state design
* Infrastructure outputs

### kp-ansible-bootstrap

Owns:

* Server preparation
* Ansible roles
* Ansible playbooks
* Inventories
* OS hardening
* Kubernetes prerequisites

### kp-k8s-platform

Owns:

* K3s bootstrap structure
* Kubernetes platform components
* Ingress
* Storage
* Certificates
* Namespaces
* Platform upgrades
* Day-2 operations

### kp-gitops

Owns:

* Argo CD configuration
* App-of-apps structure
* Argo CD applications
* Argo CD projects
* Sync policies
* Promotion model

### kp-applications

Owns:

* Sample applications
* Dockerfiles
* Helm charts
* Kubernetes manifests
* Environment values
* Application rollback examples

### kp-observability

Owns:

* Prometheus
* Grafana
* Loki
* Alertmanager
* Alerts
* Dashboards
* SLOs
* Observability runbooks

### kp-security

Owns:

* RBAC
* Pod Security
* Network Policies
* Secrets strategy
* Image scanning
* Compliance controls
* Security runbooks

### kp-ops-automation

Owns:

* Bash automation
* Python automation
* Health checks
* Maintenance scripts
* Upgrade helpers
* Backup helpers
* Certificate checks
* Reporting scripts

### kp-runbooks

Owns:

* Incident response procedures
* Troubleshooting guides
* Upgrade runbooks
* Rollback runbooks
* Maintenance procedures
* Alert response guides

### kp-disaster-recovery

Owns:

* Backup strategy
* Restore procedures
* RPO definitions
* RTO definitions
* Failure scenarios
* DR test plans
* Recovery checklists

### kp-design-docs

Owns:

* ADRs
* Design rationale
* Trade-off analysis
* Scaling design
* Networking design
* Storage design
* Air-gapped design
* Failure scenario analysis

## Consequences

### Positive Consequences

Using multiple repositories provides:

* Clear ownership boundaries
* Easier navigation
* More realistic platform structure
* Better separation of concerns
* Cleaner documentation
* Easier future expansion
* Better alignment with production-style platform teams
* Independent review of different platform areas
* Cleaner GitHub portfolio presentation

This structure helps show that the platform is not just a Kubernetes lab, but a full platform engineering system.

### Negative Consequences

Using multiple repositories also introduces some complexity:

* More repositories must be created and maintained
* Cross-repository links must stay accurate
* Standards must be applied consistently
* Changes that span multiple areas may require updates in multiple repositories
* Navigation must be clearly documented

These trade-offs are acceptable because the project goal is to demonstrate realistic platform engineering practices.

## Alternatives Considered

### Alternative 1: Single Monolithic Repository

All code and documentation could be placed in one repository.

Example:

```text id="g14fn9"
kubernetes-platform/
  terraform/
  ansible/
  k8s/
  gitops/
  observability/
  security/
  scripts/
  runbooks/
```

Advantages:

* Easier to start
* Fewer repositories to manage
* Simpler local cloning
* Easier global search

Disadvantages:

* Can become large and difficult to navigate
* Ownership boundaries are less clear
* Less realistic for a mature platform organization
* Harder to show separation of responsibilities
* One repository would contain too many unrelated concerns

This option was rejected because the project is intended to demonstrate production-style platform engineering, not just a compact lab.

### Alternative 2: Small Number of Repositories

The project could use only a few repositories.

Example:

```text id="gic6nb"
kubernetes-platform
kp-infrastructure
kp-operations
kp-applications
```

Advantages:

* Less complex than many repositories
* Better separation than a monorepo
* Easier to maintain than many small repos

Disadvantages:

* Still groups too many responsibilities together
* Security, observability, runbooks, and disaster recovery may become secondary
* Less clear ownership
* Less detailed portfolio structure

This option was rejected because the project benefits from explicit ownership for each platform domain.

### Alternative 3: Multi-Repository Architecture

The selected option is a full multi-repository architecture.

Advantages:

* Strong separation of concerns
* Clear repository purpose
* Realistic platform engineering model
* Better documentation structure
* Better interview presentation
* Easier to expand each area independently

Disadvantages:

* Requires more setup
* Requires consistent standards
* Requires good navigation

This option was selected.

## GitHub-First Impact

Because the project follows a GitHub-first approach, the multi-repository structure will be created before execution begins.

This means:

```text id="h06lf7"
Create all repositories.
Create all documentation.
Create all code structures.
Create all scripts.
Create all manifests.
Create all workflows.
Create all runbooks.
Review everything.
Execute later.
```

No repository should depend on live deployment during the current phase.

## Review Criteria

This decision should be reviewed if:

* The repository structure becomes too difficult to maintain
* Cross-repository navigation becomes confusing
* Several repositories remain empty or unnecessary
* A better ownership model becomes clear
* Execution later shows that some repositories should be combined or split

## Related Documents

* `README.md`
* `ARCHITECTURE.md`
* `ROADMAP.md`
* `REPOSITORIES.md`
* `PROJECT-STANDARDS.md`
* `docs/repositories/repository-map.md`

## Summary

The Kubernetes Platform project will use a multi-repository architecture because it provides clear ownership, realistic platform organization, and strong portfolio presentation.

This decision supports the project goal of building a complete production-style Kubernetes Platform rather than a simple tutorial or lab.
