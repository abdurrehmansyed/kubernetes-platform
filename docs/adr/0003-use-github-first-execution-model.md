# ADR-0003: Use GitHub-First Execution Model

## Status

Accepted

## Date

2026-07-02

## Context

The Kubernetes Platform project is designed to build a production-style Kubernetes platform from scratch.

The platform includes many moving parts:

* Terraform infrastructure code
* Ansible bootstrap automation
* Kubernetes platform manifests
* Helm charts
* GitOps configuration
* Observability configuration
* Security policies
* Operations automation
* Disaster recovery documentation
* Runbooks
* Architecture documentation

A common mistake in infrastructure projects is to start executing too early. This can lead to incomplete documentation, unclear rollback plans, inconsistent naming, missing security controls, and operational confusion.

For this project, the goal is not to quickly deploy Kubernetes. The goal is to create a complete, professional, reviewable platform engineering project.

Because of that, execution should be delayed until the full platform exists in GitHub.

## Decision

The Kubernetes Platform project will use a GitHub-first execution model.

This means:

```text id="dyz7ks"
Create all repositories first.
Create all architecture documents first.
Create all code first.
Create all scripts first.
Create all manifests first.
Create all workflows first.
Create all runbooks first.
Review everything.
Execute later.
```

No infrastructure, Kubernetes cluster, platform component, GitOps sync, or automation script should be executed until the repository structure is complete and reviewed.

## What This Means

During the current phase, the project will create:

* Repository structures
* README files
* Architecture documents
* Standards documents
* Terraform modules
* Ansible playbooks
* Kubernetes manifests
* Helm charts
* GitHub Actions workflows
* Bash scripts
* Python scripts
* GitOps configuration
* Observability files
* Security policies
* Runbooks
* Disaster recovery plans
* Architecture Decision Records

But the project will not run:

```bash id="h4r7rl"
terraform apply
ansible-playbook
kubectl apply
helm install
argocd app sync
k3s installation commands
production automation scripts
```

These commands may appear in documentation as future execution steps, but they should not be executed during the design phase.

## Reasoning

This decision supports the project goal of building a complete production-style platform instead of a quick lab.

The GitHub-first model helps ensure:

* The architecture is clear before deployment
* Repositories have consistent structure
* Documentation exists before execution
* Security controls are planned early
* Rollback procedures are documented
* Runbooks exist before incidents happen
* Automation can be reviewed before use
* Changes are version-controlled
* The platform is easier to explain in interviews
* The project looks like a serious Platform Engineering effort

## Execution Order

The planned execution order is:

```text id="8y0pro"
1. Create the master repository
2. Create all platform repositories
3. Add documentation to every repository
4. Add Terraform code
5. Add Ansible code
6. Add Kubernetes platform manifests
7. Add Helm charts
8. Add GitOps configuration
9. Add sample applications
10. Add observability configuration
11. Add security policies
12. Add operations automation
13. Add runbooks
14. Add disaster recovery documentation
15. Review all repositories
16. Create an execution plan
17. Execute later
```

## What Is Allowed During the GitHub-First Phase

The following activities are allowed:

* Creating repositories
* Creating folders
* Writing documentation
* Writing Terraform code
* Writing Ansible code
* Writing Kubernetes YAML
* Writing Helm charts
* Writing GitHub Actions validation workflows
* Writing Bash and Python scripts
* Writing runbooks
* Writing ADRs
* Reviewing files
* Improving naming
* Improving structure
* Checking for secrets
* Checking documentation quality

## What Is Not Allowed During the GitHub-First Phase

The following activities are not allowed yet:

* Provisioning infrastructure
* Installing Kubernetes
* Applying Kubernetes manifests
* Installing Helm charts into a real cluster
* Syncing Argo CD to a real cluster
* Running Ansible against real servers
* Running destructive scripts
* Running production maintenance automation
* Rotating real certificates
* Performing real backup or restore actions

## Consequences

### Positive Consequences

Using a GitHub-first model provides:

* Better planning
* Better documentation
* Better review process
* Safer future execution
* Clearer architecture
* Stronger portfolio presentation
* More realistic platform engineering workflow
* Reduced risk of undocumented changes
* Better separation between design and execution

### Negative Consequences

This model also has trade-offs:

* It takes longer before anything is deployed
* Some files may need changes once execution begins
* Some assumptions may need validation later
* The project may feel slower at the beginning
* More discipline is required to avoid executing too early

These trade-offs are acceptable because the goal is to build a professional, production-style platform, not a quick demo.

## Alternatives Considered

### Alternative 1: Deploy First, Document Later

One option would be to quickly deploy Kubernetes and document the project afterward.

Advantages:

* Faster visible progress
* Early technical feedback
* Quicker demo environment

Disadvantages:

* Documentation may be incomplete
* Design decisions may not be captured
* Security may be added too late
* Rollback planning may be skipped
* Repository structure may become messy
* Harder to show mature platform engineering process

This option was rejected.

### Alternative 2: Build One Repository Fully Before Planning Others

Another option would be to build one repository completely, then move to the next.

Advantages:

* Simple focus
* Easier short-term progress
* Less context switching

Disadvantages:

* Cross-repository dependencies may be missed
* Standards may become inconsistent
* Architecture may evolve unevenly
* Some repositories may not align well later

This option was rejected because the project requires a connected platform design.

### Alternative 3: GitHub-First Execution Model

The selected option is to create all repositories, documentation, code, scripts, manifests, workflows, and runbooks before execution.

Advantages:

* Strong planning
* Clear ownership
* Better documentation
* Safer execution later
* Better interview presentation
* Realistic platform engineering workflow

Disadvantages:

* Slower initial deployment
* Requires more upfront writing
* Requires careful organization

This option was selected.

## Review Criteria

This decision should be reviewed if:

* The design phase becomes too large without producing useful structure
* Execution reveals major architecture changes are needed
* Some repositories become unnecessary
* The platform scope changes significantly
* The GitHub-first approach blocks meaningful progress instead of supporting it

## Related Documents

* `README.md`
* `ARCHITECTURE.md`
* `ROADMAP.md`
* `REPOSITORIES.md`
* `PROJECT-STANDARDS.md`
* `docs/roadmap/phases.md`
* `docs/standards/documentation-standards.md`

## Summary

The Kubernetes Platform project will use a GitHub-first execution model.

This ensures the full platform is planned, documented, structured, and reviewed before any infrastructure or Kubernetes deployment begins. This decision supports the goal of building a realistic, professional, production-style platform engineering project.
