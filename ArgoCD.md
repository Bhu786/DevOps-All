# ARGO CD — INTERVIEW NOTES

**Start-to-End • Simple to Learn • Easy to Remember • Interview Ready**

> This Markdown version keeps the complete topic coverage from the uploaded PATHNEX Argo CD PDF and reorganizes it into simple interview explanations, memory tricks, commands, YAML examples, scenarios, and quick revision. The source defines Argo CD as a declarative GitOps tool for Kubernetes that continuously monitors Git and syncs changes to clusters. fileciteturn4file0L5-L18

---

# 1. What is Argo CD?

**Argo CD** stands for:

> **Argo Continuous Delivery**

It is:

> **A declarative GitOps tool for Kubernetes.**

Argo CD continuously monitors Git repositories and syncs changes to Kubernetes clusters.

The main GitOps idea is:

> **Git is the source of truth.**

That means infrastructure and application definitions are stored in Git, and Argo CD uses that Git state to manage Kubernetes deployments. fileciteturn4file0L6-L12

### Interview Answer

> **Argo CD is a declarative GitOps continuous delivery tool for Kubernetes. It continuously monitors the Git repository and reconciles the Kubernetes cluster with the desired state defined in Git. Git acts as the source of truth.**

### Memory Trick

**ARGO CD = GIT → KUBERNETES**

---

# 2. Why Use Argo CD?

The source gives these major benefits:

- Git-based single source of truth
- Automates application deployment
- Supports rollback
- Corrects drift
- Provides CLI
- Provides Web UI
- Good visibility
- Good auditability
- Supports Helm
- Supports Kustomize
- Supports plain YAML
- Supports Jsonnet fileciteturn4file0L13-L18

### Simple Meaning

```text
Git
 ↓
Source of Truth
 ↓
Argo CD
 ↓
Kubernetes
```

### Interview Answer

> **We use Argo CD to implement GitOps for Kubernetes. It automates deployment, rollback and drift correction, provides UI and CLI visibility, and supports tools such as Helm, Kustomize, YAML and Jsonnet.**

### Memory Trick

**DEPLOY + ROLLBACK + DRIFT + VISIBILITY**

---

# 3. GitOps

GitOps is the foundation of Argo CD.

The source says:

- Git is the source of truth for deployments.
- Changes are made through Git commits. fileciteturn4file0L19-L22

### Simple Flow

```text
Developer
   ↓
Git Commit
   ↓
Git Repository
   ↓
Argo CD
   ↓
Kubernetes Cluster
```

### Interview Answer

> **GitOps means Git is the source of truth for deployment configuration. Changes are made through Git commits, and Argo CD uses that desired state to reconcile Kubernetes.**

### Memory Trick

**GIT = TRUTH**

---

# 4. Core Argo CD Concepts

The source covers:

1. Application
2. Sync
3. Health Status
4. Sync Status

---

# 5. Application

An **Application** is the main object in Argo CD.

It defines:

- What to deploy
- Where to deploy
- How to deploy

### Interview Answer

> **An Argo CD Application is the main object that defines the source of the application, the destination cluster/namespace, and the deployment or sync configuration.**

### Memory Trick

**APPLICATION = WHAT + WHERE + HOW**

---

# 6. Sync

Argo CD compares:

```text
Desired State
     ↓
Git
```

with:

```text
Actual State
     ↓
Kubernetes Cluster
```

If they are different, Argo CD can synchronize them.

### Simple Diagram

```text
        Git
   Desired State
        |
        | compare
        ↓
     Argo CD
        |
        | reconcile/sync
        ↓
 Kubernetes
   Actual State
```

Sync can be:

- Automatic
- Manual

The source explicitly describes Argo CD comparing cluster actual state with Git desired state and syncing automatically or manually when there is a difference. fileciteturn4file0L28-L37

### Interview Answer

> **Argo CD sync compares the desired state stored in Git with the actual state in Kubernetes. If there is a difference, Argo CD can synchronize the cluster either automatically or manually.**

### Memory Trick

**SYNC = MAKE CLUSTER MATCH GIT**

---

# 7. Health Status

The source lists these health states:

- `Healthy`
- `Degraded`
- `Progressing`
- `Missing`

### Easy Meaning

| Health Status | Simple Meaning |
|---|---|
| Healthy | Application is healthy |
| Degraded | Application has a problem |
| Progressing | Application is still progressing |
| Missing | Expected resource is missing |

### Memory Trick

**H-D-P-M**

> **Healthy → Degraded → Progressing → Missing**

---

# 8. Sync Status

The source lists:

- `Synced`
- `OutOfSync`
- `Unknown`

### Easy Meaning

| Sync Status | Simple Meaning |
|---|---|
| Synced | Cluster matches Git |
| OutOfSync | Cluster differs from Git |
| Unknown | Sync state cannot be determined |

### Memory Trick

**S-O-U**

> **Synced → OutOfSync → Unknown**

---

# 9. Health vs Sync Status

This is a very useful interview distinction.

## Sync Status asks:

> **Does the cluster match Git?**

## Health Status asks:

> **Is the deployed application/resource healthy?**

### Memory Trick

```text
SYNC
= MATCH?

HEALTH
= WORKING?
```

---

# 10. Argo CD Architecture

The source lists these components:

1. API Server
2. Repository Server
3. Application Controller
4. Dex — optional

fileciteturn4file0L38-L42

---

# 11. API Server

The API Server handles:

- CLI
- UI
- API requests

### Interview Answer

> **The Argo CD API Server provides the interface for the CLI, web UI, and API operations.**

### Memory Trick

**API SERVER = ENTRY POINT**

---

# 12. Repository Server

The Repository Server:

- Clones Git repositories.
- Reads Git repositories.

### Interview Answer

> **The Repository Server is responsible for accessing Git repositories by cloning and reading the application manifests or configuration.**

### Memory Trick

**REPO SERVER = READ GIT**

---

# 13. Application Controller

The Application Controller:

> **Reconciles desired state with the live Kubernetes cluster.**

This is one of the most important Argo CD interview concepts.

### Simple Flow

```text
Git Desired State
       ↓
Application Controller
       ↓
Kubernetes Live State
       ↓
Reconcile
```

### Interview Answer

> **The Application Controller continuously reconciles the desired state from Git with the live state in Kubernetes and takes action when they differ.**

### Memory Trick

**CONTROLLER = RECONCILE**

---

# 14. Dex

Dex is optional.

The source says it provides authentication such as:

- SSO
- LDAP
- etc.

### Interview Answer

> **Dex is an optional authentication component used to integrate Argo CD with authentication systems such as SSO and LDAP.**

### Memory Trick

**DEX = AUTH**

---

# 15. Architecture — One-Line Memory

```text
API Server
→ CLI / UI / API

Repository Server
→ Git

Application Controller
→ Reconcile

Dex
→ Authentication
```

### Master Trick

> **API talks, Repo reads, Controller reconciles, Dex authenticates.**

---

# 16. Argo CD Architecture Diagram Understanding

The diagram on page 1 shows the main relationship:

```text
Git Repository
      |
      | fetch
      ↓
Repository Controller / Server
      |
      ↓
Application Controller
      |
      ↓
Argo CD Applications
      |
      ↓
Kubernetes Cluster
      |
      ↓
Helm Releases / Kubernetes Resources
```

The visual also shows the Kubernetes control plane, including the Kubernetes API and etcd, interacting with the Argo CD-managed resources.

### Interview Explanation

> **Argo CD reads the desired configuration from Git, the controller reconciles it, and the Kubernetes cluster is brought toward that desired state.**

---

# 17. Installing Argo CD

## Prerequisites

The source requires:

- Kubernetes cluster
  - Minikube
  - Kind
  - EKS
- `kubectl` configured fileciteturn4file0L43-L46

### Memory Trick

**K8s + kubectl = READY**

---

# 18. Create Argo CD Namespace

```bash
kubectl create namespace argocd
```

### Meaning

Creates a dedicated Kubernetes namespace:

```text
argocd
```

---

# 19. Install Argo CD

The source gives:

```bash
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
```

This installs Argo CD into the `argocd` namespace.

### Interview Answer

> **I create the argocd namespace and apply the official Argo CD installation manifest into that namespace.**

---

# 20. Access Argo CD UI

Use:

```bash
kubectl port-forward svc/argocd-server -n argocd 8080:443
```

Then visit:

```text
https://localhost:8080
```

### Memory Trick

**PORT-FORWARD = LOCAL UI ACCESS**

---

# 21. Get the Admin Password

The source gives:

```bash
kubectl get secret argocd-initial-admin-secret -n argocd -o yaml
```

This retrieves the initial admin secret.

### Interview Line

> **After installation, I retrieve the initial admin secret from the argocd namespace and use it to access the Argo CD UI.**

---

# 22. Creating Your First Application

Create:

```text
app.yaml
```

The source's example is a Guestbook application.

---

# 23. Argo CD Application YAML

```yaml
apiVersion: argoproj.io/v1alpha1
kind: Application

metadata:
  name: guestbook
  namespace: argocd

spec:
  project: default

  source:
    repoURL: https://github.com/argoproj/argocd-example-apps
    targetRevision: HEAD
    path: guestbook

  destination:
    server: https://kubernetes.default.svc
    namespace: default

  syncPolicy:
    automated:
      selfHeal: true
      prune: true
```

This structure comes directly from the source's first-application example. fileciteturn4file0L63-L86

---

# 24. Understand the Application YAML

## `apiVersion`

```yaml
apiVersion: argoproj.io/v1alpha1
```

Identifies the Argo CD Application API version.

---

## `kind`

```yaml
kind: Application
```

Tells Kubernetes this is an Argo CD Application object.

---

## `metadata.name`

```yaml
name: guestbook
```

Application name:

```text
guestbook
```

---

## `metadata.namespace`

```yaml
namespace: argocd
```

The Application object is created in:

```text
argocd
```

---

## `project`

```yaml
project: default
```

Uses the default Argo CD project.

---

# 25. Application Source

```yaml
source:
  repoURL: https://github.com/argoproj/argocd-example-apps
  targetRevision: HEAD
  path: guestbook
```

### `repoURL`

Where the desired manifests/configuration are stored.

### `targetRevision`

Which Git revision to use.

The source uses:

```text
HEAD
```

### `path`

The directory containing the Guestbook application configuration.

### Memory Trick

**SOURCE = WHERE + WHICH VERSION + WHICH PATH**

---

# 26. Application Destination

```yaml
destination:
  server: https://kubernetes.default.svc
  namespace: default
```

This tells Argo CD where to deploy.

### `server`

The target Kubernetes API server.

### `namespace`

The target Kubernetes namespace.

### Memory Trick

**DESTINATION = WHERE TO DEPLOY**

---

# 27. Automated Sync

The source uses:

```yaml
syncPolicy:
  automated:
    selfHeal: true
    prune: true
```

This enables automatic synchronization.

---

# 28. `selfHeal`

```yaml
selfHeal: true
```

Self-heal fixes drift when someone manually changes Kubernetes resources.

### Example

```text
Git says replicas = 3
        ↓
Someone manually changes cluster to 1
        ↓
Argo CD detects drift
        ↓
Self-heal
        ↓
Cluster returns toward Git state
```

### Interview Answer

> **Self-heal allows Argo CD to automatically correct drift caused by manual changes in the cluster.**

### Memory Trick

**SELF-HEAL = FIX DRIFT**

---

# 29. `prune`

```yaml
prune: true
```

Prune deletes resources that were removed from Git.

### Example

```text
Resource exists in cluster
        ↓
Resource removed from Git
        ↓
Argo CD detects it
        ↓
Prune
        ↓
Resource removed
```

### Interview Answer

> **Prune removes Kubernetes resources that are no longer defined in the Git desired state.**

### Memory Trick

**PRUNE = DELETE REMOVED RESOURCES**

---

# 30. Apply the Application

Use:

```bash
kubectl apply -f app.yaml
```

### Flow

```text
app.yaml
   ↓
kubectl apply
   ↓
Argo CD Application
   ↓
Git source
   ↓
Kubernetes deployment
```

---

# 31. Argo CD CLI Basics

The source covers:

1. Login
2. List applications
3. Sync application
4. Delete application

---

# 32. Login

```bash
argocd login localhost:8080
```

### Memory Trick

**LOGIN = CONNECT CLI TO ARGO CD**

---

# 33. List Applications

```bash
argocd app list
```

Shows Argo CD applications.

### Interview Line

> **I use `argocd app list` to view the applications managed by Argo CD.**

---

# 34. Manually Sync an Application

```bash
argocd app sync guestbook
```

### Interview Answer

> **`argocd app sync` manually triggers synchronization for the selected Argo CD application.**

### Memory Trick

**SYNC = APPLY GIT STATE**

---

# 35. Delete an Application

```bash
argocd app delete guestbook
```

Deletes the Argo CD application.

### Memory Trick

**DELETE = REMOVE APP**

---

# 36. Sync Strategies

The source describes two strategies:

1. Manual Sync
2. Automatic Sync

---

# 37. Manual Sync

With manual sync:

> You manually click or run the command to sync changes.

Example:

```bash
argocd app sync guestbook
```

### Interview Answer

> **In manual sync, Argo CD detects the desired state but synchronization is triggered manually by the user.**

### Memory Trick

**MANUAL = YOU TRIGGER**

---

# 38. Automatic Sync

Example:

```yaml
syncPolicy:
  automated:
    selfHeal: true
    prune: true
```

Argo CD automatically synchronizes changes.

### Interview Answer

> **Automatic sync allows Argo CD to synchronize the cluster with the Git desired state automatically.**

### Memory Trick

**AUTO = ARGO TRIGGERS**

---

# 39. Manual vs Automatic Sync

| Feature | Manual | Automatic |
|---|---|---|
| Who triggers sync? | User | Argo CD |
| Git change | Detected | Detected |
| Deployment | Manual trigger | Automatic |
| Useful for | Controlled deployments | Continuous GitOps |

---

# 40. Authentication and RBAC

The source says Argo CD supports SSO through Dex.

Examples:

- GitHub
- LDAP
- Google
- SAML

Roles and permissions can be configured using:

```text
argocd-rbac-cm
```

### Interview Answer

> **Argo CD supports SSO integrations through Dex, including providers such as GitHub, LDAP, Google and SAML. RBAC roles and permissions can be configured through the argocd-rbac-cm ConfigMap.**

### Memory Trick

**DEX = AUTH**

**RBAC = PERMISSIONS**

---

# 41. Advanced Features

The source lists five important advanced features:

1. Helm support
2. Kustomize support
3. Multi-cluster support
4. App of Apps
5. PreSync/PostSync hooks

---

# 42. Helm Support

Argo CD can use Helm charts as a source.

### Interview Answer

> **Argo CD supports Helm charts as an application source.**

### Memory Trick

**ARGO + HELM = HELM DEPLOYMENT THROUGH GITOPS**

---

# 43. Kustomize Support

Kustomize allows:

- Patching
- YAML overlays

The source says Argo CD supports Kustomize for patching and overlaying YAML files.

### Interview Answer

> **Argo CD supports Kustomize, allowing Kubernetes YAML to be customized using patches and overlays.**

---

# 44. Multi-Cluster Support

Argo CD can deploy applications to different Kubernetes clusters.

### Interview Answer

> **Argo CD supports multi-cluster deployment, allowing applications to be deployed to different Kubernetes clusters.**

### Memory Trick

**MULTI-CLUSTER = ONE ARGO, MANY CLUSTERS**

---

# 45. App of Apps Pattern

The source describes:

> Manage multiple Argo CD applications from a single Git repository.

### Simple Idea

```text
Git Repository
      |
      ↓
Parent Application
      |
 +----+----+----+
 ↓    ↓    ↓    ↓
App1 App2 App3 App4
```

### Interview Answer

> **The App of Apps pattern uses one Argo CD application to manage multiple child applications, with their definitions maintained through Git.**

### Memory Trick

**APP OF APPS = PARENT → MANY APPS**

---

# 46. PreSync / PostSync Hooks

These hooks customize the deployment process.

### PreSync

Runs before synchronization.

### PostSync

Runs after synchronization.

### Interview Answer

> **PreSync and PostSync hooks allow us to customize steps around the synchronization process, such as actions that should happen before or after deployment.**

### Memory Trick

**PRE = BEFORE**

**POST = AFTER**

---

# 47. Example Use Case — Guestbook Demo

The source gives this demo flow:

1. Deploy Guestbook using the example repository.
2. Open the UI and watch the deployment.
3. Change something in Git, such as replica count.
4. Commit and push the change.
5. Argo CD detects the change and syncs automatically.
6. Manually delete a pod and watch Argo CD recreate it through self-heal. fileciteturn4file0L125-L137

### Complete Flow

```text
Developer
   ↓
Change Git
   ↓
git commit
   ↓
git push
   ↓
Argo CD detects change
   ↓
Automatic Sync
   ↓
Kubernetes updated
   ↓
Delete Pod Manually
   ↓
Self-Heal
   ↓
Pod recreated
```

### Interview Answer

> **In the Guestbook demo, I change the desired configuration in Git, commit and push it, Argo CD detects the Git change and synchronizes the cluster. If I manually delete a pod, self-heal detects the drift and recreates the resource.**

---

# 48. Common Argo CD Commands

The source provides this command table. fileciteturn4file0L138-L146

| Command | Purpose |
|---|---|
| `kubectl get pods -n argocd` | Check Argo CD pods |
| `kubectl port-forward svc/argocd-server -n argocd 8080:443` | Access Argo CD UI |
| `argocd app create` | Create a new app |
| `argocd app sync <app-name>` | Trigger sync |
| `argocd app delete <app-name>` | Delete app |

---

# 49. Complete Installation Cheat Sheet

```bash
# Create namespace
kubectl create namespace argocd

# Install Argo CD
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml

# Check pods
kubectl get pods -n argocd

# Access UI
kubectl port-forward svc/argocd-server -n argocd 8080:443

# Get initial admin secret
kubectl get secret argocd-initial-admin-secret -n argocd -o yaml
```

Then:

```text
https://localhost:8080
```

---

# 50. Complete CLI Cheat Sheet

```bash
# Login
argocd login localhost:8080

# List apps
argocd app list

# Sync
argocd app sync guestbook

# Delete
argocd app delete guestbook

# Create app
argocd app create
```

---

# 51. Argo CD Decision Tree

```text
What do I need?

        |
        +---- Git is the source of truth?
        |         |
        |         +---- GITOPS
        |
        +---- Deploy to Kubernetes?
        |         |
        |         +---- ARGO CD
        |
        +---- Need to define deployment?
        |         |
        |         +---- APPLICATION
        |
        +---- Git != Cluster?
        |         |
        |         +---- OUTOFSYNC
        |
        +---- Need to make Cluster = Git?
        |         |
        |         +---- SYNC
        |
        +---- Someone manually changed resources?
        |         |
        |         +---- SELF-HEAL
        |
        +---- Resource removed from Git?
        |         |
        |         +---- PRUNE
        |
        +---- Need Helm?
        |         |
        |         +---- HELM SUPPORT
        |
        +---- Need YAML overlays?
        |         |
        |         +---- KUSTOMIZE
        |
        +---- Many clusters?
        |         |
        |         +---- MULTI-CLUSTER
        |
        +---- Many Argo apps?
        |         |
        |         +---- APP OF APPS
        |
        +---- Before/after sync actions?
                  |
                  +---- PRESYNC / POSTSYNC
```

---

# 52. Most Important Interview Comparisons

## Sync Status vs Health Status

```text
Sync Status
= Is Git state equal to cluster state?

Health Status
= Is the application healthy?
```

---

## Manual vs Automatic Sync

```text
Manual
= User triggers

Automatic
= Argo CD triggers
```

---

## Self-Heal vs Prune

```text
Self-Heal
= Fix manually changed resources

Prune
= Delete resources removed from Git
```

### Master Trick

> **Self-heal fixes. Prune removes.**

---

# 53. GitOps Interview Question

### Q: What is GitOps?

### Answer

> **GitOps is a deployment approach where Git acts as the source of truth for infrastructure and application configuration. Changes are made through Git commits, and Argo CD continuously reconciles the Kubernetes cluster with the desired state stored in Git.**

---

# 54. Why Argo CD Instead of Manual Kubernetes Deployment?

### Interview Answer

> **Instead of manually applying Kubernetes manifests, Argo CD allows Git to become the source of truth and continuously reconciles the cluster with that desired state. It provides automated synchronization, rollback and drift correction, along with UI and CLI visibility.**

---

# 55. What Happens When Someone Manually Changes Kubernetes?

### Answer

If the cluster becomes different from Git:

```text
Git Desired State
        ≠
Kubernetes Actual State
```

Argo CD detects:

```text
OutOfSync
```

If automatic sync/self-heal is enabled:

```text
Argo CD
   ↓
Reconcile
   ↓
Cluster returns toward Git
```

### Interview Answer

> **If someone manually changes a resource and the cluster differs from Git, Argo CD detects the drift. With self-heal enabled, Argo CD can automatically correct that drift.**

---

# 56. What Happens When a Resource Is Removed from Git?

If:

```text
Resource exists in Cluster
```

but it is removed from:

```text
Git
```

and pruning is enabled:

```yaml
prune: true
```

Argo CD removes the resource.

### Interview Answer

> **When a resource is removed from Git and prune is enabled, Argo CD can remove that resource from the cluster as well.**

---

# 57. Ready-to-Speak Architecture Answer

If interviewer asks:

> **“Explain Argo CD architecture.”**

Say:

> **Argo CD has an API Server, Repository Server, Application Controller and optional Dex. The API Server handles CLI, UI and API requests. The Repository Server clones and reads Git repositories. The Application Controller continuously reconciles the desired state from Git with the live Kubernetes state. Dex can provide authentication integrations such as SSO and LDAP.**

---

# 58. Ready-to-Speak Project Answer

If asked:

> **“How did you use Argo CD?”**

Use this source-aligned answer:

> **I used Argo CD as the GitOps continuous delivery tool for Kubernetes. I kept the desired deployment configuration in Git, created an Argo CD Application pointing to the Git repository and Kubernetes destination, and configured automated sync with self-heal and prune. When I pushed changes to Git, Argo CD detected the changes and synchronized the cluster. I also used self-healing to recover from manual pod changes.**

---

# 59. 30-Second Argo CD Revision

```text
ARGO CD
= Argo Continuous Delivery

GITOPS
= Git is source of truth

APPLICATION
= What + Where + How

SYNC
= Make cluster match Git

SYNC STATUS
= Synced / OutOfSync / Unknown

HEALTH
= Healthy / Degraded / Progressing / Missing

API SERVER
= CLI / UI / API

REPOSITORY SERVER
= Clone + Read Git

APPLICATION CONTROLLER
= Reconcile

DEX
= Authentication

SELF-HEAL
= Fix drift

PRUNE
= Delete resources removed from Git

MANUAL SYNC
= User triggers

AUTO SYNC
= Argo triggers

HELM
= Helm charts

KUSTOMIZE
= YAML patches/overlays

MULTI-CLUSTER
= Deploy to different clusters

APP OF APPS
= One app manages many apps

PRESYNC
= Before sync

POSTSYNC
= After sync
```

---

# 60. Final Master Memory

> **“Argo CD is a declarative GitOps tool for Kubernetes. Git is the source of truth. The Application defines what, where and how to deploy. The Repository Server reads Git, the Application Controller reconciles Git with Kubernetes, and the API Server provides UI/CLI/API access. Sync makes the cluster match Git, self-heal fixes drift, and prune removes resources deleted from Git.”**

---

# 61. FINAL MASTER DIAGRAM

```text
                         GIT
                    Source of Truth
                         |
                         | Git changes
                         ↓
                 +----------------+
                 |  ARGO CD       |
                 |                |
                 | API Server     |
                 | Repo Server    |
                 | App Controller |
                 | Dex (optional) |
                 +----------------+
                         |
                         | Reconcile / Sync
                         ↓
                KUBERNETES CLUSTER
                         |
            +------------+------------+
            |            |            |
           App          Pods       Services
            |
        Desired State
        vs Live State
            |
      +-----+------+
      |            |
    MATCH       DIFFERENCE
      |            |
    SYNCED      OUTOFSYNC
                   |
              Auto Sync /
              Self-Heal
                   |
                   ↓
             Cluster fixed
```

---

# 62. Source Coverage Check

This document preserves the source's complete topic coverage:

- Argo CD definition
- Argo Continuous Delivery
- Declarative GitOps
- Kubernetes
- Continuous Git monitoring
- Automatic synchronization
- Git as source of truth
- Git-based single source of truth
- Deployment automation
- Rollback
- Drift correction
- CLI
- Web UI
- Visibility
- Auditability
- Helm
- Kustomize
- Plain YAML
- Jsonnet
- GitOps
- Application
- Sync
- Health status
- Sync status
- Healthy
- Degraded
- Progressing
- Missing
- Synced
- OutOfSync
- Unknown
- API Server
- Repository Server
- Application Controller
- Dex
- Kubernetes prerequisites
- Minikube
- Kind
- EKS
- kubectl
- Argo CD installation
- `argocd` namespace
- Installation manifest
- Port forwarding
- Argo CD UI
- Initial admin secret
- First Application
- Guestbook
- Application YAML
- Project
- Source
- repoURL
- targetRevision
- path
- Destination
- server
- namespace
- syncPolicy
- automated sync
- selfHeal
- prune
- `kubectl apply`
- Argo CD CLI
- Login
- List apps
- Manual sync
- Delete app
- Manual Sync
- Automatic Sync
- Self-heal
- Prune
- Authentication
- SSO
- GitHub
- LDAP
- Google
- SAML
- Dex
- RBAC
- `argocd-rbac-cm`
- Helm support
- Kustomize support
- Multi-cluster
- App of Apps
- PreSync hooks
- PostSync hooks
- Guestbook demo
- Git change
- Commit and push
- Automatic sync
- Manual pod deletion
- Self-healing
- Common commands
- Architecture diagrams/screenshots shown in the source

---

# FINAL ONE-LINE INTERVIEW ANSWER

> **“Argo CD is a declarative GitOps continuous delivery tool for Kubernetes where Git is the source of truth; Argo CD continuously compares Git's desired state with the cluster's live state and reconciles them through synchronization, with features such as automated deployment, self-healing, pruning, rollback, Helm/Kustomize support, and multi-cluster deployment.”**

