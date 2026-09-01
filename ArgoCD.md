# deployment tools hai
# why we need argocd already we have jenkins and gitactions 
Jenkins ya GitHub Actions traditional CI/CD tools hain jo **Imperative (Push-based)** model par kaam karte hain. Inme drawbacks the, jise solve karne ke liye ArgoCD (Declarative GitOps) aaya.

===
# 🚀 Argo CD — VERY SHORT MASTER MIND MAP

> **Goal:** PDF ka **poora important content**, but **minimum words** mein.
> Source: uploaded Argo CD PDF. 

```text
ARGO CD
│
├── 1. WHAT?
│   ├── Argo Continuous Delivery
│   ├── Declarative GitOps tool
│   ├── Mainly for Kubernetes
│   ├── Git → Source of Truth
│   └── Git changes → Automatically sync → K8s
│
├── 2. WHY?
│   ├── Git-based single source of truth
│   ├── Deployment
│   ├── Rollback
│   ├── Drift correction
│   ├── CLI + Web UI
│   ├── Visibility + Auditability
│   └── Supports:
│       ├── Helm
│       ├── Kustomize
│       ├── YAML
│       └── Jsonnet
│
├── 3. CORE CONCEPTS
│   │
│   ├── GitOps
│   │   ├── Git = Source of Truth
│   │   └── Changes via Git commits
│   │
│   ├── Application
│   │   └── Defines WHAT + WHERE + HOW to deploy
│   │
│   ├── Sync
│   │   ├── Compare:
│   │   │   Git = Desired State
│   │   │   K8s = Actual State
│   │   └── Difference → Sync
│   │       ├── Manual
│   │       └── Automatic
│   │
│   ├── Health Status
│   │   ├── Healthy
│   │   ├── Degraded
│   │   ├── Progressing
│   │   └── Missing
│   │
│   └── Sync Status
│       ├── Synced
│       ├── OutOfSync
│       └── Unknown
│
├── 4. ARCHITECTURE
│   ├── API Server
│   │   └── CLI / UI / API handling
│   ├── Repository Server
│   │   └── Clone + read Git repos
│   ├── Application Controller
│   │   └── Reconcile desired ↔ live cluster
│   └── Dex (Optional)
│       └── Authentication / SSO / LDAP
│
├── 5. INSTALL
│   │
│   ├── Prerequisites
│   │   ├── Kubernetes cluster
│   │   │   └── Minikube / Kind / EKS
│   │   └── kubectl configured
│   │
│   ├── Create namespace
│   │   └── kubectl create namespace argocd
│   │
│   ├── Install manifests
│   │   └── kubectl apply -n argocd -f <install.yaml>
│   │
│   └── UI
│       ├── port-forward
│       └── https://localhost:8080
│
├── 6. FIRST APPLICATION
│   │
│   ├── Create app.yaml
│   ├── kind: Application
│   ├── project: default
│   ├── source
│   │   ├── repoURL
│   │   ├── targetRevision
│   │   └── path
│   ├── destination
│   │   ├── cluster/server
│   │   └── namespace
│   └── syncPolicy
│       └── automated
│           ├── selfHeal: true
│           └── prune: true
│
├── 7. CLI BASICS
│   ├── Login
│   │   └── argocd login
│   ├── List apps
│   │   └── argocd app list
│   ├── Manual sync
│   │   └── argocd app sync <app>
│   └── Delete app
│       └── argocd app delete <app>
│
├── 8. SYNC STRATEGIES
│   ├── Manual Sync
│   │   └── User manually syncs
│   │
│   └── Automatic Sync
│       ├── selfHeal
│       │   └── Fix manually-created drift
│       └── prune
│           └── Delete resources removed from Git
│
├── 9. AUTHENTICATION + RBAC
│   ├── SSO via Dex
│   │   ├── GitHub
│   │   ├── LDAP
│   │   ├── Google
│   │   └── SAML
│   └── Roles/Permissions
│       └── argocd-rbac-cm
│
├── 10. ADVANCED
│   ├── Helm → Helm charts
│   ├── Kustomize → Patch/Overlay YAML
│   ├── Multi-cluster → Multiple K8s clusters
│   ├── App of Apps
│   │   └── Manage multiple Argo apps
│   │       from one Git repo
│   └── PreSync / PostSync Hooks
│       └── Customize deployment
│
├── 11. DEMO FLOW
│   ├── Deploy Guestbook
│   ├── Watch in UI
│   ├── Change Git
│   │   └── e.g. replica count
│   ├── Commit + Push
│   ├── Argo CD detects change
│   ├── Auto Sync
│   └── Delete pod manually
│       └── Self-heal → Pod recreated
│
└── 12. IMPORTANT COMMANDS
    ├── kubectl get pods -n argocd
    │   └── Check Argo CD pods
    │
    ├── kubectl port-forward svc/argocd-server -n argocd 8080:443
    │   └── Access UI
    │
    ├── argocd app create
    │   └── Create app
    │
    ├── argocd app sync <app-name>
    │   └── Trigger sync
    │
    └── argocd app delete <app-name>
        └── Delete app
```

### 🔥 MOST IMPORTANT FLOW

```text
Developer
    ↓
Git Commit
    ↓
Git Repository
    ↓
Argo CD
    ↓
Compare:
Git Desired State
        ↕
K8s Actual State
    ↓
Difference?
    ↓
OutOfSync / Drift
    ↓
Sync / Reconcile
    ↓
Kubernetes
    ↓
Healthy
```

PDF ke **page 7 ke architecture diagram** mein bhi overall CI/CD flow dikhaya gaya hai: code/change → GitLab CI/build & scans → Docker image/repository → Argo → test/deployment environments. 

### 🧠 10-second revision

```text
Argo CD
= Kubernetes CD + GitOps

Git
= Source of Truth

Application
= What + Where + How

Sync
= Desired vs Actual → Same

Drift
= Difference

Self-Heal
= Fix Drift

Prune
= Delete removed resources

Controller
= Reconcile

PreSync
= Before deployment

PostSync
= After deployment
```

This keeps the PDF's **all 12 sections + commands + concepts**, but removes the long explanations and repetition.  


===
---

### **Traditional CI/CD (Jenkins / GitHub Actions) ke Main Drawbacks**

* **Direct `kubectl` Commands & Script Maintenance:**
Jenkins ya GitHub Actions mein aapko deployment ke liye `kubectl apply -f deployment.yaml` jaise commands scripts mein likhne padte hain. Agar pipeline fail ho jaye ya script break ho, toh cluster incomplete state mein phans jata hai.
* **No Drift Detection (Configuration Drift):**
Suppose aapne Jenkins se deployment kar di (jisme 3 replicas the). Baad mein kisi engineer ne emergency mein cluster mein login karke manually 5 replicas kar diye. Jenkins ko is manual change ka pata hi nahi chalega. Jab tak next build nahi chalegi, Git code aur Actual Cluster state mein antar (Drift) bana rahega.
* **Security Risks (Cluster Credentials in CI):**
Jenkins ya GitHub Actions ko deployment karne ke liye Kubernetes cluster ke admin credentials (`kubeconfig` or Service Account Tokens) chahiye hote hain. Agar CI server compromise ho gaya, toh poore cluster ka control leak ho sakta hai.
* **Multi-Cluster Complexity:**
Aapko alag-alag environments (Dev, QA, Prod) ya multiple Kubernetes clusters par deploy karne ke liye complex SSH keys, dynamic contexts, aur scripts handle karni padti hain.

---

### **ArgoCD In Drawbacks Ko Kaise Solve Karta Hai?**

| Scenario | Jenkins / GitHub Actions | ArgoCD (GitOps) |
| --- | --- | --- |
| **Model** | **Push-Based:** Outer pipeline cluster ko command bhejti hai. | **Pull-Based:** ArgoCD cluster ke andar se Git ko sync karta hai. |
| **Cluster Credentials** | External CI Runner mein credentials store karne padte hain. | Zero Secrets Leak! ArgoCD cluster ke andar hi chalta hai. |
| **Drift Management** | Revert nahi kar sakta jab tak manual trigger na ho. | **Self-Healing:** Agar cluster mein koi manual badlaav karega, ArgoCD use automatically detect karke Git state se sync kar dega. |
| **Rollback** | Complex rollback scripts run karni padti hain. | Instant rollback! Bas Git commit revert karo, ArgoCD sync kar lega. |

---

### **Industry Standard Setup (CI + CD Split)**

Aaj enterprise companies mein Jenkins/GitHub Actions ko poori tarah replace nahi kiya gaya hai, balki unka kaam split kar diya gaya hai:

```text
[ Developer Commit ] ──► [ GitHub Actions / Jenkins ] ──► Builds Code, Runs Tests & Pushes Docker Image
                                                                      │
                                                                      ▼
[ Kubernetes Cluster ] ◄── Syncs Manifests ◄── [ ArgoCD ] ◄── Updates Image Tag in Git Repo

```

* **Jenkins / GitHub Actions (CI - Continuous Integration):** Code compile karna, unit tests chalana, aur Docker image build karke registry mein push karna.
* **ArgoCD (CD - Continuous Deployment):** Image build hone ke baad Git repository se K8s manifests ko cluster ke andar safely sync aur reconcile karna.

* ===========================
* ===================================



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
==========================
> =======================
Bilkul. Neeche **Argo CD ke ab tak poore discussion + tumhare asked questions** ko ek hi jagah **start-to-end master short notes** mein rakha hai. Content compromise nahi kiya, bas language simple rakhi hai.

# ARGO CD — MASTER NOTES

## 1. What is Argo CD?

**Argo CD = Kubernetes ke liye Continuous Delivery (CD) + GitOps tool.**

Iska main kaam:

> **Git mein jo desired configuration hai, uske according Kubernetes application ko deploy aur continuously sync rakhna.**

Example:

```text
Git
replicas: 3
image: v2
   ↓
Argo CD
   ↓
Kubernetes
3 Pods
image: v2
```

### Simple words

Argo CD baar-baar check karta hai:

```text
Git              Kubernetes
Desired State    Actual State
    3 replicas      2 replicas
          ↓
       Difference
          ↓
         Drift
```

Agar auto-sync enabled hai, Argo CD difference ko fix karke Kubernetes ko Git ke according kar sakta hai.

---

# 2. What is GitOps?

**GitOps koi tool nahi hai.**

Ye **deployment/operations karne ka approach/method** hai.

### GitOps ka basic idea:

> **Git ko source of truth bana do.**

Matlab:

```text
Developer
    ↓
Change in Git
    ↓
Argo CD
    ↓
Kubernetes
```

Git mein jo configuration hai, wahi **desired state** hai.

### Example

Git:

```yaml
replicas: 3
image: myapp:v2
```

Argo CD ensure karega:

```text
Kubernetes:
3 replicas
myapp:v2
```

### Naam kaise yaad rakho?

```text
Git + Operations
       ↓
     GitOps
```

**GitOps = Git ke through deployment/operations manage karna.**

---

# 3. GitOps ka alternative kya hai?

GitOps ka koi ek specific alternative tool nahi hai.

Alternative approach ho sakta hai:

### Traditional / Push-based deployment

```text
Developer
   ↓
Jenkins / GitHub Actions
   ↓
kubectl
   ↓
Kubernetes
```

Pipeline directly Kubernetes mein deployment push karti hai.

### GitOps / Pull + Reconciliation approach

```text
Developer
   ↓
Git
   ↓
Argo CD
   ↓
Kubernetes
```

Argo CD Git ko read karta hai aur Kubernetes ko Git ke according maintain karta hai.

---

# 4. Jenkins/GitHub Actions se bhi ye possible hai?

### YES. ✅

Ye bahut important hai.

Jenkins/GitHub Actions bhi Kubernetes deploy kar sakte hain.

Example:

```text
Jenkins
   ↓
kubectl apply -f deployment.yaml
   ↓
Kubernetes
```

Aur theoretically Jenkins/GitHub Actions ko aise configure bhi kar sakte ho ki:

```text
Check Git
   ↓
Check Kubernetes
   ↓
Difference?
   ↓
YES
   ↓
Fix it
```

### To Argo CD ka benefit kya?

Argo CD mein **GitOps + continuous reconciliation + Kubernetes CD** core functionality hai.

Jenkins/GitHub Actions mein ye logic tumhe generally **pipeline/scripts se build/configure** karna padega.

### Simple difference:

> **Jenkins/GitHub Actions = Pipeline/automation tool**

> **Argo CD = Kubernetes GitOps/CD specialist**

---

# 5. Why Argo CD if Jenkins/GitHub Actions can deploy?

Suppose:

```text
Git:
replicas: 3
```

Argo CD deploy karta hai:

```text
Kubernetes:
3 replicas
```

Ab kisi ne manually Kubernetes mein change kar diya:

```text
Kubernetes:
2 replicas
```

Now:

```text
Git          Kubernetes
3 replicas   2 replicas
      ↓           ↓
       DIFFERENT
          ↓
        DRIFT
```

Argo CD continuously compare karta hai:

```text
Desired State
     ↓
    Git
     ↕
 Argo CD
     ↕
Actual State
     ↓
 Kubernetes
```

Difference mila to:

```text
OutOfSync
```

Aur auto-sync enabled ho to Kubernetes ko desired state ke according synchronize kar sakta hai.

---

# 6. Drift kya hai?

**Drift = Git ke desired state aur Kubernetes ke actual state mein difference.**

Example:

```text
Git:
replicas = 3

Kubernetes:
replicas = 2
```

Difference = **Drift**

### Simple definition:

> **Drift means actual infrastructure/application state has moved away from the desired state defined in Git.**

---

# 7. Reconciliation kya hai?

Ye Argo CD ka **bahut important concept** hai.

**Reconciliation = desired state aur actual state ko compare karke actual state ko desired state ke saath match karna.**

```text
Desired State
Git
   ↓
Compare
   ↕
Actual State
Kubernetes
   ↓
Difference?
   ↓
Fix / Sync
```

### Yaad rakho:

> **Argo CD ka heart = Reconciliation**

---

# 8. Argo CD Kubernetes ke liye hi hai?

Interview mein:

> **Argo CD is primarily designed for Kubernetes-based Continuous Delivery and GitOps.**

Simple:

> **Argo CD mainly Kubernetes applications ko deploy/manage karne ke liye use hota hai.**

"Only Kubernetes" bolne ke bajay **primarily designed for Kubernetes** bolna interview mein safer/better hai.

---

# 9. Argo CD ke Components

Important components:

```text
                 ARGO CD
                    │
        ┌───────────┼────────────┐
        ↓           ↓            ↓
   API Server   Repo Server   Application
                              Controller
        │           │            │
        ↓           ↓            ↓
      User        Git Repo    Kubernetes
```

---

## 9.1 API Server

**API Server = Argo CD ka entry point.**

User/UI/CLI Argo CD se API Server ke through communicate karta hai.

Example:

```bash
argocd app sync my-app
```

Flow:

```text
User / CLI / UI
       ↓
   API Server
       ↓
    Argo CD
```

### Remember:

> **API Server → User aur Argo CD ke beech communication.**

---

# 10. Repository Server

**Repo Server = Git repository se application configuration laata hai.**

Git mein ho sakta hai:

```text
deployment.yaml
service.yaml
configmap.yaml
```

Repo Server Git se ye configuration retrieve/process karta hai.

### Remember:

> **Repo Server → Git se desired configuration laata hai.**

---

# 11. Application Controller

**Application Controller = Argo CD ka most important component.**

Iska main kaam:

> **Desired state aur actual state ko compare karna aur required synchronization/reconciliation karna.**

Example:

```text
Git                  Kubernetes
3 replicas            2 replicas
     ↓                    ↓
     └──── Compare ───────┘
              ↓
            Drift
              ↓
       Reconciliation
              ↓
          Sync/Fix
```

### Remember:

> **Application Controller → Compare + Reconcile + Sync**

---

# 12. Argo CD UI / CLI

Argo CD ko operate karne ke liye:

```text
Web UI
  OR
CLI
```

use kar sakte ho.

Examples:

```bash
argocd app list
argocd app get my-app
argocd app sync my-app
```

---

# 13. Argo CD Health Statuses

Health status batata hai:

> **Application/resource ki current health condition kya hai?**

Important statuses:

```text
Healthy
Progressing
Degraded
Suspended
Missing
Unknown
```

---

## 13.1 Healthy 🟢

Application properly running hai.

Example:

```text
Desired replicas = 3
Running replicas = 3
```

### Meaning:

> **Everything is healthy/working properly.**

---

## 13.2 Progressing 🟡

Application abhi deploy/update ho rahi hai.

Example:

```text
Desired = 3
Running = 1
```

Kubernetes abhi remaining pods create kar raha hai.

### Meaning:

> **Application is still becoming ready.**

---

## 13.3 Degraded 🔴

Application expected way mein work nahi kar rahi.

Example:

```text
Desired = 3
Running = 0
```

Ya pods repeatedly crash ho rahe hain.

### Meaning:

> **Application has a problem / unhealthy condition.**

---

## 13.4 Suspended ⏸️

Application/resource temporarily paused/suspended hai.

### Meaning:

> **Application temporarily stopped/paused.**

---

## 13.5 Missing ❌

Argo CD expected resource ko Kubernetes mein find nahi kar paa raha.

Example:

```text
Git:
Deployment exists

Kubernetes:
Deployment doesn't exist
```

### Meaning:

> **Expected resource is missing from the cluster.**

---

## 13.6 Unknown ❓

Argo CD health determine nahi kar pa raha.

### Meaning:

> **Argo CD cannot determine the health status.**

---

# 14. PreSync Hook

**PreSync = Sync/deployment se PEHLE koi special task run karna.**

```text
Pre = Before
```

Flow:

```text
Git
 ↓
Argo CD
 ↓
PreSync Hook
 ↓
Special Task
 ↓
Application Deployment
```

### Example: Database Migration

Application deploy karne se pehle:

```text
DB Migration
```

run karni hai.

To:

```text
PreSync
   ↓
DB Migration
   ↓
Application Deployment
```

### Remember:

> **PreSync = deployment se pehle ka kaam.**

---

# 15. PostSync Hook

**PostSync = successful sync/deployment KE BAAD special task run karna.**

```text
Post = After
```

Flow:

```text
Git
 ↓
Argo CD
 ↓
Application Deployment
 ↓
Deployment Successful
 ↓
PostSync Hook
 ↓
Smoke Test / Notification / Other Task
```

### Example

Application deploy hone ke baad:

```text
Smoke Test
```

run karna hai.

To:

```text
Deployment
     ↓
PostSync
     ↓
Smoke Test
```

### Remember:

> **PostSync = successful deployment ke baad ka kaam.**

---

# 🔥 PreSync vs PostSync

| Hook         | Kab run hota hai?             | Example      |
| ------------ | ----------------------------- | ------------ |
| **PreSync**  | Deployment se pehle           | DB Migration |
| **PostSync** | Successful deployment ke baad | Smoke Test   |

### Super easy trick:

> **PRE = PEHLE**
> **POST = BAAD**

---

# 16. Complete Argo CD Architecture

```text
                    Developer
                        │
                        ↓
                       Git
                 (Source of Truth)
                        │
                        ↓
                    Argo CD
                        │
          ┌─────────────┼──────────────┐
          ↓             ↓              ↓
     API Server    Repo Server    Application
                                   Controller
                                        │
                                        ↓
                                   Kubernetes
                                        │
                                        ↓
                                   Application
```

Application Controller continuously checks:

```text
Git Desired State
       ↕
    Compare
       ↕
Kubernetes Actual State
```

If different:

```text
DRIFT
  ↓
OutOfSync
  ↓
Reconciliation
  ↓
Sync
```

---

# 🧠 FINAL MASTER MIND MAP

```text
ARGO CD
│
├── What?
│   └── Kubernetes CD + GitOps tool
│
├── GitOps
│   ├── Deployment approach
│   ├── Git = Source of Truth
│   └── Git → Argo CD → Kubernetes
│
├── Alternative approach
│   └── Jenkins/GitHub Actions → kubectl → Kubernetes
│
├── Core Concept
│   ├── Desired State = Git
│   ├── Actual State = Kubernetes
│   ├── Difference = Drift
│   └── Reconciliation = Make Actual = Desired
│
├── Components
│   ├── API Server
│   │   └── User/UI/CLI communication
│   │
│   ├── Repo Server
│   │   └── Gets config from Git
│   │
│   └── Application Controller
│       └── Compare + Reconcile + Sync
│
├── Health
│   ├── Healthy
│   ├── Progressing
│   ├── Degraded
│   ├── Suspended
│   ├── Missing
│   └── Unknown
│
└── Hooks
    ├── PreSync
    │   └── Before deployment
    │
    └── PostSync
        └── After successful deployment
```

# 🎯 Interview Questions — Direct Answers

### Q1. What is Argo CD?

> **Argo CD is a Kubernetes-focused GitOps Continuous Delivery tool. It uses Git as the source of truth and continuously reconciles the desired state in Git with the actual state in Kubernetes.**

### Q2. What are the main components?

> **The main components include API Server, Repository Server, and Application Controller. API Server handles communication, Repo Server retrieves application configuration from Git, and Application Controller compares and reconciles the desired and actual states.**

### Q3. What are health statuses?

> **Healthy, Progressing, Degraded, Suspended, Missing, and Unknown.**

### Q4. What is PreSync?

> **PreSync is a hook that runs before the application synchronization/deployment. It can be used for tasks such as database migration.**

### Q5. What is PostSync?

> **PostSync is a hook that runs after a successful synchronization. It can be used for tasks such as smoke testing or notifications.**

### Q6. What is GitOps?

> **GitOps is an approach where Git is treated as the source of truth for application or infrastructure configuration, and changes in Git are synchronized to the target environment.**

### Q7. Can Jenkins/GitHub Actions also detect and fix drift?

> **Yes. It is technically possible to build this functionality using Jenkins or GitHub Actions, but Argo CD provides continuous reconciliation and Kubernetes GitOps functionality as a core capability.**

### Q8. What is drift?

> **Drift is the difference between the desired state defined in Git and the actual state running in Kubernetes.**

### Q9. What is reconciliation?

> **Reconciliation is the process of comparing the desired state with the actual state and making the actual state match the desired state.**

## ⭐ One-line memory trick

> **Git = kya hona chahiye → Argo CD = compare/reconcile → Kubernetes = actually kya chal raha hai.**

And:

> **PreSync = Pehle | PostSync = Baad | Drift = Difference | Reconciliation = Difference ko fix karke same banana.**
=================
====================
> ========================

# 🚀 ARGO CD — FINAL MASTER NOTES

### Start → End | Questions + Easy Answers + Mind Map

> **Goal:** Short notes, easy language, but **PDF ke important content ko miss nahi karna**. PDF mein Argo CD ke 12 sections cover hain. 

---

# 1. What is Argo CD?

### Simple

**Argo CD = Kubernetes ke liye Continuous Delivery + GitOps tool.**

* Argo = **Argo Continuous Delivery**
* Declarative GitOps tool
* Kubernetes applications ko deploy/manage karta hai
* Git ko **Source of Truth** maanta hai
* Git changes ko Kubernetes ke saath sync karta hai
* Deployment, rollback aur drift correction mein help karta hai. 

### Flow

```text
Developer
   ↓
Git
(Source of Truth)
   ↓
Argo CD
   ↓
Kubernetes
```

### Interview answer

> **Argo CD is a declarative GitOps Continuous Delivery tool for Kubernetes that uses Git as the source of truth and synchronizes the desired state from Git with the Kubernetes cluster.**

---

# 2. What is GitOps?

**GitOps = deployment/operations karne ka approach.**

Ye **tool nahi hai**.

Main idea:

> **Git = Source of Truth**

```text
Developer
   ↓
Git Commit
   ↓
Argo CD
   ↓
Kubernetes
```

Git mein jo configuration hai = **Desired State**

Kubernetes mein jo actually chal raha hai = **Actual State**

### Example

```text
Git                Kubernetes
3 replicas         2 replicas
Desired            Actual
```

Difference = **Drift**

Argo CD difference ko reconcile/sync karta hai.

PDF bhi GitOps mein Git ko deployments ka source of truth aur changes ko Git commits ke through manage karne ki baat karta hai. 

---

# 3. GitOps ka alternative kya hai?

GitOps ka koi single alternative **tool** nahi hai.

Ek traditional approach:

```text
Code
 ↓
Jenkins / GitHub Actions
 ↓
kubectl
 ↓
Kubernetes
```

Jenkins/GitHub Actions bhi Kubernetes deploy kar sakte hain.

### Difference

```text
Traditional:
Jenkins → Kubernetes

GitOps:
Git → Argo CD → Kubernetes
```

Jenkins/GitHub Actions se drift detection/fixing technically possible hai, **lekin uske liye custom pipeline/scripts banana pad sakta hai.**

Argo CD mein **continuous reconciliation + GitOps** core functionality hai.

---

# 4. What is an Argo CD Application?

**Application = Argo CD ka main object.**

Ye define karta hai:

```text
WHAT   → kya deploy karna hai
WHERE  → kis cluster/namespace mein
HOW    → kis configuration/source se
```

PDF ke according Application Argo CD ka main object hai jo what, where and how define karta hai. 

---

# 5. What is Sync?

**Sync = Git ki desired state ko Kubernetes ki actual state ke saath match karna.**

Argo CD compare karta hai:

```text
Git
Desired State
     ↕
   Compare
     ↕
Kubernetes
Actual State
```

Difference mila:

```text
Difference
    ↓
Sync
```

Sync ho sakta hai:

* **Manual**
* **Automatic** 

---

# 6. What is Drift?

**Drift = Desired State aur Actual State mein difference.**

Example:

```text
Git                 K8s
replicas = 3        replicas = 2
       ↓                ↓
          DIFFERENCE
              ↓
             DRIFT
```

---

# 7. What is Reconciliation?

**Reconciliation = Desired aur Actual state ko compare karke Actual State ko Desired State ke according match karna.**

```text
Git = 3 replicas
K8s = 2 replicas
       ↓
Application Controller
       ↓
Compare
       ↓
Difference
       ↓
Reconcile / Sync
       ↓
K8s = 3 replicas
```

### Important

> **Reconciliation ka main kaam Application Controller karta hai.** 

### Yaad rakho:

**Reconciliation = Compare + Correct + Match**

---

# 8. Health Status kya hai?

Health status batata hai ki application/resource ki **health condition** kya hai.

PDF mein:

```text
Healthy
Degraded
Progressing
Missing
```



### 🟢 Healthy

Application properly working.

### 🔴 Degraded

Application mein problem/unhealthy condition.

### 🟡 Progressing

Application abhi ready/deploy hone ki process mein.

### ❌ Missing

Expected resource Kubernetes mein nahi mil raha.

---

# 9. Sync Status kya hai?

Health Status aur Sync Status **alag cheez hain**.

### Sync Status:

```text
Synced
OutOfSync
Unknown
```



### Synced

Git aur Kubernetes state match.

```text
Git = K8s
```

### OutOfSync

Git aur Kubernetes state different.

```text
Git ≠ K8s
```

### Unknown

Sync status determine nahi ho pa raha.

---

# 10. Health vs Sync — Important

| Health      | Meaning                      |
| ----------- | ---------------------------- |
| Healthy     | Application properly healthy |
| Progressing | Abhi progress/ready ho rahi  |
| Degraded    | Application mein problem     |
| Missing     | Resource missing             |

| Sync      | Meaning               |
| --------- | --------------------- |
| Synced    | Git = K8s             |
| OutOfSync | Git ≠ K8s             |
| Unknown   | Status determine nahi |

### Example

Application:

```text
Health = Healthy
Sync  = OutOfSync
```

Possible hai.

Matlab application currently healthy ho sakti hai, **but Git ke according nahi hai.**

---

# 11. Argo CD Components

Main architecture:

```text
                ARGO CD
                   │
       ┌───────────┼────────────┐
       ↓           ↓            ↓
 API Server   Repository     Application
              Server         Controller
       │           │            │
       ↓           ↓            ↓
   CLI/UI/API     Git        Kubernetes
```

PDF ke architecture section mein API Server, Repository Server, Application Controller aur optional Dex diye gaye hain. 

---

## 11.1 API Server

**User aur Argo CD ke beech communication.**

Handles:

```text
CLI
UI
API
```

### Remember:

> **API Server → CLI/UI/API handling**

---

## 11.2 Repository Server

**Git repository ko clone/read karta hai.**

```text
Git Repository
      ↓
Repository Server
      ↓
Argo CD
```

### Remember:

> **Repo Server → Git se configuration read karta hai.**

---

## 11.3 Application Controller ⭐

**Sabse important reconciliation component.**

Kaam:

```text
Git Desired State
       ↕
    Compare
       ↕
K8s Actual State
       ↓
Reconcile / Sync
```

### Remember:

> **Application Controller = Compare + Reconcile**

---

## 11.4 Dex

**Optional authentication component.**

Supports authentication such as:

```text
SSO
LDAP
```

PDF mein Dex ko optional authentication ke liye diya gaya hai. 

---

# 12. Why use Argo CD?

Main benefits:

```text
Git = Single Source of Truth
        ↓
Automatic Deployment
        ↓
Rollback
        ↓
Drift Correction
        ↓
Visibility
        ↓
Auditability
```

Also:

* CLI
* Web UI
* Helm
* Kustomize
* Plain YAML
* Jsonnet support 

---

# 13. Manual Sync vs Automatic Sync

## Manual Sync

User manually sync karta hai:

```text
Git Change
   ↓
Argo CD
   ↓
User clicks Sync
   ↓
Kubernetes
```

Ya CLI:

```bash
argocd app sync guestbook
```

---

## Automatic Sync

Argo CD automatically changes sync karta hai.

```text
Git Change
   ↓
Argo CD detects
   ↓
Automatic Sync
   ↓
Kubernetes
```

PDF automatic sync ke saath `selfHeal` aur `prune` options dikhata hai. 

---

# 14. What is Self-Heal?

**Self-Heal = manually kiya gaya drift automatically fix karna.**

Example:

Git:

```text
replicas = 3
```

Kubernetes:

```text
replicas = 3
```

Kisi ne manually pod/resource change/delete kar diya.

Argo CD:

```text
Detect difference
       ↓
Self-Heal
       ↓
Restore desired state
```

PDF ke demo mein manually pod delete karne par Argo CD ke self-heal se pod recreate hota hai. 

---

# 15. What is Prune?

**Prune = Git se remove kiye gaye resources ko Kubernetes se bhi delete karna.**

Example:

```text
Git:
deployment.yaml ❌ removed
        ↓
Argo CD
        ↓
Prune
        ↓
Kubernetes resource deleted
```

### Remember:

> **Self-Heal = Drift fix**

> **Prune = Git se removed resource ko K8s se remove**



---

# 16. PreSync Hook

**PreSync = Sync/deployment se PEHLE special task.**

```text
Git
 ↓
PreSync
 ↓
Application Deployment
```

Example:

```text
PreSync
   ↓
DB Migration
   ↓
Application Deploy
```

### Remember:

> **PRE = PEHLE**

---

# 17. PostSync Hook

**PostSync = Successful sync/deployment ke BAAD special task.**

```text
Application Deploy
       ↓
Successful Sync
       ↓
PostSync
```

Example:

```text
Deployment
    ↓
PostSync
    ↓
Smoke Test / Notification
```

### Remember:

> **POST = BAAD**

PDF advanced features mein PreSync/PostSync hooks ko deployment process customize karne ke liye mention karta hai. 

---

# 18. Authentication & RBAC

### Authentication

Argo CD supports SSO through Dex, including:

```text
GitHub
LDAP
Google
SAML
```

### RBAC

Roles and permissions configure karne ke liye:

```text
argocd-rbac-cm
```

use hota hai. 

---

# 19. Advanced Features

### Helm

Helm charts ko application source ke roop mein use kar sakte ho.

### Kustomize

YAML ko:

```text
Patch
Overlay
```

kar sakte ho.

### Multi-Cluster

Ek Argo CD se:

```text
Cluster 1
Cluster 2
Cluster 3
```

manage/deploy kar sakte ho.

### App of Apps

Ek Git repo se multiple Argo CD applications manage karna.

### Hooks

```text
PreSync
PostSync
```

deployment process customize karte hain.



---

# 20. Installation — Short Notes

### Prerequisites

```text
Kubernetes Cluster
+
kubectl configured
```

Examples:

```text
Minikube
Kind
EKS
```



### Namespace

```bash
kubectl create namespace argocd
```

### Install

```bash
kubectl apply -n argocd -f <argocd-install-manifest>
```

### UI

```bash
kubectl port-forward svc/argocd-server -n argocd 8080:443
```

Then:

```text
https://localhost:8080
```



### Admin password

```bash
kubectl get secret argocd-initial-admin-secret -n argocd -o yaml
```



---

# 21. Creating Application

Argo CD Application object mein mainly:

```text
Application
│
├── project
├── source
│   ├── repoURL
│   ├── targetRevision
│   └── path
│
├── destination
│   ├── server
│   └── namespace
│
└── syncPolicy
    └── automated
        ├── selfHeal
        └── prune
```

PDF example mein `guestbook` application Git repo se source lekar Kubernetes cluster ke `default` namespace ko target karta hai. 

---

# 22. Important CLI Commands

| Command                                                     | Meaning            |
| ----------------------------------------------------------- | ------------------ |
| `kubectl get pods -n argocd`                                | Argo CD pods check |
| `kubectl port-forward svc/argocd-server -n argocd 8080:443` | UI access          |
| `argocd login localhost:8080`                               | Login              |
| `argocd app list`                                           | Apps list          |
| `argocd app create`                                         | Create app         |
| `argocd app sync <app-name>`                                | Sync app           |
| `argocd app delete <app-name>`                              | Delete app         |

 

---

# 23. Complete Real Example

Suppose Git mein:

```text
replicas: 3
image: v2
```

### Step 1

Developer Git mein change karta hai.

```text
Git Commit
```

### Step 2

Argo CD Git change detect karta hai.

### Step 3

Application Controller compare karta hai:

```text
Git              K8s
Desired          Actual
3 replicas       2 replicas
```

### Step 4

Difference:

```text
DRIFT
↓
OutOfSync
```

### Step 5

Automatic sync enabled:

```text
Argo CD
   ↓
Reconciliation
   ↓
Kubernetes
```

### Step 6

Kubernetes:

```text
3 replicas
```

### Step 7

Health:

```text
Progressing
   ↓
Healthy
```

### Step 8

Kisi ne pod manually delete kiya:

```text
Self-Heal
   ↓
Pod recreated
```

---

# 🔥 FINAL MIND MAP

```text
                         ARGO CD
                            │
          ┌─────────────────┴─────────────────┐
          │                                   │
       GITOPS                               CD
          │                                   │
   Git = Source of Truth              Kubernetes Deployment
          │
          ↓
        ARGO CD
          │
          ↓
     KUBERNETES
          │
          │
   ┌──────┴───────┐
   │              │
Desired          Actual
(Git)            (K8s)
   │              │
   └── Compare ───┘
          │
      Difference?
          │
        DRIFT
          │
     Reconciliation
          │
 Application Controller
          │
        Sync
          │
       K8s Match
```

```text
ARGO CD
│
├── What?
│   └── Kubernetes CD + GitOps
│
├── GitOps
│   └── Git = Source of Truth
│
├── Application
│   └── What + Where + How
│
├── Sync
│   └── Desired ↔ Actual
│
├── Drift
│   └── Difference
│
├── Reconciliation
│   └── Compare + Correct + Match
│
├── Components
│   ├── API Server → CLI/UI/API
│   ├── Repo Server → Git
│   ├── Application Controller → Reconcile
│   └── Dex → Authentication
│
├── Health
│   ├── Healthy
│   ├── Progressing
│   ├── Degraded
│   └── Missing
│
├── Sync Status
│   ├── Synced
│   ├── OutOfSync
│   └── Unknown
│
├── Sync
│   ├── Manual
│   └── Automatic
│       ├── Self-Heal → Fix Drift
│       └── Prune → Delete removed resources
│
├── Hooks
│   ├── PreSync → Before
│   └── PostSync → After
│
├── Auth/RBAC
│   ├── SSO
│   ├── Dex
│   └── Roles/Permissions
│
├── Advanced
│   ├── Helm
│   ├── Kustomize
│   ├── Multi-Cluster
│   ├── App of Apps
│   └── Hooks
│
└── CLI
    ├── login
    ├── app list
    ├── app create
    ├── app sync
    └── app delete
```

## 🧠 15-second revision

> **Argo CD = Kubernetes CD + GitOps**
> **Git = Source of Truth**
> **Application = What + Where + How**
> **Controller = Compare + Reconcile**
> **Drift = Difference**
> **Reconciliation = Difference ko correct karke match karna**
> **Sync = Git → K8s**
> **Self-Heal = Manual drift fix**
> **Prune = Git se removed resource delete**
> **PreSync = Before**
> **PostSync = After**
> **Healthy = Health OK**
> **OutOfSync = Git/K8s different**
> **Repo Server = Git**
> **API Server = UI/CLI/API**
> **Dex = Authentication**

