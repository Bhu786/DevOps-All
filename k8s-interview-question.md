The video "[Kubernetes Interview Questions 2026 | Kubernetes (K8s) Interview Questions and Answers](https://www.youtube.com/watch?v=WRDf3aKH3X0)" by [MindMajix](https://www.youtube.com/watch?v=WRDf3aKH3X0) breaks down 30 interview questions into three experience levels:

---

### Beginner / Freshers Level (Questions 1–10)

**1. What is Kubernetes and why is it used?** [[01:52](https://www.youtube.com/watch?v=WRDf3aKH3X0&t=112)]

* **Answer:** Kubernetes is an open-source container orchestration platform. It automates deployment, scaling, and management of containerized applications across on-premise, cloud, or hybrid environments.

**2. What are Pods in Kubernetes?** [[02:53](https://www.youtube.com/watch?v=WRDf3aKH3X0&t=173)]

* **Answer:** A Pod is the smallest Deployable unit in Kubernetes. It holds one or more containers that share storage, network IP, and execution specs.

**3. What is a Kubernetes Node?** [[03:37](https://www.youtube.com/watch?v=WRDf3aKH3X0&t=217)]

* **Answer:** A Node is a physical or virtual machine in a cluster that runs containerized workloads. It hosts key components like `kubelet`, container runtime, and `kube-proxy`.

**4. What is a Deployment in Kubernetes?** [[04:22](https://www.youtube.com/watch?v=WRDf3aKH3X0&t=262)]

* **Answer:** A Deployment is a API resource that manages the life cycle and desired state of Pods, ensuring high availability and rolling updates/rollbacks.

**5. How does Kubernetes perform load balancing?** [[05:01](https://www.youtube.com/watch?v=WRDf3aKH3X0&t=301)]

* **Answer:** Kubernetes uses Services to provide internal load balancing. A Service assigns a stable IP to a group of Pods and routes traffic across them based on availability.

**6. Scenario: How do you troubleshoot a Pod that keeps crashing frequently?** [[05:36](https://www.youtube.com/watch?v=WRDf3aKH3X0&t=336)]

* **Answer:**
1. Check Pod logs: `kubectl logs <pod-name>`
2. Describe Pod events: `kubectl describe pod <pod-name>`
3. Check CPU/Memory limits.
4. View container restart history: `kubectl get pod <pod-name> -o wide`



**7. What is a ConfigMap in Kubernetes?** [[07:47](https://www.youtube.com/watch?v=WRDf3aKH3X0&t=467)]

* **Answer:** A ConfigMap is an API object used to store non-confidential configuration data separately from container images to keep applications flexible.

**8. Scenario: How do you debug a Service that is not reaching the correct Pods?** [[08:16](https://www.youtube.com/watch?v=WRDf3aKH3X0&t=496)]

* **Answer:**
1. Check running Pods: `kubectl get pods -o wide`
2. Verify Service configuration: `kubectl get service <service-name>`
3. Check Network Policies for blocked communication.
4. Describe the Service: `kubectl describe service <service-name>`



**9. What is the purpose of Namespaces in Kubernetes?** [[09:31](https://www.youtube.com/watch?v=WRDf3aKH3X0&t=571)]

* **Answer:** Namespaces logically isolate cluster resources for multiple teams or environments (e.g., Development and Production) without conflicts.

**10. How do you scale a Kubernetes Deployment?** [[10:15](https://www.youtube.com/watch?v=WRDf3aKH3X0&t=615)]

* **Answer:** Using the CLI command `kubectl scale deployment <deployment-name> --replicas=<count>` or by updating the `replicas` field in the deployment YAML file.

---

### Intermediate Level (Questions 11–20)

**11. What is a StatefulSet in Kubernetes?** [[11:06](https://www.youtube.com/watch?v=WRDf3aKH3X0&t=666)]

* **Answer:** A StatefulSet manages stateful applications (like MySQL, Kafka, Redis) requiring unique network identities, persistent storage, and ordered deployment/scaling.

**12. How does Kubernetes handle rolling updates and rollbacks?** [[12:12](https://www.youtube.com/watch?v=WRDf3aKH3X0&t=732)]

* **Answer:** Rolling updates replace old Pods with new ones gradually to avoid downtime. If an update fails, rollbacks revert to a stable revision using:
* Rollback: `kubectl rollout undo deployment/<name>`
* View history: `kubectl rollout history deployment/<name>`
* Specific revision rollback: `kubectl rollout undo deployment/<name> --to-revision=<number>`



**13. What is a DaemonSet?** [[14:12](https://www.youtube.com/watch?v=WRDf3aKH3X0&t=852)]

* **Answer:** A DaemonSet ensures that a copy of a specific Pod runs on every (or selected) Node in a cluster, commonly used for background tasks like logging agents (e.g., Fluentd) or monitoring agents.

**14. Scenario: How do you debug a Pod stuck in a Pending state?** [[15:03](https://www.youtube.com/watch?v=WRDf3aKH3X0&t=903)]

* **Answer:** Check Node capacity, verify persistent storage (PVC availability), view Pod events via `kubectl describe`, check scheduler logs, ensure container images can be pulled, and review Network Policies/CNI setup.

**15. How do you secure Kubernetes Secrets?** [[18:01](https://www.youtube.com/watch?v=WRDf3aKH3X0&t=1081)]

* **Answer:** Enable encryption at rest in `etcd`, apply RBAC to restrict access, integrate external vault tools (HashiCorp Vault, AWS Secrets Manager), rotate secrets regularly, and avoid environment variables for secret injection.

**16. Scenario: How do you prevent deployment updates from causing downtime?** [[19:19](https://www.youtube.com/watch?v=WRDf3aKH3X0&t=1159)]

* **Answer:** Use a `RollingUpdate` strategy instead of `Recreate`, configure readiness probes, and define parameters like setting `maxUnavailable` to `1` (or appropriate low values).

**17. What is PersistentVolume (PV) and PersistentVolumeClaim (PVC)?** [[19:58](https://www.youtube.com/watch?v=WRDf3aKH3X0&t=1198)]

* **Answer:** PV provides cluster-level persistent storage, while PVC is a request for storage by a Pod. StorageClasses enable dynamic volume provisioning.

**18. How do you set up autoscaling in Kubernetes?** [[20:43](https://www.youtube.com/watch?v=WRDf3aKH3X0&t=1243)]

* **Answer:** Use Horizontal Pod Autoscaler (HPA) via `kubectl autoscale deployment <name> --cpu-percent=50 --min=2 --max=5` to automatically scale Pods based on metrics.

**19. What is a Network Policy in Kubernetes?** [[21:24](https://www.youtube.com/watch?v=WRDf3aKH3X0&t=1284)]

* **Answer:** A Network Policy defines rules governing how Pods communicate with each other and external endpoints (Ingress/Egress traffic controls).

**20. Scenario: How do you expose a Kubernetes application externally?** [[22:41](https://www.youtube.com/watch?v=WRDf3aKH3X0&t=1361)]

* **Answer:**
* **LoadBalancer:** Uses cloud provider external IPs (Best for Cloud).
* **NodePort:** Opens a static port on each Node IP (Best for small/on-prem setups).
* **Ingress Controller:** Manages HTTP/HTTPS routing under single domains.
* **External DNS / Service Mesh:** Provides advanced routing and discovery for large-scale setups.



---

### Advanced Level (Questions 21–30)

**21. How does Kubernetes handle node failures?** [[25:16](https://www.youtube.com/watch?v=WRDf3aKH3X0&t=1516)]

* **Answer:** The node controller detects missed heartbeats (marks `NotReady` after 5s, evicts after 40s). Kubernetes then reschedules Pods on healthy nodes, detaches/reattaches PVs, and restores replicas.

**22. What are Custom Resource Definitions (CRDs)?** [[26:42](https://www.youtube.com/watch?v=WRDf3aKH3X0&t=1602)]

* **Answer:** CRDs allow users to extend Kubernetes capability by defining custom API objects beyond default built-in resources.

**23. How do you implement GitOps in Kubernetes?** [[27:35](https://www.youtube.com/watch?v=WRDf3aKH3X0&t=1655)]

* **Answer:** Store declarative manifests in Git and use synchronization tools like Argo CD or Flux to automatically sync state changes to the cluster.

**24. How do you troubleshoot a memory leak in a Kubernetes application?** [[28:42](https://www.youtube.com/watch?v=WRDf3aKH3X0&t=1722)]

* **Answer:** Check Pod memory usage (`kubectl top pod --containers`), analyze container logs, describe Pods for OOMKilled errors, set explicit resource limits in manifests, and use profiling/monitoring tools (Prometheus, Grafana, pprof).

**25. What is a Kubernetes Operator?** [[30:30](https://www.youtube.com/watch?v=WRDf3aKH3X0&t=1830)]

* **Answer:** An Operator combines CRDs with custom controllers to automate the operational domain knowledge of complex stateful applications (e.g., backups, failover, upgrades).

**26. How does Kubernetes RBAC work?** [[31:36](https://www.youtube.com/watch?v=WRDf3aKH3X0&t=1896)]

* **Answer:** Role-Based Access Control uses Roles/ClusterRoles to set permissions and RoleBindings/ClusterRoleBindings to attach them to subjects (users, groups, service accounts).

**27. How do you secure Kubernetes clusters?** [[32:31](https://www.youtube.com/watch?v=WRDf3aKH3X0&t=1951)]

* **Answer:** Enable RBAC, configure Network Policies, authenticate/authorize API server access, scan container images, restrict privileged containers, enable audit logs, and routinely patch Kubernetes versions.

**28. Scenario: How do you optimize a slow-performing cluster?** [[36:00](https://www.youtube.com/watch?v=WRDf3aKH3X0&t=2160)]

* **Answer:** Audit node usage/add nodes via Cluster Autoscaler, enable HPA for workload scaling, optimize network latency/internal service routing, and clean up unneeded resources (completed jobs, unused Pods).

**29. How do you handle multi-cluster Kubernetes deployments?** [[38:28](https://www.youtube.com/watch?v=WRDf3aKH3X0&t=2308)]

* **Answer:** Utilize Kubernetes Federation, service meshes (Istio/Linkerd) for cross-cluster traffic, GitOps tools (Argo CD) for deployment synchronization, and HashiCorp Vault for multi-cluster secret management.

**30. What are Kubernetes Admission Controllers?** [[40:12](https://www.youtube.com/watch?v=WRDf3aKH3X0&t=2412)]

* **Answer:** Admission controllers are plugins that intercept API requests before storage in `etcd` to mutate or validate operations against security and compliance policies (e.g., OPA Gatekeeper, Kyverno).
