# KUBERNETES — INTERVIEW NOTES

**Start-to-End • Simple to Learn • Easy to Remember • Interview Ready**

> This Markdown is based on the uploaded PATHNEX Kubernetes PDF. It preserves the source topics, examples, commands, YAML, flow charts, production flows, and interview-style memory aids without removing the original coverage. fileciteturn5file0L5-L17

---

# 1. Kubernetes Overview

## What is Kubernetes?

**Kubernetes (K8s)** is an open-source container orchestration platform used to automate:

- Deployment
- Scaling
- Management of containerized applications

It manages applications across a cluster of machines and helps provide:

- High availability
- Scalability
- Reliability

Kubernetes handles tasks such as:

- Deploying and managing containers, e.g. Docker
- Scaling applications up or down
- Load balancing traffic
- Managing networking
- Managing storage
- Maintaining desired application state fileciteturn5file0L5-L17

### Interview Answer

> **Kubernetes is an open-source container orchestration platform used to automate the deployment, scaling and management of containerized applications across a cluster of machines. It helps maintain high availability, scalability, reliability and the desired state of applications.**

### Memory Trick

**Kubernetes = D-S-M + N-S**

```text
D = Deploy
S = Scale
M = Manage
N = Networking
S = Storage
```

---

# 2. Kubernetes Architecture

Kubernetes architecture has two main parts:

1. **Control Plane / Master Node**
2. **Worker Nodes**

The Control Plane manages the cluster and makes global decisions. Worker Nodes run the actual application workloads. fileciteturn5file0L23-L30

### Master Memory Trick

```text
CONTROL PLANE
= DECIDES

WORKER NODE
= RUNS
```

---

# 3. Control Plane

The Control Plane is responsible for:

- Overall cluster management
- Global decisions
- Scheduling
- Deciding where Pods run
- Maintaining desired state

## Main Control Plane Components

1. API Server
2. etcd
3. Controller Manager
4. Scheduler
5. Cloud Controller Manager fileciteturn5file0L27-L35

### Memory Trick

> **A-E-C-S-C**

```text
A = API Server
E = etcd
C = Controller Manager
S = Scheduler
C = Cloud Controller Manager
```

---

# 4. API Server — kube-apiserver

The API Server is:

> **The entry point to the Kubernetes cluster.**

It:

- Exposes the Kubernetes API
- Acts as the communication hub
- Communicates with workers
- Communicates with etcd
- Communicates with controllers
- Processes REST requests
- Validates requests
- Updates system state accordingly fileciteturn5file0L31-L35 fileciteturn5file0L41-L42

### Interview Answer

> **The API Server is the entry point and communication hub of Kubernetes. It exposes the Kubernetes API, processes and validates REST requests, and coordinates communication between Kubernetes components.**

### Memory Trick

**API SERVER = ENTRY + COMMUNICATION**

---

# 5. etcd

`etcd` is a distributed key-value store.

It stores cluster state data such as:

- Configuration data
- Resource details
- Cluster metadata
- Pods
- Deployments
- Services
- Other Kubernetes resources

It is important for maintaining the desired state of the cluster. fileciteturn5file0L43-L47

### Interview Answer

> **etcd is the distributed key-value store used by Kubernetes to store cluster state, configuration, resource details and metadata.**

### Memory Trick

**etcd = CLUSTER DATA / STATE**

---

# 6. Controller Manager — kube-controller-manager

The Controller Manager ensures:

> **Current state matches desired state.**

It continuously watches for changes and takes corrective actions.

Controllers mentioned in the source:

- ReplicaSet Controller
- Deployment Controller
- Job Controller
- Node Controller fileciteturn5file0L48-L56

### Interview Answer

> **The Controller Manager runs controllers that continuously compare the current state with the desired state and take corrective actions to reconcile them.**

### Memory Trick

**CONTROLLER = RECONCILE**

---

# 7. Important Controllers

## ReplicaSet Controller

Ensures the desired number of Pod replicas are maintained.

```text
Desired = 3 Pods
Actual  = 2 Pods

Controller
    ↓
Creates another Pod
```

---

## Deployment Controller

Manages Deployments.

---

## Job Controller

Handles batch Jobs.

---

## Node Controller

Handles node lifecycle.

### Master Trick

```text
ReplicaSet → Replicas
Deployment → Deployment
Job → Batch
Node → Node lifecycle
```

---

# 8. Scheduler — kube-scheduler

The Scheduler:

- Watches newly created Pods
- Finds Pods without an assigned node
- Selects an appropriate worker node

It considers:

- CPU
- Memory
- Affinity rules
- Constraints

fileciteturn5file0L57-L61

### Interview Answer

> **The Kubernetes Scheduler watches for unscheduled Pods and selects the appropriate worker node based on resources, affinity rules and scheduling constraints.**

### Memory Trick

**SCHEDULER = WHERE SHOULD POD RUN?**

---

# 9. Cloud Controller Manager

The Cloud Controller Manager manages cloud-specific components.

Examples:

- Load balancers
- Storage volumes

It is used when Kubernetes runs in cloud environments such as:

- AWS
- GCP
- Azure

It separates cloud-provider-specific logic from the Controller Manager. fileciteturn5file0L62-L66

### Interview Answer

> **The Cloud Controller Manager handles cloud-provider-specific functionality such as load balancers and storage when Kubernetes runs in a cloud environment.**

### Memory Trick

**CLOUD CONTROLLER = CLOUD-SPECIFIC LOGIC**

---

# 10. Worker Nodes

Worker Nodes are where:

> **Actual application workloads run.**

The source also calls them **Minions**.

Worker nodes run important components needed to execute applications. fileciteturn5file0L67-L70

### Worker Components

1. Kubelet
2. Kube-proxy
3. Container Runtime
4. Pods

### Memory Trick

**K-K-C-P**

```text
Kubelet
Kube-proxy
Container Runtime
Pods
```

---

# 11. Kubelet

Kubelet is an agent running on each worker node.

It:

- Ensures containers are running in Pods
- Ensures Pods are in desired state
- Communicates with the API Server
- Helps ensure nodes and Pods are correctly configured

fileciteturn5file0L71-L77

### Interview Answer

> **Kubelet is the node-level agent that runs on every worker node. It ensures that the containers defined in Pods are running according to the desired state and communicates with the API Server.**

### Memory Trick

**KUBELET = NODE AGENT**

---

# 12. Kube-proxy

Kube-proxy maintains network rules on nodes.

It allows:

- Pod-to-Pod communication
- Pod-to-Service communication

It can configure:

- iptables
- IPVS

to route traffic between Pods and Services. fileciteturn5file0L78-L88

### Interview Answer

> **Kube-proxy maintains network rules on each node and helps route traffic between Pods and Services.**

### Memory Trick

**KUBE-PROXY = NETWORK RULES**

---

# 13. Container Runtime

The Container Runtime is the software responsible for running containers.

The source mentions:

- Docker daemon / Dockerd — noted as not being used after Kubernetes version 1.23
- containerd
- CRI-O

The runtime:

- Pulls container images
- Creates containers
- Manages container lifecycle

fileciteturn5file0L89-L94

### Interview Answer

> **The container runtime is responsible for pulling images, creating containers and managing their lifecycle on worker nodes.**

### Memory Trick

**RUNTIME = RUN CONTAINER**

---

# 14. Pods

A Pod is:

> **The smallest and simplest Kubernetes object.**

A Pod is a logical host for:

- One container
- Or more than one container

Containers in the same Pod:

- Share networking
- Can share storage
- Are scheduled together on the same worker node

Each Pod gets its own IP address, and containers inside the Pod share storage volumes. fileciteturn5file0L95-L101

### Interview Answer

> **A Pod is the smallest deployable Kubernetes object and provides a logical host for one or more containers. Containers in the same Pod share networking and can share storage, and the Pod is scheduled as one unit.**

### Memory Trick

**POD = CONTAINER HOST**

---

# 15. Control Plane vs Worker Node

| Control Plane | Worker Node |
|---|---|
| Manages cluster | Runs applications |
| Makes decisions | Executes workloads |
| API Server | Kubelet |
| etcd | Kube-proxy |
| Controller Manager | Container Runtime |
| Scheduler | Pods |
| Cloud Controller Manager | Containers |

### One-Line Trick

> **Control Plane decides; Worker Node executes.**

---

# 16. Complete Kubernetes Flow

The source uses:

```bash
kubectl create deployment nginx --image=nginx --replicas=2
```

The flow is:

```text
USER
  |
  | kubectl create deployment nginx
  ↓
API SERVER
  |
  | Authentication
  | Authorization (RBAC)
  | Validation
  | Admission checks
  ↓
etcd
  |
  | Stores desired state
  | "nginx = 2 replicas"
  ↓
Controller Manager
  |
  ↓
Deployment Controller
  |
  ↓
ReplicaSet Controller
  |
  ↓
Creates Pod objects
  |
  ↓
Pods = Pending
Node = NONE
  |
  ↓
Scheduler
  |
  | CPU / Memory
  | Taints / Tolerations
  | Affinity
  | Node constraints
  ↓
Node selected
  |
  +---- Pod 1 → Worker Node 1
  |
  +---- Pod 2 → Worker Node 2
  |
  ↓
Kubelet
  |
  ↓
CRI / Container Runtime
  |
  | Pull image
  | Create container
  | Start container
  ↓
NGINX CONTAINER
  |
  ↓
RUNNING
```

The source's page 4–5 flow chart explicitly shows API authentication/authorization/validation/admission, etcd storing the desired state, controller/ReplicaSet creation, scheduler decisions, kubelet, CRI/containerd or CRI-O, and the NGINX container reaching Running. fileciteturn5file0L102-L137 fileciteturn5file0L138-L201

---

# 17. Kubernetes Feedback Loop

Kubernetes does not stop after creating the application.

It continuously compares:

```text
Desired State
      ↓
Controllers
      ↓
Actual State
```

Then:

```text
Does it match?

YES
 ↓
Continue

NO
 ↓
Take corrective action / reconcile
 ↓
Repeat
```

The source summarizes the core idea as:

> **You declare what you want → Kubernetes continuously works to make the actual state match.** fileciteturn5file0L208-L230

### Most Important Kubernetes Concept

**Desired State → Actual State → Reconcile**

### Interview Answer

> **Kubernetes is declarative. We define the desired state, and Kubernetes continuously reconciles the actual state to match that desired state.**

### Memory Trick

**DECLARE → COMPARE → RECONCILE → REPEAT**

---

# 18. Namespaces

Namespaces divide cluster resources into separate virtual environments within the same Kubernetes cluster.

They help with:

- Organizing resources
- Isolating applications
- Managing access
- Managing quotas
- Supporting multiple teams/projects

fileciteturn5file0L232-L240

### Memory Trick

**NAMESPACE = ORGANIZE + ISOLATE**

---

# 19. Default Kubernetes Namespaces

The source lists:

### 1. `default`

Used when no namespace is specified while creating resources.

### 2. `kube-system`

Contains system components such as:

- DNS
- Scheduler
- Controller Manager
- etc.

### 3. `kube-public`

Accessible to all users and mainly used for public cluster information.

### 4. `kube-node-lease`

Used for:

- Node heartbeat
- Node availability tracking

fileciteturn5file0L241-L252

### Memory Trick

```text
default
→ normal apps

kube-system
→ Kubernetes system

kube-public
→ public information

kube-node-lease
→ node heartbeat
```

---

# 20. Services

A Kubernetes Service:

> **Defines a logical group of Pods and provides a stable way to access them.**

Pods are temporary and their IPs can change.

A Service provides:

- Stable IP address
- DNS name
- Load balancing across Pods

Services use:

- Labels
- Selectors

to identify Pods and route traffic to available Pods, even when Pods restart or scale. fileciteturn5file0L253-L263

### Interview Answer

> **A Kubernetes Service provides stable network access to a logical group of Pods. It provides a stable IP and DNS name and distributes traffic to matching Pods using labels and selectors.**

### Memory Trick

**SERVICE = STABLE ACCESS TO PODS**

---

# 21. Why Do We Need a Service?

Suppose:

```text
Pod 1 → 10.x.x.1
Pod 2 → 10.x.x.2
Pod 3 → 10.x.x.3
```

Pods can be recreated.

Their IPs may change.

Instead of users calling Pods directly:

```text
User
 ↓
Service
 ↓
Pod 1 / Pod 2 / Pod 3
```

The Service provides stable access.

### Interview Line

> **Pods are ephemeral, so their IP addresses can change. A Service provides a stable endpoint and routes traffic to the correct Pods.**

---

# 22. Service Types

The source covers:

1. ClusterIP
2. NodePort
3. LoadBalancer
4. ExternalName
5. Headless Service

---

# 23. ClusterIP

**ClusterIP is the default Service type.**

### Scope

Internal to the cluster.

### Use Case

Microservices communicating with each other.

### EKS Behavior

No external access; the source describes it as reachable by Pods within the cluster. fileciteturn5file0L264-L269

### Memory Trick

**ClusterIP = INTERNAL**

---

# 24. NodePort

NodePort provides limited external access.

It opens a static port on worker nodes.

The source states that in EKS:

```text
30000–32767
```

is the NodePort range.

Access pattern:

```text
<NodeIP>:<NodePort>
```

The source describes NodePort as commonly used for development/testing rather than production. fileciteturn5file0L270-L276

### Memory Trick

**NodePort = NODE IP + PORT**

---

# 25. LoadBalancer

LoadBalancer is external and is described as preferred for production in the source.

It can expose services to the internet using an AWS-managed Elastic Load Balancer.

In EKS, the source mentions:

- Classic Load Balancer
- NLB
- ALB

depending on configuration.

Traffic is routed to backend Pods.

Common use:

- Web applications
- APIs requiring public access

fileciteturn5file0L282-L289

### Memory Trick

**LoadBalancer = PUBLIC ENTRY**

---

# 26. ExternalName

ExternalName maps a Kubernetes Service name to an external DNS name.

### Use Case

Integrating with:

- External database
- Legacy system
- External service

The source notes that it does not create typical Kubernetes endpoints. fileciteturn5file0L290-L296

### Memory Trick

**ExternalName = SERVICE NAME → EXTERNAL DNS**

---

# 27. Headless Service

A Headless Service is a special case of ClusterIP using:

```yaml
clusterIP: None
```

### Use Case

Service discovery, especially with StatefulSets such as:

- Kafka
- Cassandra

In EKS, the source states that DNS returns Pod IPs rather than a single Service IP.

Used for direct Pod-to-Pod communication. fileciteturn5file0L297-L302

### Memory Trick

**HEADLESS = NO SERVICE IP**

---

# 28. Service Types — Master Table

| Type | Main Purpose | Simple Memory |
|---|---|---|
| ClusterIP | Internal access | Internal |
| NodePort | External via node port | Node + Port |
| LoadBalancer | Public external access | Public |
| ExternalName | External DNS mapping | DNS |
| Headless | Direct Pod discovery | No ClusterIP |

---

# 29. Deployment

A Deployment:

> **Manages a group of Pods and controls their lifecycle.**

It ensures the desired number of Pods are running and replaces failed Pods.

Deployment provides:

- Scaling
- Rolling updates
- Rollback

fileciteturn5file0L303-L312

### Interview Answer

> **A Kubernetes Deployment manages the lifecycle of application Pods. It maintains the desired number of replicas and supports scaling, rolling updates and rollback.**

### Memory Trick

**Deployment = SCALE + UPDATE + ROLLBACK**

---

# 30. ReplicaSet

A ReplicaSet ensures:

> **The specified number of Pod replicas are running.**

It works alongside Deployments to manage:

- Scaling
- Application health

fileciteturn5file0L318-L321

### Memory Trick

**ReplicaSet = KEEP N PODS RUNNING**

---

# 31. Deployment vs ReplicaSet

```text
Deployment
   ↓
ReplicaSet
   ↓
Pods
```

### Simple Difference

> **Deployment manages application rollout/lifecycle; ReplicaSet maintains the desired number of Pods.**

---

# 32. StatefulSet

StatefulSet is used for stateful applications that require persistent storage.

Example:

- Databases

It provides:

- Ordered deployment
- Ordered scaling
- Stable unique network identifiers
- Persistent storage use cases

fileciteturn5file0L322-L325

### Memory Trick

**StatefulSet = STATE + IDENTITY + ORDER**

---

# 33. DaemonSet

A DaemonSet ensures a particular Pod runs on:

- All nodes
- Or selected nodes

Common uses:

- Logging agents
- Monitoring agents
- Networking agents

fileciteturn5file0L326-L329

### Memory Trick

**DaemonSet = ONE POD PER NODE**

---

# 34. Job

A Job ensures a specified number of Pods successfully complete/terminate.

Useful for:

- Batch processing

### Memory Trick

**Job = RUN ONCE / FINISH**

---

# 35. CronJob

A CronJob runs Jobs on a schedule.

It is similar to Unix/Linux cron jobs.

fileciteturn5file0L330-L333

### Memory Trick

**CronJob = SCHEDULED JOB**

---

# 36. Ingress

Ingress manages external access to services inside a Kubernetes cluster.

Typically:

- HTTP
- HTTPS

It can provide:

- SSL termination
- Load balancing
- Name-based virtual hosting

fileciteturn5file0L334-L337

### Interview Answer

> **Ingress manages external HTTP/HTTPS access to Kubernetes Services and can provide routing, SSL termination, load balancing and name-based virtual hosting.**

### Memory Trick

**INGRESS = HTTP/HTTPS ENTRY + ROUTING**

---

# 37. Real-Time Production Setup

The source introduces:

> **There are 2 ways to deploy an application.**

The following pages show two production-style flows:

1. Standard NGINX Ingress flow
2. Service Mesh / Istio flow

fileciteturn5file0L343-L345

---

# 38. Standard Production Flow — NGINX Ingress

The source's page 11 flow is:

```text
User
  ↓
pathnex.com
  ↓
DNS
  ↓
External IP
  ↓
Cloud Load Balancer
  ↓
NGINX Ingress Controller
  ↓
Ingress Resource
  ↓
Kubernetes Service
  ↓
Pod
```

### Key Points from the Source

- LoadBalancer = public entry point
- NGINX Ingress = HTTP routing / host/path
- ClusterIP = internal Service communication
- No need to expose NodePort separately in this flow because it is abstracted away

fileciteturn5file0L346-L350

### Interview Answer

> **In a standard production setup, DNS points the domain to the external Load Balancer. The Load Balancer sends traffic to the NGINX Ingress Controller, which uses Ingress rules for routing and forwards traffic to a Kubernetes Service, which finally routes to the application Pods.**

---

# 39. NGINX Ingress Flow — Memory

```text
DNS
 ↓
LoadBalancer
 ↓
NGINX Ingress
 ↓
Ingress Rules
 ↓
ClusterIP Service
 ↓
Pods
```

### Master Trick

> **Public → Route → Service → Pod**

---

# 40. Service Mesh Flow — Istio

The source's Istio flow is:

```text
User
  ↓
pathnex.com
  ↓
DNS
  ↓
Cloud Load Balancer
  ↓
Istio Ingress Gateway
  ↓
VirtualService
  ↓
Kubernetes Service (ClusterIP)
  ↓
Pod
   +
Sidecar Proxy (Envoy)
```

Key points from the source:

- Istio Gateway replaces NGINX Ingress in this flow
- VirtualService manages ingress routing rules
- Each Pod has a sidecar proxy (Envoy)
- More powerful traffic splitting, retries and observability

fileciteturn5file0L351-L355

---

# 41. NGINX vs Istio

The source provides this simple comparison:

| Feature | NGINX Ingress | Istio |
|---|---|---|
| Simplicity | Easy | Complex |
| Routing | Basic | Advanced |
| Traffic control | Limited | Powerful |
| Overhead | Low | Higher |

### Memory Trick

**NGINX = SIMPLE**

**ISTIO = POWERFUL**

---

# 42. Kubernetes Networking

The source covers three major networking concepts:

1. Pod-to-Pod Networking
2. Service Discovery
3. Network Policies

---

# 43. Pod-to-Pod Networking

Pods can communicate with each other over a flat network.

Each Pod gets a unique IP address within the cluster.

fileciteturn5file0L360-L363

### Memory Trick

**POD = UNIQUE IP**

---

# 44. Service Discovery

Kubernetes automatically assigns a DNS name to Services.

Pods can discover Services by name.

fileciteturn5file0L364-L366

### Example Concept

```text
Pod
 ↓
Service DNS
 ↓
Target Pods
```

### Memory Trick

**SERVICE = DNS NAME**

---

# 45. Network Policies

Network Policies control communication between Pods.

The source describes policy based on:

- Labels
- Namespaces

This improves security. fileciteturn5file0L367-L369

### Interview Answer

> **Network Policies control which Pods can communicate with each other based on rules such as labels and namespaces, improving network security.**

---

# 46. EKS Pricing

The source includes an AWS EKS pricing reference:

```text
https://aws.amazon.com/eks/pricing/
```

This is included as part of the source material. fileciteturn5file0L370-L370

---

# 47. Affinity

Affinity is about controlling:

> **Where Pods should be scheduled.**

The source explains it as telling Kubernetes:

> “I want my Pod to run near something or avoid something.”

It controls Pod placement using scheduling rules. fileciteturn5file0L371-L374

### Main Types

1. Node Affinity
2. Pod Affinity
3. Pod Anti-Affinity

---

# 48. Node Affinity

Node Affinity tells Kubernetes:

> **Run this Pod on certain nodes.**

Useful when Pods require:

- Specific hardware
- Specific environment
- Specific zone

Examples from the source:

- Nodes with SSD disks
- `us-east-1` zone
- GPU-enabled nodes

fileciteturn5file0L375-L383

### Memory Trick

**NODE AFFINITY = WHICH NODE?**

---

# 49. Node Affinity YAML

The source gives:

```yaml
affinity:
  nodeAffinity:
    requiredDuringSchedulingIgnoredDuringExecution:
      nodeSelectorTerms:
        - matchExpressions:
            - key: disk
              operator: In
              values:
                - ssd
```

### Meaning

```text
key = disk
operator = In
value = ssd
```

So the Pod requires a node matching:

```text
disk=ssd
```

The source's YAML is shown on page 14. fileciteturn5file0L385-L398

---

# 50. Pod Affinity

Pod Affinity controls placement relative to other Pods.

It tells Kubernetes:

> **Place this Pod close to specific Pods.**

Examples:

- Backend Pods near frontend Pods
- Related services in the same zone

fileciteturn5file0L399-L406

### Memory Trick

**POD AFFINITY = WHICH PODS TO BE NEAR?**

---

# 51. Pod Anti-Affinity

Pod Anti-Affinity tells Kubernetes:

> **Do not place this Pod near specific Pods.**

Examples:

- Do not put two replicas on the same node
- Spread Pods across nodes for high availability

fileciteturn5file0L407-L412

### Memory Trick

**ANTI-AFFINITY = WHICH PODS TO AVOID?**

---

# 52. Pod Anti-Affinity YAML

Source example:

```yaml
affinity:
  podAntiAffinity:
    requiredDuringSchedulingIgnoredDuringExecution:
      - labelSelector:
          matchExpressions:
            - key: app
              operator: In
              values:
                - my-app
        topologyKey: "kubernetes.io/hostname"
```

The source uses `kubernetes.io/hostname` as the topology key to spread Pods across nodes. fileciteturn5file0L413-L423

---

# 53. Required vs Preferred

This is very important for interviews.

## Required

```text
requiredDuringSchedulingIgnoredDuringExecution
```

Means:

> **Hard rule — must follow.**

## Preferred

```text
preferredDuringSchedulingIgnoredDuringExecution
```

Means:

> **Soft rule — try your best.**

fileciteturn5file0L429-L434

### Memory Trick

**Required = MUST**

**Preferred = TRY**

---

# 54. Affinity Mental Model

The source gives a very useful model:

```text
Node Affinity
→ Choose WHICH node

Pod Affinity
→ Choose WHICH pods to be near

Pod Anti-Affinity
→ Choose WHICH pods to avoid
```

fileciteturn5file0L435-L438

---

# 55. Affinity Comparison

| Type | Meaning | Based On |
|---|---|---|
| Node Affinity | Run on specific kinds of nodes | Node labels |
| Pod Affinity | Run near specific Pods | Pod labels |
| Pod Anti-Affinity | Avoid specific Pods | Pod labels |

fileciteturn5file0L440-L444

---

# 56. Real-Life Affinity Example

Suppose you deploy 3 copies of an application.

### Pod Anti-Affinity

You tell Kubernetes:

> **Spread them out so they are not all on the same machine.**

Benefit:

> High availability.

### Node Affinity

You tell Kubernetes:

> **Only use nodes with `type=fast`.**

Benefit:

> Performance.

fileciteturn5file0L445-L452

---

# 57. Taints

A Taint is like putting a sign on a node:

> **“Don't come here unless you can handle this.”**

It prevents most Pods from being scheduled on that node unless they tolerate the taint. fileciteturn5file0L453-L456

### Memory Trick

**TAINT = NODE SAYS NO**

---

# 58. Tolerations

A Toleration is placed on a Pod.

It means:

> **“I am allowed to run on that tainted node.”**

So:

```text
Taint → Node
Toleration → Pod
```

fileciteturn5file0L462-L465

### Memory Trick

**TAINT = BLOCK**

**TOLERATION = ALLOW**

---

# 59. GPU Node Example

Suppose you have expensive GPU hardware and only special Pods should use it.

## Add Taint

```bash
kubectl taint nodes gpu-node key=gpu:NoSchedule
```

This means:

```text
No Pod is allowed here
unless it tolerates key=gpu
```

## Add Pod Toleration

```yaml
tolerations:
  - key: "gpu"
    operator: "Equal"
    value: "true"
    effect: "NoSchedule"
```

This Pod says:

> **I can tolerate the GPU taint.**

The source gives this exact example. fileciteturn5file0L466-L480

---

# 60. Taint Effects

The source lists:

| Effect | Meaning |
|---|---|
| `NoSchedule` | Don't schedule Pods here unless they tolerate it |
| `PreferNoSchedule` | Try to avoid scheduling here, but not strictly |
| `NoExecute` | Remove existing Pods that don't tolerate it and block new ones |

fileciteturn5file0L481-L485

### Memory Trick

```text
NoSchedule
= Don't put new Pod

PreferNoSchedule
= Try not to put

NoExecute
= Remove existing + block new
```

---

# 61. Taint vs Toleration

| Concept | Where? | Purpose |
|---|---|---|
| Taint | Node | Keeps most Pods away |
| Toleration | Pod | Allows Pod onto tainted node |

fileciteturn5file0L486-L489

### Interview Answer

> **A taint is applied to a node to repel Pods unless they tolerate it. A toleration is applied to a Pod to allow it to be scheduled on that tainted node.**

### Master Memory

> **Taint on Node, Toleration on Pod.**

---

# 62. Probes in Kubernetes / EKS

Probes are health checks for application containers.

Think of them as:

```text
Is my app alive?
Is it ready to serve users?
Should I restart it?
```

The source covers three types:

1. Liveness Probe
2. Readiness Probe
3. Startup Probe fileciteturn5file0L495-L502

---

# 63. Liveness Probe

Question:

> **Is the application alive?**

It checks whether the application is still running properly.

If it fails:

> **Kubernetes restarts the container.**

Source analogy:

> A machine is completely stuck → reboot it.

fileciteturn5file0L503-L507

### Memory Trick

**LIVENESS = RESTART**

---

# 64. Readiness Probe

Question:

> **Can the application take traffic?**

It checks whether the application is ready to handle requests.

If it fails:

> **Traffic is stopped, but the container is NOT restarted.**

Source analogy:

> Restaurant is open but not ready to serve → don't send customers.

fileciteturn5file0L508-L512

### Memory Trick

**READINESS = TRAFFIC**

---

# 65. Startup Probe

Question:

> **Has the application started yet?**

Useful for:

- Slow-starting applications

It prevents the liveness probe from killing the application too early. fileciteturn5file0L513-L517

### Memory Trick

**STARTUP = WAIT**

---

# 66. Liveness vs Readiness vs Startup

| Probe | Question | Action |
|---|---|---|
| Liveness | Is it broken/alive? | Restart container |
| Readiness | Can it serve users? | Stop traffic |
| Startup | Has it started? | Wait before checks |

The source gives this exact simplified model on page 18. fileciteturn5file0L548-L552

### Master Trick

```text
STARTUP
→ Wait

READINESS
→ Traffic

LIVENESS
→ Restart
```

---

# 67. Why Probes Matter in EKS

Without probes:

- App may crash silently
- Users may hit broken services
- Kubernetes may not know when to fix things

With probes:

- Broken applications can be automatically restarted
- Traffic is sent only to healthy/ready Pods
- Reliability improves

fileciteturn5file0L523-L531

### Interview Answer

> **Probes allow Kubernetes to understand the health and readiness of application containers. They help restart broken applications, prevent traffic from reaching unready Pods, and improve reliability.**

---

# 68. Probe YAML Example

The source gives:

```yaml
containers:
  - name: my-app
    image: my-app-image

    livenessProbe:
      httpGet:
        path: /health
        port: 8080
      initialDelaySeconds: 10
      periodSeconds: 5

    readinessProbe:
      httpGet:
        path: /ready
        port: 8080
      initialDelaySeconds: 5
      periodSeconds: 5
```

fileciteturn5file0L532-L547

### Understand It

## Liveness

```text
/health
port 8080
wait 10 sec
check every 5 sec
```

## Readiness

```text
/ready
port 8080
wait 5 sec
check every 5 sec
```

---

# 69. Food Delivery App Analogy

The source gives this analogy:

```text
Startup Probe
→ App is launching

Readiness Probe
→ App is ready to take orders

Liveness Probe
→ App froze → restart it
```

fileciteturn5file0L553-L557

### Easy Memory

> **Startup = Launching**

> **Readiness = Taking Orders**

> **Liveness = Frozen → Restart**

---

# 70. Kubernetes Master Revision

```text
KUBERNETES
= Container orchestration

CONTROL PLANE
= DECIDES

WORKER NODE
= RUNS

API SERVER
= ENTRY POINT

etcd
= STATE

CONTROLLER
= RECONCILE

SCHEDULER
= CHOOSE NODE

KUBELET
= NODE AGENT

KUBE-PROXY
= NETWORK RULES

CONTAINER RUNTIME
= RUN CONTAINER

POD
= SMALLEST K8S OBJECT

SERVICE
= STABLE POD ACCESS

DEPLOYMENT
= SCALE + UPDATE + ROLLBACK

REPLICASET
= KEEP N PODS

STATEFULSET
= STATE + IDENTITY + ORDER

DAEMONSET
= POD ON NODES

JOB
= BATCH

CRONJOB
= SCHEDULED JOB

INGRESS
= HTTP/HTTPS ROUTING

CLUSTERIP
= INTERNAL

NODEPORT
= NODE IP + PORT

LOADBALANCER
= PUBLIC

EXTERNALNAME
= EXTERNAL DNS

HEADLESS
= POD IP DISCOVERY

NODE AFFINITY
= WHICH NODE?

POD AFFINITY
= NEAR WHICH POD?

POD ANTI-AFFINITY
= AVOID WHICH POD?

TAINT
= NODE SAYS NO

TOLERATION
= POD SAYS OK

LIVENESS
= RESTART

READINESS
= TRAFFIC

STARTUP
= WAIT
```

---

# 71. Most Important Interview Questions

## Q1. What is Kubernetes?

> **Kubernetes is an open-source container orchestration platform used to automate deployment, scaling and management of containerized applications across clusters.**

---

## Q2. What are the two main parts of Kubernetes architecture?

> **Control Plane and Worker Nodes. The Control Plane manages the cluster and makes decisions, while Worker Nodes run the application workloads.**

---

## Q3. What does the API Server do?

> **It is the entry point and communication hub of Kubernetes. It exposes the Kubernetes API, validates requests and coordinates communication between cluster components.**

---

## Q4. What is etcd?

> **etcd is a distributed key-value store that stores Kubernetes cluster state, configuration, resource details and metadata.**

---

## Q5. What does the Controller Manager do?

> **It continuously watches the cluster and reconciles the current state with the desired state.**

---

## Q6. What does the Scheduler do?

> **It selects an appropriate worker node for newly created Pods that don't yet have a node assigned, considering resources, affinity and constraints.**

---

## Q7. What is Kubelet?

> **Kubelet is the agent running on each worker node that ensures Pods and their containers are running according to the desired state.**

---

## Q8. What is Kube-proxy?

> **Kube-proxy maintains node network rules and helps route traffic between Pods and Services.**

---

## Q9. What is a Pod?

> **A Pod is the smallest Kubernetes object and a logical host for one or more containers. Containers in a Pod share networking and can share storage.**

---

## Q10. What is a Service?

> **A Service provides stable network access to a logical group of Pods, including a stable IP, DNS name and load balancing.**

---

## Q11. ClusterIP vs NodePort vs LoadBalancer?

> **ClusterIP provides internal access, NodePort exposes a service through a node port, and LoadBalancer provides external access through a cloud load balancer.**

---

## Q12. What is a Deployment?

> **A Deployment manages application Pods and provides scaling, rolling updates and rollback.**

---

## Q13. Deployment vs ReplicaSet?

> **Deployment manages the application rollout and lifecycle, while ReplicaSet ensures the desired number of Pods are running.**

---

## Q14. StatefulSet vs Deployment?

> **StatefulSet is intended for stateful applications requiring stable identity, ordering and persistent storage, while Deployment is generally used for stateless application workloads.**

---

## Q15. What is a DaemonSet?

> **A DaemonSet ensures a particular Pod runs on all or selected nodes, commonly for logging, monitoring or networking agents.**

---

## Q16. Job vs CronJob?

> **A Job runs a batch workload to completion, while a CronJob runs Jobs on a schedule.**

---

## Q17. What is Ingress?

> **Ingress manages external HTTP/HTTPS access to Kubernetes Services and can provide routing, SSL termination, load balancing and name-based virtual hosting.**

---

## Q18. What is Node Affinity?

> **Node Affinity controls which nodes a Pod should run on based on node labels and scheduling rules.**

---

## Q19. What is Pod Affinity?

> **Pod Affinity tells Kubernetes to place a Pod near selected Pods.**

---

## Q20. What is Pod Anti-Affinity?

> **Pod Anti-Affinity tells Kubernetes to avoid placing a Pod near selected Pods, often to improve high availability.**

---

## Q21. What is a Taint?

> **A Taint is placed on a node to prevent most Pods from being scheduled there unless they have a matching toleration.**

---

## Q22. What is a Toleration?

> **A Toleration is placed on a Pod to allow it to run on a node with a matching taint.**

---

## Q23. What are Kubernetes probes?

> **Probes are health checks used to determine whether an application is alive, ready to receive traffic, or still starting.**

---

## Q24. Liveness vs Readiness?

> **Liveness checks whether the container should be restarted. Readiness checks whether the application should receive traffic.**

---

## Q25. What is Startup Probe?

> **Startup Probe protects slow-starting applications by allowing them time to start before liveness checks become effective.**

---

# 72. Scenario: Pod Is Not Running

Think:

```text
Pod Pending?
    ↓
Scheduler
    ↓
Check:
- CPU
- Memory
- Affinity
- Taints/Tolerations
- Node constraints
```

### Interview Approach

> **If a Pod is Pending, I first check scheduling-related conditions such as available CPU/memory, node affinity, taints/tolerations and node constraints.**

---

# 73. Scenario: Pod Keeps Restarting

Think:

```text
Pod restarting
      ↓
Liveness Probe?
      ↓
Application crash?
      ↓
Container runtime?
```

### Interview Approach

> **If a container repeatedly restarts, I would check the application/container state and liveness probe configuration because a failed liveness probe can cause Kubernetes to restart the container.**

---

# 74. Scenario: Users Cannot Access Application

Think:

```text
User
 ↓
DNS
 ↓
LoadBalancer / Ingress
 ↓
Service
 ↓
Pods
```

Check each layer.

### Memory Trick

**D-L-I-S-P**

```text
D = DNS
L = LoadBalancer
I = Ingress
S = Service
P = Pod
```

---

# 75. Scenario: Application Is Running but Users Get No Traffic

Check:

```text
Readiness Probe
      ↓
Service endpoints
      ↓
Pod labels/selectors
      ↓
Ingress routing
```

Important concept:

> A failed readiness probe can stop traffic to the Pod without restarting its container.

---

# 76. Scenario: Need Pods on GPU Nodes

Use:

```text
Node Affinity
+
Taint/Toleration
```

Possible approach:

```text
GPU Node
  ↓
Taint
  ↓
Only GPU Pods with matching toleration
  ↓
Node Affinity selects GPU node
```

### Interview Answer

> **For specialized GPU nodes, I can taint the node so normal workloads are repelled, add a toleration to the GPU workload, and use node affinity to select the appropriate GPU nodes.**

---

# 77. Scenario: Need High Availability for Replicas

Use:

```text
Pod Anti-Affinity
```

Goal:

```text
Replica 1 → Node 1
Replica 2 → Node 2
Replica 3 → Node 3
```

instead of:

```text
Node 1
 ├── Replica 1
 ├── Replica 2
 └── Replica 3
```

### Interview Answer

> **I can use Pod Anti-Affinity to spread replicas across different nodes, reducing the impact of a single-node failure.**

---

# 78. Scenario: Need Application on Specific Hardware

Use:

```text
Node Affinity
```

Example:

```text
disk=ssd
```

or:

```text
GPU-enabled node
```

### Interview Answer

> **I would use Node Affinity based on node labels to schedule the application on the required hardware or environment.**

---

# 79. Scenario: Need Internal Microservice Communication

Use:

```text
ClusterIP
```

Flow:

```text
Service A
   ↓
ClusterIP Service
   ↓
Service B Pods
```

### Interview Answer

> **For internal microservice communication, I would normally use a ClusterIP Service.**

---

# 80. Scenario: Need Public Application Access

Source's standard production flow:

```text
DNS
 ↓
Cloud LoadBalancer
 ↓
NGINX Ingress
 ↓
Ingress Rules
 ↓
ClusterIP Service
 ↓
Pods
```

### Interview Answer

> **For public HTTP/HTTPS access, I can expose the ingress layer through a cloud LoadBalancer, use NGINX Ingress for routing, then route to a ClusterIP Service and finally to application Pods.**

---

# 81. Scenario: Need Advanced Traffic Control

Source's Istio flow:

```text
DNS
 ↓
Cloud LoadBalancer
 ↓
Istio Ingress Gateway
 ↓
VirtualService
 ↓
ClusterIP
 ↓
Pod + Envoy sidecar
```

Use this when the source's described service-mesh capabilities are needed:

- Advanced routing
- Traffic splitting/control
- Retries
- Observability

---

# 82. Kubernetes Architecture — 1 Minute Answer

> **Kubernetes has a Control Plane and Worker Nodes. The API Server is the entry point and communication hub. etcd stores the cluster state. The Controller Manager reconciles the actual state with the desired state. The Scheduler selects nodes for unscheduled Pods. In cloud environments, the Cloud Controller Manager handles cloud-specific resources. Worker Nodes contain Kubelet, Kube-proxy, the container runtime and Pods. Kubelet ensures Pods run, Kube-proxy handles network rules, and the container runtime runs the containers.**

---

# 83. Kubernetes Request Flow — Interview Answer

If interviewer asks:

> **“What happens when you run kubectl create deployment?”**

Say:

> **First, kubectl sends the request to the API Server. The API Server handles authentication, authorization, validation and admission checks. The desired state is stored in etcd. Controllers watch the state and the Deployment/ReplicaSet controllers create the required Pod objects. The Scheduler selects appropriate worker nodes. Kubelet on those nodes watches the assigned Pods and asks the container runtime through CRI to pull the image, create and start the containers. Kubernetes then continuously reconciles actual state with desired state.**

---

# 84. Kubernetes Production Flow — Interview Answer

### NGINX Ingress

> **The user accesses the domain. DNS resolves it to the external IP of the cloud LoadBalancer. The LoadBalancer forwards traffic to the NGINX Ingress Controller. The Ingress resource contains routing rules, which route traffic to a ClusterIP Service, and the Service sends traffic to the application Pods.**

### Istio

> **With Istio, the cloud LoadBalancer sends traffic to the Istio Ingress Gateway. VirtualService rules control routing, traffic goes to a ClusterIP Service and then to Pods that have Envoy sidecar proxies.**

---

# 85. Kubernetes Master Decision Tree

```text
Need to deploy application?
        ↓
Deployment
        ↓
Need N replicas?
        ↓
ReplicaSet

Need stable identity/storage?
        ↓
StatefulSet

Need one Pod per node?
        ↓
DaemonSet

Need batch work?
        ↓
Job

Need scheduled batch work?
        ↓
CronJob

Need stable Pod access?
        ↓
Service

Internal?
        ↓
ClusterIP

Node-based external access?
        ↓
NodePort

Public cloud access?
        ↓
LoadBalancer

External DNS mapping?
        ↓
ExternalName

Direct Pod discovery?
        ↓
Headless Service

HTTP/HTTPS routing?
        ↓
Ingress

Specific node?
        ↓
Node Affinity

Near specific Pods?
        ↓
Pod Affinity

Away from specific Pods?
        ↓
Pod Anti-Affinity

Block Pods from node?
        ↓
Taint

Allow selected Pods?
        ↓
Toleration

Check alive?
        ↓
Liveness

Allow traffic?
        ↓
Readiness

Slow startup?
        ↓
Startup Probe
```

---

# 86. Ultimate Memory Map

```text
                    KUBERNETES
                         |
              +----------+----------+
              |                     |
        CONTROL PLANE          WORKER NODE
              |                     |
       +------+------+------+       |
       |      |      |      |       |
      API    etcd Controller Scheduler
                                  |
                              NODE SELECTION
                                        |
                              +---------+---------+
                              |         |         |
                           Kubelet  Kube-proxy Runtime
                              |
                             Pods
                              |
                      +-------+-------+
                      |               |
                  Containers       Storage
```

---

# 87. Kubernetes Objects Memory

```text
Pod
= Smallest object

Deployment
= Manage Pods

ReplicaSet
= Keep replicas

StatefulSet
= Stateful workloads

DaemonSet
= Node-based Pods

Job
= Batch

CronJob
= Scheduled batch

Service
= Stable access

Ingress
= External HTTP/HTTPS routing

Namespace
= Organization/isolation
```

---

# 88. Scheduling Memory

```text
Node Affinity
= WHICH NODE?

Pod Affinity
= NEAR WHICH POD?

Pod Anti-Affinity
= AVOID WHICH POD?

Taint
= NODE SAYS NO

Toleration
= POD SAYS OK

Required
= MUST

Preferred
= TRY
```

---

# 89. Probe Memory

```text
Startup
= WAIT

Readiness
= TRAFFIC

Liveness
= RESTART
```

---

# 90. Service Memory

```text
ClusterIP
= Internal

NodePort
= Node IP + Port

LoadBalancer
= Public

ExternalName
= External DNS

Headless
= Pod IP discovery
```

---

# 91. Final 30-Second Revision

> **Kubernetes is a container orchestration platform. It has a Control Plane and Worker Nodes. The API Server is the entry point, etcd stores cluster state, Controllers reconcile desired and actual state, Scheduler chooses nodes, Kubelet manages Pods on nodes, Kube-proxy manages network rules and the container runtime runs containers. Pods are the smallest objects. Deployments manage Pods and provide scaling, rolling updates and rollback. Services provide stable access. ClusterIP is internal, NodePort exposes a node port, LoadBalancer provides external access, ExternalName maps to external DNS, and Headless Services provide Pod discovery. Ingress handles HTTP/HTTPS routing. Affinity controls placement, taints repel Pods and tolerations allow selected Pods. Liveness restarts broken containers, readiness controls traffic, and startup protects slow-starting applications.**

---

# 92. Final Master Interview Statement

> **“In Kubernetes, I define the desired state declaratively. The API Server receives and validates the request, etcd stores the cluster state, controllers reconcile the desired and actual state, and the Scheduler assigns Pods to suitable worker nodes. Kubelet ensures the Pods run and the container runtime manages the containers. Services provide stable communication, Deployments manage application lifecycle, Ingress handles external HTTP/HTTPS routing, and scheduling features such as affinity, anti-affinity, taints and tolerations control Pod placement. Probes provide application health and traffic management through liveness, readiness and startup checks.”**

---

# 93. Source Coverage Checklist

This document covers the complete topic sequence from the uploaded PDF:

- Kubernetes Overview
- Container orchestration
- Deployment
- Scaling
- Management
- High availability
- Scalability
- Reliability
- Load balancing
- Networking
- Storage
- Desired state
- Kubernetes architecture
- Control Plane
- Master Node
- Worker Nodes
- API Server
- REST requests
- Validation
- etcd
- Cluster state
- Cluster metadata
- Controller Manager
- ReplicaSet Controller
- Deployment Controller
- Job Controller
- Node Controller
- Scheduler
- CPU
- Memory
- Affinity
- Constraints
- Cloud Controller Manager
- AWS
- GCP
- Azure
- Kubelet
- Kube-proxy
- iptables
- IPVS
- Container Runtime
- Dockerd note
- containerd
- CRI-O
- CRI
- Pods
- Pod networking
- Pod storage
- Complete `kubectl create deployment` flow
- Authentication
- RBAC
- Admission checks
- Feedback loop
- Desired vs actual state
- Namespaces
- `default`
- `kube-system`
- `kube-public`
- `kube-node-lease`
- Services
- Labels
- Selectors
- ClusterIP
- NodePort
- LoadBalancer
- ExternalName
- Headless Service
- Deployments
- ReplicaSets
- StatefulSets
- DaemonSets
- Jobs
- CronJobs
- Ingress
- Production deployment flow
- NGINX Ingress
- DNS
- Cloud LoadBalancer
- Ingress Resource
- ClusterIP
- Istio
- Istio Ingress Gateway
- VirtualService
- Envoy sidecar
- NGINX vs Istio
- Kubernetes networking
- Pod-to-Pod
- Service Discovery
- Network Policies
- EKS pricing reference
- Node Affinity
- Pod Affinity
- Pod Anti-Affinity
- Required scheduling
- Preferred scheduling
- Node labels
- Pod labels
- `topologyKey`
- Taints
- Tolerations
- GPU node example
- `NoSchedule`
- `PreferNoSchedule`
- `NoExecute`
- Kubernetes probes
- Liveness
- Readiness
- Startup
- Probe YAML
- EKS reliability
- Real-world probe analogy
- Interview questions
- Troubleshooting scenarios
- Decision trees
- Memory tricks
- Final interview answers

---

# END — KUBERNETES INTERVIEW NOTES

