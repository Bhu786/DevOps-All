The problem described is that while **Horizontal Pod Autoscaler (HPA)** can increase the number of application pods during high traffic, those pods end up in a **Pending** state when the existing worker nodes lack the necessary CPU or memory capacity to host them (1:24 - 2:06).

The solution is to implement a **Cluster Autoscaler** (3:01). This component automatically monitors the cluster for pending pods and provisions additional worker nodes to provide the necessary capacity (3:09 - 3:15). 
( cluster autoscaler ==> matlab node ko increase or decrease as per traffic)

**Key steps for implementation include:**
* **Prepare Environment:** Set up an *Amazon EKS* cluster with a managed worker node group (4:10).
* **IAM Configuration:** Enable an *IAM OIDC* provider and configure the necessary permissions to allow the autoscaler to manage EC2 instances (11:57 - 13:16).
* **Deployment:** Use *Helm* to deploy the Cluster Autoscaler, ensuring the `values.yaml` file is correctly configured with your cluster name, region, and scaling policies (14:10 - 22:24).
* **Verification:** Once installed, the autoscaler detects resource shortages, adds nodes automatically, and removes them when they are underutilized, which helps optimize costs (24:43 - 29:55).


The problem described is that while **Horizontal Pod Autoscaler (HPA)** can increase the number of application pods during high traffic, those pods end up in a **Pending** state when the existing worker nodes lack the necessary CPU or memory capacity to host them (1:24 - 2:06).

The solution is to implement a **Cluster Autoscaler** (3:01). This component automatically monitors the cluster for pending pods and provisions additional worker nodes to provide the necessary capacity (3:09 - 3:15). 

**Key steps for implementation include:**
* **Prepare Environment:** Set up an *Amazon EKS* cluster with a managed worker node group (4:10).
* **IAM Configuration:** Enable an *IAM OIDC* provider and configure the necessary permissions to allow the autoscaler to manage EC2 instances (11:57 - 13:16).
* **Deployment:** Use *Helm* to deploy the Cluster Autoscaler, ensuring the `values.yaml` file is correctly configured with your cluster name, region, and scaling policies (14:10 - 22:24).
* **Verification:** Once installed, the autoscaler detects resource shortages, adds nodes automatically, and removes them when they are underutilized, which helps optimize costs (24:43 - 29:55).


"
pod increase liken penbding me chala ja toh solution haio cluster autoscaler" yejhi  simple me

=======================
# Kubernetes — 20 Interview Questions & Answers

### 1. What is Kubernetes and what problem does it solve?

**Answer:** Kubernetes is a **container orchestration platform** that runs containerized applications reliably at scale.

It helps with:

* Deployment
* Scaling
* Failure recovery
* Networking
* Service discovery
* Managing containers

---

### 2. What is "Desired State" and who enforces it?

**Desired State** = What you want the Kubernetes cluster to look like.

Example:
`3 replicas of an application should always be running.`

**Controllers** continuously check the actual state against the desired state and fix differences.

Example:

* Desired = 3 Pods
* Actual = 2 Pods
* Controller creates 1 new Pod

This continuous fixing is called **reconciliation**.

---

### 3. Pods are running, but users are getting errors. What do you check?

Check in this order:

1. **Readiness Probe** → Is the Pod ready to receive traffic?
2. **Service Endpoints** → Are Pods connected to the Service?
3. **Pod Events** → Check `kubectl describe pod`
4. **Application Logs**
5. Check **labels and selectors**

---

### 4. Difference between Readiness and Liveness Probe

**Readiness Probe**

* Checks whether the application is ready to receive traffic.
* If it fails → Pod is removed from Service endpoints.
* Container is **not necessarily restarted**.

**Liveness Probe**

* Checks whether the container is alive/healthy.
* If it fails → Kubernetes restarts the container.

**Easy memory:**

`Readiness = Can I send traffic?`

`Liveness = Is the application alive?`

---

### 5. How does Kubernetes decide which node a Pod runs on?

The **kube-scheduler** selects a suitable node.

It checks things such as:

* CPU/Memory availability
* Taints & Tolerations
* Node Selector
* Node Affinity
* Storage requirements

If no suitable node exists → Pod stays **Pending**.

---

### 6. Why are Resource Requests and Limits important?

**Requests**
→ Minimum resources required by the Pod.
→ Scheduler uses requests to select a node.

**Limits**
→ Maximum resources the container can use.

If limits are exceeded:

* CPU → **Throttling**
* Memory → **OOM Kill**

Without requests/limits, one application can consume too many node resources and affect other applications.

---

### 7. What are Kubernetes QoS Classes?

QoS = **Quality of Service**

There are 3 main classes:

**BestEffort**

* No requests/limits
* Lowest protection
* Evicted first

**Burstable**

* Requests and limits are configured but don't match in the Guaranteed pattern
* Medium protection

**Guaranteed**

* CPU and memory requests = limits
* Highest protection

---

### 8. How does Autoscaling work in Kubernetes?

**HPA = Horizontal Pod Autoscaler**

HPA increases/decreases the **number of Pods** based on metrics.

Example:

`CPU high → increase Pods`

Prerequisites:

* Metrics must be available, commonly through Metrics Server.
* Resource requests should be defined.

Important:

**HPA → adds/removes Pods**

**Cluster Autoscaler → adds/removes Nodes**

---

### 9. How does Kubernetes update an application?

Kubernetes normally uses **Rolling Updates**.

Instead of stopping everything:

`Old Pods → gradually replaced → New Pods`

Two important settings:

**maxSurge**
→ Maximum extra Pods that can be created during update.

**maxUnavailable**
→ Maximum Pods that can be unavailable during update.

Readiness probes help ensure traffic goes only to properly started Pods.

---

### 10. How do you manage configuration without hardcoding it in images?

Use:

**ConfigMap**
→ Non-sensitive configuration.

Examples:

* URLs
* Feature flags
* Application settings

**Secret**
→ Sensitive configuration.

Examples:

* Passwords
* API keys
* Credentials

The image stays **environment-agnostic**, and configuration is injected when the container runs.

---

### 11. What are Namespaces and RBAC?

**Namespace**
→ Organizes Kubernetes resources and provides an organizational/policy boundary.

**RBAC = Role-Based Access Control**
→ Controls **who can do what**.

Common objects:

* Role
* ClusterRole
* RoleBinding
* ClusterRoleBinding

Prefer namespace-scoped **Role** when possible.

Use groups rather than giving permissions individually to every user.

---

### 12. How do you prevent insecure workloads from being deployed?

Use **Admission Controllers / Policy Engines**.

Examples:

* Kyverno
* OPA Gatekeeper

They check deployment requests before resources are created.

They can enforce rules such as:

* Don't allow privileged containers
* Don't allow host-path mounts
* Require mandatory labels

---

### 13. How do you investigate `CrashLoopBackOff`?

`CrashLoopBackOff` means:

**Container starts → crashes/exits → Kubernetes restarts it → crashes again**

Check:

1. `kubectl describe pod`
2. Pod Events
3. Application logs
4. Previous container logs:
   `kubectl logs --previous`

Look for:

* Broken entrypoint
* Missing environment variables
* Application startup failure
* Database connection failure
* Dependency failure

---

### 14. Why use Helm instead of raw YAML?

**Helm** packages Kubernetes manifests into a reusable **Chart**.

Benefits:

* Reusable configuration
* Different environments
* Versioning
* Easier upgrades
* Rollbacks

Example:

`values.yaml → environment-specific values`

If deployment fails:

`helm rollback`

---

### 15. How do PV, PVC and StorageClass work together?

**PVC = PersistentVolumeClaim**
→ Application's request for storage.

**PV = PersistentVolume**
→ Actual storage resource.

**StorageClass**
→ Defines how storage should be dynamically created.

Simple flow:

`Application → PVC → PV → Actual Storage`

With dynamic provisioning:

`PVC → StorageClass → PV automatically created`

---

### 16. How are storage failures different from compute failures?

A Pod may have enough CPU and memory but still fail because storage isn't available.

Possible problems:

* Volume cannot mount
* StorageClass doesn't exist
* Storage provisioner fails
* Storage isn't available in the required zone

Pod may remain in:

`Pending` or `ContainerCreating`

---

### 17. Job vs CronJob

**Job**
→ Runs a task **once until completion**.

Examples:

* Database migration
* Batch processing
* Data backfill

**CronJob**
→ Runs Jobs on a **schedule**.

Example:

`Every day at 1 AM → run Job`

Easy memory:

`Job = Once`

`CronJob = Repeated/Scheduled`

---

### 18. How do you make Jobs/CronJobs reliable?

Important settings:

**backoffLimit**
→ Controls retry attempts after failure.

**activeDeadlineSeconds**
→ Stops a Job that runs for too long.

**concurrencyPolicy**
→ Controls overlapping CronJob runs.

**successfulJobsHistoryLimit**
→ Controls old successful Job history.

Also make application logic **idempotent**.

**Idempotent = Running the same operation multiple times should not corrupt the result/state.**

---

### 19. How do you troubleshoot Pod scheduling failures?

Run:

`kubectl describe pod <pod-name>`

Look at the **Events** section.

It tells you why the scheduler rejected nodes.

Common reasons:

* Insufficient CPU
* Insufficient memory
* Taints
* Affinity rules
* Storage constraints

Example:

`0/1 nodes available: insufficient cpu`

---

### 20. What is Kyverno?

**Kyverno** is a Kubernetes-native **policy engine**.

It works as an **Admission Controller**.

It checks Kubernetes resources against policies during creation/update.

Example policy:

`privileged: true → REJECT`

So:

**Developer → Kubernetes API → Kyverno checks policy → Allow / Reject**

---

# 🔥 Super Short Revision Mind Map

```text
KUBERNETES
│
├── Orchestration
│   ├── Deploy
│   ├── Scale
│   ├── Recover
│   └── Networking
│
├── Desired State
│   └── Controllers → Reconciliation
│
├── Pod Health
│   ├── Readiness → Traffic
│   └── Liveness → Restart
│
├── Scheduling
│   └── Scheduler → Node
│
├── Resources
│   ├── Request → Scheduling
│   └── Limit → Runtime
│
├── QoS
│   ├── BestEffort
│   ├── Burstable
│   └── Guaranteed
│
├── Scaling
│   ├── HPA → Pods
│   └── Cluster Autoscaler → Nodes
│
├── Deployment
│   └── Rolling Update
│       ├── maxSurge
│       └── maxUnavailable
│
├── Configuration
│   ├── ConfigMap → Non-sensitive
│   └── Secret → Sensitive
│
├── Security
│   ├── Namespace
│   ├── RBAC
│   └── Admission Controller
│
├── Troubleshooting
│   ├── CrashLoopBackOff
│   ├── describe pod
│   ├── Events
│   └── Logs
│
├── Helm
│   └── Package + Version + Upgrade + Rollback
│
├── Storage
│   ├── PVC → Request
│   ├── PV → Storage
│   └── StorageClass → Provisioning
│
├── Jobs
│   ├── Job → Once
│   └── CronJob → Schedule
│
└── Kyverno
    └── Policy → Allow / Reject
```

This keeps the **full 20-question content** from your file while removing the unwanted video links/timestamps. 

