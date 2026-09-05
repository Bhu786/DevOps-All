# Kubernetes Troubleshooting Interview Question Bank — Exhaustive

Below is a **troubleshooting-only** question bank, built from the supplied Kubernetes PDFs and expanded with additional senior/production-level Kubernetes failure scenarios. The PDFs specifically cover Pending Pods, Service routing, latency, Node NotReady, CrashLoopBackOff, etcd failure, probes, networking, autoscaling, node draining, upgrades, and production incidents.  

---

## A. General Kubernetes Troubleshooting

1. How do you troubleshoot a Kubernetes issue when you do not know the root cause?
2. What is your first step when a Kubernetes application is reported as down?
3. How do you determine whether the problem is with the application or Kubernetes?
4. How do you determine whether the issue is at Pod, Service, Ingress, Node, or Cluster level?
5. What Kubernetes commands do you normally run first during an incident?
6. How do you troubleshoot a production Kubernetes issue without immediately restarting anything?
7. How do you collect evidence before making a change?
8. How do you use Kubernetes events during troubleshooting?
9. How do you identify the timeline of a Kubernetes failure?
10. How do you determine whether a problem started after a deployment?
11. How do you determine whether a problem started after a node change?
12. How do you determine whether a problem started after a configuration change?
13. How do you determine whether a problem started after a Kubernetes upgrade?
14. How do you determine whether a problem is isolated to one namespace?
15. How do you determine whether a problem is isolated to one Pod?
16. How do you determine whether a problem is isolated to one node?
17. How do you determine whether a problem affects the entire cluster?
18. How do you troubleshoot an intermittent Kubernetes issue?
19. How do you troubleshoot an issue that disappears before you can investigate it?
20. How do you troubleshoot an issue that cannot be reproduced?
21. How do you troubleshoot a Kubernetes incident when application logs are unavailable?
22. How do you troubleshoot a Kubernetes incident when metrics are unavailable?
23. How do you troubleshoot a Kubernetes incident when API server access is unavailable?
24. How do you distinguish control-plane problems from data-plane problems?
25. How do you determine whether a Kubernetes component is responsible for an outage?
26. How do you perform root-cause analysis for a Kubernetes incident?
27. How do you identify the blast radius of a Kubernetes failure?
28. How do you determine whether an issue is caused by recent configuration drift?
29. How do you troubleshoot Kubernetes when everything appears healthy but users still report failures?
30. How do you troubleshoot an issue where Kubernetes reports Running but the application is unavailable?

---

# B. Pod Pending Troubleshooting

31. A Pod is stuck in Pending state; how do you troubleshoot it?
32. What are the most common reasons for a Pod to remain Pending?
33. How do you determine whether a Pending Pod has been scheduled?
34. How do you determine whether the scheduler rejected every available node?
35. How do you troubleshoot Pending caused by insufficient CPU?
36. How do you troubleshoot Pending caused by insufficient memory?
37. How do you troubleshoot Pending caused by taints?
38. How do you troubleshoot Pending caused by missing tolerations?
39. How do you troubleshoot Pending caused by node affinity?
40. How do you troubleshoot Pending caused by Pod affinity?
41. How do you troubleshoot Pending caused by Pod anti-affinity?
42. How do you troubleshoot Pending caused by topology constraints?
43. How do you troubleshoot Pending caused by nodeSelector?
44. How do you troubleshoot Pending caused by resource requests?
45. How do you troubleshoot Pending caused by PVC binding?
46. How do you troubleshoot Pending caused by an unavailable StorageClass?
47. How do you troubleshoot Pending caused by volume topology?
48. How do you troubleshoot Pending caused by node conditions?
49. How do you troubleshoot Pending caused by an unavailable node pool?
50. How do you troubleshoot Pending caused by Cluster Autoscaler?
51. How do you troubleshoot a Pod that is Pending even though nodes appear to have enough CPU?
52. How do you troubleshoot a Pod that is Pending even though nodes appear to have enough memory?
53. How do you troubleshoot a Pod when aggregate cluster resources are sufficient but scheduling still fails?
54. How do you troubleshoot a Pod that cannot satisfy required node affinity?
55. How do you troubleshoot a Pod that cannot satisfy required Pod anti-affinity?
56. How do you troubleshoot a Pod that cannot satisfy topology spread constraints?
57. How do you troubleshoot a Pod that is Pending because all suitable nodes are tainted?
58. How do you troubleshoot a Pod that remains Pending after adding a toleration?
59. How do you troubleshoot a Pending Pod after a node pool change?
60. How do you troubleshoot Pending Pods after a cluster upgrade?
61. How do you troubleshoot hundreds of Pods suddenly entering Pending?
62. How do you troubleshoot only one application's Pods becoming Pending?
63. How do you troubleshoot Pending Pods only in one namespace?
64. How do you troubleshoot Pending Pods only in one availability zone?
65. How do you troubleshoot a scheduler-related Pending issue?
66. How do you determine whether kube-scheduler is healthy?
67. How do you troubleshoot a scheduler that is running but not scheduling Pods?
68. How do you troubleshoot Pods remaining Pending when scheduler logs show no obvious errors?
69. How do you troubleshoot a Pod whose scheduling constraints were recently changed?
70. How do you troubleshoot a Pending Pod during a production deployment?

The supplied interview notes specifically recommend checking CPU/memory, taints/tolerations, affinity, PVC binding, and scheduler events for Pending Pods. 

---

# C. CrashLoopBackOff Troubleshooting

71. A Pod is in CrashLoopBackOff; how do you troubleshoot it?
72. What does CrashLoopBackOff actually mean?
73. What are the most common causes of CrashLoopBackOff?
74. How do you determine why the container exited?
75. How do you check the previous container's logs?
76. How do you troubleshoot CrashLoopBackOff caused by application startup failure?
77. How do you troubleshoot CrashLoopBackOff caused by an incorrect command?
78. How do you troubleshoot CrashLoopBackOff caused by an incorrect argument?
79. How do you troubleshoot CrashLoopBackOff caused by missing environment variables?
80. How do you troubleshoot CrashLoopBackOff caused by a missing Secret?
81. How do you troubleshoot CrashLoopBackOff caused by a missing ConfigMap?
82. How do you troubleshoot CrashLoopBackOff caused by database connectivity?
83. How do you troubleshoot CrashLoopBackOff caused by dependency failure?
84. How do you troubleshoot CrashLoopBackOff caused by a failed health check?
85. How do you troubleshoot CrashLoopBackOff caused by liveness probes?
86. How do you troubleshoot CrashLoopBackOff caused by startup probes?
87. How do you troubleshoot CrashLoopBackOff caused by insufficient memory?
88. How do you troubleshoot CrashLoopBackOff caused by OOMKilled?
89. How do you troubleshoot CrashLoopBackOff caused by permission problems?
90. How do you troubleshoot CrashLoopBackOff caused by filesystem permissions?
91. How do you troubleshoot CrashLoopBackOff caused by a missing mounted volume?
92. How do you troubleshoot CrashLoopBackOff caused by a read-only filesystem?
93. How do you troubleshoot CrashLoopBackOff caused by incorrect image configuration?
94. How do you troubleshoot CrashLoopBackOff when logs show nothing?
95. How do you troubleshoot CrashLoopBackOff when the container exits too quickly to exec into it?
96. How do you troubleshoot CrashLoopBackOff after a new image deployment?
97. How do you troubleshoot CrashLoopBackOff after a ConfigMap change?
98. How do you troubleshoot CrashLoopBackOff after a Secret rotation?
99. How do you troubleshoot CrashLoopBackOff affecting only one replica?
100. How do you troubleshoot CrashLoopBackOff affecting every replica?
101. How do you distinguish application crash from Kubernetes probe failure?
102. How do you distinguish OOMKilled from an application exit?
103. How do you identify the container exit code?
104. How do you investigate a container that repeatedly exits with exit code 1?
105. How do you investigate a container that repeatedly exits with exit code 137?
106. How do you investigate a container that repeatedly exits with exit code 143?
107. How do you troubleshoot a restart loop caused by incorrect startup timing?
108. How do you troubleshoot a restart loop caused by dependency initialization?
109. How do you troubleshoot a restart loop caused by an incorrect working directory?
110. How do you troubleshoot a restart loop caused by an incorrect entrypoint?

The supplied PDF explicitly lists container logs, Pod events, environment variables, resource limits, and startup probe settings for CrashLoopBackOff troubleshooting. 

---

# D. ImagePullBackOff / Image Problems

111. A Pod is stuck in ImagePullBackOff; how do you troubleshoot it?
112. What causes ImagePullBackOff?
113. What causes ErrImagePull?
114. How do you determine whether the image name is wrong?
115. How do you determine whether the image tag is wrong?
116. How do you determine whether the registry is unavailable?
117. How do you troubleshoot private registry authentication?
118. How do you troubleshoot missing imagePullSecrets?
119. How do you troubleshoot expired registry credentials?
120. How do you troubleshoot image pulls failing only on certain nodes?
121. How do you troubleshoot image pulls failing only in one availability zone?
122. How do you troubleshoot image pulls failing after a node replacement?
123. How do you troubleshoot image pulls failing because of DNS?
124. How do you troubleshoot image pulls failing because of network connectivity?
125. How do you troubleshoot image pulls failing because of proxy configuration?
126. How do you troubleshoot image pulls failing because of TLS certificates?
127. How do you troubleshoot an image that works on one node but not another?
128. How do you troubleshoot slow image pulls?
129. How do you troubleshoot Pods taking several minutes to start because of image pulling?
130. How do you troubleshoot image pull failures after a Kubernetes upgrade?
131. How do you troubleshoot image pull failures after changing the container runtime?
132. How do you troubleshoot an image that exists in the registry but cannot be pulled?
133. How do you troubleshoot an incorrect image architecture?
134. How do you troubleshoot an image that works locally but fails in Kubernetes?
135. How do you troubleshoot authentication errors from a private registry?
136. How do you troubleshoot unauthorized errors during image pulling?
137. How do you troubleshoot manifest-not-found errors?
138. How do you troubleshoot image pull timeout errors?
139. How do you troubleshoot image pull certificate errors?
140. How do you troubleshoot image pull failures caused by registry rate limits?

---

# E. Pod Creating / ContainerCreating Troubleshooting

141. A Pod is stuck in ContainerCreating; how do you troubleshoot it?
142. What are the common reasons for ContainerCreating to remain for a long time?
143. How do you troubleshoot ContainerCreating caused by volume mounting?
144. How do you troubleshoot ContainerCreating caused by CNI?
145. How do you troubleshoot ContainerCreating caused by image pulling?
146. How do you troubleshoot ContainerCreating caused by Secrets?
147. How do you troubleshoot ContainerCreating caused by ConfigMaps?
148. How do you troubleshoot ContainerCreating caused by container runtime?
149. How do you troubleshoot ContainerCreating caused by node problems?
150. How do you troubleshoot ContainerCreating caused by filesystem problems?
151. How do you troubleshoot ContainerCreating when there are no obvious Pod events?
152. How do you troubleshoot one Pod stuck in ContainerCreating while others work?
153. How do you troubleshoot all Pods stuck in ContainerCreating on one node?
154. How do you troubleshoot all newly created Pods stuck in ContainerCreating?
155. How do you troubleshoot ContainerCreating after a node reboot?
156. How do you troubleshoot ContainerCreating after a CNI upgrade?
157. How do you troubleshoot ContainerCreating after a storage-driver change?
158. How do you troubleshoot ContainerCreating after a Kubernetes upgrade?
159. How do you determine whether containerd is responsible for ContainerCreating?
160. How do you determine whether kubelet is responsible for ContainerCreating?

---

# F. Pod Terminating Troubleshooting

161. A Pod is stuck in Terminating; how do you troubleshoot it?
162. What causes a Pod to remain in Terminating state?
163. How do you troubleshoot a Pod stuck because of a finalizer?
164. How do you troubleshoot a Pod stuck because of volume unmounting?
165. How do you troubleshoot a Pod stuck because of a preStop hook?
166. How do you troubleshoot a Pod stuck because the application does not handle SIGTERM?
167. How do you troubleshoot a Pod stuck because kubelet is unavailable?
168. How do you troubleshoot a Pod stuck because the node is NotReady?
169. How do you troubleshoot a Pod stuck during node drain?
170. How do you troubleshoot a Pod stuck because of PDB?
171. How do you troubleshoot a StatefulSet Pod stuck Terminating?
172. How do you troubleshoot a DaemonSet Pod stuck Terminating?
173. How do you troubleshoot a Pod that remains Terminating after force deletion?
174. When would you use force deletion during troubleshooting?
175. What risks are associated with force deleting a Pod?
176. How do you troubleshoot orphaned resources after Pod deletion?
177. How do you troubleshoot Pods stuck Terminating after a node failure?
178. How do you troubleshoot Pods stuck Terminating after a Kubernetes upgrade?
179. How do you troubleshoot a namespace stuck in Terminating?
180. How do you troubleshoot a namespace that cannot be deleted because of finalizers?

---

# G. Readiness / Liveness / Startup Probe Troubleshooting

181. A Pod is Running but NotReady; how do you troubleshoot it?
182. What causes readiness probes to fail?
183. How do you troubleshoot HTTP readiness probe failures?
184. How do you troubleshoot TCP readiness probe failures?
185. How do you troubleshoot exec readiness probe failures?
186. How do you troubleshoot readiness probe timeout?
187. How do you troubleshoot readiness probe connection refused?
188. How do you troubleshoot readiness probe returning HTTP 500?
189. How do you troubleshoot readiness probe returning HTTP 404?
190. How do you troubleshoot readiness probe failing only after deployment?
191. How do you troubleshoot readiness probe failing intermittently?
192. How do you troubleshoot all replicas becoming NotReady?
193. How do you troubleshoot only one replica becoming NotReady?
194. How do you troubleshoot readiness failure caused by application startup?
195. How do you troubleshoot readiness failure caused by database dependency?
196. How do you troubleshoot readiness failure caused by DNS?
197. How do you troubleshoot readiness failure caused by network policy?
198. How do you troubleshoot readiness failure caused by wrong port?
199. How do you troubleshoot readiness failure caused by wrong path?
200. How do you troubleshoot readiness failure caused by authentication?
201. How do you troubleshoot liveness probe failures?
202. What happens if a liveness probe is too aggressive?
203. How do you troubleshoot containers restarting because of liveness probes?
204. How do you troubleshoot startup probe failures?
205. How do you troubleshoot a slow-starting application being killed by liveness probes?
206. How do you troubleshoot incorrect initialDelaySeconds?
207. How do you troubleshoot incorrect timeoutSeconds?
208. How do you troubleshoot incorrect failureThreshold?
209. How do you troubleshoot incorrect periodSeconds?
210. How do you troubleshoot a probe that works manually but fails from kubelet?
211. How do you troubleshoot a probe when localhost works but Pod IP fails?
212. How do you troubleshoot probes after an application port change?
213. How do you troubleshoot probes after an Ingress change?
214. How do you troubleshoot probes during rolling deployment?
215. How do failing readiness probes affect Service endpoints?

The supplied probe material explicitly distinguishes liveness, readiness, and startup behavior and notes that readiness failure stops traffic while liveness failure causes container restart. 

---

# H. Deployment Troubleshooting

216. A Deployment is not creating the expected number of Pods; how do you troubleshoot it?
217. A Deployment has fewer available replicas than desired; how do you troubleshoot it?
218. A Deployment rollout is stuck; how do you troubleshoot it?
219. A Deployment rollout is progressing very slowly; how do you troubleshoot it?
220. A Deployment rollout is failing; how do you troubleshoot it?
221. A Deployment rollout shows ProgressDeadlineExceeded; how do you troubleshoot it?
222. A Deployment creates Pods but they never become Ready; how do you troubleshoot it?
223. A Deployment creates new Pods but old Pods do not terminate; how do you troubleshoot it?
224. A Deployment is continuously creating new ReplicaSets; how do you troubleshoot it?
225. A Deployment is continuously replacing Pods; how do you troubleshoot it?
226. A Deployment has the correct replica count but no traffic reaches it; how do you troubleshoot it?
227. A Deployment works before an update but fails afterward; how do you troubleshoot it?
228. How do you troubleshoot a failed rolling update?
229. How do you troubleshoot a rollout caused by an invalid image?
230. How do you troubleshoot a rollout caused by a broken ConfigMap?
231. How do you troubleshoot a rollout caused by a broken Secret?
232. How do you troubleshoot a rollout caused by failing readiness probes?
233. How do you troubleshoot a rollout caused by failing liveness probes?
234. How do you troubleshoot a rollout caused by insufficient capacity?
235. How do you troubleshoot a rollout caused by PDB restrictions?
236. How do you troubleshoot a rollout where only some replicas update?
237. How do you troubleshoot a Deployment with old and new versions running unexpectedly?
238. How do you troubleshoot an unexpected ReplicaSet created by a Deployment?
239. How do you troubleshoot a Deployment that does not scale?
240. How do you troubleshoot a Deployment that scales down unexpectedly?
241. How do you troubleshoot Deployment availability during node failure?
242. How do you troubleshoot Deployment availability during cluster upgrade?
243. How do you troubleshoot Deployment rollback?
244. How do you determine whether rollback is safer than fixing forward?
245. How do you troubleshoot a rollback that also fails?
246. How do you troubleshoot zero-downtime deployment failure?
247. How do you troubleshoot an outage caused by incorrect maxUnavailable?
248. How do you troubleshoot an outage caused by incorrect maxSurge?
249. How do you troubleshoot deployment capacity problems during maxSurge?
250. How do you troubleshoot deployment failure when PDB blocks eviction?

The supplied PDF identifies rolling updates, rollback, readiness probes, and `maxUnavailable`/`maxSurge` as production deployment concerns. 

---

# I. ReplicaSet Troubleshooting

251. A ReplicaSet is not creating Pods; how do you troubleshoot it?
252. A ReplicaSet has fewer Pods than desired; how do you troubleshoot it?
253. A ReplicaSet has more Pods than expected; how do you troubleshoot it?
254. A ReplicaSet keeps recreating deleted Pods; why?
255. A ReplicaSet is not adopting an existing Pod; how do you troubleshoot it?
256. Multiple ReplicaSets appear to select the same Pods; how do you troubleshoot it?
257. A ReplicaSet exists but no Pods are running; how do you troubleshoot it?
258. A ReplicaSet creates Pods that remain Pending; how do you troubleshoot it?
259. A ReplicaSet creates Pods that enter CrashLoopBackOff; how do you troubleshoot it?
260. A ReplicaSet suddenly stops maintaining replicas; what would you investigate?

---

# J. Service Troubleshooting

261. Pods are Running but the Service is not routing traffic; how do you troubleshoot it?
262. A Service has no endpoints; how do you troubleshoot it?
263. A Service has endpoints but traffic does not reach Pods; how do you troubleshoot it?
264. A Service selector appears correct but endpoints are empty; what do you check?
265. How do you troubleshoot Service labels versus Pod labels?
266. How do you troubleshoot a Service whose selector was accidentally changed?
267. How do you troubleshoot a Service after Pods were redeployed?
268. How do you troubleshoot a Service that works intermittently?
269. How do you troubleshoot a Service that routes traffic to only one Pod?
270. How do you troubleshoot a Service that routes traffic to unhealthy Pods?
271. How do you troubleshoot a Service after readiness probes start failing?
272. How do you troubleshoot a Service when EndpointSlices are empty?
273. How do you troubleshoot a Service when EndpointSlices contain incorrect addresses?
274. How do you troubleshoot ClusterIP connectivity?
275. How do you troubleshoot NodePort connectivity?
276. How do you troubleshoot LoadBalancer Service connectivity?
277. How do you troubleshoot a Service that is reachable from one Pod but not another?
278. How do you troubleshoot a Service that works inside the node but not from another node?
279. How do you troubleshoot a Service that works by Pod IP but not by Service IP?
280. How do you troubleshoot a Service that works by Service IP but not by DNS?
281. How do you troubleshoot Service connectivity after a kube-proxy restart?
282. How do you troubleshoot Service connectivity when kube-proxy is unhealthy?
283. How do you troubleshoot Service connectivity after a CNI upgrade?
284. How do you troubleshoot Service connectivity when NetworkPolicy is enabled?
285. How do you troubleshoot Service connectivity after changing `externalTrafficPolicy`?
286. How do you troubleshoot source-IP preservation problems?
287. How do you troubleshoot Service traffic distribution problems?
288. How do you troubleshoot Service session-affinity problems?
289. How do you troubleshoot a Service that has a correct ClusterIP but no traffic?
290. How do you troubleshoot a Service whose ClusterIP cannot be reached?
291. How do you troubleshoot a Service whose port is correct but targetPort is wrong?
292. How do you troubleshoot a Service whose targetPort points to the wrong container port?
293. How do you troubleshoot a Service after changing container ports?
294. How do you troubleshoot a Service when Pods are listening on localhost only?
295. How do you troubleshoot a Service that works from the node but not from Pods?
296. How do you troubleshoot a Service that works from Pods but not externally?
297. How do you troubleshoot NodePort when the node is reachable but NodePort is not?
298. How do you troubleshoot NodePort when the backend Pods are on different nodes?
299. How do you troubleshoot LoadBalancer when the external IP is missing?
300. How do you troubleshoot a LoadBalancer that exists but receives no traffic?

The supplied material specifically identifies selector/label matching, endpoints, readiness, and kube-proxy rules as the primary Service troubleshooting path. 

---

# K. DNS / CoreDNS Troubleshooting

301. A Pod cannot resolve a Kubernetes Service name; how do you troubleshoot it?
302. DNS works from one Pod but not another; how do you troubleshoot it?
303. DNS works in one namespace but not another; how do you troubleshoot it?
304. DNS suddenly stops working cluster-wide; how do you troubleshoot it?
305. How do you troubleshoot CoreDNS Pods?
306. How do you troubleshoot CoreDNS CrashLoopBackOff?
307. How do you troubleshoot CoreDNS Pending?
308. How do you troubleshoot CoreDNS readiness failures?
309. How do you troubleshoot CoreDNS high CPU?
310. How do you troubleshoot CoreDNS high memory usage?
311. How do you troubleshoot CoreDNS timeout errors?
312. How do you troubleshoot DNS SERVFAIL?
313. How do you troubleshoot DNS NXDOMAIN?
314. How do you troubleshoot DNS resolution from inside a Pod?
315. How do you troubleshoot DNS when direct Pod IP communication works?
316. How do you troubleshoot DNS when Service IP works but Service DNS does not?
317. How do you troubleshoot DNS after a CoreDNS upgrade?
318. How do you troubleshoot DNS after a CNI change?
319. How do you troubleshoot DNS after changing cluster DNS configuration?
320. How do you troubleshoot DNS when `/etc/resolv.conf` inside Pods is incorrect?
321. How do you troubleshoot DNS when only external domains fail?
322. How do you troubleshoot DNS when only Kubernetes Service names fail?
323. How do you troubleshoot DNS when Pod-to-Pod communication works but service discovery fails?
324. How do you troubleshoot DNS latency?
325. How do you troubleshoot intermittent DNS failures?
326. How do you troubleshoot DNS failures caused by NetworkPolicy?
327. How do you troubleshoot DNS failures caused by blocked UDP traffic?
328. How do you troubleshoot DNS failures caused by blocked TCP DNS traffic?
329. How do you troubleshoot DNS failures when CoreDNS Pods are healthy?
330. How do you troubleshoot DNS failures caused by upstream DNS servers?

---

# L. Ingress Troubleshooting

331. Ingress has no external IP; how do you troubleshoot it?
332. Ingress returns 404; how do you troubleshoot it?
333. Ingress returns 502; how do you troubleshoot it?
334. Ingress returns 503; how do you troubleshoot it?
335. Ingress returns 504; how do you troubleshoot it?
336. Ingress works for one hostname but not another; how do you troubleshoot it?
337. Ingress works for one path but not another; how do you troubleshoot it?
338. Ingress routes to the wrong Service; how do you troubleshoot it?
339. Ingress routes to a Service with no endpoints; how do you troubleshoot it?
340. Ingress Controller is running but traffic fails; how do you troubleshoot it?
341. Ingress Controller Pods are crashing; how do you troubleshoot them?
342. Ingress Controller Pods are Pending; how do you troubleshoot them?
343. Ingress Controller readiness probes fail; how do you troubleshoot them?
344. Ingress works internally but not externally; how do you troubleshoot it?
345. Ingress works externally but backend communication fails; how do you troubleshoot it?
346. Ingress TLS certificate is not being served; how do you troubleshoot it?
347. Ingress returns TLS handshake errors; how do you troubleshoot them?
348. Ingress redirects HTTP incorrectly; how do you troubleshoot it?
349. Ingress path rewriting is not working; how do you troubleshoot it?
350. Ingress sends traffic to an unhealthy Pod; how do you troubleshoot it?
351. Ingress stops routing after a Deployment; how do you troubleshoot it?
352. Ingress stops routing after a Service change; how do you troubleshoot it?
353. Ingress stops routing after an Ingress Controller upgrade; how do you troubleshoot it?
354. Ingress latency suddenly increases; how do you troubleshoot it?
355. Ingress returns intermittent 502 errors; how do you troubleshoot it?
356. Ingress returns intermittent 503 errors; how do you troubleshoot it?
357. Ingress returns intermittent 504 errors; how do you troubleshoot it?
358. How do you troubleshoot Ingress-to-Service connectivity?
359. How do you troubleshoot Ingress-to-Pod connectivity?
360. How do you troubleshoot an Ingress when backend Pods are healthy?
361. How do you troubleshoot an Ingress when Service endpoints are healthy?
362. How do you troubleshoot an Ingress when only one availability zone fails?
363. How do you troubleshoot an Ingress when the load balancer health checks fail?
364. How do you troubleshoot an Ingress Controller when its configuration is not reloaded?
365. How do you troubleshoot conflicting Ingress rules?
366. How do you troubleshoot a default backend problem?
367. How do you troubleshoot host-header-related routing problems?
368. How do you troubleshoot path-prefix matching problems?
369. How do you troubleshoot TLS Secret-related Ingress failures?
370. How do you troubleshoot an Ingress after Kubernetes API version changes?

---

# M. NetworkPolicy Troubleshooting

371. A Pod cannot communicate with another Pod after applying NetworkPolicy; how do you troubleshoot it?
372. A Pod can communicate before NetworkPolicy but not afterward; how do you troubleshoot it?
373. NetworkPolicy blocks frontend-to-backend traffic; how do you troubleshoot it?
374. NetworkPolicy blocks backend-to-database traffic; how do you troubleshoot it?
375. NetworkPolicy blocks DNS; how do you troubleshoot it?
376. NetworkPolicy blocks external API access; how do you troubleshoot it?
377. NetworkPolicy allows ingress but blocks egress; how do you troubleshoot it?
378. NetworkPolicy allows egress but blocks ingress; how do you troubleshoot it?
379. How do you troubleshoot multiple NetworkPolicies affecting the same Pod?
380. How do you troubleshoot incorrect namespaceSelector?
381. How do you troubleshoot incorrect podSelector?
382. How do you troubleshoot incorrect IPBlock configuration?
383. How do you troubleshoot NetworkPolicy port mismatches?
384. How do you troubleshoot NetworkPolicy protocol mismatches?
385. How do you troubleshoot a default-deny policy breaking applications?
386. How do you troubleshoot a NetworkPolicy that appears correct but does not work?
387. How do you determine whether the CNI actually enforces NetworkPolicy?
388. How do you troubleshoot NetworkPolicy after a CNI upgrade?
389. How do you troubleshoot NetworkPolicy differences between nodes?
390. How do you troubleshoot NetworkPolicy differences between namespaces?

The supplied material specifically identifies CNI, NetworkPolicies, DNS, endpoints, and Pod-to-Pod connectivity as the main network troubleshooting areas. 

---

# N. Pod-to-Pod Networking Troubleshooting

391. Two Pods cannot communicate; how do you troubleshoot it?
392. Two Pods on the same node cannot communicate; how do you troubleshoot it?
393. Two Pods on different nodes cannot communicate; how do you troubleshoot it?
394. Pod-to-Pod traffic works within a node but not across nodes; what do you investigate?
395. Pod-to-Pod traffic fails only in one availability zone; what do you investigate?
396. Pod-to-Pod traffic fails only for newly created Pods; what do you investigate?
397. Pod has an IP but cannot communicate; how do you troubleshoot it?
398. Pod does not receive an IP address; how do you troubleshoot it?
399. Pod IP allocation suddenly fails cluster-wide; how do you troubleshoot it?
400. Pod networking fails after CNI upgrade; how do you troubleshoot it?
401. Pod networking fails after node replacement; how do you troubleshoot it?
402. Pod networking fails after Kubernetes upgrade; how do you troubleshoot it?
403. How do you identify whether CNI is responsible for networking failure?
404. How do you troubleshoot CNI DaemonSet failures?
405. How do you troubleshoot CNI Pods in CrashLoopBackOff?
406. How do you troubleshoot CNI Pods in Pending?
407. How do you troubleshoot CNI IP exhaustion?
408. How do you troubleshoot Pod CIDR exhaustion?
409. How do you troubleshoot node CIDR problems?
410. How do you troubleshoot routing between Pod CIDRs?
411. How do you troubleshoot MTU-related Pod networking problems?
412. How do you troubleshoot packet fragmentation between Pods?
413. How do you troubleshoot packet loss between Pods?
414. How do you troubleshoot intermittent Pod connectivity?
415. How do you troubleshoot asymmetric routing between Pods?
416. How do you troubleshoot Pod networking when node networking works?
417. How do you troubleshoot Pod networking when Pod IPs are correct?
418. How do you troubleshoot Pod networking when NetworkPolicy is disabled?
419. How do you troubleshoot Pod networking when only one application is affected?
420. How do you troubleshoot Pod networking when only one node is affected?

---

# O. kube-proxy Troubleshooting

421. Services are not routing traffic; how do you determine whether kube-proxy is responsible?
422. How do you troubleshoot kube-proxy?
423. What happens when kube-proxy is not running?
424. How do you troubleshoot kube-proxy Pods in CrashLoopBackOff?
425. How do you troubleshoot kube-proxy Pods not running on every node?
426. How do you troubleshoot kube-proxy after a Kubernetes upgrade?
427. How do you troubleshoot kube-proxy after a CNI upgrade?
428. How do you troubleshoot incorrect iptables rules?
429. How do you troubleshoot incorrect IPVS rules?
430. How do you troubleshoot Service routing that fails only on one node?
431. How do you troubleshoot Service routing that fails only for Pods on one node?
432. How do you troubleshoot Service routing when endpoints are correct but traffic fails?
433. How do you troubleshoot stale Service rules?
434. How do you troubleshoot stale EndpointSlice rules?
435. How do you troubleshoot kube-proxy CPU spikes?
436. How do you troubleshoot kube-proxy memory problems?
437. How do you troubleshoot kube-proxy configuration problems?
438. How do you troubleshoot kube-proxy when Pod-to-Pod communication works but Service traffic fails?
439. How do you troubleshoot kube-proxy when ClusterIP works from some nodes but not others?
440. How do you troubleshoot kube-proxy during a production outage?

The supplied architecture notes identify kube-proxy as maintaining node-level networking rules and Service connectivity. 

---

# P. Node NotReady Troubleshooting

441. A worker node is NotReady; how do you troubleshoot it?
442. What are the common causes of Node NotReady?
443. How do you troubleshoot kubelet on a NotReady node?
444. How do you troubleshoot container runtime on a NotReady node?
445. How do you troubleshoot disk pressure?
446. How do you troubleshoot memory pressure?
447. How do you troubleshoot PID pressure?
448. How do you troubleshoot network problems causing Node NotReady?
449. How do you troubleshoot a node that repeatedly changes between Ready and NotReady?
450. How do you troubleshoot a node that suddenly disappears?
451. How do you troubleshoot a node that stops sending heartbeats?
452. How do you troubleshoot kubelet certificate problems?
453. How do you troubleshoot kubelet authentication problems?
454. How do you troubleshoot kubelet authorization problems?
455. How do you troubleshoot kubelet unable to reach API server?
456. How do you troubleshoot API server unreachable from one node?
457. How do you troubleshoot API server reachable from some nodes but not one node?
458. How do you troubleshoot node filesystem corruption?
459. How do you troubleshoot node disk exhaustion?
460. How do you troubleshoot node inode exhaustion?
461. How do you troubleshoot node memory exhaustion?
462. How do you troubleshoot node CPU saturation?
463. How do you troubleshoot node network interface problems?
464. How do you troubleshoot node DNS problems?
465. How do you troubleshoot node container runtime problems?
466. How do you troubleshoot node CNI problems?
467. How do you troubleshoot a NotReady node during peak traffic?
468. How do you troubleshoot multiple nodes becoming NotReady simultaneously?
469. How do you troubleshoot all nodes in one availability zone becoming NotReady?
470. How do you troubleshoot nodes becoming NotReady after an upgrade?

The supplied production scenario specifically recommends kubelet status/logs, node conditions, disk pressure, memory pressure, network connectivity, and container runtime health for Node NotReady incidents. 

---

# Q. kubelet Troubleshooting

471. kubelet is not running; how do you troubleshoot it?
472. kubelet is running but node remains NotReady; how do you troubleshoot it?
473. kubelet cannot communicate with API server; how do you troubleshoot it?
474. kubelet cannot start Pods; how do you troubleshoot it?
475. kubelet reports container runtime errors; how do you troubleshoot them?
476. kubelet reports CNI errors; how do you troubleshoot them?
477. kubelet reports volume mount errors; how do you troubleshoot them?
478. kubelet reports probe failures; how do you troubleshoot them?
479. kubelet CPU usage is high; how do you troubleshoot it?
480. kubelet memory usage is high; how do you troubleshoot it?
481. kubelet logs show repeated Pod synchronization failures; how do you troubleshoot them?
482. kubelet repeatedly restarts; how do you troubleshoot it?
483. kubelet cannot register the node; how do you troubleshoot it?
484. kubelet certificate has expired; how do you troubleshoot it?
485. kubelet cannot authenticate with the API server; how do you troubleshoot it?
486. kubelet cannot pull images; how do you troubleshoot it?
487. kubelet cannot create containers; how do you troubleshoot it?
488. kubelet cannot mount volumes; how do you troubleshoot it?
489. kubelet cannot configure Pod networking; how do you troubleshoot it?
490. kubelet reports disk pressure unexpectedly; how do you troubleshoot it?
491. kubelet reports memory pressure unexpectedly; how do you troubleshoot it?
492. kubelet reports PID pressure unexpectedly; how do you troubleshoot it?
493. kubelet is healthy but Pods are not starting; what do you investigate?
494. kubelet is unhealthy on only one node; what do you investigate?
495. kubelet failures begin after a node upgrade; how do you troubleshoot them?

---

# R. Container Runtime Troubleshooting

496. containerd is down; how do you troubleshoot it?
497. CRI-O is down; how do you troubleshoot it?
498. Containers are not starting although kubelet is healthy; how do you troubleshoot it?
499. Image pulls fail from containerd; how do you troubleshoot them?
500. containerd repeatedly crashes; how do you troubleshoot it?
501. container runtime CPU usage is high; how do you troubleshoot it?
502. container runtime memory usage is high; how do you troubleshoot it?
503. container runtime reports filesystem errors; how do you troubleshoot them?
504. container runtime cannot create a container; how do you troubleshoot it?
505. container runtime cannot delete containers; how do you troubleshoot it?
506. container runtime cannot create Pod sandbox; how do you troubleshoot it?
507. Pod sandbox creation fails; how do you troubleshoot it?
508. Pod sandbox networking fails; how do you troubleshoot it?
509. Containers work on one node but not another; how do you troubleshoot runtime differences?
510. Container runtime problems start after an OS upgrade; how do you troubleshoot them?
511. Container runtime problems start after Kubernetes upgrade; how do you troubleshoot them?
512. Container runtime problems start after changing CNI; how do you troubleshoot them?
513. Container runtime cannot access the image registry; how do you troubleshoot it?
514. Container runtime cannot access mounted storage; how do you troubleshoot it?
515. Container runtime leaves stale containers; how do you troubleshoot them?

---

# S. Node Resource / Performance Troubleshooting

516. A node is running out of CPU; how do you troubleshoot it?
517. A node is running out of memory; how do you troubleshoot it?
518. A node is running out of disk space; how do you troubleshoot it?
519. A node is running out of inodes; how do you troubleshoot it?
520. A node has high load average; how do you troubleshoot it?
521. A node has high CPU but Pods show low CPU usage; how do you investigate?
522. A node has high memory but Pods appear normal; how do you investigate?
523. A node has high disk I/O; how do you troubleshoot it?
524. A node has high network utilization; how do you troubleshoot it?
525. A node has packet loss; how do you troubleshoot it?
526. A node has network latency; how do you troubleshoot it?
527. A node repeatedly hits DiskPressure; how do you troubleshoot it?
528. A node repeatedly hits MemoryPressure; how do you troubleshoot it?
529. A node repeatedly hits PIDPressure; how do you troubleshoot it?
530. How do you identify which Pod is consuming the most resources?
531. How do you identify a noisy-neighbor workload?
532. How do you identify CPU throttling?
533. How do you identify memory leaks?
534. How do you identify excessive ephemeral-storage usage?
535. How do you troubleshoot excessive container logs filling node disks?
536. How do you troubleshoot excessive image storage usage?
537. How do you troubleshoot Pods being evicted because of node pressure?
538. How do you troubleshoot a node where system processes consume unexpected resources?
539. How do you troubleshoot a node that becomes unhealthy only under peak traffic?
540. How do you troubleshoot resource exhaustion after increasing application replicas?

---

# T. OOMKilled / Memory Troubleshooting

541. A container is OOMKilled; how do you troubleshoot it?
542. What causes OOMKilled?
543. How do you determine whether the container exceeded its memory limit?
544. How do you determine whether the node itself was under memory pressure?
545. How do you troubleshoot repeated OOMKilled events?
546. How do you troubleshoot OOMKilled after increasing traffic?
547. How do you troubleshoot OOMKilled after increasing replicas?
548. How do you troubleshoot OOMKilled after a deployment?
549. How do you troubleshoot OOMKilled when application memory usage looks normal?
550. How do you troubleshoot memory leaks in Kubernetes?
551. How do memory requests affect scheduling?
552. How do memory limits affect container behavior?
553. How do QoS classes affect memory eviction?
554. How do you troubleshoot BestEffort Pods being evicted?
555. How do you troubleshoot Burstable Pods being evicted?
556. How do you troubleshoot Guaranteed Pods being evicted?
557. How do you troubleshoot node-level OOM?
558. How do you troubleshoot sudden memory spikes?
559. How do you troubleshoot memory growth that occurs only after scaling?
560. How do you troubleshoot memory problems after changing JVM/container memory settings?

---

# U. CPU / Throttling Troubleshooting

561. Application latency suddenly increases because of CPU throttling; how do you troubleshoot it?
562. How do you detect CPU throttling?
563. How do you determine whether CPU limits are too low?
564. How do you troubleshoot high CPU usage in one Pod?
565. How do you troubleshoot high CPU usage across all replicas?
566. How do you troubleshoot CPU spikes after deployment?
567. How do you troubleshoot CPU spikes after scaling?
568. How do you troubleshoot CPU throttling when node CPU is available?
569. How do you troubleshoot CPU throttling caused by container limits?
570. How do you troubleshoot an application that becomes slower as replicas increase?
571. How do you troubleshoot CPU starvation caused by incorrect requests?
572. How do you troubleshoot CPU starvation caused by node overcommitment?
573. How do you troubleshoot CPU usage that causes HPA to scale unexpectedly?
574. How do you troubleshoot HPA scaling caused by CPU requests being incorrectly configured?
575. How do you troubleshoot high CPU on one node but not others?

---

# V. Storage / PVC Troubleshooting

576. A PVC is stuck in Pending; how do you troubleshoot it?
577. What causes a PVC to remain Pending?
578. How do you troubleshoot PVC when no PV is available?
579. How do you troubleshoot PVC when StorageClass is missing?
580. How do you troubleshoot PVC when dynamic provisioning fails?
581. How do you troubleshoot PVC when access mode is unsupported?
582. How do you troubleshoot PVC when requested capacity is unavailable?
583. How do you troubleshoot PVC when volume topology prevents binding?
584. How do you troubleshoot PVC after a StorageClass change?
585. How do you troubleshoot PVC after a cluster upgrade?
586. How do you troubleshoot a PV stuck in Pending?
587. How do you troubleshoot a PV stuck in Released?
588. How do you troubleshoot a PV stuck in Terminating?
589. How do you troubleshoot a PVC stuck in Terminating?
590. How do you troubleshoot a Pod stuck because its PVC cannot mount?
591. How do you troubleshoot FailedMount?
592. How do you troubleshoot FailedAttachVolume?
593. How do you troubleshoot volume attachment timeout?
594. How do you troubleshoot volume mount permission errors?
595. How do you troubleshoot filesystem errors on mounted volumes?
596. How do you troubleshoot read-only volume problems?
597. How do you troubleshoot storage latency?
598. How do you troubleshoot application latency caused by storage?
599. How do you troubleshoot storage failure affecting only one node?
600. How do you troubleshoot storage failure affecting one availability zone?
601. How do you troubleshoot a volume that is attached to the wrong node?
602. How do you troubleshoot a volume that cannot detach from an old node?
603. How do you troubleshoot StatefulSet Pods waiting for volumes?
604. How do you troubleshoot volume failures during node replacement?
605. How do you troubleshoot volume failures during cluster upgrade?
606. How do you troubleshoot CSI driver failures?
607. How do you troubleshoot CSI controller Pods?
608. How do you troubleshoot CSI node Pods?
609. How do you troubleshoot CSI driver after an upgrade?
610. How do you troubleshoot dynamic provisioning after a CSI upgrade?

---

# W. StatefulSet Troubleshooting

611. A StatefulSet Pod is stuck Pending; how do you troubleshoot it?
612. A StatefulSet Pod is stuck Terminating; how do you troubleshoot it?
613. A StatefulSet Pod is stuck ContainerCreating; how do you troubleshoot it?
614. A StatefulSet Pod is repeatedly restarting; how do you troubleshoot it?
615. A StatefulSet cannot create the next ordinal Pod; how do you troubleshoot it?
616. A StatefulSet is not scaling as expected; how do you troubleshoot it?
617. A StatefulSet Pod gets recreated with storage problems; how do you troubleshoot it?
618. A StatefulSet Pod cannot find its stable DNS name; how do you troubleshoot it?
619. A Headless Service does not provide expected StatefulSet DNS; how do you troubleshoot it?
620. A StatefulSet Pod cannot mount its PVC; how do you troubleshoot it?
621. A StatefulSet Pod is scheduled to an unexpected node; how do you troubleshoot it?
622. A StatefulSet becomes unavailable after node failure; how do you troubleshoot it?
623. A StatefulSet becomes unavailable after zone failure; how do you troubleshoot it?
624. A StatefulSet rollout is stuck; how do you troubleshoot it?
625. A StatefulSet update causes application downtime; how do you troubleshoot it?
626. A StatefulSet Pod starts before its dependency is ready; how do you troubleshoot it?
627. A StatefulSet Pod cannot communicate with another replica; how do you troubleshoot it?
628. A StatefulSet's persistent data appears missing; how do you troubleshoot it?
629. A StatefulSet Pod has the correct name but incorrect storage; how do you troubleshoot it?
630. A StatefulSet fails after storage migration; how do you troubleshoot it?

---

# X. DaemonSet Troubleshooting

631. A DaemonSet is not running on every node; how do you troubleshoot it?
632. A DaemonSet Pod is missing from one node; how do you troubleshoot it?
633. A DaemonSet Pod is Pending; how do you troubleshoot it?
634. A DaemonSet Pod is CrashLoopBackOff; how do you troubleshoot it?
635. A DaemonSet Pod is NotReady; how do you troubleshoot it?
636. A DaemonSet is not scheduled because of taints; how do you troubleshoot it?
637. A DaemonSet is not scheduled because of node affinity; how do you troubleshoot it?
638. A DaemonSet stops running after adding new nodes; how do you troubleshoot it?
639. A DaemonSet fails only on one node; how do you troubleshoot it?
640. A DaemonSet upgrade causes networking problems; how do you troubleshoot it?
641. A CNI DaemonSet is failing; how do you troubleshoot it?
642. A logging DaemonSet is failing; how do you troubleshoot it?
643. A monitoring DaemonSet is failing; how do you troubleshoot it?
644. A DaemonSet prevents node drain; how do you troubleshoot it?
645. A DaemonSet consumes excessive node resources; how do you troubleshoot it?

---

# Y. Job / CronJob Troubleshooting

646. A Job never completes; how do you troubleshoot it?
647. A Job keeps creating failed Pods; how do you troubleshoot it?
648. A Job reaches backoffLimit; how do you troubleshoot it?
649. A Job Pod enters CrashLoopBackOff; how do you troubleshoot it?
650. A Job Pod remains Pending; how do you troubleshoot it?
651. A Job Pod cannot pull its image; how do you troubleshoot it?
652. A Job cannot access a Secret; how do you troubleshoot it?
653. A Job cannot access a PVC; how do you troubleshoot it?
654. A CronJob does not create Jobs; how do you troubleshoot it?
655. A CronJob creates duplicate Jobs; how do you troubleshoot it?
656. A CronJob runs at the wrong time; how do you troubleshoot it?
657. A CronJob overlaps with its previous execution; how do you troubleshoot it?
658. A CronJob stops executing; how do you troubleshoot it?
659. A CronJob creates Jobs that immediately fail; how do you troubleshoot it?
660. A CronJob works manually but fails on schedule; how do you troubleshoot it?

---

# Z. Scheduling / Affinity / Taints Troubleshooting

661. A Pod cannot be scheduled because of nodeSelector; how do you troubleshoot it?
662. A Pod cannot be scheduled because of node affinity; how do you troubleshoot it?
663. A Pod cannot be scheduled because of Pod affinity; how do you troubleshoot it?
664. A Pod cannot be scheduled because of Pod anti-affinity; how do you troubleshoot it?
665. A Pod cannot be scheduled because of topology spread constraints; how do you troubleshoot it?
666. A Pod cannot be scheduled because of taints; how do you troubleshoot it?
667. A Pod has the correct toleration but is still Pending; how do you troubleshoot it?
668. A Pod has toleration but lands on an unexpected node; how do you troubleshoot it?
669. A Pod has node affinity but lands somewhere unexpected; how do you troubleshoot it?
670. A Pod anti-affinity rule causes unexpected Pending Pods; how do you troubleshoot it?
671. Two replicas are scheduled on the same node despite HA requirements; how do you troubleshoot it?
672. All replicas are scheduled in the same availability zone; how do you troubleshoot it?
673. Pods are distributed unevenly across nodes; how do you troubleshoot it?
674. Pods are distributed unevenly across availability zones; how do you troubleshoot it?
675. Scheduling fails after adding a new taint; how do you troubleshoot it?
676. Scheduling fails after removing a toleration; how do you troubleshoot it?
677. Scheduling fails after changing node labels; how do you troubleshoot it?
678. Scheduling fails after changing affinity rules; how do you troubleshoot it?
679. Scheduling fails after changing topology constraints; how do you troubleshoot it?
680. Scheduling becomes slow after increasing cluster size; how do you troubleshoot it?

---

# AA. HPA Troubleshooting

681. HPA is not scaling Pods; how do you troubleshoot it?
682. HPA scales too slowly; how do you troubleshoot it?
683. HPA scales too quickly; how do you troubleshoot it?
684. HPA continuously scales up and down; how do you troubleshoot it?
685. HPA shows unknown metrics; how do you troubleshoot it?
686. HPA cannot retrieve CPU metrics; how do you troubleshoot it?
687. HPA cannot retrieve memory metrics; how do you troubleshoot it?
688. HPA does not scale because CPU requests are missing; how do you troubleshoot it?
689. HPA scales to maxReplicas unexpectedly; how do you troubleshoot it?
690. HPA remains at minReplicas unexpectedly; how do you troubleshoot it?
691. HPA scales up but application latency does not improve; how do you troubleshoot it?
692. HPA scales up but latency becomes worse; how do you troubleshoot it?
693. HPA scales down and application becomes unstable; how do you troubleshoot it?
694. HPA behaves differently between environments; how do you troubleshoot it?
695. HPA stops working after a Kubernetes upgrade; how do you troubleshoot it?
696. HPA stops working after Metrics Server upgrade; how do you troubleshoot it?
697. HPA scales unexpectedly after changing resource requests; how do you troubleshoot it?
698. HPA causes excessive node scaling; how do you troubleshoot it?
699. HPA and Cluster Autoscaler are not working together correctly; how do you troubleshoot it?
700. How do you troubleshoot HPA when metrics appear correct but scaling does not occur?

The supplied notes explicitly call out HPA troubleshooting, Metrics Server, resource requests/limits, scaling latency, and Cluster Autoscaler interaction. 

---

# AB. Cluster Autoscaler Troubleshooting

701. Cluster Autoscaler is not adding nodes; how do you troubleshoot it?
702. Cluster Autoscaler is not removing nodes; how do you troubleshoot it?
703. Cluster Autoscaler adds nodes but Pods remain Pending; how do you troubleshoot it?
704. Cluster Autoscaler repeatedly adds and removes nodes; how do you troubleshoot it?
705. Cluster Autoscaler cannot scale because of node-group configuration; how do you troubleshoot it?
706. Cluster Autoscaler cannot scale because of Pod constraints; how do you troubleshoot it?
707. Cluster Autoscaler cannot scale because of taints; how do you troubleshoot it?
708. Cluster Autoscaler cannot scale because of affinity rules; how do you troubleshoot it?
709. Cluster Autoscaler cannot scale because of PDB; how do you troubleshoot it?
710. Cluster Autoscaler cannot remove a node because Pods cannot be evicted; how do you troubleshoot it?
711. Cluster Autoscaler cannot remove a node because of local storage; how do you troubleshoot it?
712. Cluster Autoscaler cannot remove a node because of unmanaged Pods; how do you troubleshoot it?
713. Cluster Autoscaler stops after an upgrade; how do you troubleshoot it?
714. Cluster Autoscaler CPU usage becomes high; how do you troubleshoot it?
715. Cluster Autoscaler logs show repeated scale-up failures; how do you troubleshoot them?
716. Cluster Autoscaler scales the wrong node group; how do you troubleshoot it?
717. Cluster Autoscaler does not scale despite many Pending Pods; how do you troubleshoot it?
718. Cluster Autoscaler scales but new nodes never become Ready; how do you troubleshoot it?
719. Cluster Autoscaler scales nodes but workloads cannot schedule; how do you troubleshoot it?
720. Cluster Autoscaler causes capacity oscillation; how do you troubleshoot it?

---

# AC. PDB / Drain Troubleshooting

721. Node drain is stuck; how do you troubleshoot it?
722. `kubectl drain` refuses to evict a Pod; how do you troubleshoot it?
723. PDB prevents node drain; how do you troubleshoot it?
724. PDB has zero allowed disruptions; how do you troubleshoot it?
725. PDB is too restrictive; how do you troubleshoot it?
726. PDB is not protecting the application; how do you troubleshoot it?
727. Pods cannot be evicted during node maintenance; how do you troubleshoot it?
728. Drain fails because of unmanaged Pods; how do you troubleshoot it?
729. Drain fails because of DaemonSet Pods; how do you troubleshoot it?
730. Drain fails because of local storage; how do you troubleshoot it?
731. Drain fails because of StatefulSet Pods; how do you troubleshoot it?
732. Drain succeeds but application becomes unavailable; how do you troubleshoot it?
733. Drain causes too many replicas to become unavailable; how do you troubleshoot it?
734. Drain causes application latency; how do you troubleshoot it?
735. Drain takes much longer than expected; how do you troubleshoot it?
736. A node cannot be drained during a production incident; what do you investigate?
737. A node cannot be drained because PDB is blocking eviction; what do you investigate?
738. A node cannot be drained because replacement capacity is unavailable; what do you investigate?
739. A node cannot be drained because of topology constraints; what do you investigate?
740. How do you troubleshoot a failed zero-downtime node maintenance operation?

---

# AD. ConfigMap Troubleshooting

741. Application does not receive updated ConfigMap values; how do you troubleshoot it?
742. Application still uses old configuration after ConfigMap update; how do you troubleshoot it?
743. ConfigMap is missing; how do you troubleshoot the resulting Pod failure?
744. ConfigMap key is missing; how do you troubleshoot it?
745. ConfigMap is mounted but application cannot read it; how do you troubleshoot it?
746. ConfigMap file exists but contains unexpected data; how do you troubleshoot it?
747. Application works before ConfigMap change but fails afterward; how do you troubleshoot it?
748. ConfigMap update causes application restart loop; how do you troubleshoot it?
749. ConfigMap update does not trigger a Deployment rollout; how do you troubleshoot it?
750. Different Pods appear to have different configuration; how do you troubleshoot it?

---

# AE. Secret Troubleshooting

751. Application cannot start because a Secret is missing; how do you troubleshoot it?
752. Application receives an incorrect Secret value; how do you troubleshoot it?
753. Secret was rotated but application still uses the old value; how do you troubleshoot it?
754. Secret environment variable is not updated; how do you troubleshoot it?
755. Secret volume is not updated; how do you troubleshoot it?
756. Pod cannot mount a Secret; how do you troubleshoot it?
757. Pod cannot read a Secret because of permissions; how do you troubleshoot it?
758. ServiceAccount cannot access a Secret; how do you troubleshoot it?
759. Secret exists in the wrong namespace; how do you troubleshoot it?
760. Application authentication fails after Secret rotation; how do you troubleshoot it?

---

# AF. RBAC Troubleshooting

761. User receives Forbidden from Kubernetes API; how do you troubleshoot it?
762. ServiceAccount receives Forbidden; how do you troubleshoot it?
763. User can read Pods but cannot delete them; how do you troubleshoot it?
764. User can access one namespace but not another; how do you troubleshoot it?
765. ServiceAccount can access one resource but not another; how do you troubleshoot it?
766. RoleBinding exists but permission still fails; how do you troubleshoot it?
767. ClusterRole exists but permission still fails; how do you troubleshoot it?
768. RoleBinding points to the wrong ServiceAccount; how do you troubleshoot it?
769. RoleBinding references the wrong namespace; how do you troubleshoot it?
770. ClusterRoleBinding gives unexpected permissions; how do you troubleshoot it?
771. A Pod cannot access the Kubernetes API; how do you troubleshoot its ServiceAccount?
772. `kubectl auth can-i` says no; how do you troubleshoot the RBAC configuration?
773. `kubectl auth can-i` says yes but application still gets Forbidden; how do you troubleshoot it?
774. RBAC breaks after deployment; how do you troubleshoot it?
775. RBAC breaks after namespace recreation; how do you troubleshoot it?

---

# AG. API Server Troubleshooting

776. Kubernetes API server is unavailable; how do you troubleshoot it?
777. kubectl returns connection refused; how do you troubleshoot it?
778. kubectl requests are timing out; how do you troubleshoot them?
779. API server returns 500 errors; how do you troubleshoot them?
780. API server returns 401 errors; how do you troubleshoot them?
781. API server returns 403 errors; how do you troubleshoot them?
782. API server returns 404 for an expected resource; how do you troubleshoot it?
783. API server latency suddenly increases; how do you troubleshoot it?
784. API server CPU becomes high; how do you troubleshoot it?
785. API server memory usage becomes high; how do you troubleshoot it?
786. API server connections are exhausted; how do you troubleshoot it?
787. API server cannot communicate with etcd; how do you troubleshoot it?
788. API server certificate problems occur; how do you troubleshoot them?
789. API server authentication fails; how do you troubleshoot it?
790. API server authorization fails; how do you troubleshoot it?
791. API server admission webhook requests time out; how do you troubleshoot them?
792. API server becomes slow only during deployments; how do you troubleshoot it?
793. API server becomes slow only during large-scale Pod creation; how do you troubleshoot it?
794. API server becomes unavailable after a control-plane change; how do you troubleshoot it?
795. API server is healthy but kubectl cannot connect; how do you troubleshoot the network path?
796. API server is reachable from one location but not another; how do you troubleshoot it?
797. API server returns errors only for one API group; how do you troubleshoot it?
798. API server returns errors only for one namespace; how do you troubleshoot it?
799. API server becomes unstable after an upgrade; how do you troubleshoot it?
800. How do you troubleshoot API server overload in a production cluster?

---

# AH. etcd Troubleshooting

801. etcd is unavailable; how do you troubleshoot it?
802. etcd loses quorum; how do you troubleshoot it?
803. One etcd member fails; how do you troubleshoot it?
804. Two etcd members fail in a three-member cluster; how do you troubleshoot it?
805. etcd latency suddenly increases; how do you troubleshoot it?
806. etcd disk latency becomes high; how do you troubleshoot it?
807. etcd disk becomes full; how do you troubleshoot it?
808. etcd database size becomes unexpectedly large; how do you troubleshoot it?
809. etcd CPU becomes high; how do you troubleshoot it?
810. etcd memory becomes high; how do you troubleshoot it?
811. API server cannot read from etcd; how do you troubleshoot it?
812. Kubernetes objects cannot be created because etcd is unavailable; how do you troubleshoot it?
813. Existing workloads are running but cluster changes cannot be made; how do you troubleshoot it?
814. etcd reports leader-election problems; how do you troubleshoot them?
815. etcd reports unhealthy members; how do you troubleshoot them?
816. etcd backup fails; how do you troubleshoot it?
817. etcd restore fails; how do you troubleshoot it?
818. Kubernetes control plane is unavailable after an etcd restore; how do you troubleshoot it?
819. etcd certificates are invalid; how do you troubleshoot them?
820. etcd communication between members fails; how do you troubleshoot it?
821. etcd performance degrades during high API activity; how do you troubleshoot it?
822. etcd becomes unhealthy after a node failure; how do you troubleshoot it?
823. How do you troubleshoot an etcd quorum-loss incident without making the situation worse?
824. How do you troubleshoot cluster recovery after complete etcd loss?
825. How do you verify that an etcd backup is usable?

The supplied interview notes explicitly identify etcd failure as a critical control-plane incident and recommend restoration from an etcd snapshot. 

---

# AI. Scheduler Troubleshooting

826. kube-scheduler is not scheduling Pods; how do you troubleshoot it?
827. kube-scheduler is Running but no Pods are being assigned; how do you troubleshoot it?
828. kube-scheduler is crashing; how do you troubleshoot it?
829. kube-scheduler logs show scheduling errors; how do you troubleshoot them?
830. Scheduler latency becomes high; how do you troubleshoot it?
831. Scheduler CPU becomes high; how do you troubleshoot it?
832. Scheduler memory becomes high; how do you troubleshoot it?
833. Scheduler stops responding after an upgrade; how do you troubleshoot it?
834. Scheduler schedules Pods to unexpected nodes; how do you troubleshoot it?
835. Scheduler leaves Pods Pending even though suitable nodes exist; how do you troubleshoot it?
836. Scheduler fails only for one workload; how do you troubleshoot it?
837. Scheduler fails only in one namespace; how do you troubleshoot it?
838. Scheduler fails because of affinity rules; how do you troubleshoot it?
839. Scheduler fails because of taints; how do you troubleshoot it?
840. Scheduler fails because of resource requests; how do you troubleshoot it?

---

# AJ. Controller Manager Troubleshooting

841. Controller-manager is unavailable; how do you troubleshoot it?
842. Controller-manager is Running but Deployments are not reconciling; how do you troubleshoot it?
843. ReplicaSets are not maintaining desired replicas; how do you troubleshoot it?
844. Jobs are not being reconciled; how do you troubleshoot it?
845. Nodes are not being handled correctly after failure; how do you troubleshoot it?
846. Controller-manager crashes repeatedly; how do you troubleshoot it?
847. Controller-manager CPU is high; how do you troubleshoot it?
848. Controller-manager memory is high; how do you troubleshoot it?
849. Controllers stop reconciling after an API server problem; how do you troubleshoot it?
850. Deployment desired state differs from actual state for a long time; how do you troubleshoot it?

---

# AK. Control Plane Failure Scenarios

851. API server goes down; how do you troubleshoot the incident?
852. Scheduler goes down; how do you troubleshoot the incident?
853. Controller-manager goes down; how do you troubleshoot the incident?
854. etcd goes down; how do you troubleshoot the incident?
855. Multiple control-plane components fail simultaneously; how do you troubleshoot it?
856. Control plane is unavailable but existing Pods continue running; how do you investigate?
857. Control plane is unavailable and new Pods cannot be scheduled; how do you investigate?
858. Control plane becomes unavailable during deployment; how do you troubleshoot it?
859. Control plane becomes unavailable during node drain; how do you troubleshoot it?
860. Control plane becomes unavailable during cluster upgrade; how do you troubleshoot it?
861. Control plane becomes unavailable during peak traffic; how do you troubleshoot it?
862. One control-plane node fails; how do you troubleshoot it?
863. Two control-plane nodes fail; how do you troubleshoot it?
864. Control-plane components repeatedly restart; how do you troubleshoot them?
865. Control-plane latency suddenly increases; how do you troubleshoot it?

---

# AL. Application Latency Troubleshooting

866. Application latency suddenly increases after deployment; how do you troubleshoot it?
867. Application latency suddenly increases after scaling; how do you troubleshoot it?
868. Application latency increases although CPU usage is low; how do you troubleshoot it?
869. Application latency increases although memory usage is low; how do you troubleshoot it?
870. Application latency increases only for one Pod; how do you troubleshoot it?
871. Application latency increases only on one node; how do you troubleshoot it?
872. Application latency increases only in one availability zone; how do you troubleshoot it?
873. Application latency increases after node replacement; how do you troubleshoot it?
874. Application latency increases after CNI upgrade; how do you troubleshoot it?
875. Application latency increases after Kubernetes upgrade; how do you troubleshoot it?
876. Application latency increases after changing resource limits; how do you troubleshoot it?
877. Application latency increases because of CPU throttling; how do you troubleshoot it?
878. Application latency increases because of memory pressure; how do you troubleshoot it?
879. Application latency increases because of network bottleneck; how do you troubleshoot it?
880. Application latency increases because of uneven traffic distribution; how do you troubleshoot it?
881. Application latency increases because of cold starts; how do you troubleshoot it?
882. Application latency increases because HPA scaled the application; how do you troubleshoot it?
883. Application latency increases because HPA failed to scale; how do you troubleshoot it?
884. Application latency increases after changing readiness probes; how do you troubleshoot it?
885. Application latency increases after changing liveness probes; how do you troubleshoot it?
886. Application latency increases after changing Service configuration; how do you troubleshoot it?
887. Application latency increases after changing Ingress configuration; how do you troubleshoot it?
888. Application latency increases after enabling NetworkPolicy; how do you troubleshoot it?
889. Application latency increases after enabling service mesh; how do you troubleshoot it?
890. How do you determine whether latency is application-side or Kubernetes-side?

The supplied production incident explicitly asks the engineer to investigate resource utilization, CPU throttling, memory pressure, HPA, node health, network latency, images, probes, ConfigMaps, Secrets, rollback, and canary traffic. 

---

# AM. Production Deployment Incident Troubleshooting

891. A new deployment causes a complete production outage; how do you troubleshoot it?
892. A new deployment causes only 10% of traffic to fail; how do you troubleshoot it?
893. A new deployment causes latency but no errors; how do you troubleshoot it?
894. A new deployment causes HTTP 500 errors; how do you troubleshoot it?
895. A new deployment causes HTTP 502 errors; how do you troubleshoot it?
896. A new deployment causes HTTP 503 errors; how do you troubleshoot it?
897. A new deployment causes HTTP 504 errors; how do you troubleshoot it?
898. A new deployment causes Pods to CrashLoopBackOff; how do you troubleshoot it?
899. A new deployment causes readiness probes to fail; how do you troubleshoot it?
900. A new deployment causes liveness probes to fail; how do you troubleshoot it?
901. A new deployment causes Pods to remain Pending; how do you troubleshoot it?
902. A new deployment causes HPA to scale unexpectedly; how do you troubleshoot it?
903. A new deployment causes nodes to become overloaded; how do you troubleshoot it?
904. A new deployment causes DNS failures; how do you troubleshoot it?
905. A new deployment causes Service connectivity failures; how do you troubleshoot it?
906. A new deployment causes Ingress failures; how do you troubleshoot it?
907. A new deployment causes only one availability zone to fail; how do you troubleshoot it?
908. A new deployment causes only one replica to fail; how do you troubleshoot it?
909. A new deployment causes all new Pods to fail but old Pods work; how do you troubleshoot it?
910. A new deployment causes both old and new versions to fail; how do you troubleshoot it?
911. A rollback does not restore application health; how do you troubleshoot it?
912. How do you decide whether to rollback, scale, or investigate further?
913. How do you perform a safe rollback during a production incident?
914. How do you verify that rollback actually restored the previous state?
915. How do you investigate configuration drift between old and new Pods?

---

# AN. Networking Production Incident

916. Production Pods suddenly cannot communicate; how do you troubleshoot it?
917. Production Services suddenly stop routing; how do you troubleshoot it?
918. External traffic suddenly stops reaching the cluster; how do you troubleshoot it?
919. Internal traffic works but external traffic fails; how do you troubleshoot it?
920. External traffic works but internal Service traffic fails; how do you troubleshoot it?
921. Only cross-node traffic fails; how do you troubleshoot it?
922. Only cross-zone traffic fails; how do you troubleshoot it?
923. Only one namespace loses network connectivity; how do you troubleshoot it?
924. Only one node loses network connectivity; how do you troubleshoot it?
925. Network connectivity breaks after CNI upgrade; how do you troubleshoot it?
926. Network connectivity breaks after kube-proxy upgrade; how do you troubleshoot it?
927. Network connectivity breaks after Kubernetes upgrade; how do you troubleshoot it?
928. Network connectivity breaks after applying NetworkPolicy; how do you troubleshoot it?
929. Network latency suddenly increases; how do you troubleshoot it?
930. Packet loss suddenly increases; how do you troubleshoot it?
931. DNS and Service connectivity fail simultaneously; how do you troubleshoot it?
932. DNS works but Service connectivity fails; how do you troubleshoot it?
933. Service connectivity works but DNS fails; how do you troubleshoot it?
934. Pod IP connectivity works but Service IP connectivity fails; how do you troubleshoot it?
935. Service IP connectivity works but external connectivity fails; how do you troubleshoot it?

---

# AO. Cluster Upgrade Troubleshooting

936. Kubernetes upgrade fails; how do you troubleshoot it?
937. Control-plane upgrade completes but workloads fail; how do you troubleshoot it?
938. Worker-node upgrade causes Pods to fail; how do you troubleshoot it?
939. Pods fail after upgrading CoreDNS; how do you troubleshoot it?
940. Pods fail after upgrading CNI; how do you troubleshoot it?
941. Pods fail after upgrading kube-proxy; how do you troubleshoot it?
942. HPA fails after Kubernetes upgrade; how do you troubleshoot it?
943. Ingress fails after Kubernetes upgrade; how do you troubleshoot it?
944. Stateful workloads fail after Kubernetes upgrade; how do you troubleshoot it?
945. Storage fails after Kubernetes upgrade; how do you troubleshoot it?
946. Deprecated API errors appear after upgrade; how do you troubleshoot them?
947. Some workloads work and others fail after upgrade; how do you troubleshoot it?
948. New Pods cannot start after upgrade; how do you troubleshoot it?
949. Existing Pods work but new Pods fail after upgrade; how do you troubleshoot it?
950. Nodes become NotReady after upgrade; how do you troubleshoot it?
951. kubelet fails after node upgrade; how do you troubleshoot it?
952. container runtime fails after node upgrade; how do you troubleshoot it?
953. CNI fails after node upgrade; how do you troubleshoot it?
954. Pods cannot be drained during upgrade; how do you troubleshoot it?
955. PDB prevents upgrade progress; how do you troubleshoot it?
956. New node group cannot receive workloads; how do you troubleshoot it?
957. Old node group cannot be drained; how do you troubleshoot it?
958. Application downtime occurs during node upgrade; how do you troubleshoot it?
959. Add-on versions become incompatible after upgrade; how do you troubleshoot them?
960. How do you validate the cluster after a failed upgrade?

The supplied upgrade document covers add-on compatibility, control-plane upgrade, worker migration, cordon/drain, post-upgrade validation, and recovery considerations.  

---

# AP. Backup / Disaster Recovery Troubleshooting

961. etcd backup fails; how do you troubleshoot it?
962. etcd restore fails; how do you troubleshoot it?
963. Kubernetes workload backup fails; how do you troubleshoot it?
964. Persistent volume backup fails; how do you troubleshoot it?
965. Restored Pods remain Pending; how do you troubleshoot them?
966. Restored Pods cannot mount PVCs; how do you troubleshoot them?
967. Restored Services have no endpoints; how do you troubleshoot them?
968. Restored Ingress does not work; how do you troubleshoot it?
969. Restored application cannot access Secrets; how do you troubleshoot it?
970. Restored application cannot access ConfigMaps; how do you troubleshoot it?
971. Restored application cannot communicate across namespaces; how do you troubleshoot it?
972. Restored cluster has DNS problems; how do you troubleshoot it?
973. Restored cluster has CNI problems; how do you troubleshoot it?
974. Restored cluster has storage topology problems; how do you troubleshoot it?
975. Restored application starts but data is missing; how do you troubleshoot it?
976. Restored application starts but data is inconsistent; how do you troubleshoot it?
977. Disaster-recovery cluster is healthy but users cannot reach it; how do you troubleshoot it?
978. Failover occurs but DNS still points to the old cluster; how do you troubleshoot it?
979. Failover cluster has insufficient capacity; how do you troubleshoot it?
980. Multi-region failover causes split-brain; how do you troubleshoot it?

---

# AQ. Security Troubleshooting

981. Pod cannot access the Kubernetes API; how do you troubleshoot it?
982. Pod receives RBAC Forbidden; how do you troubleshoot it?
983. Pod cannot read a Secret; how do you troubleshoot it?
984. Pod cannot communicate with another namespace; how do you troubleshoot it?
985. Pod becomes privileged unexpectedly; how do you troubleshoot it?
986. Pod fails after applying Pod Security restrictions; how do you troubleshoot it?
987. Container fails because it requires root; how do you troubleshoot it?
988. Container fails because of securityContext; how do you troubleshoot it?
989. Container fails because of dropped Linux capabilities; how do you troubleshoot it?
990. Container fails because root filesystem is read-only; how do you troubleshoot it?
991. Admission webhook blocks deployments; how do you troubleshoot it?
992. Admission webhook times out; how do you troubleshoot it?
993. Admission webhook causes API server latency; how do you troubleshoot it?
994. Admission webhook is unavailable; how do you troubleshoot it?
995. NetworkPolicy blocks security-sensitive traffic; how do you troubleshoot it?
996. TLS certificates expire and applications fail; how do you troubleshoot it?
997. Service-to-service TLS authentication fails; how do you troubleshoot it?
998. Kubernetes API authentication suddenly fails; how do you troubleshoot it?
999. Kubernetes API authorization suddenly fails; how do you troubleshoot it?
1000. How do you investigate a suspected Kubernetes security misconfiguration without disrupting production?

---

# AR. Multi-Tenant Kubernetes Troubleshooting

1001. One tenant's Pods cannot communicate with another tenant; how do you troubleshoot it?
1002. One namespace cannot access another namespace; how do you troubleshoot it?
1003. A tenant consumes excessive cluster resources; how do you troubleshoot it?
1004. ResourceQuota prevents a tenant from deploying; how do you troubleshoot it?
1005. LimitRange prevents Pods from starting; how do you troubleshoot it?
1006. Tenant Pods are scheduled onto unexpected nodes; how do you troubleshoot it?
1007. Tenant workloads are affected by another tenant's workload; how do you troubleshoot it?
1008. NetworkPolicy isolation fails between tenants; how do you troubleshoot it?
1009. RBAC isolation fails between tenants; how do you troubleshoot it?
1010. One tenant's deployment causes node pressure for another tenant; how do you troubleshoot it?

---

# AS. High Availability Troubleshooting

1011. One replica fails and application becomes unavailable; how do you troubleshoot it?
1012. Multiple replicas fail simultaneously; how do you troubleshoot it?
1013. All replicas are scheduled on one node; how do you troubleshoot it?
1014. All replicas are scheduled in one availability zone; how do you troubleshoot it?
1015. One availability zone fails and application availability drops; how do you troubleshoot it?
1016. One worker node fails and application availability drops; how do you troubleshoot it?
1017. PDB does not provide expected availability; how do you troubleshoot it?
1018. Pod anti-affinity does not distribute replicas as expected; how do you troubleshoot it?
1019. Topology spread constraints do not distribute replicas correctly; how do you troubleshoot it?
1020. Load balancer sends traffic to an unhealthy zone; how do you troubleshoot it?
1021. Control-plane HA fails after one control-plane node goes down; how do you troubleshoot it?
1022. etcd remains unavailable after one member failure; how do you troubleshoot it?
1023. API server load balancing sends traffic to an unhealthy API server; how do you troubleshoot it?
1024. Cluster remains partially functional after control-plane failure; how do you troubleshoot the remaining issues?
1025. Application survives node failure but fails during node drain; how do you troubleshoot it?

---

# AT. End-to-End Traffic Troubleshooting

1026. Internet request cannot reach the application; how do you troubleshoot it end to end?
1027. How do you trace traffic from Internet to LoadBalancer to Ingress to Service to Pod?
1028. How do you troubleshoot traffic failing between the external load balancer and Ingress?
1029. How do you troubleshoot traffic failing between Ingress and Service?
1030. How do you troubleshoot traffic failing between Service and Pod?
1031. How do you troubleshoot traffic failing between frontend and backend Services?
1032. How do you troubleshoot traffic failing between backend and database Pods?
1033. How do you troubleshoot traffic that reaches the Pod but gets refused?
1034. How do you troubleshoot traffic that reaches the Pod but times out?
1035. How do you troubleshoot traffic that reaches the wrong Pod?
1036. How do you troubleshoot traffic that reaches only one replica?
1037. How do you troubleshoot traffic when Pods are healthy but Service has no endpoints?
1038. How do you troubleshoot traffic when endpoints are healthy but kube-proxy is broken?
1039. How do you troubleshoot traffic when kube-proxy is healthy but NetworkPolicy blocks it?
1040. How do you troubleshoot traffic when Service networking works but DNS does not?
1041. How do you troubleshoot traffic when DNS works but Service networking does not?
1042. How do you troubleshoot traffic when Service works internally but Ingress fails?
1043. How do you troubleshoot traffic when Ingress works but external load balancer fails?
1044. How do you troubleshoot intermittent end-to-end traffic failures?
1045. How do you troubleshoot traffic failures affecting only one availability zone?

The supplied architecture flow explicitly describes external traffic as Internet → LoadBalancer/Ingress → Service → Pods. 

---

# AU. "Everything Looks Healthy" Scenarios

1046. All Pods are Running but application is down; how do you troubleshoot it?
1047. All Pods are Ready but application is down; how do you troubleshoot it?
1048. All nodes are Ready but application is down; how do you troubleshoot it?
1049. Service has endpoints but application is unreachable; how do you troubleshoot it?
1050. Ingress is healthy but application is unreachable; how do you troubleshoot it?
1051. HPA is healthy but application is slow; how do you troubleshoot it?
1052. Metrics look normal but users report high latency; how do you troubleshoot it?
1053. Kubernetes events show nothing but traffic fails; how do you troubleshoot it?
1054. Application logs show nothing but traffic fails; how do you troubleshoot it?
1055. Pod restart count is zero but application is unavailable; how do you troubleshoot it?
1056. CPU and memory are normal but latency is high; how do you troubleshoot it?
1057. Service and endpoints are correct but traffic is dropped; how do you troubleshoot it?
1058. DNS works but application requests fail; how do you troubleshoot it?
1059. Direct Pod IP works but application domain fails; how do you troubleshoot it?
1060. Application works from one Pod but not another; how do you troubleshoot it?
1061. Application works from inside the cluster but not externally; how do you troubleshoot it?
1062. Application works externally but not internally; how do you troubleshoot it?
1063. Application works from one node but not another; how do you troubleshoot it?
1064. Application works from one availability zone but not another; how do you troubleshoot it?
1065. How do you troubleshoot an outage where Kubernetes health checks remain green?

---

# AV. Senior "What Would You Check?" Questions

1066. If a production Pod is down, what exactly would you check first?
1067. If a production Service is down, what exactly would you check first?
1068. If production Ingress is down, what exactly would you check first?
1069. If one node is down, what exactly would you check first?
1070. If the entire cluster is slow, what exactly would you check first?
1071. If only one application is slow, what exactly would you check first?
1072. If only one namespace is affected, what exactly would you check first?
1073. If only one availability zone is affected, what exactly would you check first?
1074. If only new Pods are failing, what exactly would you check first?
1075. If only old Pods are failing, what exactly would you check first?
1076. If only one replica is failing, what exactly would you check first?
1077. If every replica fails simultaneously, what exactly would you check first?
1078. If Pods are Pending, what exactly would you check first?
1079. If Pods are CrashLoopBackOff, what exactly would you check first?
1080. If Pods are ImagePullBackOff, what exactly would you check first?
1081. If Pods are Terminating, what exactly would you check first?
1082. If Pods are NotReady, what exactly would you check first?
1083. If Nodes are NotReady, what exactly would you check first?
1084. If Services have no endpoints, what exactly would you check first?
1085. If Services have endpoints but no traffic, what exactly would you check first?
1086. If DNS fails, what exactly would you check first?
1087. If Ingress returns 502, what exactly would you check first?
1088. If Ingress returns 503, what exactly would you check first?
1089. If Ingress returns 504, what exactly would you check first?
1090. If HPA does not scale, what exactly would you check first?

---

# AW. Deep Cross-Troubleshooting Questions

1091. If a Pod is Pending because of PVC binding, how would you prove the PVC is the actual root cause?
1092. If a Pod is Pending because of affinity, how would you prove affinity is the root cause?
1093. If a Pod is Pending because of taints, how would you prove taints are the root cause?
1094. If a Pod is CrashLoopBackOff and readiness is failing, which problem would you investigate first?
1095. If a Pod is Running but Service has no endpoints, what Kubernetes object chain would you inspect?
1096. If Service endpoints exist but traffic fails, which layer would you investigate next?
1097. If Service traffic fails only from one node, what component would you suspect?
1098. If Service traffic fails only cross-node, what component would you suspect?
1099. If Service traffic works by IP but not DNS, which components would you investigate?
1100. If DNS works but Service IP fails, which components would you investigate?
1101. If Ingress returns 503 but Service works, what layer would you investigate?
1102. If Ingress returns 502 but backend Pods are healthy, what would you investigate?
1103. If Ingress returns 504 intermittently, how would you isolate network versus application latency?
1104. If HPA scales up but Pods remain Pending, how would you troubleshoot the complete chain?
1105. If HPA scales up and Cluster Autoscaler adds nodes but Pods remain Pending, what would you investigate?
1106. If Cluster Autoscaler adds nodes but nodes remain NotReady, what would you investigate?
1107. If nodes are Ready but Pods remain Pending, what scheduling constraints would you investigate?
1108. If a node becomes NotReady and Pods are not rescheduled, what components would you investigate?
1109. If Pods cannot be rescheduled because of PDB, how would you prove it?
1110. If Pods cannot be rescheduled because of PVC topology, how would you prove it?
1111. If a Deployment rollout is stuck because new Pods are NotReady, how would you isolate probe versus application failure?
1112. If a Deployment rollout is stuck because new Pods are Pending, how would you isolate capacity versus scheduling?
1113. If a Deployment rollout causes latency, how would you determine whether maxSurge is responsible?
1114. If a Deployment rollout causes all traffic to fail, how would you decide whether to rollback?
1115. If rollback does not resolve the issue, what would you investigate next?
1116. If Kubernetes components are healthy but traffic fails, how would you investigate external networking?
1117. If application logs are healthy but traffic fails, how would you investigate networking?
1118. If networking is healthy but application logs show errors, how would you isolate application failure?
1119. If etcd is unhealthy but workloads continue running, what operations would you expect to fail?
1120. If API server is unavailable but existing Pods continue running, what would you expect to continue working?
1121. If kubelet is unavailable but containers are running, what would you expect to happen?
1122. If containerd is unavailable, what would you expect for existing versus new containers?
1123. If kube-proxy is unavailable, what would you expect for Pod-to-Pod versus Service traffic?
1124. If CoreDNS is unavailable, what would you expect for DNS versus direct IP communication?
1125. If CNI is unavailable, what would you expect for existing versus newly created Pods?
1126. If scheduler is unavailable, what would happen to already-running Pods?
1127. If controller-manager is unavailable, what happens when a Deployment Pod dies?
1128. If all control-plane components are unavailable, what happens to existing workloads?
1129. If one control-plane component is unhealthy, how would you identify which component is responsible?
1130. How would you troubleshoot an incident where multiple Kubernetes layers fail simultaneously?

---

# AX. Extreme Production Scenarios

1131. 30% of production Pods suddenly become Pending; how do you troubleshoot it?
1132. 30% of production Pods suddenly become CrashLoopBackOff; how do you troubleshoot it?
1133. All production Pods suddenly become NotReady; how do you troubleshoot it?
1134. All Services suddenly lose endpoints; how do you troubleshoot it?
1135. All Services still have endpoints but external traffic stops; how do you troubleshoot it?
1136. All Pods in one node fail; how do you troubleshoot it?
1137. All Pods in one availability zone fail; how do you troubleshoot it?
1138. All Pods in one namespace fail; how do you troubleshoot it?
1139. All new Pods fail but existing Pods work; how do you troubleshoot it?
1140. All existing Pods work but new deployments fail; how do you troubleshoot it?
1141. Kubernetes API is slow but applications remain healthy; how do you troubleshoot it?
1142. Applications are slow but Kubernetes API is healthy; how do you troubleshoot it?
1143. etcd is slow but applications appear healthy; how do you troubleshoot it?
1144. Scheduler is slow but existing workloads are healthy; how do you troubleshoot it?
1145. kubelet is slow on one node; how do you troubleshoot it?
1146. kube-proxy is slow on one node; how do you troubleshoot it?
1147. CoreDNS is slow but Service IP traffic works; how do you troubleshoot it?
1148. CNI is healthy but cross-node networking is slow; how do you troubleshoot it?
1149. Storage is healthy but database latency increases; how do you troubleshoot it?
1150. Application latency increases immediately after HPA scaling; how do you troubleshoot it?
1151. Application latency increases immediately after Cluster Autoscaler scaling; how do you troubleshoot it?
1152. Application latency increases immediately after node replacement; how do you troubleshoot it?
1153. Application latency increases immediately after CNI replacement; how do you troubleshoot it?
1154. Application latency increases immediately after Kubernetes upgrade; how do you troubleshoot it?
1155. Application latency increases immediately after Ingress Controller upgrade; how do you troubleshoot it?
1156. Application latency increases immediately after CoreDNS upgrade; how do you troubleshoot it?
1157. Application latency increases immediately after kube-proxy upgrade; how do you troubleshoot it?
1158. Application latency increases immediately after changing resource limits; how do you troubleshoot it?
1159. Application latency increases immediately after changing NetworkPolicy; how do you troubleshoot it?
1160. How would you lead the complete troubleshooting process for a major Kubernetes production outage?

---

# AY. Interviewer Cross-Questions — "Why?"

1161. Why would you check events before changing the Pod?
1162. Why would you check `describe` for a Pending Pod?
1163. Why would you check logs for CrashLoopBackOff?
1164. Why would you check previous logs for a restarted container?
1165. Why would you check resource requests when troubleshooting Pending?
1166. Why would you check resource limits when troubleshooting OOMKilled?
1167. Why would you check readiness when troubleshooting Service traffic?
1168. Why would you check selectors when troubleshooting Services?
1169. Why would you check EndpointSlices when troubleshooting Services?
1170. Why would you check kube-proxy when endpoints exist but traffic fails?
1171. Why would you check CoreDNS when Service name resolution fails?
1172. Why would you check CNI for cross-node networking failures?
1173. Why would you check NetworkPolicy after confirming CNI health?
1174. Why would you check kubelet when a node becomes NotReady?
1175. Why would you check containerd when Pods cannot start?
1176. Why would you check disk pressure during Node NotReady troubleshooting?
1177. Why would you check memory pressure during Node NotReady troubleshooting?
1178. Why would you check PDB when node drain fails?
1179. Why would you check affinity when Pods remain Pending?
1180. Why would you check taints when Pods remain Pending?
1181. Why would you check PVC when StatefulSet Pods remain Pending?
1182. Why would you check HPA metrics when autoscaling fails?
1183. Why would you check Cluster Autoscaler when HPA creates Pending Pods?
1184. Why would you check maxSurge during rollout capacity problems?
1185. Why would you check maxUnavailable during availability problems?
1186. Why would you check probes after a deployment?
1187. Why would you check ConfigMaps after an application configuration change?
1188. Why would you check Secrets after authentication failures?
1189. Why would you check etcd during control-plane failures?
1190. Why would you check API server before investigating scheduler failures?

---

# AZ. "How Would You Prove the Root Cause?"

1191. How would you prove that CPU shortage caused the Pod to remain Pending?
1192. How would you prove that memory shortage caused the Pod to remain Pending?
1193. How would you prove that a taint caused the scheduling failure?
1194. How would you prove that affinity caused the scheduling failure?
1195. How would you prove that PVC binding caused the scheduling failure?
1196. How would you prove that an image-pull failure caused the Pod startup failure?
1197. How would you prove that an application crash caused CrashLoopBackOff?
1198. How would you prove that OOMKilled caused the container restart?
1199. How would you prove that liveness probe failure caused the restart?
1200. How would you prove that readiness failure caused traffic removal?
1201. How would you prove that a Service selector caused missing endpoints?
1202. How would you prove that kube-proxy caused Service connectivity failure?
1203. How would you prove that NetworkPolicy caused traffic failure?
1204. How would you prove that CoreDNS caused application connectivity failure?
1205. How would you prove that CNI caused cross-node networking failure?
1206. How would you prove that kubelet caused Node NotReady?
1207. How would you prove that containerd caused Pod startup failure?
1208. How would you prove that PDB caused node drain failure?
1209. How would you prove that HPA caused unexpected scaling?
1210. How would you prove that Cluster Autoscaler caused node instability?
1211. How would you prove that a Deployment caused the production outage?
1212. How would you prove that a Kubernetes upgrade caused the production outage?
1213. How would you prove that an Ingress Controller caused 502 errors?
1214. How would you prove that storage caused application latency?
1215. How would you prove that etcd caused control-plane instability?
1216. How would you prove that API server overload caused cluster-wide symptoms?
1217. How would you prove that a recent configuration change caused the incident?
1218. How would you prove that the problem is external to Kubernetes?
1219. How would you prove that the problem is inside the application?
1220. How would you prove the final root cause to an interviewer?

---

# BA. Final Senior-Level Incident Questions

1221. You receive a page saying "Kubernetes production is down"; what do you do in the first five minutes?
1222. Production has 5xx errors across multiple services; how do you troubleshoot it?
1223. Production has high latency across multiple services; how do you troubleshoot it?
1224. Production has high latency in only one service; how do you troubleshoot it?
1225. Production has intermittent failures; how do you troubleshoot them?
1226. Production failures started exactly after deployment; how do you troubleshoot them?
1227. Production failures started without deployment; how do you troubleshoot them?
1228. Production failures started after node maintenance; how do you troubleshoot them?
1229. Production failures started after cluster upgrade; how do you troubleshoot them?
1230. Production failures started after a CNI upgrade; how do you troubleshoot them?
1231. Production failures started after an Ingress upgrade; how do you troubleshoot them?
1232. Production failures started after a storage upgrade; how do you troubleshoot them?
1233. Production failures started after a Secret rotation; how do you troubleshoot them?
1234. Production failures started after a ConfigMap change; how do you troubleshoot them?
1235. Production failures started after enabling NetworkPolicy; how do you troubleshoot them?
1236. Production failures started after enabling HPA; how do you troubleshoot them?
1237. Production failures started after enabling Cluster Autoscaler; how do you troubleshoot them?
1238. Production failures affect only one AZ; how do you troubleshoot them?
1239. Production failures affect only one node; how do you troubleshoot them?
1240. Production failures affect only one namespace; how do you troubleshoot them?
1241. Production failures affect only new Pods; how do you troubleshoot them?
1242. Production failures affect only old Pods; how do you troubleshoot them?
1243. Production failures affect only external traffic; how do you troubleshoot them?
1244. Production failures affect only internal traffic; how do you troubleshoot them?
1245. Production failures affect only Service DNS; how do you troubleshoot them?
1246. Production failures affect only Service IPs; how do you troubleshoot them?
1247. Production failures affect only Ingress; how do you troubleshoot them?
1248. Production failures affect only storage-backed workloads; how do you troubleshoot them?
1249. Production failures affect only stateful workloads; how do you troubleshoot them?
1250. Production failures affect the entire Kubernetes control plane; how do you troubleshoot and recover it?
