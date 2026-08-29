Bilkul. Main **same 1–10 list** ko 4 columns mein kar deta hoon:

**Metric → High/Abnormal → Kya indicate karta hai → Problem ho to kya karein**

> Thresholds system-dependent hain; ye practical interview-level signals hain.

### 1. API / Application Metrics

| Metric          | High / Abnormal | Indicate                | Short Resolution                  |
| --------------- | --------------- | ----------------------- | --------------------------------- |
| Request rate    | अचानक ↑         | High traffic            | **Scale / rate-limit**            |
| Response time   | ↑               | API slow                | **Find bottleneck → optimize**    |
| P95/P99 latency | ↑               | Some requests very slow | **Trace slow requests**           |
| Error rate      | ↑               | App/dependency issue    | **Check logs + fix root cause**   |
| 5xx             | ↑               | Server/app problem      | **Check logs/code/dependency**    |
| 4xx             | ↑               | Client/request issue    | **Validate request/API contract** |
| Throughput      | ↓               | Processing bottleneck   | **Optimize / scale**              |

---

### 2. JVM Metrics

| Metric             | High / Abnormal   | Indicate              | Short Resolution              |
| ------------------ | ----------------- | --------------------- | ----------------------------- |
| Heap usage         | Continuously ↑    | Memory pressure/leak  | **Heap dump → fix leak**      |
| Old Gen            | Continuously high | Objects retained      | **Find retained objects**     |
| GC frequency       | ↑                 | Memory pressure       | **Tune heap/app allocation**  |
| GC pause           | ↑                 | Application pauses    | **Analyze GC → tune JVM**     |
| Thread count       | ↑ continuously    | Thread leak/overload  | **Check thread dump → fix**   |
| Deadlocked threads | > 0               | Deadlock              | **Thread dump → fix locking** |
| Non-heap           | High              | Metaspace/class issue | **Analyze classes/metaspace** |

---

### 3. Server / Container

| Metric             | High / Abnormal    | Indicate            | Short Resolution                 |
| ------------------ | ------------------ | ------------------- | -------------------------------- |
| CPU                | ~90–100% sustained | CPU bottleneck      | **Optimize / scale**             |
| Memory             | ~90%+              | Memory pressure     | **Find leak / increase limit**   |
| Disk usage         | ~90%+              | Disk full risk      | **Clean / increase disk**        |
| Disk I/O           | High               | I/O bottleneck      | **Optimize I/O / storage**       |
| Network            | Saturated          | Network bottleneck  | **Increase capacity / optimize** |
| File descriptors   | Near limit         | Resource exhaustion | **Close leaks / increase limit** |
| Container restarts | ↑                  | App instability     | **Check logs/events**            |
| OOMKilled          | Yes                | Memory exceeded     | **Fix memory / increase limit**  |
| CPU throttling     | High               | CPU limit too low   | **Tune CPU limit**               |

---

### 4. Database

| Metric         | High / Abnormal | Indicate               | Short Resolution                      |
| -------------- | --------------- | ---------------------- | ------------------------------------- |
| DB CPU         | High            | DB CPU bottleneck      | **Optimize queries / scale DB**       |
| DB connections | Near max        | Connection pressure    | **Find long connections / tune pool** |
| Hikari active  | Near max        | Pool heavily used      | **Find slow DB work / tune**          |
| Hikari pending | ↑               | Waiting for connection | **Fix slow queries / pool carefully** |
| Hikari idle    | 0               | Pool fully occupied    | **Investigate DB bottleneck**         |
| Query latency  | ↑               | Slow query/DB          | **Optimize query / index**            |
| Slow queries   | ↑               | Query problem          | **EXPLAIN + optimize**                |
| Locks          | ↑               | Blocking               | **Find blocking transaction**         |
| Deadlocks      | > 0             | Transaction conflict   | **Fix locking/order**                 |
| DB errors      | ↑               | DB problem             | **Check DB/logs/config**              |

---

### 5. Downstream / Microservices

| Metric               | High / Abnormal | Indicate             | Short Resolution                  |
| -------------------- | --------------- | -------------------- | --------------------------------- |
| Downstream latency   | ↑               | Service slow         | **Trace + optimize dependency**   |
| Timeout              | ↑               | Service/network slow | **Timeout + circuit breaker**     |
| Connection failure   | ↑               | Service unavailable  | **Check network/service health**  |
| 5xx                  | ↑               | Downstream failure   | **Check downstream logs**         |
| Retry count          | ↑               | Dependency unstable  | **Limit retry + backoff**         |
| Circuit breaker OPEN | Yes             | Dependency unhealthy | **Fallback / recover dependency** |

---

### 6. Kafka

| Metric                        | High / Abnormal | Indicate             | Short Resolution                  |
| ----------------------------- | --------------- | -------------------- | --------------------------------- |
| Consumer lag                  | ↑ continuously  | Consumer too slow    | **Optimize / scale consumers**    |
| Producer rate > consumer rate | Yes             | Lag increasing       | **Increase processing capacity**  |
| Processing time               | ↑               | Consumer slow        | **Optimize consumer**             |
| Rebalances                    | ↑               | Consumer instability | **Check consumer/session config** |
| Consumer errors               | ↑               | Processing failure   | **Check logs/code**               |
| Commit latency                | ↑               | Commit/broker issue  | **Check broker/network**          |
| Under-replicated partitions   | > 0             | Replica/broker issue | **Check broker health**           |

---

### 7. Kubernetes

| Metric         | High / Abnormal | Indicate                  | Short Resolution                |
| -------------- | --------------- | ------------------------- | ------------------------------- |
| Pod CPU        | High            | CPU pressure              | **Increase resources / scale**  |
| Pod memory     | High            | Memory pressure           | **Fix leak / increase memory**  |
| Pod restarts   | ↑               | Pod instability           | **Check logs/events**           |
| OOMKilled      | Yes             | Memory limit exceeded     | **Fix memory / increase limit** |
| CPU throttling | High            | CPU limit low             | **Increase/tune CPU limit**     |
| Pending pods   | ↑               | Scheduling/resource issue | **Check node capacity**         |
| Failed pods    | ↑               | App/deployment issue      | **Check events/logs**           |
| Ready replicas | < desired       | Availability problem      | **Fix pods / scale**            |
| Node CPU       | High            | Node pressure             | **Scale/add nodes**             |
| Node memory    | High            | Node pressure             | **Scale/add nodes**             |

---

### 8. Network

| Metric            | High / Abnormal | Indicate                | Short Resolution                 |
| ----------------- | --------------- | ----------------------- | -------------------------------- |
| Latency           | ↑               | Network delay           | **Check network path**           |
| Packet loss       | ↑               | Network problem         | **Check network/infrastructure** |
| Throughput        | Saturated       | Bandwidth bottleneck    | **Increase capacity**            |
| Connection errors | ↑               | Connectivity issue      | **Check DNS/firewall/service**   |
| DNS latency       | ↑               | DNS problem             | **Check DNS**                    |
| DNS failures      | ↑               | Service discovery issue | **Fix DNS/config**               |

---

### 9. Infrastructure

| Metric            | High / Abnormal | Indicate             | Short Resolution             |
| ----------------- | --------------- | -------------------- | ---------------------------- |
| Disk usage        | ~90%+           | Disk full risk       | **Clean/increase disk**      |
| Disk latency      | ↑               | Storage slow         | **Optimize/upgrade storage** |
| IOPS              | Near limit      | Storage bottleneck   | **Increase IOPS/optimize**   |
| Network bandwidth | Near limit      | Network saturation   | **Increase capacity**        |
| LB 5xx            | ↑               | Backend/LB problem   | **Check backend/LB**         |
| LB latency        | ↑               | Backend/network slow | **Trace backend**            |
| Instance health   | Unhealthy       | Infrastructure issue | **Replace/recover instance** |

---

### 10. Security

| Metric              | High / Abnormal | Indicate             | Short Resolution                 |
| ------------------- | --------------- | -------------------- | -------------------------------- |
| Login failures      | Suddenly ↑      | Suspicious activity  | **Rate-limit/block/investigate** |
| 401                 | ↑               | Authentication issue | **Check token/auth**             |
| 403                 | ↑               | Authorization issue  | **Check permissions**            |
| Rate-limit hits     | ↑               | Excessive traffic    | **Rate-limit/block client**      |
| Suspicious requests | ↑               | Possible attack      | **Investigate/WAF rules**        |
| Certificate expiry  | Near expiry     | TLS outage risk      | **Renew certificate**            |

### 🔥 Interview ke liye ultimate shortcut

**Metric ↑ → Problem suspect → Logs/Trace se confirm → Root cause → Fix**

Example:

**Hikari pending ↑**
→ DB connections unavailable
→ logs/query metrics check
→ slow query found
→ **query/index optimize** ✅

**Consumer lag ↑**
→ consumer slow
→ processing time/logs check
→ slow DB call found
→ **optimize DB / scale consumer** ✅

**CPU ↑**
→ CPU bottleneck suspect
→ thread/profile check
→ expensive code found
→ **optimize code / scale** ✅
