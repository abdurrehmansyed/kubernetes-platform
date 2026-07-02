# ADR-0004: Use K3s for Initial Kubernetes Platform

## Status

Accepted

## Date

2026-07-02

## Context

The Kubernetes Platform project is designed to demonstrate how a production-style Kubernetes platform can be built, automated, secured, observed, operated, and documented from scratch.

The project needs a Kubernetes distribution that supports the following goals:

* Can run on virtual machines
* Can later support bare metal or private infrastructure
* Is lightweight enough for a lab or portfolio environment
* Supports production-style operational concepts
* Works well with GitOps, ingress, observability, security, and automation
* Does not require paid cloud services
* Is simple enough to bootstrap while still showing real Kubernetes operations

Several Kubernetes options are available, including upstream Kubernetes with kubeadm, K3s, RKE2, MicroK8s, Minikube, Kind, and managed cloud Kubernetes services.

The project needs a balance between realism and practicality.

## Decision

The Kubernetes Platform project will use K3s as the initial Kubernetes distribution.

K3s will be used for the first implementation because it is lightweight, open-source, CNCF-certified, and suitable for virtual machines, private infrastructure, edge environments, and smaller production-style clusters.

The project will design K3s as a real long-running Kubernetes platform, not as a throwaway demo cluster.

## Why K3s

K3s was selected because it provides:

* Lightweight Kubernetes installation
* Lower resource requirements
* Simpler bootstrap process
* Good fit for virtual machines and private infrastructure
* Support for multi-node clusters
* Compatibility with standard Kubernetes tools
* Good fit for GitOps workflows
* Good fit for portfolio execution later
* Easier path to simulate production operations without cloud costs

## Expected Platform Usage

K3s will support the following platform areas:

* Cluster bootstrap
* Control plane and worker node separation
* Ingress
* Storage integration
* cert-manager
* Argo CD
* Prometheus
* Grafana
* Loki
* Alertmanager
* RBAC
* Network Policies
* GitOps-based application delivery
* Backup and restore planning
* Upgrade and rollback runbooks
* Day-2 operations automation

## Initial Environment Model

The platform is designed to support three environments:

```text id="lyh22k"
dev
staging
prod
```

The initial implementation may start with virtual machines.

The design should still support future expansion toward:

```text id="xyot8l"
bare metal servers
private infrastructure
air-gapped environments
larger multi-cluster designs
```

## Target Cluster Model

The long-term design can support multiple clusters:

```text id="1dhtlp"
development cluster
staging cluster
production cluster
```

Each cluster may eventually include:

```text id="9smih8"
control plane nodes
worker nodes
ingress components
storage components
monitoring components
security policies
GitOps-managed workloads
```

## Consequences

### Positive Consequences

Using K3s provides:

* Faster future bootstrap
* Lower resource requirements
* Easier testing on virtual machines
* Lower cost
* Better fit for private infrastructure
* Simpler learning and review experience
* Compatibility with standard Kubernetes manifests
* Strong fit for GitHub portfolio execution
* Room to demonstrate production-style operations

K3s allows the project to focus on platform engineering concepts instead of spending too much time on complex cluster installation mechanics.

### Negative Consequences

Using K3s also has trade-offs:

* It is not the same as a large managed Kubernetes service
* Some enterprise environments may prefer kubeadm, RKE2, OpenShift, EKS, AKS, or GKE
* Some default components may need to be disabled or customized
* High availability design still requires careful planning
* Storage, networking, backup, and upgrades must be documented clearly
* Some assumptions may need adjustment during execution

These trade-offs are acceptable because the project goal is to demonstrate a production-style platform using free and open-source tools.

## Alternatives Considered

### Alternative 1: kubeadm

kubeadm is a common way to bootstrap upstream Kubernetes.

Advantages:

* Very close to upstream Kubernetes
* Strong learning value
* Common in self-managed Kubernetes environments
* Flexible and customizable

Disadvantages:

* More complex bootstrap process
* More moving parts to configure
* Higher operational overhead for initial implementation
* May slow down the GitHub-first platform build

This option was not selected for the initial implementation, but it remains a possible future alternative.

### Alternative 2: RKE2

RKE2 is a hardened Kubernetes distribution from Rancher/SUSE.

Advantages:

* More security-focused
* Good for enterprise-style environments
* Stronger default hardening
* Good option for production clusters

Disadvantages:

* Slightly heavier than K3s
* More complex than needed for the initial platform
* May introduce additional design overhead

This option may be considered later if the project expands toward a more hardened enterprise Kubernetes design.

### Alternative 3: MicroK8s

MicroK8s is a lightweight Kubernetes distribution.

Advantages:

* Easy to install
* Good for local development
* Lightweight
* Useful for quick testing

Disadvantages:

* Less aligned with the intended private infrastructure and production-style platform direction
* Snap-based installation may not fit all environments
* Less suitable for the project’s long-term architecture goals

This option was not selected.

### Alternative 4: Kind or Minikube

Kind and Minikube are useful for local Kubernetes testing.

Advantages:

* Very easy to start
* Good for learning Kubernetes basics
* Good for local development
* Fast to reset

Disadvantages:

* Not suitable for the production-style platform goal
* Not realistic for long-running operations
* Limited value for demonstrating infrastructure, server bootstrap, upgrades, backup, and day-2 operations

This option was rejected because the project is not intended to be a local-only demo.

### Alternative 5: Managed Kubernetes

Examples:

```text id="hfwczb"
Amazon EKS
Azure AKS
Google GKE
```

Advantages:

* Production-ready managed control plane
* Cloud-native integrations
* Easier lifecycle management
* Strong enterprise adoption

Disadvantages:

* Requires cloud accounts
* May create costs
* Makes the project cloud-provider-specific
* Hides some platform engineering details
* Does not align with the free and open-source private infrastructure goal

This option was rejected for the default implementation.

## GitHub-First Impact

Because the project uses a GitHub-first execution model, K3s will not be installed immediately.

During the current phase, the project will create:

* K3s architecture documentation
* Bootstrap scripts
* Ansible preparation roles
* Cluster configuration files
* Upgrade documentation
* Rollback documentation
* Health check automation
* Runbooks
* GitOps integration structure

But the project will not run K3s installation commands yet.

Do not run:

```bash id="giznl2"
curl -sfL https://get.k3s.io | sh -
```

Do not run any K3s install, uninstall, upgrade, or cluster join commands during the design phase.

## Operational Requirements

The K3s platform design should include:

* Installation procedure
* Control plane bootstrap
* Worker node join procedure
* Kubeconfig handling
* Upgrade procedure
* Rollback procedure
* Node replacement procedure
* Backup and restore procedure
* Certificate handling
* Health checks
* Log collection
* Troubleshooting steps

## Security Requirements

The K3s platform design should include:

* Secure node access assumptions
* No committed kubeconfig credentials
* RBAC planning
* Namespace isolation
* Network Policies
* Pod Security standards
* TLS certificate management
* Secrets strategy
* Image source strategy
* Registry strategy for offline support

## Future Review

This decision should be reviewed if:

* K3s does not meet the platform requirements during execution
* The project moves toward a larger enterprise-only design
* A hardened Kubernetes distribution becomes more appropriate
* Air-gapped requirements are better served by another distribution
* kubeadm becomes necessary for deeper upstream Kubernetes control
* Managed Kubernetes becomes part of a future cloud-specific version

## Related Documents

* `README.md`
* `ARCHITECTURE.md`
* `ROADMAP.md`
* `REPOSITORIES.md`
* `docs/architecture/overview.md`
* `docs/adr/0002-use-free-and-open-source-stack.md`
* `docs/adr/0003-use-github-first-execution-model.md`

## Summary

The Kubernetes Platform project will use K3s for the initial Kubernetes implementation.

K3s provides the right balance of realism, simplicity, low cost, and operational learning value. It allows the project to demonstrate production-style platform engineering practices while remaining accessible for future execution on virtual machines, bare metal, private infrastructure, or air-gapped environments.
