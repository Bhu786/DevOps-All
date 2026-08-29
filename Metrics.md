Bilkul. Tum basically pooch rahe ho: **1–10 metrics mein kaunsi value/problem kya indicate karti hai**. Interview/troubleshooting ke liye isko aise yaad karo.

> **Note:** Exact thresholds system-dependent hote hain. Neeche practical **warning/signals** hain, fixed rules nahi.

### 1. API / Application Metrics

| Metric          | Agar high/increase ho | Indicate                       |
| --------------- | --------------------- | ------------------------------ |
| Request rate    | अचानक ↑               | High traffic                   |
| Response time   | ↑                     | API slow / bottleneck          |
| P95/P99 latency | ↑                     | Kuch requests bahut slow       |
| Error rate      | ↑                     | Application/dependency problem |
| 5xx             | ↑                     | Server/application problem     |
| 4xx             | ↑                     | Client/request problem         |
| Throughput      | ↓                     | Processing bottleneck          |

**Example:** Response time 200ms → 5 sec = **problem signal**.

---

### 2. JVM Metrics

| Metric             | High/abnormal     | Indicate                       |
| ------------------ | ----------------- | ------------------------------ |
| Heap usage         | Continuously ↑    | Memory pressure/leak           |
| Old Gen            | Continuously high | Objects not getting released   |
| GC frequency       | ↑                 | Memory pressure                |
| GC pause           | ↑                 | Application pauses/slow        |
| Thread count       | ↑ continuously    | Thread leak/concurrency issue  |
| Deadlocked threads | > 0               | **Deadlock**                   |
| Non-heap           | High              | Class/metaspace issue possible |

**Strong signal:** GC ke baad bhi heap continuously high → **memory leak suspect**.

---

### 3. Server / Container

| Metric             | High/abnormal      | Indicate                          |
| ------------------ | ------------------ | --------------------------------- |
| CPU                | ~90–100% sustained | CPU bottleneck                    |
| Memory             | ~90%+              | Memory pressure                   |
| Disk usage         | ~90%+              | Disk full risk                    |
| Disk I/O           | High               | I/O bottleneck                    |
| Network            | Saturated          | Network bottleneck                |
| File descriptors   | Near limit         | Connection/resource issue         |
| Container restarts | ↑                  | Application/container instability |
| OOMKilled          | Yes                | Memory limit exceeded             |
| CPU throttling     | High               | Container CPU limit problem       |

---

### 4. Database

| Metric         | High/abnormal | Indicate                        |
| -------------- | ------------- | ------------------------------- |
| DB CPU         | High          | DB CPU bottleneck               |
| DB connections | Near max      | Connection pressure             |
| Hikari active  | Near max      | Pool heavily used               |
| Hikari pending | ↑             | Requests waiting for connection |
| Hikari idle    | 0             | Pool fully occupied             |
| Query latency  | ↑             | Slow DB/query                   |
| Slow queries   | ↑             | Query/index problem             |
| Locks          | ↑             | Blocking                        |
| Deadlocks      | > 0           | Transaction conflict            |
| DB errors      | ↑             | DB issue                        |

**Example:**

`Active=20, Max=20, Pending=50`

→ **Connection pool exhausted.**

---

### 5. Downstream / Microservices

| Metric               | High/abnormal | Indicate                    |
| -------------------- | ------------- | --------------------------- |
| Downstream latency   | ↑             | Service slow                |
| Timeout              | ↑             | Service/network slow        |
| Connection failure   | ↑             | Service/network unavailable |
| 5xx                  | ↑             | Downstream service problem  |
| Retry count          | ↑             | Dependency instability      |
| Circuit breaker OPEN | Yes           | Dependency unhealthy        |

**Example:**

`Service A = 100ms`
`Service B = 8 sec`

→ **Service B likely bottleneck.**

---

### 6. Kafka

| Metric                      | High/abnormal   | Indicate                   |
| --------------------------- | --------------- | -------------------------- |
| Consumer lag                | ↑ continuously  | Consumer can't keep up     |
| Producer rate               | > Consumer rate | Lag will increase          |
| Consumer processing time    | ↑               | Consumer slow              |
| Rebalances                  | ↑               | Consumer-group instability |
| Consumer errors             | ↑               | Processing problem         |
| Commit latency              | ↑               | Commit/broker issue        |
| Under-replicated partitions | > 0             | Replica/broker problem     |

**Most important:** **Consumer Lag continuously increasing = problem.**

---

### 7. Kubernetes

| Metric         | High/abnormal | Indicate                       |
| -------------- | ------------- | ------------------------------ |
| Pod CPU        | High          | CPU pressure                   |
| Pod memory     | High          | Memory pressure                |
| Pod restarts   | ↑             | Pod instability                |
| OOMKilled      | Yes           | Memory exceeded                |
| CPU throttling | High          | CPU limit too low              |
| Pending pods   | ↑             | Scheduling/resource problem    |
| Failed pods    | ↑             | Deployment/application problem |
| Ready replicas | < desired     | Availability problem           |
| Node CPU       | High          | Node resource pressure         |
| Node memory    | High          | Node memory pressure           |

---

### 8. Network

| Metric            | High/abnormal    | Indicate                |
| ----------------- | ---------------- | ----------------------- |
| Latency           | ↑                | Network/service delay   |
| Packet loss       | > 0 / increasing | Network problem         |
| Throughput        | Saturated        | Bandwidth bottleneck    |
| Connection errors | ↑                | Connectivity issue      |
| DNS latency       | ↑                | DNS problem             |
| DNS failures      | ↑                | Service discovery issue |

---

### 9. Infrastructure

| Metric            | High/abnormal | Indicate               |
| ----------------- | ------------- | ---------------------- |
| Disk usage        | ~90%+         | Disk full risk         |
| Disk latency      | ↑             | Storage slow           |
| IOPS              | Near limit    | Storage bottleneck     |
| Network bandwidth | Near limit    | Network saturation     |
| Load balancer 5xx | ↑             | Backend/LB problem     |
| LB latency        | ↑             | Backend/network issue  |
| Instance health   | Unhealthy     | Infrastructure problem |

---

### 10. Security

| Metric              | High/abnormal | Indicate                        |
| ------------------- | ------------- | ------------------------------- |
| Login failures      | अचानक ↑       | Brute-force/suspicious activity |
| 401                 | ↑             | Authentication issue            |
| 403                 | ↑             | Authorization/access issue      |
| Rate-limit hits     | ↑             | Excessive traffic/client issue  |
| Suspicious requests | ↑             | Possible attack                 |
| Certificate expiry  | Near expiry   | TLS outage risk                 |

---

## 🔥 Sabse important shortcut

Agar **API slow** hai, dashboard mein pehle ye dekho:

**1. Latency ↑** → API slow
**2. Error ↑** → failures
**3. CPU ↑** → CPU problem
**4. Memory ↑** → memory problem
**5. GC ↑** → JVM/memory problem
**6. Threads ↑** → thread bottleneck
**7. DB Pool Pending ↑** → DB connections problem
**8. DB Query Latency ↑** → DB problem
**9. Downstream Latency ↑** → another service problem
**10. Kafka Lag ↑** → consumer problem

### Ek golden rule:

**Metric abnormal hai → suspect problem → logs/traces se confirm → root cause fix.**

Metrics ko **“proof” nahi**, pehle **“signal”** samjho.
