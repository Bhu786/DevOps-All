Yes. I checked current DevOps interview-oriented references and port cheat sheets. The important point is: **interviewers usually ask default/common ports, not every possible port**. ([AWS Builder Center][1])

For your stack, I would memorize the following **master port sheet**.

# 🔥 MASTER DEVOPS PORT NUMBER SHEET

## 🟢 1. Linux / Networking — MUST KNOW

|      Port | Protocol/Service | Why                     |
| --------: | ---------------- | ----------------------- |
|    **22** | SSH / SFTP / SCP | Linux remote access     |
|    **21** | FTP              | File transfer           |
|    **23** | Telnet           | Remote access, insecure |
|    **25** | SMTP             | Email                   |
|    **53** | DNS              | Name resolution         |
| **67/68** | DHCP             | IP assignment           |
|    **80** | HTTP             | Web                     |
|   **443** | HTTPS            | Secure web              |
|   **123** | NTP              | Time synchronization    |
|   **389** | LDAP             | Directory               |
|   **636** | LDAPS            | Secure LDAP             |
|   **445** | SMB              | File sharing            |
|  **2049** | NFS              | Network filesystem      |
|  **3389** | RDP              | Windows remote desktop  |

These are common networking questions alongside DevOps ports. ([DEV Community][2])

---

# 🐳 2. Docker

|     Port | Service           | Meaning                |
| -------: | ----------------- | ---------------------- |
| **2375** | Docker Engine API | Unencrypted Docker API |
| **2376** | Docker Engine API | TLS-secured Docker API |
| **5000** | Docker Registry   | Private registry       |

### Interview questions

**Q: Docker default port?**
→ `2375` HTTP / `2376` HTTPS for Docker daemon API.

**Q: 2375 vs 2376?**

```text
2375 → Docker API without TLS
2376 → Docker API with TLS
```

⚠️ `2375` should not be exposed publicly because an exposed Docker daemon can effectively provide host-level control. ([AWS Builder Center][1])

---

# ☸️ 3. Kubernetes — VERY IMPORTANT 🔥

This is one of the **highest-priority port groups for interviews**.

|            Port | Component               | Meaning                |
| --------------: | ----------------------- | ---------------------- |
|        **6443** | kube-apiserver          | Kubernetes API         |
|        **2379** | etcd                    | Client communication   |
|        **2380** | etcd                    | Peer communication     |
|       **10250** | kubelet                 | Kubelet API            |
|       **10256** | kube-proxy              | Health check           |
| **30000–32767** | NodePort                | External service range |
|          **53** | CoreDNS                 | DNS                    |
|       **10257** | kube-controller-manager | Secure endpoint        |
|       **10259** | kube-scheduler          | Secure endpoint        |

### Most important:

```text
6443  → API Server
10250 → Kubelet
2379  → etcd client
2380  → etcd peer
30000-32767 → NodePort
53 → DNS
```

The Kubernetes API, kubelet, etcd and NodePort ranges are repeatedly included in DevOps interview references. ([Scribd][3])

### Interview:

**Q: What port does kubectl communicate with?**

```text
kubectl
   ↓
6443
   ↓
kube-apiserver
```

---

# 📦 4. Helm

Helm itself generally **doesn't have its own special default network port**.

```text
Helm
  ↓
Kubernetes API
  ↓
6443
```

So:

> **Q: What is Helm's port?**

**Answer:** Helm CLI itself doesn't have a dedicated default port; when interacting with a Kubernetes cluster, it communicates through the Kubernetes API server.

---

# 🔵 5. Ansible

Ansible itself doesn't have a default network port.

Normally:

```text
Ansible Control Node
        ↓
       SSH
        ↓
     Port 22
        ↓
Managed Linux Server
```

### Important

```text
Linux → 22
Windows → commonly 5985 / 5986
```

For Windows management:

|     Port | Protocol    |
| -------: | ----------- |
| **5985** | WinRM HTTP  |
| **5986** | WinRM HTTPS |

So if interviewer asks:

> **What port does Ansible use?**

Don't blindly say "22".

Say:

> **For Linux/Unix managed nodes, Ansible commonly uses SSH on port 22. For Windows, it commonly uses WinRM on 5985/5986.**

---

# 🟣 6. Git

Git itself has **no single default port**.

Depends on protocol:

|     Port | Git usage      |
| -------: | -------------- |
|   **22** | Git over SSH   |
|  **443** | Git over HTTPS |
| **9418** | Git protocol   |

Most commonly you'll encounter:

```text
git clone git@github.com:...
             ↓
            22
```

or:

```text
https://...
     ↓
    443
```

---

# 🚀 7. CI/CD

Since you mentioned CI/CD rather than one specific product, remember the major CI/CD tools.

### Jenkins

|      Port | Meaning                                                                |
| --------: | ---------------------------------------------------------------------- |
|  **8080** | Jenkins web UI                                                         |
| **50000** | Jenkins inbound agent communication — common traditional/default setup |

```text
Browser
   ↓
8080
   ↓
Jenkins
```

([AWS Builder Center][1])

### GitLab

Common:

```text
80  → HTTP
443 → HTTPS
22  → SSH
```

### SonarQube

```text
9000
```

### Nexus

```text
8081
```

These are useful because interviewers frequently connect CI/CD questions with artifact repositories and code-quality tools. ([DEV Community][2])

---

# ☁️ 8. AWS — IMPORTANT CLARIFICATION

**AWS itself does NOT have one "AWS port".**

Different AWS services expose different ports depending on the protocol/service.

For interviews, the biggest AWS port questions are usually around:

```text
EC2
RDS
ElastiCache
OpenSearch
EKS
Load Balancer
```

## EC2

EC2 is just a compute instance, so the port depends on what's running.

Most common:

```text
22   → SSH
80   → HTTP
443  → HTTPS
3389 → RDP
```

---

## RDS 🔥

| Database          | Default Port |
| ----------------- | -----------: |
| MySQL / MariaDB   |     **3306** |
| PostgreSQL        |     **5432** |
| Oracle            |     **1521** |
| SQL Server        |     **1433** |
| Db2               |    **50000** |
| Aurora MySQL      |     **3306** |
| Aurora PostgreSQL |     **5432** |

AWS documentation confirms these RDS default database ports. ([AWS Documentation][4])

---

## ElastiCache

### Redis

```text
6379
```

### Memcached

```text
11211
```

---

## Amazon OpenSearch

Commonly:

```text
443 → HTTPS
9200 → Elasticsearch/OpenSearch HTTP API in self-managed/common setups
```

For AWS-managed OpenSearch, **443 is the important one** because clients commonly connect over HTTPS.

---

## EKS

EKS is Kubernetes, therefore the important cluster API port is:

```text
6443
```

Worker-node/Kubernetes networking introduces the other Kubernetes ports above.

---

# 🟡 9. Kafka 🔥

|     Port | Component                                                       |
| -------: | --------------------------------------------------------------- |
| **9092** | Kafka broker                                                    |
| **9093** | Commonly used for a TLS/SSL listener depending on configuration |
| **2181** | ZooKeeper — legacy Kafka deployments                            |

### Basic architecture

```text
Producer
   ↓
9092
   ↓
Kafka Broker
   ↓
9092
   ↓
Consumer
```

**Important:** Kafka listener ports are configurable, so don't say "Kafka always runs on 9092." Say **9092 is the common/default broker listener in many setups**.

---

# 🟠 10. ELK Stack 🔥🔥

This is another **must-memorize group**.

| Tool          |     Port | Purpose                          |
| ------------- | -------: | -------------------------------- |
| Elasticsearch | **9200** | HTTP/API                         |
| Elasticsearch | **9300** | Node/transport communication     |
| Logstash      | **5044** | Beats input — common             |
| Logstash      | **5000** | TCP input — common configuration |
| Kibana        | **5601** | Web UI                           |

### Architecture

```text
Application
     ↓
 Logstash
   5044
     ↓
Elasticsearch
  9200 / 9300
     ↓
Kibana
   5601
```

The common ELK ports are consistently listed in DevOps references. ([Scribd][3])

### Memory trick:

```text
ELASTICSEARCH → 9200
LOGSTASH      → 5044
KIBANA        → 5601
```

---

# 📊 11. Prometheus + Grafana 🔥

| Tool          |     Port | Purpose       |
| ------------- | -------: | ------------- |
| Prometheus    | **9090** | UI/API        |
| Alertmanager  | **9093** | Alerts        |
| Node Exporter | **9100** | Linux metrics |
| Grafana       | **3000** | Dashboard     |

### Architecture

```text
Linux Server
    ↓
Node Exporter
    ↓ 9100
Prometheus
    ↓ 9090
Grafana
    ↓ 3000
Browser
```

Very common interview question:

> **Prometheus vs Node Exporter port?**

```text
Prometheus     → 9090
Node Exporter  → 9100
```

([SkillVeris][5])

---

# 🔐 12. SSL / TLS

This is easy:

```text
HTTP  → 80
HTTPS → 443
```

HTTPS essentially means:

```text
HTTP + TLS
```

### Interview questions

**Q: SSL/TLS uses which port?**

Usually:

```text
HTTPS → 443
```

But important concept:

> **TLS itself is not tied to one universal port.** Applications can use TLS on other ports too.

For example:

```text
LDAPS → 636
HTTPS → 443
```

---

# 🟢 13. SRE

SRE itself **doesn't have a port**.

SRE is a practice/discipline, not a network service.

But SRE interviews commonly involve:

```text
Prometheus → 9090
Grafana → 3000
Alertmanager → 9093
Node Exporter → 9100
```

---

# 🔒 14. DevSecOps

DevSecOps itself **doesn't have a port**.

It is a methodology/practice.

But its tools can have ports:

```text
SonarQube → 9000
Jenkins   → 8080
Nexus     → 8081
Git       → 22 / 443
Docker    → 2375 / 2376
K8s       → 6443
```

---

# 🐶 15. Datadog

Datadog is different because the agent commonly sends telemetry **outbound to Datadog over HTTPS**.

Most important:

```text
443 → HTTPS
```

So remember:

```text
Datadog Agent
      ↓
    443
      ↓
Datadog
```

The exact endpoints/ports can vary by Datadog site and product, but **443 is the key interview answer**.

---

# 🧠 NOW THE ONE-PAGE MASTER LIST

This is the one I recommend you actually memorize:

|            Port | Remember as                                        |
| --------------: | -------------------------------------------------- |
|          **21** | FTP                                                |
|          **22** | SSH / SFTP / SCP / Git SSH / Ansible Linux         |
|          **23** | Telnet                                             |
|          **25** | SMTP                                               |
|          **53** | DNS / K8s CoreDNS                                  |
|          **80** | HTTP                                               |
|         **443** | HTTPS / TLS / Git HTTPS / Datadog                  |
|         **123** | NTP                                                |
|         **389** | LDAP                                               |
|         **445** | SMB                                                |
|         **636** | LDAPS                                              |
|        **1433** | SQL Server                                         |
|        **1521** | Oracle                                             |
|        **2049** | NFS                                                |
|        **2181** | ZooKeeper                                          |
|        **2375** | Docker API HTTP                                    |
|        **2376** | Docker API HTTPS/TLS                               |
|        **2379** | etcd client                                        |
|        **2380** | etcd peer                                          |
|        **3000** | Grafana                                            |
|        **3306** | MySQL                                              |
|        **3389** | RDP                                                |
|        **5000** | Docker Registry / Logstash TCP common              |
|        **5432** | PostgreSQL                                         |
|        **5601** | Kibana                                             |
|        **6379** | Redis                                              |
|        **8080** | Jenkins                                            |
|        **8081** | Nexus                                              |
|        **9090** | Prometheus                                         |
|        **9092** | Kafka                                              |
|        **9093** | Alertmanager / Kafka TLS listener depending config |
|        **9100** | Node Exporter                                      |
|        **9200** | Elasticsearch HTTP                                 |
|        **9300** | Elasticsearch node/transport                       |
|       **10250** | Kubelet                                            |
| **30000–32767** | Kubernetes NodePort                                |
|       **50000** | Jenkins agents — traditional/default setup         |
|        **5985** | WinRM HTTP                                         |
|        **5986** | WinRM HTTPS                                        |
|       **11211** | Memcached                                          |
|       **27017** | MongoDB                                            |

---

# 🔥 The "Top 20" — If You Have Very Less Time

Don't try to memorize 50 first.

Memorize these **20**:

```text
22       → SSH
53       → DNS
80       → HTTP
443      → HTTPS
2375     → Docker HTTP
2376     → Docker TLS
3000     → Grafana
3306     → MySQL
5432     → PostgreSQL
5601     → Kibana
6379     → Redis
6443     → K8s API
8080     → Jenkins
9090     → Prometheus
9092     → Kafka
9093     → Alertmanager
9100     → Node Exporter
9200     → Elasticsearch
10250    → Kubelet
30000-32767 → K8s NodePort
```

### 🧠 And make these associations:

```text
22
 ↓
SSH → Linux → Git SSH → Ansible
```

```text
80 / 443
 ↓
HTTP / HTTPS
 ↓
Web → AWS → SSL/TLS → CI/CD → Datadog
```

```text
2375 / 2376
 ↓
Docker
```

```text
6443 / 10250 / 2379 / 2380
 ↓
Kubernetes
```

```text
3000 / 9090 / 9093 / 9100
 ↓
Grafana / Prometheus / Alertmanager / Node Exporter
```

```text
9200 / 5044 / 5601
 ↓
ELK
```

```text
9092
 ↓
Kafka
```

```text
3306 / 5432 / 1433 / 1521
 ↓
AWS RDS / Databases
```

## 🎯 Most likely interview questions

You should be able to answer these **without thinking**:

1. What is SSH port? → **22**
2. HTTP vs HTTPS? → **80 / 443**
3. Docker ports? → **2375 / 2376**
4. Kubernetes API server? → **6443**
5. Kubelet? → **10250**
6. etcd? → **2379 / 2380**
7. Kubernetes NodePort range? → **30000–32767**
8. Jenkins? → **8080**
9. Prometheus? → **9090**
10. Grafana? → **3000**
11. Alertmanager? → **9093**
12. Node Exporter? → **9100**
13. Kafka? → **9092**
14. Elasticsearch? → **9200 / 9300**
15. Logstash Beats? → **5044**
16. Kibana? → **5601**
17. MySQL/RDS? → **3306**
18. PostgreSQL/RDS? → **5432**
19. Redis? → **6379**
20. Ansible Linux? → **SSH 22**
21. Git SSH vs HTTPS? → **22 / 443**
22. SSL/HTTPS? → **443**
23. RDP? → **3389**
24. DNS? → **53**
25. NFS? → **2049**
