# Kubernetes Troubleshooting Guide

## 1) POD STUCK IN PENDING

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: pending-pod
spec:
  containers:
  - name: nginx
    image: nginx:1.23
  nodeSelector:
    disktype: ssd
```

## 2) IMAGEPULLBACKOFF

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: imagepull-pod
spec:
  containers:
  - name: app
    image: nginx:nonexistent-tag-1234
```

## 3) CRASHLOOPBACKOFF

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: crash-pod
spec:
  containers:
  - name: crash
    image: busybox:1.36
    command: ["/bin/sh","-c"]
    args: ["echo 'start'; sleep 1; exit 1"]
```

## 4) OOMKILLED

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: oom-pod
spec:
  containers:
  - name: mem-eater
    image: python:3.9-slim
    command: ["python","-c"]
    args: ["a = 'x' * (100 * 1024 * 1024); import time; time.sleep(3600)"]
    resources:
      limits:
        memory: "64Mi"
      requests:
        memory: "64Mi"
```

## 5) PVC STUCK IN PENDING

```yaml
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: data-pvc
spec:
  accessModes:
  - ReadWriteOnce
  resources:
    requests:
      storage: 1Gi
  storageClassName: nonexistent-sc
```

## 6) SERVICE NOT ACCESSIBLE

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: web
spec:
  replicas: 1
  selector:
    matchLabels:
      app: web
  template:
    metadata:
      labels:
        app: web
    spec:
      containers:
      - name: web
        image: hashicorp/http-echo:0.2.3
        args:
          - "-text=hello"
          - "-listen=:8080"
        ports:
        - containerPort: 5678
```

```yaml
apiVersion: v1
kind: Service
metadata:
  name: web-svc
spec:
  selector:
    app: web
  ports:
  - protocol: TCP
    port: 80
    targetPort: 5678
  type: ClusterIP
```
==================================
No. **Kubernetes troubleshooting sirf 3 sections — Control Plane, Data Plane, Pods — tak limited nahi hai.**
Image mein jo 3 sections hain woh **good starting point** hain, but interview + real production troubleshooting ke liye kaafi important areas missing hain.

I would structure your **Kubernetes Troubleshooting Master List** like this:

# 🚨 Kubernetes Troubleshooting — Complete Master List

## 1. 🧠 Control Plane Troubleshooting

### API Server

* API Server down
* API Server unreachable
* `connection refused`
* API Server high CPU/memory
* API Server slow response
* Authentication/authorization failures
* API Server certificate problems
* Check API Server logs
* Check API Server socket/ports

### etcd

* etcd unavailable
* etcd unhealthy
* etcd disk full
* etcd high latency
* etcd certificate/SAN problems
* etcd data directory problems
* etcd member failure
* etcd quorum loss
* etcd snapshot/restore problems

### Controller Manager

* Controller Manager down
* Controller Manager not creating/reconciling resources
* Leader election problems
* Controller Manager certificate issues
* High CPU/memory

### Scheduler

* Scheduler down
* Pods stuck in `Pending`
* Scheduler unreachable
* Scheduling failures
* Taints/tolerations problems
* Node affinity problems
* Resource shortage
* Topology constraints

---

# 2. 🖥️ Node / Data Plane Troubleshooting

This is **more than just Node NotReady**.

### Node

* Node `NotReady`
* Node unreachable
* Node `Unknown`
* Node becomes Ready → NotReady repeatedly
* Disk pressure
* Memory pressure
* PID pressure
* Network unavailable
* CPU exhaustion

### Kubelet

* Kubelet stopped
* Kubelet crashloop
* Kubelet certificate problem
* Kubelet cannot contact API Server
* Kubelet logs
* Pod creation failures
* Pod deletion stuck

### Container Runtime

* containerd/CRI-O problems
* Runtime unavailable
* Image pull failures
* Container cannot start
* Container runtime socket issues
* Runtime disk problems

### kube-proxy

* kube-proxy not running
* Service connectivity problems
* iptables/IPVS problems
* ClusterIP not reachable

---

# 3. 📦 Pod / Workload Troubleshooting

Your image has this, but I would expand it heavily.

### Pod States

* `Pending`
* `ContainerCreating`
* `Running`
* `CrashLoopBackOff`
* `ImagePullBackOff`
* `ErrImagePull`
* `Error`
* `Completed`
* `Terminating`
* `Unknown`

### Container Problems

* Application crash
* OOMKilled
* Exit code 1
* Exit code 137
* Exit code 139
* Startup failure
* Readiness failure
* Liveness failure
* Startup probe failure

### Pod Lifecycle

* Pod creation
* Scheduling
* Initialization
* Container startup
* Readiness
* Running
* Termination
* Graceful shutdown

### Restart Problems

* `restartPolicy`
* CrashLoopBackOff
* Repeated container restart
* Backoff
* OOMKilled

---

# 4. 🌐 Networking Troubleshooting

**This is a major missing section from your image.**

### Pod Networking

* Pod → Pod communication fails
* Pod → Service fails
* Pod → Internet fails
* Node → Pod fails
* Cross-node communication fails

### Service

* ClusterIP not working
* Service has no endpoints
* Wrong selector
* Wrong `targetPort`
* Wrong `port`
* Service DNS not resolving

### CNI

* CNI failure
* CNI plugin problems
* Pod gets no IP
* IP address exhaustion
* Network interface problems

### NetworkPolicy

* Traffic blocked
* Incorrect ingress rule
* Incorrect egress rule
* Namespace selector problems

### Ingress

* Ingress not reachable
* Ingress controller down
* Wrong host
* Wrong path
* TLS/certificate issue
* 404/502/503

---

# 5. 💾 Storage Troubleshooting

**Another major missing section.**

### PV / PVC

* PVC stuck in `Pending`
* PV not binding
* PVC cannot mount
* PVC cannot attach
* Wrong StorageClass
* StorageClass missing

### Volume

* Mount failure
* Permission denied
* Read-only filesystem
* Volume attachment failure
* Volume detach stuck
* CSI driver failure

### CSI

* CSI controller problems
* CSI node problems
* CSI driver unavailable
* Volume provisioning failure

---

# 6. 📅 Scheduling Troubleshooting

Although Scheduler belongs to control plane, **scheduling deserves its own troubleshooting section**.

* Pod stuck in `Pending`
* Insufficient CPU
* Insufficient memory
* Taints
* Tolerations
* NodeSelector
* NodeAffinity
* PodAffinity
* PodAntiAffinity
* TopologySpreadConstraints
* Resource requests
* Resource limits
* Node labels
* Unschedulable node

Example:

```text
0/5 nodes are available:
2 Insufficient memory
2 node(s) had taint
1 node(s) didn't match node affinity
```

---

# 7. 🔐 Security / RBAC Troubleshooting

**Missing from your image.**

### Authentication

* Certificate authentication
* ServiceAccount
* Token problems
* User authentication

### Authorization

* RBAC
* Role
* ClusterRole
* RoleBinding
* ClusterRoleBinding

Typical:

```text
Forbidden
User cannot get pods
```

Troubleshoot:

```bash
kubectl auth can-i get pods
```

---

# 8. ⚙️ Configuration Troubleshooting

### ConfigMap

* ConfigMap missing
* Wrong key
* Wrong value
* Application not reading ConfigMap

### Secret

* Secret missing
* Wrong secret
* Wrong key
* Secret mount failure
* Environment variable not injected

### Environment

* Wrong environment variable
* Wrong command
* Wrong args
* Wrong working directory

---

# 9. 🔍 DNS Troubleshooting

Your image has **DNS lookup fails**, but this deserves its own section.

* CoreDNS down
* CoreDNS CrashLoopBackOff
* DNS resolution failure
* Service name not resolving
* External DNS not resolving
* `/etc/resolv.conf`
* DNS policy
* CoreDNS configuration
* NetworkPolicy blocking DNS

Typical:

```bash
nslookup kubernetes.default
```

---

# 10. 🔄 Deployment / ReplicaSet Troubleshooting

Very important for interviews.

### Deployment

* Deployment not creating Pods
* Rollout stuck
* Rollout failure
* Old Pods not terminating
* New Pods not becoming Ready
* Wrong image
* Wrong environment
* Failed rollout

### ReplicaSet

* ReplicaSet not creating expected replicas
* Replica mismatch
* Selector problems

### Rollout

* RollingUpdate problems
* `maxSurge`
* `maxUnavailable`
* Rollback
* Revision history

---

# 11. ❤️ Service Health / Probes

This should be separate because it appears constantly in production.

### Liveness Probe

* Container repeatedly restarted

### Readiness Probe

* Pod running but Service doesn't send traffic

### Startup Probe

* Slow application incorrectly killed

Troubleshoot:

```text
Pod = Running
Container = Running
Ready = 0/1
```

Very common interview scenario.

---

# 12. 📈 Resource / Performance Troubleshooting

**Also missing.**

### CPU

* High CPU
* CPU throttling
* CPU requests/limits

### Memory

* High memory
* OOMKilled
* Memory limits
* Memory leaks

### Disk

* Disk pressure
* Disk full
* Container logs consuming disk
* Image layers consuming disk

### PID

* PID pressure
* Too many processes

Useful:

```bash
kubectl top nodes
kubectl top pods
```

---

# 13. 🔁 Autoscaling Troubleshooting

* HPA not scaling
* HPA metrics unavailable
* CPU metrics missing
* Pods not increasing
* Pods not decreasing
* VPA issues
* Cluster Autoscaler issues
* Nodes not being added
* Nodes not being removed

---

# 14. 🏗️ Stateful Workload Troubleshooting

Important for databases and Kafka-like workloads.

* StatefulSet problems
* Ordered pod creation
* Persistent volume problems
* Stable network identity
* Headless Service problems
* Pod identity problems
* Stateful Pod stuck terminating

---

# 15. 🛡️ DaemonSet Troubleshooting

* DaemonSet not running on every node
* Node selector mismatch
* Taints/tolerations
* DaemonSet Pod pending
* Rolling update problems

---

# 16. 🔗 Ingress / External Access

Separate from internal networking.

```text
Internet
   ↓
LoadBalancer
   ↓
Ingress
   ↓
Service
   ↓
Pod
```

Troubleshoot every layer:

* LoadBalancer
* NodePort
* Ingress
* Ingress Controller
* Service
* Endpoints
* Pod
* Application

---

# 17. 📊 Observability / Logging Troubleshooting

* Pod logs missing
* Container logs
* Previous container logs
* Events
* Application logs
* Kubernetes events
* Metrics unavailable
* Prometheus scraping problems
* Grafana dashboards empty
* OpenTelemetry issues

Important commands:

```bash
kubectl logs
kubectl logs --previous
kubectl describe
kubectl get events
```

---

# 18. 🔄 Cluster Upgrade / Certificate Troubleshooting

Especially important for Kubernetes administration.

* Certificate expired
* Certificate renewal
* kubeadm certificate problems
* API Server certificate
* etcd certificate
* kubelet certificate
* Upgrade failure
* Version mismatch
* Node upgrade problems

---

# 19. 🧹 Namespace / Resource / Object Problems

* Namespace stuck in `Terminating`
* Finalizers
* Resource deletion stuck
* Object not found
* ResourceVersion conflicts
* Admission webhook failures
* Mutating webhook problems
* Validating webhook problems

---

# 20. 🪝 Admission / Webhook Troubleshooting

Often missed by beginners.

* ValidatingWebhookConfiguration
* MutatingWebhookConfiguration
* Webhook unavailable
* TLS problems
* API requests timing out
* Resource creation rejected

---

# 21. 🏢 Cluster-Level Problems

Finally, problems that affect the **whole cluster**:

* API Server unavailable
* etcd quorum lost
* Multiple nodes down
* Network-wide failure
* CNI-wide failure
* DNS-wide failure
* Storage backend failure
* Certificate expiration
* Control-plane resource exhaustion

---

# 🎯 Final Master Structure

So instead of only the **3 sections in your image**, I recommend this structure:

```text
KUBERNETES TROUBLESHOOTING
│
├── 1. Control Plane
│   ├── API Server
│   ├── etcd
│   ├── Controller Manager
│   └── Scheduler
│
├── 2. Nodes / Data Plane
│   ├── Node
│   ├── Kubelet
│   ├── Container Runtime
│   └── kube-proxy
│
├── 3. Pods / Containers
│   ├── Pod Lifecycle
│   ├── Pod States
│   ├── CrashLoopBackOff
│   ├── ImagePullBackOff
│   ├── OOMKilled
│   └── Termination
│
├── 4. Networking
│   ├── Pod-to-Pod
│   ├── Service
│   ├── CNI
│   ├── NetworkPolicy
│   └── Ingress
│
├── 5. DNS
│   └── CoreDNS
│
├── 6. Storage
│   ├── PV
│   ├── PVC
│   ├── StorageClass
│   └── CSI
│
├── 7. Scheduling
│   ├── Resources
│   ├── Taints/Tolerations
│   ├── Affinity
│   └── Topology
│
├── 8. Deployment / ReplicaSet
│
├── 9. Probes
│   ├── Liveness
│   ├── Readiness
│   └── Startup
│
├── 10. ConfigMap / Secret
│
├── 11. RBAC / Security
│
├── 12. Resources / Performance
│   ├── CPU
│   ├── Memory
│   ├── Disk
│   └── PID
│
├── 13. Autoscaling
│   ├── HPA
│   ├── VPA
│   └── Cluster Autoscaler
│
├── 14. StatefulSet
│
├── 15. DaemonSet
│
├── 16. External Access
│   ├── LoadBalancer
│   ├── NodePort
│   └── Ingress
│
├── 17. Logging / Monitoring
│
├── 18. Certificates / Upgrade
│
├── 19. Namespace / Finalizers / Webhooks
│
└── 20. Cluster-Wide Failures
```

### ⭐ For your interview preparation

The **highest-priority troubleshooting areas** I'd master first are:

**Control Plane → Node/Kubelet → Pod → Scheduling → Networking → Service → DNS → Storage → Deployment → Probes → ConfigMap/Secret → RBAC → Resources**

Your image is therefore **not wrong**; it's just a **high-level 3-part grouping**. In fact, many of the sections above can be considered subcategories of those 3, but for interview preparation I would **keep them separate**, because interviewers ask scenario-based questions like:

> "Pod is Running but application is not receiving traffic. How will you troubleshoot?"

That requires **Pod + Probe + Service + Endpoint + Network + DNS**, not just "Data Plane troubleshooting."
