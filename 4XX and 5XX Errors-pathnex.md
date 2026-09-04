Absolutely. Based on the uploaded **“HTTP Errors DevOps Engineers Should Troubleshoot”** PDF, the core areas are **5xx server errors, 4xx client errors, troubleshooting tools, NGINX/HAProxy, load balancers, health checks, autoscaling, DNS, API Gateway, rate limiting, APM, logs, containers, and inter-service latency**. 

For an **8-year DevOps/SRE engineer**, interviewers usually go beyond “What is 502?” and ask **how you diagnose it in production, how you isolate the layer, what commands/tools you use, and how you prevent recurrence**.

# 🔥 Complete HTTP 4xx/5xx DevOps Interview Question Bank

## 1. HTTP Status Code Fundamentals

1. What are HTTP status codes?
2. Explain the difference between **1xx, 2xx, 3xx, 4xx, and 5xx**.
3. What is the difference between a **4xx and 5xx** error?
4. Which HTTP errors are primarily client-side?
5. Which HTTP errors are primarily server-side?
6. As a DevOps engineer, which HTTP errors are most important to monitor?
7. What is the difference between an application error and an infrastructure error?
8. Can a 4xx error actually be caused by infrastructure?
9. Can a 5xx error be caused by the client?
10. How would you determine which layer generated an HTTP error?

---

# 🔥 500 Internal Server Error

The PDF describes 500 as an application crash/unhandled exception and recommends checking logs, APM, backend services, and container status. 

### Basic

11. What is HTTP 500?
12. What are common causes of 500 errors?
13. How do you troubleshoot HTTP 500?
14. Where would you check logs for a 500 error?
15. How do you determine whether the issue is application or infrastructure?
16. What is the difference between 500 and 502?
17. What is the difference between 500 and 503?
18. What is the difference between 500 and 504?

### 8-Year Scenario Questions

19. **Production suddenly starts returning 500 errors. What will you check first?**
20. Application Pods are running, but users receive 500. How do you troubleshoot?
21. CPU and memory are normal, but application returns 500. What do you investigate?
22. Only one API endpoint is returning 500. How do you isolate the issue?
23. 500 errors started immediately after deployment. What would you do?
24. How would you correlate HTTP 500 with application logs?
25. How would Datadog/APM help you troubleshoot 500?
26. How do you identify whether a database failure is causing 500?
27. How would you troubleshoot intermittent 500 errors?
28. How would you distinguish application exceptions from infrastructure failures?

---

# 🔥 502 Bad Gateway

The PDF identifies 502 as an upstream problem—for example, an application behind NGINX/API Gateway being down or returning errors—and recommends checking proxy logs, service mesh, and upstream health. 

29. What is HTTP 502?
30. What does “Bad Gateway” mean?
31. What is an upstream server?
32. What can cause a 502 error?
33. How does NGINX generate 502?
34. What is the difference between 502 and 504?
35. How do you troubleshoot 502 in NGINX?
36. How do you troubleshoot 502 behind a load balancer?
37. How do you troubleshoot 502 in Kubernetes?
38. What role does a service mesh play in 502 errors?

### Production Scenarios

39. **NGINX is returning 502 but the application Pod is Running. What do you check?**
40. Application works with `curl localhost:8080`, but NGINX returns 502. Why?
41. NGINX can resolve the backend hostname but cannot connect. What could be wrong?
42. Backend service is listening on port 8080 but NGINX expects 80. How would you identify it?
43. Some Pods return 502 while others work. How do you troubleshoot?
44. 502 started after a Kubernetes deployment. What would you investigate?
45. How would you check whether Kubernetes Service endpoints are correct?
46. How would you troubleshoot 502 caused by Istio?
47. How would you distinguish a DNS issue from a TCP connectivity issue?
48. What NGINX logs would you inspect for 502?

---

# 🔥 503 Service Unavailable

The PDF associates 503 with overloaded servers/maintenance and specifically highlights **scaling, health checks, availability zones, load balancers, CPU/RAM, and resource limits**.  

49. What is HTTP 503?
50. What are common causes of 503?
51. What is the difference between 503 and 502?
52. What happens when all backend servers become unhealthy?
53. How can a load balancer generate 503?
54. How can Kubernetes generate 503?
55. How can an application generate 503?
56. How does autoscaling help prevent 503?
57. How can incorrect health checks cause 503?
58. What is the relationship between CPU/memory limits and 503?

### Senior-Level Scenarios

59. **Production traffic increases suddenly and users receive 503. What is your troubleshooting process?**
60. All Pods are Running but the Load Balancer returns 503. Why?
61. Kubernetes Service exists, but requests return 503. What do you check?
62. HPA is configured but Pods are not scaling. How do you investigate?
63. Pods are constantly restarting and users get 503. How do you troubleshoot?
64. Load balancer health checks are failing. What could cause this?
65. Application health endpoint returns 500. What happens to traffic?
66. One Availability Zone is unhealthy and 503 increases. How do you handle it?
67. How do you prevent 503 during deployment?
68. How would you troubleshoot resource exhaustion causing 503?

---

# 🔥 504 Gateway Timeout

The PDF describes 504 as a timeout between gateway and backend and recommends checking **backend performance, timeout settings, DNS resolution, and inter-service latency**.  

69. What is HTTP 504?
70. What causes a 504?
71. Difference between 502 and 504?
72. What is a gateway timeout?
73. What timeout configurations exist in NGINX?
74. What timeout configurations exist in a Load Balancer?
75. What timeout configurations exist in an API Gateway?
76. How does backend latency cause 504?
77. How can DNS cause a 504?
78. How can network latency cause a 504?

### Production Scenarios

79. **API Gateway returns 504 but backend application is healthy. What do you check?**
80. Application takes 40 seconds but gateway timeout is 30 seconds. What happens?
81. How would you identify which timeout is responsible?
82. Backend responds successfully when accessed directly but returns 504 through LB. Why?
83. Only large requests return 504. What could be the reason?
84. Only one microservice causes 504. How do you troubleshoot it?
85. Database query takes 60 seconds and API Gateway times out after 30 seconds. How would you solve it?
86. How do you differentiate network latency from application latency?
87. How would you troubleshoot intermittent 504 errors?
88. How would you use APM to identify the source of a 504?

---

# 501 Not Implemented

The PDF mentions 501 as less common and potentially caused by an unsupported feature or misconfigured routing. 

89. What is HTTP 501?
90. What causes a 501?
91. Difference between 501 and 404?
92. Difference between 501 and 405?
93. How can incorrect routing produce 501?
94. How would you troubleshoot a 501 in production?

---

# ⚠️ 400 Bad Request

The PDF identifies malformed requests as the common cause and notes that frequent 400s may involve a **proxy, WAF, or misrouted request**. 

95. What is HTTP 400?
96. What causes 400 Bad Request?
97. How can a proxy cause 400?
98. How can WAF configuration cause 400?
99. How can incorrect headers cause 400?
100. How can malformed JSON cause 400?
101. How do you troubleshoot 400 errors?
102. How do you determine whether 400 originated from the application, proxy, or WAF?

### Scenario

103. **API suddenly starts returning 400 after an NGINX configuration change. How do you troubleshoot?**
104. 400 happens only through the Load Balancer but not directly. What do you check?
105. 400 happens only for large requests. What could be wrong?

---

# 🔐 401 Unauthorized

The PDF points to authentication configuration, missing headers, IAM, and firewall rules for 401/403 problems. 

106. What is 401 Unauthorized?
107. What is the difference between 401 and 403?
108. What causes 401?
109. What is an Authorization header?
110. How do you troubleshoot missing authentication headers?
111. How can an API Gateway cause 401?
112. How can IAM configuration cause authentication failures?
113. How would you troubleshoot JWT-related 401 errors?
114. How do you troubleshoot 401 after deployment?

---

# 🚫 403 Forbidden

115. What is 403 Forbidden?
116. Difference between 401 and 403?
117. What can cause 403?
118. How can IAM permissions cause 403?
119. How can firewall rules cause 403?
120. How can WAF rules cause 403?
121. How can NGINX configuration cause 403?
122. How would you troubleshoot 403 in Kubernetes?
123. How would you troubleshoot 403 from CloudFront/API Gateway?
124. How do you identify whether WAF or application generated the 403?

---

# 🔎 404 Not Found

The PDF specifically highlights **broken routing, DNS, and misdeployment** as possible DevOps concerns for 404. 

125. What is 404?
126. What causes 404?
127. Difference between 404 and 403?
128. How can incorrect DNS/routing cause 404?
129. How can a deployment cause 404?
130. How can NGINX routing cause 404?
131. How can Kubernetes Ingress cause 404?
132. How would you troubleshoot 404 after deployment?
133. API endpoint works internally but returns 404 externally. Why?
134. One path works while another path returns 404. What do you check?

---

# ⏱️ 408 Request Timeout

The PDF associates 408 with **application responsiveness, timeout settings, and network latency**.  

135. What is 408?
136. Difference between 408 and 504?
137. What causes client request timeout?
138. How can network latency cause 408?
139. How can application slowness cause 408?
140. How do you troubleshoot 408?
141. Which timeout settings would you inspect?
142. How do you differentiate 408 from 504 in a distributed architecture?

---

# 🚨 429 Too Many Requests

The PDF identifies 429 as rate limiting and recommends checking **DoS/bot traffic, throttling policies, and autoscaling thresholds**.  

143. What is HTTP 429?
144. Why does rate limiting happen?
145. Difference between 429 and 503?
146. What is throttling?
147. Where can rate limiting be implemented?
148. How does API Gateway rate limiting work?
149. How would you troubleshoot unexpected 429 errors?
150. How can a misconfigured throttling policy cause 429?
151. How can bot traffic cause 429?
152. How can a DoS attack result in 429?
153. How does autoscaling relate to 429?
154. What metrics would you monitor for 429?
155. How would you design rate limiting for a production API?

### Senior Scenario

156. **Customers report 429 even though traffic hasn't increased. What would you investigate?**
157. Only one customer receives 429 while others work. Why?
158. Rate limit is 1,000 requests/minute but customer gets 429 at 500 requests. What do you check?
159. How would you distinguish legitimate traffic from bot/DoS traffic?
160. How would you tune throttling without impacting legitimate customers?

---

# 🛠️ Production Troubleshooting Questions

The PDF's action plan maps each error to concrete troubleshooting areas such as **ELK/Loki, Datadog/New Relic, NGINX/HAProxy, Istio, load-balancer health checks, autoscaling, CPU/RAM, DNS, API Gateway, and network latency**. 

161. A customer reports intermittent 5xx errors. Walk me through your complete troubleshooting process.

162. What is your **first command** when investigating a production HTTP error?

163. How do you determine which component generated the error?

164. How do you troubleshoot:

```text
Client
  ↓
DNS
  ↓
Load Balancer
  ↓
NGINX
  ↓
Ingress
  ↓
Kubernetes Service
  ↓
Pod
  ↓
Application
  ↓
Database
```

165. Where would you check logs at each layer?

166. How do you correlate a user's request across multiple microservices?

167. What is a correlation ID?

168. How do distributed traces help troubleshoot HTTP errors?

169. How would Datadog help troubleshoot 5xx?

170. How would ELK help?

171. How would Loki help?

172. What metrics would you check during a 5xx incident?

173. What dashboards would you open first?

174. How do you determine whether the problem is CPU, memory, network, DNS, application, or database?

---

# 🔥 Kubernetes-Specific Scenarios

175. Pod is `Running`, but API returns 502. Why?

176. Pod is `Running`, but Service returns 503. Why?

177. Pod is `Ready`, but users receive 504. What do you check?

178. Service has no endpoints. How do you troubleshoot?

179. Ingress returns 404. What do you check?

180. Ingress returns 502. What do you check?

181. Ingress returns 503. What do you check?

182. Ingress returns 504. What do you check?

183. How do readiness probes affect 503?

184. How do liveness probes contribute to outages?

185. How do resource limits cause application failures?

186. How do CPU throttling and memory limits affect HTTP latency?

187. How do you troubleshoot a Pod that is constantly restarting?

188. How do you verify Service → Pod connectivity?

189. How do you verify DNS inside a Pod?

190. How do you verify that the application is listening on the expected port?

191. How do you check Kubernetes endpoints?

192. How do you troubleshoot intermittent errors when traffic is distributed across multiple Pods?

---

# 🌐 NGINX / HAProxy Questions

193. What is the role of NGINX in a production architecture?

194. What is an upstream in NGINX?

195. How does NGINX communicate with an upstream application?

196. What causes NGINX 502?

197. What causes NGINX 504?

198. What causes NGINX 503?

199. How do you troubleshoot NGINX access logs?

200. How do you troubleshoot NGINX error logs?

201. What timeout configurations are important in NGINX?

202. How does NGINX load balancing work?

203. How would you troubleshoot one unhealthy upstream?

204. What is the difference between NGINX and HAProxy?

---

# ☁️ Load Balancer Questions

205. How does a Load Balancer generate 4xx/5xx responses?

206. What happens if all targets become unhealthy?

207. How do health checks work?

208. What makes a health check fail?

209. How can incorrect health-check configuration cause an outage?

210. What is the difference between health check success and application availability?

211. How do you troubleshoot LB → backend connectivity?

212. How would you troubleshoot intermittent LB 5xx?

213. How do Availability Zones affect 503?

214. How do you design a highly available Load Balancer architecture?

---

# 🌐 DNS Questions

215. How can DNS cause HTTP errors?

216. Can DNS cause 502?

217. Can DNS cause 504?

218. How would you troubleshoot DNS resolution?

219. What is the difference between DNS resolution failure and TCP connection failure?

220. What commands do you use to troubleshoot DNS?

221. How do you troubleshoot DNS from inside a Kubernetes Pod?

222. What happens if DNS points to the wrong Load Balancer?

---

# 🔥 Real Production Incident Questions

These are especially important for an **8-year candidate**.

### Scenario 1

223. **At 10 AM production starts showing 502. No deployment happened. What do you do?**

### Scenario 2

224. **After deployment, 5xx increases from 0.1% to 20%. Walk me through your incident response.**

### Scenario 3

225. **Pods are healthy but Load Balancer reports 503. Explain your debugging.**

### Scenario 4

226. **Application latency increased from 200 ms to 10 seconds and users receive 504. What do you investigate?**

### Scenario 5

227. **Only 10% of requests return 502. What does that tell you?**

### Scenario 6

228. **Only one Availability Zone is generating 503. How would you isolate the issue?**

### Scenario 7

229. **Only one Kubernetes Pod generates 500 while other Pods work. What do you do?**

### Scenario 8

230. **All Pods are healthy, CPU is normal, memory is normal, but 504 is increasing. What next?**

### Scenario 9

231. **Users receive 429 even though infrastructure looks healthy. What do you investigate?**

### Scenario 10

232. **404 errors increase immediately after an Ingress configuration change. How do you troubleshoot?**

---

# 🧠 Architecture-Level Questions

233. Design an architecture that minimizes 5xx errors.

234. How would you design a highly available API platform?

235. How would you prevent cascading failures?

236. What is a circuit breaker?

237. What is retry logic?

238. Why can aggressive retries make an outage worse?

239. What is exponential backoff?

240. How would you handle downstream service failure?

241. How would you design timeout values across microservices?

242. How do you prevent one slow microservice from affecting the entire application?

243. How would you implement graceful degradation?

244. How would you implement zero-downtime deployments?

245. How would you use blue-green deployment to reduce HTTP errors?

246. How would you use canary deployment to detect 5xx before full rollout?

247. What SLI would you use for HTTP availability?

248. What SLO would you define for HTTP 5xx?

249. How would you create alerts for 5xx?

250. Would you alert on absolute 5xx count or percentage? Why?

---

# 🚀 Most Important Questions to Master

If your interview is coming soon, **don't memorize all 250 equally**.

Master these first:

1. **502 vs 503 vs 504**
2. **Complete 5xx troubleshooting flow**
3. **500 troubleshooting**
4. **NGINX 502 troubleshooting**
5. **Load Balancer 503 troubleshooting**
6. **504 timeout troubleshooting**
7. **Kubernetes Service → Pod troubleshooting**
8. **Readiness probe and 503**
9. **DNS troubleshooting**
10. **CPU/memory/resource-limit troubleshooting**
11. **429/rate limiting**
12. **4xx vs 5xx**
13. **How to identify which layer generated the error**
14. **Production incident after deployment**
15. **Intermittent 502/503/504 troubleshooting**
16. **Datadog/APM/log correlation**
17. **Health-check failures**
18. **Autoscaling failures**
19. **Ingress 404/502/503**
20. **End-to-end incident response**

### The answer pattern you should use as an 8-year engineer

For almost every scenario, answer in this structure:

**Detect → Scope → Identify layer → Check metrics → Check logs → Test connectivity → Isolate component → Mitigate → Root cause → Prevent recurrence**

For example:

> “First I confirm the error rate and scope—whether it affects all users, one endpoint, one AZ, or a subset of Pods. Then I identify which layer is generating the response by checking LB/NGINX/Ingress/application logs. I correlate the request using a request ID, check latency, CPU, memory, health checks and upstream connectivity. Once I isolate the failing component, I mitigate using rollback, scaling, traffic shifting or configuration correction. After recovery, I perform RCA and add monitoring/alerting or preventive controls.”

That **incident-oriented answer style** is much stronger for an 8-year DevOps/SRE interview than simply defining HTTP status codes.
