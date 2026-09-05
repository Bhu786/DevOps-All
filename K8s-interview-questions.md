# Kubernetes Interview Question Bank — 1000 Questions

## 1. Kubernetes Fundamentals

1. What is Kubernetes?
2. Why was Kubernetes introduced?
3. What problems does Kubernetes solve?
4. What are the major features of Kubernetes?
5. What are the advantages of Kubernetes?
6. What are the limitations of Kubernetes?
7. How is Kubernetes different from Docker?
8. Is Kubernetes a container runtime?
9. Is Kubernetes responsible for building container images?
10. What is container orchestration?
11. Why do we need container orchestration?
12. What is a Kubernetes cluster?
13. What is the difference between a cluster and a node?
14. What is a control plane?
15. What is a worker node?
16. What is a master node?
17. Is the term master node still preferred in Kubernetes?
18. What are the major components of a Kubernetes cluster?
19. What are the major control-plane components?
20. What are the major worker-node components?
21. What is the Kubernetes API?
22. Why is Kubernetes API important?
23. What does declarative configuration mean in Kubernetes?
24. What does desired state mean in Kubernetes?
25. What does actual state mean in Kubernetes?
26. How does Kubernetes maintain desired state?
27. What is reconciliation in Kubernetes?
28. What is a controller in Kubernetes?
29. Why is Kubernetes called a declarative system?
30. What happens when actual state differs from desired state?
31. What is an object in Kubernetes?
32. What is a Kubernetes resource?
33. What is the difference between an object and a resource?
34. What is metadata in Kubernetes?
35. What are labels in Kubernetes?
36. What are annotations in Kubernetes?
37. What is the difference between labels and annotations?
38. What is a selector in Kubernetes?
39. Why are labels important in Kubernetes?
40. Where are labels commonly used?
41. What is a namespace?
42. Why do we use namespaces?
43. What are the default Kubernetes namespaces?
44. What is the `default` namespace?
45. What is the `kube-system` namespace?
46. What is the `kube-public` namespace?
47. What is the `kube-node-lease` namespace?
48. Can every Kubernetes resource be namespaced?
49. Which Kubernetes resources are cluster-scoped?
50. Which Kubernetes resources are namespace-scoped?
51. Can two namespaces have the same resource name?
52. Can two namespaces have Pods with the same name?
53. How do you create a namespace?
54. How do you switch the default namespace for kubectl?
55. What happens if no namespace is specified?
56. Can a Pod communicate with another namespace?
57. Does a namespace provide complete security isolation?
58. What is a Kubernetes context?
59. What is kubeconfig?
60. Where is kubeconfig normally stored?
61. How does kubectl know which cluster to connect to?
62. What is the difference between cluster, context, and user in kubeconfig?
63. How do you list Kubernetes contexts?
64. How do you switch Kubernetes contexts?
65. How do you verify which cluster kubectl is connected to?
66. How does kubectl communicate with Kubernetes?
67. What protocol does kubectl use?
68. Why does kubectl use HTTPS?
69. What happens internally when you run `kubectl get pods`?
70. What happens internally when you run `kubectl apply -f deployment.yaml`?

The fundamentals, cluster architecture, desired-state/reconciliation model, namespaces, Services, workloads, and Pod lifecycle are central topics in the supplied Kubernetes material.  

---

# 2. Kubernetes Architecture

71. Explain Kubernetes architecture end to end.
72. What are the two major parts of Kubernetes architecture?
73. What is the responsibility of the control plane?
74. What is the responsibility of worker nodes?
75. What is kube-apiserver?
76. Why is kube-apiserver called the entry point to Kubernetes?
77. What components communicate with kube-apiserver?
78. Does kubelet communicate directly with etcd?
79. Does scheduler communicate directly with etcd?
80. Does controller-manager communicate directly with etcd?
81. What is etcd?
82. Why is etcd critical to Kubernetes?
83. What type of database is etcd?
84. What information does etcd store?
85. Does etcd store container images?
86. Does etcd store application logs?
87. Does etcd store Pod state?
88. Does etcd store Secrets?
89. Does etcd store ConfigMaps?
90. What happens if etcd becomes unavailable?
91. Can existing Pods continue running if etcd goes down?
92. Can new Pods be scheduled if etcd goes down?
93. Can you scale an application if etcd is unavailable?
94. Can you delete a Pod if etcd is unavailable?
95. How do you make etcd highly available?
96. How does etcd achieve consistency?
97. What is quorum in etcd?
98. Why is an odd number of etcd members recommended?
99. What happens if one etcd node fails in a three-member cluster?
100. What happens if two etcd nodes fail in a three-member cluster?
101. What happens if one etcd node fails in a five-member cluster?
102. What happens if quorum is lost?
103. How do you back up etcd?
104. How do you restore etcd?
105. What is kube-controller-manager?
106. What does controller-manager actually do?
107. Why does Kubernetes use controllers?
108. What is a reconciliation loop?
109. What controllers run inside kube-controller-manager?
110. What does the ReplicaSet controller do?
111. What does the Deployment controller do?
112. What does the Job controller do?
113. What does the Node controller do?
114. What happens when a node becomes NotReady?
115. Which controller detects node failures?
116. What is kube-scheduler?
117. What does the scheduler do?
118. Does the scheduler start containers?
119. Does the scheduler create Pods?
120. What does the scheduler actually modify?
121. How does scheduler select a node?
122. What factors does scheduler consider?
123. What is scheduling filtering?
124. What is scheduling scoring?
125. What is a scheduling constraint?
126. What is kubelet?
127. What does kubelet do?
128. Does kubelet create Pods?
129. Does kubelet create containers directly?
130. How does kubelet communicate with the API server?
131. What happens if kubelet stops?
132. What happens to existing containers when kubelet stops?
133. Can Pods continue running when kubelet is temporarily down?
134. How does Kubernetes detect node health?
135. What is kube-proxy?
136. Is kube-proxy mandatory for Kubernetes networking?
137. What does kube-proxy configure?
138. What is the relationship between kube-proxy and Services?
139. What is a container runtime?
140. What container runtimes can Kubernetes use?
141. What is CRI?
142. What is the relationship between kubelet and CRI?
143. What is containerd?
144. What is CRI-O?
145. Why was dockershim removed?
146. Does Kubernetes require Docker Engine?
147. What happens from kubelet to containerd?
148. What happens when a container image needs to be pulled?
149. What is the complete path from kubectl command to running container?
150. Which component writes desired state to etcd?
151. Which component reads desired state?
152. Which component creates the ReplicaSet?
153. Which component creates the Pod?
154. Which component assigns a node to a Pod?
155. Which component starts the container?
156. Which component performs health checks?
157. Which component maintains Service networking?
158. Which component maintains node state?
159. Which component stores cluster state?
160. Which component is the single entry point for Kubernetes API requests?

---

# 3. API Server Deep-Dive

161. What happens inside kube-apiserver when a request arrives?
162. What is authentication in Kubernetes?
163. What is authorization in Kubernetes?
164. What is admission control?
165. What is request validation?
166. In what order are authentication, authorization, and admission performed?
167. How does kube-apiserver authenticate a user?
168. What authentication mechanisms does Kubernetes support?
169. What is a ServiceAccount?
170. How does a Pod authenticate to the Kubernetes API?
171. What is a bearer token?
172. What is certificate-based authentication?
173. What is OIDC authentication?
174. What is RBAC authorization?
175. What happens if authentication fails?
176. What happens if authorization fails?
177. What happens if admission validation fails?
178. What happens if a request passes all API checks?
179. Where is the object stored after a successful API request?
180. Does kube-apiserver directly create a container?
181. Does kube-apiserver directly schedule Pods?
182. Does kube-apiserver directly restart containers?
183. How does kube-apiserver watch resources?
184. What is the Kubernetes watch mechanism?
185. Why is watch important?
186. How do controllers receive changes from the API server?
187. How does scheduler know that a Pod is unscheduled?
188. How does kubelet know that a Pod was assigned to its node?
189. What happens if API server is unavailable?
190. What happens to already-running Pods if API server goes down?
191. Can users run `kubectl get pods` if API server is down?
192. Can scheduler schedule new Pods if API server is down?
193. Can controllers reconcile resources if API server is down?
194. How would you troubleshoot API server latency?
195. How would you troubleshoot API server 5xx errors?
196. How would you troubleshoot API server connection refused?
197. How would you troubleshoot API server certificate problems?
198. How do you secure the Kubernetes API server?
199. How do you restrict API server access?
200. How do you make API server highly available?
201. Why is a load balancer used in front of multiple API servers?
202. What happens if one API server instance fails?
203. Can multiple API servers use the same etcd cluster?
204. How does API server communicate with etcd?
205. Why should etcd not be directly exposed to users?
206. What is API server audit logging?
207. Why is audit logging important?
208. How do you investigate who deleted a Kubernetes resource?
209. What is API versioning?
210. What is a Kubernetes API group?
211. What is a core API group?
212. What is a named API group?
213. What is `apps/v1`?
214. What is `batch/v1`?
215. What is `networking.k8s.io/v1`?
216. What is `storage.k8s.io/v1`?
217. What is a CustomResourceDefinition?
218. What is a CRD?
219. How does a CRD extend Kubernetes?
220. What is an operator in Kubernetes?

---

# 4. Pod Deep-Dive

221. What is a Pod?
222. Why is Pod the smallest deployable unit?
223. Why doesn't Kubernetes normally deploy containers directly?
224. Can a Pod contain multiple containers?
225. When should multiple containers be placed in one Pod?
226. What is the sidecar pattern?
227. How do containers inside the same Pod communicate?
228. Do containers inside the same Pod have different IP addresses?
229. Do containers inside the same Pod share the network namespace?
230. Do containers inside the same Pod share localhost?
231. Can two containers in the same Pod use the same port?
232. Do containers inside a Pod share storage?
233. How does a Pod get an IP address?
234. Who assigns the Pod IP?
235. What is the Pod network namespace?
236. What is the pause container?
237. Why does Kubernetes use a pause container?
238. What happens when a Pod is created?
239. What is Pod phase?
240. What are the common Pod phases?
241. What does Pending mean?
242. What does Running mean?
243. What does Succeeded mean?
244. What does Failed mean?
245. What does Unknown mean?
246. What is Pod lifecycle?
247. What is Pod termination?
248. What is graceful Pod termination?
249. What is `terminationGracePeriodSeconds`?
250. What happens when `kubectl delete pod` is executed?
251. What happens during Pod termination?
252. What is SIGTERM?
253. What is SIGKILL?
254. Why should applications handle SIGTERM?
255. What happens if an application does not exit after SIGTERM?
256. What is a Pod restart policy?
257. What are the available restart policies?
258. What is the default restart policy?
259. What is the difference between `Always`, `OnFailure`, and `Never`?
260. Which workloads normally use `Always`?
261. Which workloads normally use `OnFailure`?
262. What is a static Pod?
263. How is a static Pod different from a normal Pod?
264. Who creates static Pods?
265. Where are static Pod manifests stored?
266. How are control-plane components commonly deployed using static Pods?
267. What happens if a static Pod is deleted?
268. What happens if the static Pod manifest is removed?
269. What is an init container?
270. Why are init containers used?
271. Can init containers run in parallel?
272. Do init containers have to complete successfully?
273. What happens if an init container fails?
274. Can init containers access volumes?
275. Can init containers access the same network namespace?
276. What is an ephemeral container?
277. Why are ephemeral containers useful?
278. When would you use an ephemeral container for troubleshooting?
279. What is a multi-container Pod?
280. What is a sidecar container?
281. What is a Pod sandbox?
282. What is the difference between a Pod and a container?
283. What is the difference between a Pod and a VM?
284. Can a Pod run on multiple nodes?
285. Can containers of the same Pod run on different nodes?
286. What happens to a Pod when its node fails?
287. Does Kubernetes automatically recreate the same Pod object?
288. How does a Deployment replace a failed Pod?
289. Why are Pods considered ephemeral?
290. Should applications store persistent data directly inside a Pod filesystem?
291. What happens to container filesystem data when a container restarts?
292. What happens to Pod-local storage when the Pod is recreated?
293. What causes `CrashLoopBackOff`?
294. What causes `ImagePullBackOff`?
295. What causes `ErrImagePull`?
296. What causes `CreateContainerConfigError`?
297. What causes `CreateContainerError`?
298. What causes `ContainerCreating` to remain for a long time?
299. What causes a Pod to remain Pending?
300. How do you troubleshoot a Pending Pod?

---

# 5. Pod Lifecycle, Probes, and Application Health

301. What is a liveness probe?
302. What is a readiness probe?
303. What is a startup probe?
304. What is the difference between liveness and readiness?
305. What is the difference between readiness and startup?
306. What happens when a liveness probe fails?
307. What happens when a readiness probe fails?
308. What happens when a startup probe fails?
309. Why can a badly configured liveness probe cause outages?
310. Why can a badly configured readiness probe remove all Pods from Service endpoints?
311. When should you use a startup probe?
312. When should you use an HTTP probe?
313. When should you use a TCP probe?
314. When should you use an exec probe?
315. What is `initialDelaySeconds`?
316. What is `periodSeconds`?
317. What is `timeoutSeconds`?
318. What is `failureThreshold`?
319. What is `successThreshold`?
320. How do you design production-ready readiness probes?
321. Should readiness probe check database connectivity?
322. What are the risks of putting expensive operations inside a health endpoint?
323. How can a liveness probe create a restart loop?
324. How do probes interact with rolling deployments?
325. How do readiness probes affect Service traffic?
326. How do probes interact with load balancing?
327. How do probes behave during Pod termination?
328. How do you troubleshoot a Pod that keeps failing readiness?
329. How do you troubleshoot repeated liveness probe failures?
330. How do you troubleshoot startup probe failures?

---

# 6. Deployments and ReplicaSets

331. What is a Deployment?
332. Why do we use Deployment instead of creating Pods directly?
333. What is a ReplicaSet?
334. What is the relationship between Deployment and ReplicaSet?
335. Who creates the ReplicaSet?
336. Who creates Pods under a Deployment?
337. What happens when a Deployment replica count is increased?
338. What happens when a Deployment replica count is decreased?
339. What happens if one Deployment Pod crashes?
340. What happens if one Deployment Pod is manually deleted?
341. What happens if the ReplicaSet is manually deleted?
342. What happens if the Deployment is deleted?
343. What is a Deployment revision?
344. How does Deployment maintain revision history?
345. What is a rolling update?
346. What is `maxSurge`?
347. What is `maxUnavailable`?
348. How do `maxSurge` and `maxUnavailable` work together?
349. How would you configure zero-downtime rolling deployment?
350. Can Kubernetes guarantee zero downtime automatically?
351. What role does readiness play in zero-downtime deployment?
352. What happens if the new version never becomes Ready?
353. What is `progressDeadlineSeconds`?
354. What happens when a Deployment rollout gets stuck?
355. How do you check Deployment rollout status?
356. How do you pause a Deployment rollout?
357. How do you resume a Deployment rollout?
358. How do you roll back a Deployment?
359. How do you view Deployment rollout history?
360. What is `kubectl rollout undo`?
361. What happens during a rollback?
362. Can you roll back a Deployment after multiple revisions?
363. What happens if the new image is invalid?
364. What happens if the new image starts but readiness fails?
365. What happens if half of the Pods are running old version and half new version?
366. How do you implement canary deployment using native Kubernetes resources?
367. How do you implement blue-green deployment using Kubernetes?
368. What is the difference between rolling, blue-green, and canary deployment?
369. What happens if Deployment replicas are set to zero?
370. Can a Deployment manage multiple ReplicaSets?
371. Why does an old ReplicaSet remain after a Deployment update?
372. What is `revisionHistoryLimit`?
373. How does Kubernetes identify which Pods belong to a ReplicaSet?
374. What is the role of labels in ReplicaSets?
375. What happens if you manually change a Pod's labels?
376. What happens if two ReplicaSets select the same Pod?
377. How does Kubernetes prevent controller ownership conflicts?
378. What is `ownerReferences`?
379. How does garbage collection work with owner references?
380. What is the difference between scaling a Deployment and scaling a ReplicaSet?

---

# 7. StatefulSet, DaemonSet, Job, CronJob

381. What is a StatefulSet?
382. Why do stateful applications need StatefulSets?
383. How is StatefulSet different from Deployment?
384. What is stable identity in StatefulSet?
385. What is stable network identity?
386. Why is a Headless Service commonly used with StatefulSets?
387. What is `volumeClaimTemplates`?
388. How does StatefulSet create PVCs?
389. What happens when a StatefulSet Pod is deleted?
390. Does StatefulSet preserve Pod identity?
391. What is ordered Pod creation?
392. What is `podManagementPolicy`?
393. What is `OrderedReady`?
394. What is `Parallel` Pod management?
395. What happens when StatefulSet is scaled from 3 to 5 replicas?
396. What happens when StatefulSet is scaled from 5 to 2 replicas?
397. What happens to PVCs when StatefulSet is deleted?
398. How would you deploy a database using StatefulSet?
399. What are the limitations of using StatefulSet for databases?
400. What is a DaemonSet?
401. Why do we use DaemonSets?
402. Give examples of workloads that should run as DaemonSets.
403. How does DaemonSet differ from Deployment?
404. Does DaemonSet run one Pod per node?
405. Can DaemonSet run only on selected nodes?
406. How do node selectors affect DaemonSets?
407. How do taints and tolerations affect DaemonSets?
408. What happens when a new node joins the cluster?
409. What happens to a DaemonSet when a node is removed?
410. What is a Job?
411. What is a CronJob?
412. How does Job differ from Deployment?
413. How does CronJob differ from Job?
414. What is `completions` in a Job?
415. What is `parallelism` in a Job?
416. What is `backoffLimit`?
417. What happens when a Job fails?
418. What happens when a Job succeeds?
419. What is `activeDeadlineSeconds` in a Job?
420. What is `ttlSecondsAfterFinished`?
421. What is CronJob scheduling syntax?
422. What happens if a CronJob execution takes longer than its schedule interval?
423. What is `concurrencyPolicy`?
424. What are the CronJob concurrency policies?
425. What is `Forbid` concurrency?
426. What is `Replace` concurrency?
427. What is `Allow` concurrency?
428. How do you prevent duplicate CronJob executions?
429. How do you troubleshoot a Job that never completes?
430. How do you troubleshoot a CronJob that does not create Jobs?

---

# 8. Scheduling

431. How does Kubernetes scheduler work?
432. What happens between Pod creation and node assignment?
433. What is an unscheduled Pod?
434. What is a scheduler queue?
435. What is scheduling filtering?
436. What is scheduling scoring?
437. What is node capacity?
438. What is allocatable node capacity?
439. What is the difference between capacity and allocatable?
440. What are scheduling predicates?
441. What are scheduling priorities?
442. What is nodeSelector?
443. How does nodeSelector work?
444. What is node affinity?
445. What is required node affinity?
446. What is preferred node affinity?
447. What is the difference between required and preferred affinity?
448. What does `requiredDuringSchedulingIgnoredDuringExecution` mean?
449. What does `preferredDuringSchedulingIgnoredDuringExecution` mean?
450. What is Pod affinity?
451. What is Pod anti-affinity?
452. What is the difference between node affinity and Pod affinity?
453. When would you use Pod anti-affinity?
454. How can Pod anti-affinity improve high availability?
455. What is `topologyKey`?
456. What happens if node affinity and Pod affinity conflict?
457. What happens if a required affinity rule cannot be satisfied?
458. What is a taint?
459. What is a toleration?
460. What is the difference between taint and toleration?
461. Where is a taint defined?
462. Where is a toleration defined?
463. What does `NoSchedule` mean?
464. What does `PreferNoSchedule` mean?
465. What does `NoExecute` mean?
466. What happens to existing Pods with `NoExecute`?
467. Can toleration force a Pod onto a node?
468. Does toleration alone guarantee scheduling on a node?
469. How do you dedicate nodes to a specific workload?
470. How would you reserve GPU nodes for GPU workloads?
471. How do you combine taints and node affinity?
472. What is a node label?
473. How do you label a node?
474. How do you remove a node label?
475. What is topology spread constraint?
476. Why are topology spread constraints used?
477. How do topology spread constraints improve availability?
478. What is `topology.kubernetes.io/zone`?
479. What is `kubernetes.io/hostname`?
480. How would you distribute replicas across availability zones?
481. What is a resource request?
482. What is a resource limit?
483. How does scheduler use CPU requests?
484. How does scheduler use memory requests?
485. Does scheduler use CPU limits for placement?
486. What happens if a Pod has no resource requests?
487. What is QoS class?
488. What are the Kubernetes QoS classes?
489. What is Guaranteed QoS?
490. What is Burstable QoS?
491. What is BestEffort QoS?
492. How does QoS affect eviction?
493. How does Kubernetes choose Pods during memory pressure?
494. What is node pressure?
495. What is memory pressure?
496. What is disk pressure?
497. What is PID pressure?
498. How does scheduler behave when no node can satisfy a Pod?
499. How do you troubleshoot a Pod stuck in Pending due to scheduling?
500. Which commands would you use to investigate scheduling failures?

The supplied material specifically emphasizes CPU/memory, taints/tolerations, affinity, node constraints, and Pending-Pod troubleshooting. 

---

# 9. Kubernetes Networking Fundamentals

501. Explain Kubernetes networking architecture.
502. What are the fundamental Kubernetes networking requirements?
503. What is Pod-to-Pod networking?
504. Does every Pod get its own IP?
505. Can Pods communicate without NAT?
506. What is a Pod CIDR?
507. What is a Service CIDR?
508. What is a node CIDR?
509. What is a cluster CIDR?
510. What is CNI?
511. What does a CNI plugin do?
512. What are common Kubernetes CNI plugins?
513. What is the relationship between CNI and kubelet?
514. What happens when a Pod gets created from a networking perspective?
515. Who assigns the Pod IP?
516. How does a CNI plugin configure a Pod network interface?
517. What is the network namespace of a Pod?
518. What is `veth` pair?
519. How does a Pod communicate with the node?
520. How does one Pod communicate with another Pod on the same node?
521. How does one Pod communicate with a Pod on another node?
522. What is overlay networking?
523. What is underlay networking?
524. What is VXLAN?
525. Why are overlay networks used?
526. What is encapsulation?
527. What is routing-based Pod networking?
528. How does Kubernetes networking differ between cloud and on-premises?
529. What happens when a CNI plugin fails?
530. What happens when the CNI DaemonSet is not running?
531. Why might a newly created Pod have no IP?
532. How do you troubleshoot Pod IP allocation issues?
533. How do you troubleshoot Pod-to-Pod connectivity?
534. How do you troubleshoot cross-node Pod connectivity?
535. How do you verify Pod networking from inside a Pod?
536. How do you check the Pod IP?
537. How do you check node networking?
538. How do you identify the CNI plugin being used?
539. What is kube-proxy's role in Kubernetes networking?
540. What is iptables mode?
541. What is IPVS mode?
542. How does kube-proxy implement Service routing?
543. What happens when kube-proxy is down?
544. Can Pods still communicate directly if kube-proxy is down?
545. Can Services continue working if kube-proxy is broken?
546. What are EndpointSlices?
547. What is the relationship between Service and EndpointSlice?
548. Why were EndpointSlices introduced?
549. What happens when a Pod becomes NotReady?
550. Is a NotReady Pod automatically removed from Service endpoints?

---

# 10. Services and Service Discovery

551. What is a Kubernetes Service?
552. Why do we need Services?
553. Why can't clients directly depend on Pod IPs?
554. What is a stable Service IP?
555. What is a Service DNS name?
556. What are the different Service types?
557. What is ClusterIP?
558. What is NodePort?
559. What is LoadBalancer?
560. What is ExternalName?
561. What is a Headless Service?
562. What is `clusterIP: None`?
563. How does ClusterIP work internally?
564. How does NodePort work?
565. What port range is commonly used for NodePort?
566. Does NodePort expose the service on every node?
567. What happens if the selected node does not contain the Pod?
568. What is `externalTrafficPolicy`?
569. What is the difference between `Cluster` and `Local` external traffic policy?
570. How does `externalTrafficPolicy: Local` preserve client source IP?
571. What are the trade-offs of `externalTrafficPolicy: Local`?
572. How does LoadBalancer Service work?
573. Does LoadBalancer replace ClusterIP?
574. Does LoadBalancer normally create a Service internally?
575. Can a LoadBalancer Service be internal-only?
576. What is a cloud-controller-manager's role with LoadBalancer Services?
577. What happens if a LoadBalancer Service remains Pending?
578. How do you troubleshoot a LoadBalancer Service?
579. What is ExternalName?
580. Does ExternalName create endpoints?
581. When would you use ExternalName?
582. What is a Headless Service used for?
583. How does DNS behave for a Headless Service?
584. How does a normal Service DNS record differ from a Headless Service?
585. What is service discovery?
586. How does Kubernetes DNS work?
587. What is CoreDNS?
588. How does a Pod resolve a Service name?
589. What is `service.namespace.svc.cluster.local`?
590. Can Pods in different namespaces access each other through DNS?
591. What happens if CoreDNS is down?
592. Can applications access Services by IP if DNS is down?
593. How do you troubleshoot Kubernetes DNS?
594. How do you check CoreDNS logs?
595. How do you test DNS from a Pod?
596. How do you troubleshoot `nslookup` failures inside a Pod?
597. What is a Service selector?
598. What happens if Service selector does not match Pod labels?
599. Can a Service exist without a selector?
600. How can a Service route traffic to external endpoints?
601. What is an EndpointSlice?
602. How do readiness probes affect Service endpoints?
603. Can a Service route traffic to terminating Pods?
604. What is session affinity in Kubernetes Services?
605. What is `sessionAffinity: ClientIP`?
606. When would you use session affinity?
607. What are the limitations of Service-based load balancing?
608. How does Kubernetes distribute Service traffic across Pods?
609. Is Kubernetes Service load balancing the same as an external load balancer?
610. What is the difference between Service load balancing and Ingress load balancing?

The supplied PDF explicitly covers Service stable IP/DNS/load balancing, ClusterIP, NodePort, LoadBalancer, ExternalName, Headless Services, and Pod-to-Service flow.  

---

# 11. Ingress and HTTP Traffic

611. What is Kubernetes Ingress?
612. Why is Ingress used?
613. Is Ingress itself a load balancer?
614. What is an Ingress Controller?
615. What is the difference between Ingress and Ingress Controller?
616. Does creating an Ingress automatically create a load balancer?
617. What happens if no Ingress Controller is installed?
618. What is host-based routing?
619. What is path-based routing?
620. How does an Ingress route traffic to a Service?
621. Can Ingress route traffic directly to Pods?
622. What is TLS termination at Ingress?
623. Where is the TLS certificate stored?
624. What is a Kubernetes TLS Secret?
625. How does HTTPS traffic reach an Ingress Controller?
626. What is the typical external traffic flow through Ingress?
627. What is the difference between Ingress and NodePort?
628. What is the difference between Ingress and LoadBalancer Service?
629. Can multiple applications share one external load balancer using Ingress?
630. Why is Ingress useful for multiple microservices?
631. How would you expose frontend and backend using one domain?
632. How would you route `/api` to one Service and `/` to another?
633. How would you route `api.example.com` to one Service and `app.example.com` to another?
634. How does Ingress support name-based virtual hosting?
635. What happens when an Ingress rule does not match?
636. What is a default backend?
637. How do you troubleshoot 404 from Ingress?
638. How do you troubleshoot 502 from Ingress?
639. How do you troubleshoot 503 from Ingress?
640. How do you troubleshoot TLS handshake failures at Ingress?
641. How do you troubleshoot an Ingress that has no external IP?
642. How do you troubleshoot Ingress-to-Service connectivity?
643. How do you troubleshoot Ingress-to-Pod connectivity?
644. What happens if the backend Service has no endpoints?
645. How do readiness probes influence Ingress traffic?
646. Can Ingress perform authentication?
647. Can Ingress perform rate limiting?
648. Can Ingress perform path rewriting?
649. Can Ingress perform redirects?
650. What is the difference between Layer 4 and Layer 7 traffic handling?
651. Why is HTTP Ingress considered Layer 7?
652. Can Kubernetes expose TCP services through an Ingress?
653. What is Gateway API?
654. Why was Gateway API introduced?
655. How is Gateway API different from Ingress?
656. What are Gateway API resources?
657. What is a Gateway?
658. What is an HTTPRoute?
659. What is the difference between Gateway and Ingress?
660. When would you choose Gateway API over Ingress?

---

# 12. Storage

661. What is persistent storage in Kubernetes?
662. Why is container filesystem not suitable for persistent application data?
663. What is a volume in Kubernetes?
664. What is `emptyDir`?
665. What happens to `emptyDir` when a container restarts?
666. What happens to `emptyDir` when a Pod is deleted?
667. What is `hostPath`?
668. Why is hostPath risky for production workloads?
669. What is a PersistentVolume?
670. What is a PersistentVolumeClaim?
671. What is the difference between PV and PVC?
672. Who creates a PV?
673. Who creates a PVC?
674. How does a Pod use a PVC?
675. What is a StorageClass?
676. Why do we need StorageClasses?
677. What is dynamic provisioning?
678. What is static provisioning?
679. What happens when a PVC is created?
680. How does Kubernetes find storage for a PVC?
681. What is PV binding?
682. What are PV access modes?
683. What is ReadWriteOnce?
684. What is ReadOnlyMany?
685. What is ReadWriteMany?
686. What is ReadWriteOncePod?
687. What is volume mode?
688. What is Filesystem volume mode?
689. What is Block volume mode?
690. What is a reclaim policy?
691. What is `Retain` reclaim policy?
692. What is `Delete` reclaim policy?
693. What is `Recycle` reclaim policy?
694. What happens when a PVC is deleted?
695. What happens to the underlying storage after PVC deletion?
696. What is a CSI driver?
697. What is Container Storage Interface?
698. Why was CSI introduced?
699. What is a CSI Controller?
700. What is a CSI Node plugin?
701. How does Kubernetes attach a persistent volume?
702. How does Kubernetes mount a persistent volume?
703. What happens if a PVC remains Pending?
704. How do you troubleshoot a Pending PVC?
705. What happens if a Pod cannot mount a volume?
706. How do you troubleshoot `FailedMount`?
707. How do you troubleshoot `FailedAttachVolume`?
708. What is volume topology?
709. Why does topology matter for persistent volumes?
710. How do StatefulSets use persistent storage?
711. What is a volumeClaimTemplate?
712. Does each StatefulSet Pod get its own PVC?
713. What happens when a StatefulSet Pod is recreated?
714. Does the recreated StatefulSet Pod get the same PVC?
715. How do you migrate persistent data between clusters?
716. How do you back up Kubernetes persistent volumes?
717. What is a volume snapshot?
718. What is VolumeSnapshotClass?
719. What is VolumeSnapshot?
720. What is VolumeSnapshotContent?
721. How would you design storage for a production database?
722. How would you handle storage across multiple availability zones?
723. What happens if the node containing a volume fails?
724. How does Kubernetes reschedule stateful workloads?
725. What are the challenges of running databases on Kubernetes?

---

# 13. ConfigMaps and Secrets

726. What is a ConfigMap?
727. Why do we use ConfigMaps?
728. What types of data can ConfigMaps store?
729. How can a ConfigMap be consumed by a Pod?
730. How can ConfigMap values be exposed as environment variables?
731. How can ConfigMap data be mounted as files?
732. What happens when a ConfigMap changes?
733. Are ConfigMap environment variables automatically updated?
734. Are mounted ConfigMap files automatically updated?
735. What is a Secret?
736. Why should sensitive data be stored in Secrets?
737. Are Kubernetes Secrets encrypted by default in etcd?
738. How would you secure Secrets at rest?
739. How can Secrets be injected into Pods?
740. How can Secrets be mounted as files?
741. How can Secrets be exposed as environment variables?
742. What happens when a Secret changes?
743. What is the difference between ConfigMap and Secret?
744. What is `stringData`?
745. What is `data` in a Secret?
746. Why is Secret data base64 encoded?
747. Is base64 the same as encryption?
748. How would you prevent developers from reading production Secrets?
749. How does RBAC protect Secrets?
750. How do you rotate Kubernetes Secrets?
751. How do you troubleshoot an application receiving an old Secret value?
752. How would you integrate Kubernetes with an external secret manager?
753. What are the risks of storing Secrets directly in Git?
754. How would you design enterprise-grade Kubernetes secret management?
755. Can Secrets be mounted into init containers?
756. Can Secrets be mounted into multiple containers?
757. What happens if a referenced Secret does not exist?
758. What happens if a referenced ConfigMap does not exist?
759. How do ConfigMaps and Secrets affect rolling deployments?
760. How would you force Pods to reload changed configuration?

---

# 14. Security and RBAC

761. What is Kubernetes security architecture?
762. What is RBAC?
763. Why is RBAC important?
764. What are Role, ClusterRole, RoleBinding, and ClusterRoleBinding?
765. What is the difference between Role and ClusterRole?
766. What is the difference between RoleBinding and ClusterRoleBinding?
767. Can a RoleBinding reference a ClusterRole?
768. What is the principle of least privilege?
769. How do you give a user read-only access to one namespace?
770. How do you give a user access to multiple namespaces?
771. How do you allow a ServiceAccount to read Pods?
772. How do you allow a ServiceAccount to create Deployments?
773. How do you prevent a ServiceAccount from accessing Secrets?
774. What happens when RBAC permission is missing?
775. How do you troubleshoot a Kubernetes `Forbidden` error?
776. How do you check what permissions a user has?
777. What is `kubectl auth can-i`?
778. What is a ServiceAccount?
779. How does a Pod use a ServiceAccount?
780. What is the default ServiceAccount?
781. Should production workloads use the default ServiceAccount?
782. What is ServiceAccount token projection?
783. What is Pod Security?
784. What is Pod Security Admission?
785. What are Kubernetes Pod Security Standards?
786. What are Privileged, Baseline, and Restricted policies?
787. What is a privileged container?
788. Why are privileged containers dangerous?
789. What is Linux capability in Kubernetes?
790. How can capabilities be dropped from a container?
791. What is `runAsUser`?
792. What is `runAsNonRoot`?
793. Why should containers run as non-root?
794. What is a read-only root filesystem?
795. How can you enforce securityContext?
796. What is `allowPrivilegeEscalation`?
797. What is seccomp?
798. What is AppArmor?
799. What is SELinux?
800. How would you harden a Kubernetes cluster?
801. How would you secure the Kubernetes API server?
802. How would you secure etcd?
803. How would you secure worker nodes?
804. How would you secure container images?
805. How would you restrict container capabilities?
806. How would you prevent privileged Pods?
807. How would you prevent hostNetwork usage?
808. How would you prevent hostPath usage?
809. How would you restrict access to Secrets?
810. How would you implement network-level isolation?

---

# 15. NetworkPolicy

811. What is NetworkPolicy?
812. Why do we need NetworkPolicy?
813. Does Kubernetes NetworkPolicy work automatically without a supporting CNI?
814. What is ingress traffic in NetworkPolicy?
815. What is egress traffic in NetworkPolicy?
816. What happens when no NetworkPolicy exists?
817. How does NetworkPolicy change traffic behavior?
818. How do you allow only frontend Pods to access backend Pods?
819. How do you allow backend Pods to access database Pods?
820. How do you deny all ingress traffic to a namespace?
821. How do you deny all egress traffic?
822. How do you allow DNS traffic after applying default-deny egress?
823. How do namespace selectors work?
824. How do Pod selectors work?
825. How do IPBlock rules work?
826. Can NetworkPolicy filter traffic by port?
827. Can NetworkPolicy filter traffic by protocol?
828. What happens when multiple NetworkPolicies select the same Pod?
829. Are NetworkPolicies ordered?
830. How do you troubleshoot a NetworkPolicy blocking application traffic?
831. How would you design zero-trust networking in Kubernetes?
832. How would you isolate production and development namespaces?
833. How would you prevent one microservice from calling another?
834. How would you allow only specific service-to-service communication?
835. What are the limitations of Kubernetes NetworkPolicy?
836. What is the difference between NetworkPolicy and firewall rules?
837. What is the difference between NetworkPolicy and Security Groups?
838. What happens to DNS when egress is denied?
839. How do NetworkPolicies interact with Services?
840. How do NetworkPolicies interact with Ingress Controllers?

---

# 16. Resource Management

841. What is CPU request?
842. What is CPU limit?
843. What is memory request?
844. What is memory limit?
845. Why should production Pods have resource requests?
846. Why should production Pods have resource limits?
847. What happens when a container exceeds its CPU limit?
848. What happens when a container exceeds its memory limit?
849. What is CPU throttling?
850. How can CPU throttling affect application latency?
851. What is OOMKilled?
852. Why does a container get OOMKilled?
853. How do you troubleshoot OOMKilled?
854. What is a ResourceQuota?
855. Why do we use ResourceQuota?
856. What resources can ResourceQuota control?
857. What is LimitRange?
858. What is the difference between ResourceQuota and LimitRange?
859. How do you enforce default CPU requests?
860. How do you enforce default memory limits?
861. What happens if a namespace exceeds its ResourceQuota?
862. What is QoS classification?
863. How are QoS classes calculated?
864. Why is BestEffort QoS risky?
865. Why is Guaranteed QoS useful?
866. What happens during node memory pressure?
867. How does Kubernetes evict Pods?
868. What is an eviction?
869. What is an eviction threshold?
870. How do requests affect eviction priority?
871. How do limits affect eviction behavior?
872. What is ephemeral-storage?
873. How do you set ephemeral-storage requests?
874. How do you set ephemeral-storage limits?
875. What happens when node ephemeral storage is exhausted?

---

# 17. Autoscaling

876. What is HPA?
877. Why do we use HPA?
878. How does HPA work?
879. What metrics can HPA use?
880. What is CPU-based HPA?
881. What is memory-based HPA?
882. What are custom metrics?
883. What are external metrics?
884. What is Metrics Server?
885. Why does HPA need Metrics Server for resource metrics?
886. What happens if Metrics Server is unavailable?
887. How does HPA calculate desired replicas?
888. What is the relationship between CPU request and HPA CPU utilization?
889. Why can HPA fail to scale when CPU requests are missing?
890. What is `minReplicas`?
891. What is `maxReplicas`?
892. What is HPA scale target?
893. What is HPA stabilization?
894. Why can HPA cause scaling oscillation?
895. How do you prevent HPA flapping?
896. What is VPA?
897. What does VPA change?
898. What is the difference between HPA and VPA?
899. Can HPA and VPA be used together?
900. What is Cluster Autoscaler?
901. What does Cluster Autoscaler scale?
902. What causes Cluster Autoscaler to add nodes?
903. What causes Cluster Autoscaler to remove nodes?
904. What happens when Pods cannot be scheduled because of insufficient resources?
905. How does HPA interact with Cluster Autoscaler?
906. Can HPA scale Pods if the cluster has no capacity?
907. What happens when HPA increases replicas but no nodes are available?
908. How does Cluster Autoscaler react to Pending Pods?
909. What is node autoscaling?
910. How would you troubleshoot HPA not scaling?

---

# 18. Troubleshooting Pods and Containers

911. How do you troubleshoot a Pod in Pending state?
912. How do you troubleshoot a Pod in CrashLoopBackOff?
913. How do you troubleshoot ImagePullBackOff?
914. How do you troubleshoot ErrImagePull?
915. How do you troubleshoot CreateContainerConfigError?
916. How do you troubleshoot OOMKilled?
917. How do you troubleshoot a Pod stuck in Terminating?
918. How do you troubleshoot a Pod stuck in ContainerCreating?
919. How do you troubleshoot a Pod stuck in Init state?
920. How do you troubleshoot a Pod that repeatedly restarts?
921. What commands do you run first when troubleshooting a Pod?
922. When would you use `kubectl describe pod`?
923. When would you use `kubectl logs`?
924. When would you use `kubectl logs --previous`?
925. How do you inspect events for a Pod?
926. How do you inspect container exit codes?
927. How do you inspect the Pod specification?
928. How do you inspect environment variables?
929. How do you inspect mounted volumes?
930. How do you inspect container commands and arguments?
931. How do you troubleshoot an incorrect image tag?
932. How do you troubleshoot image registry authentication?
933. What is `imagePullSecrets`?
934. How do you troubleshoot private registry authentication?
935. What happens when an image tag does not exist?
936. What is `imagePullPolicy`?
937. What is the difference between `IfNotPresent` and `Always`?
938. How do you troubleshoot an application that starts and immediately exits?
939. How do you troubleshoot a container whose process is PID 1?
940. How do you troubleshoot incorrect CMD or ENTRYPOINT configuration?
941. How do you troubleshoot environment-variable-related application failures?
942. How do you troubleshoot Secret-related startup failures?
943. How do you troubleshoot ConfigMap-related startup failures?
944. How do you troubleshoot failed init containers?
945. How do you debug a running container without changing the image?
946. How do ephemeral containers help debugging?
947. How do you investigate a container's filesystem?
948. How do you investigate network connectivity from inside a Pod?
949. How do you investigate DNS from inside a Pod?
950. How do you investigate application listening ports inside a Pod?

The supplied scenario section explicitly asks about Pending Pods, Service routing failures, Node NotReady, CrashLoopBackOff, latency after scaling, and production incident diagnosis. 

---

# 19. Node Troubleshooting

951. What does Kubernetes Node `Ready` mean?
952. What causes a node to become NotReady?
953. How do you troubleshoot a NotReady node?
954. What is kubelet status?
955. How do you check kubelet logs?
956. What is node condition?
957. What are common node conditions?
958. What is MemoryPressure?
959. What is DiskPressure?
960. What is PIDPressure?
961. What is NetworkUnavailable?
962. What happens when a node experiences disk pressure?
963. What happens when a node experiences memory pressure?
964. What happens when kubelet crashes?
965. What happens when containerd crashes?
966. How do you troubleshoot container runtime failures?
967. How do you troubleshoot a node with high CPU?
968. How do you troubleshoot a node with high memory?
969. How do you troubleshoot a node with full disk?
970. How do you troubleshoot a node with inode exhaustion?
971. What is inode exhaustion?
972. How can log files cause disk pressure?
973. How can container images cause disk pressure?
974. How do you clean unused container images?
975. What happens when a node is cordoned?
976. What happens when a node is drained?
977. What is the difference between cordon and drain?
978. What does `kubectl cordon` do?
979. What does `kubectl drain` do?
980. Why is `--ignore-daemonsets` commonly required during drain?
981. What does `--delete-emptydir-data` do?
982. What happens to Pods managed by DaemonSets during drain?
983. What happens to Pods managed by Deployments during drain?
984. What happens to standalone Pods during drain?
985. How can PodDisruptionBudget prevent a drain?
986. How do you safely remove a node from production?
987. How do you replace a failed worker node?
988. What happens to workloads when a worker node disappears?
989. How long does Kubernetes wait before considering a node unhealthy?
990. Which controller handles node lifecycle?
991. How does Kubernetes reschedule Pods from failed nodes?
992. What happens if a Pod has local storage during node failure?
993. What happens if a Pod has a persistent volume during node failure?
994. How do topology constraints affect rescheduling?
995. How would you investigate a node failure during peak traffic?
996. How would you prevent a single node failure from causing application downtime?
997. How would you design node pools for different workloads?
998. How would you isolate system Pods from application Pods?
999. How would you isolate high-memory workloads?
1000. How would you isolate GPU workloads?

---

# 20. High Availability and Production Architecture

1001. How would you design a highly available Kubernetes cluster?
1002. How many control-plane nodes would you use for production?
1003. Why are three control-plane nodes commonly used?
1004. How would you make kube-apiserver highly available?
1005. How would you make etcd highly available?
1006. How would you make scheduler highly available?
1007. How would you make controller-manager highly available?
1008. What happens if one control-plane node fails?
1009. What happens if two control-plane nodes fail in a three-node control plane?
1010. What happens if all control-plane nodes fail?
1011. Can workloads continue running when the control plane is unavailable?
1012. What Kubernetes components are critical for application runtime?
1013. How would you design worker nodes across availability zones?
1014. Why should production worker nodes be distributed across zones?
1015. How would you prevent all replicas from running on one node?
1016. How would you prevent all replicas from running in one availability zone?
1017. What are topology spread constraints?
1018. How do Pod anti-affinity and topology spread differ?
1019. What is PodDisruptionBudget?
1020. Why do we need PDB?
1021. What is the difference between voluntary and involuntary disruption?
1022. Does PDB protect against node crashes?
1023. Does PDB protect against application crashes?
1024. Does PDB prevent Kubernetes from deleting Pods?
1025. How does PDB affect node draining?
1026. How would you configure PDB for a three-replica application?
1027. What happens if PDB is too restrictive?
1028. What happens if PDB is too permissive?
1029. How would you design a production Kubernetes cluster for zero downtime?
1030. How would you design a multi-AZ Kubernetes application?
1031. How would you design Kubernetes for 99.9% availability?
1032. How would you design Kubernetes for 99.99% availability?
1033. What are the major single points of failure in Kubernetes?
1034. How would you eliminate API server single points of failure?
1035. How would you eliminate worker-node single points of failure?
1036. How would you eliminate storage single points of failure?
1037. How would you eliminate networking single points of failure?
1038. How would you design failure domains in Kubernetes?
1039. How would you design Kubernetes for disaster recovery?
1040. What should be backed up in a Kubernetes cluster?
1041. Is backing up etcd alone sufficient for disaster recovery?
1042. How would you back up persistent application data?
1043. How would you test Kubernetes disaster recovery?
1044. What is RPO?
1045. What is RTO?
1046. How would you design Kubernetes according to an RPO requirement?
1047. How would you design Kubernetes according to an RTO requirement?
1048. What happens if the entire Kubernetes cluster is lost?
1049. How would you rebuild a Kubernetes cluster from scratch?
1050. How would you restore workloads after cluster recreation?

The production architecture material specifically emphasizes multi-AZ workers, highly available control plane, load balancing before API servers, etcd replication, separate node groups, autoscaling, centralized monitoring/logging, NetworkPolicies, backups, and multi-region recovery. 

---

# 21. Kubernetes Upgrade and Maintenance

1051. How do you upgrade a Kubernetes cluster safely?
1052. What should you check before a Kubernetes upgrade?
1053. Why should you read Kubernetes release notes before upgrading?
1054. How do you identify deprecated APIs before an upgrade?
1055. How do you identify incompatible workloads before an upgrade?
1056. What Kubernetes components need to be considered during an upgrade?
1057. Should control plane or worker nodes be upgraded first?
1058. Why is the control plane upgraded before worker nodes?
1059. What happens if worker nodes run an older Kubernetes version?
1060. What version skew is supported between control plane and kubelet?
1061. How do you upgrade worker nodes with minimal downtime?
1062. Why are cordon and drain used during node upgrades?
1063. What is a rolling node upgrade?
1064. What is an in-place node upgrade?
1065. What is a blue-green node-group upgrade?
1066. Why can creating a new node group be safer than upgrading existing nodes?
1067. How do you validate a Kubernetes upgrade?
1068. What should you validate after upgrading the control plane?
1069. What should you validate after upgrading worker nodes?
1070. How do you validate CoreDNS after an upgrade?
1071. How do you validate CNI after an upgrade?
1072. How do you validate kube-proxy after an upgrade?
1073. How do you validate workloads after an upgrade?
1074. How do you handle deprecated APIs during an upgrade?
1075. What happens if an application uses a removed API version?
1076. How do you roll back a failed Kubernetes upgrade?
1077. Can Kubernetes control-plane upgrades always be rolled back?
1078. How would you prepare a rollback strategy?
1079. How would you perform a canary node upgrade?
1080. How would you upgrade a production cluster without downtime?
1081. How do PDBs affect cluster upgrades?
1082. How do DaemonSets affect node draining?
1083. How do StatefulSets affect node draining?
1084. How do local-storage Pods affect node draining?
1085. How do static Pods affect node maintenance?
1086. How do you handle insufficient capacity during node upgrades?
1087. How do you handle workloads that cannot be evicted?
1088. How do you upgrade a cluster with critical stateful workloads?
1089. How do you verify that no workloads were accidentally disrupted?
1090. What metrics would you monitor during an upgrade?

The supplied upgrade document emphasizes pre-upgrade checks, version compatibility, add-ons, control-plane upgrade, worker-node migration using cordon/drain, and post-upgrade validation.  

---

# 22. Kubernetes Observability

1091. How do you monitor a Kubernetes cluster?
1092. What Kubernetes metrics should be monitored?
1093. What control-plane metrics are important?
1094. What node metrics are important?
1095. What Pod metrics are important?
1096. What container metrics are important?
1097. What application metrics are important?
1098. What is the difference between metrics, logs, and traces?
1099. What is Kubernetes event monitoring?
1100. How do you investigate Kubernetes events?
1101. How long are Kubernetes events retained?
1102. How do you collect container logs?
1103. Where are container logs stored on a node?
1104. How do you troubleshoot missing container logs?
1105. How do you monitor kubelet?
1106. How do you monitor kube-apiserver?
1107. How do you monitor etcd?
1108. How do you monitor scheduler?
1109. How do you monitor controller-manager?
1110. How do you monitor kube-proxy?
1111. How do you monitor CoreDNS?
1112. What metrics indicate API server overload?
1113. What metrics indicate etcd performance problems?
1114. What metrics indicate node pressure?
1115. What metrics indicate Pod resource exhaustion?
1116. What alerts would you configure for Kubernetes?
1117. How would you detect a high restart rate?
1118. How would you detect CrashLoopBackOff automatically?
1119. How would you detect Pods stuck Pending?
1120. How would you detect NotReady nodes?
1121. How would you detect failing readiness probes?
1122. How would you detect CPU throttling?
1123. How would you detect memory leaks?
1124. How would you detect DNS failures?
1125. How would you detect network packet loss?
1126. How would you detect API latency?
1127. How would you detect etcd quorum problems?
1128. How would you design Kubernetes observability for production?
1129. How would you correlate application latency with Kubernetes resource metrics?
1130. How would you investigate latency that starts immediately after a deployment?

---

# 23. Advanced Kubernetes Troubleshooting Scenarios

1131. A Pod is Pending; what is your complete troubleshooting approach?
1132. A Pod is Running but application is unreachable; what do you check?
1133. Pods are Running but Service has no endpoints; what do you check?
1134. Service has endpoints but traffic still fails; what do you check?
1135. Service works from one namespace but not another; what do you check?
1136. Pod-to-Pod communication fails across nodes; what do you check?
1137. Pod-to-Pod communication works but Service communication fails; what do you check?
1138. DNS resolution fails but direct IP communication works; what do you check?
1139. DNS works but application cannot connect to Service; what do you check?
1140. Ingress returns 404 while Service works; what do you check?
1141. Ingress returns 502 while Pods are healthy; what do you check?
1142. Ingress returns 503 while Pods are running; what do you check?
1143. LoadBalancer Service has no external IP; what do you check?
1144. A Deployment rollout is stuck; what do you check?
1145. A Deployment rollout causes increased latency; what do you check?
1146. New Pods are Ready but users still see errors; what do you investigate?
1147. Old Pods are not terminating during a rollout; why could that happen?
1148. New Pods never become Ready; what is your troubleshooting approach?
1149. A Pod keeps restarting every few seconds; how do you investigate?
1150. A Pod works manually but fails under Deployment; why could that happen?
1151. A Pod works in one namespace but not another; what could be different?
1152. Application configuration changed but Pods still use old values; what do you check?
1153. Secret was rotated but application still uses the old credential; what do you check?
1154. PVC is Pending; what is your troubleshooting process?
1155. PVC is Bound but Pod cannot mount it; what do you check?
1156. Volume attaches but does not mount; what do you check?
1157. StatefulSet Pod is stuck Pending; what could cause it?
1158. StatefulSet Pod starts on the wrong node; what scheduling rules do you inspect?
1159. Node becomes NotReady during peak traffic; what is your response?
1160. One worker node suddenly disappears; what happens to workloads?
1161. Three worker nodes fail simultaneously; how would you recover?
1162. Kubernetes nodes are Ready but application latency is high; what do you investigate?
1163. CPU usage is low but latency is high; what could be happening?
1164. CPU is throttled but usage appears normal; why?
1165. Memory usage keeps increasing; how do you investigate?
1166. Pods are OOMKilled after scaling; what could be wrong?
1167. HPA scales up but latency increases; why could scaling make things worse?
1168. HPA scales down and application becomes unstable; what do you investigate?
1169. Cluster Autoscaler is not adding nodes; what do you check?
1170. Cluster Autoscaler adds nodes but Pods remain Pending; why?
1171. Pods are evicted unexpectedly; what do you investigate?
1172. Pods cannot be drained from a node; what could block eviction?
1173. Node drain hangs indefinitely; how do you troubleshoot?
1174. kubelet is healthy but Pods cannot start; what do you investigate?
1175. kubelet is down but containers appear running; what happens?
1176. containerd is down; what happens to existing containers?
1177. containerd restarts repeatedly; how do you troubleshoot?
1178. CNI Pods are failing; what happens to new Pods?
1179. CoreDNS Pods are failing; what symptoms would users see?
1180. kube-proxy is failing; what symptoms would you expect?
1181. API server latency suddenly increases; how would you troubleshoot?
1182. API server returns 500 errors; what would you inspect?
1183. etcd latency increases; what impact could this have?
1184. etcd loses quorum; what is your recovery approach?
1185. Scheduler stops assigning Pods; what would you inspect?
1186. Controller-manager stops reconciling resources; what symptoms appear?
1187. Deployment replicas differ from desired replicas; what would you investigate?
1188. Service selector is correct but no endpoints exist; what could be wrong?
1189. Service endpoints exist but traffic reaches only one Pod; what could be wrong?
1190. Application works through Pod IP but not through Service IP; what would you check?
1191. Application works through Service IP but not through DNS; what would you check?
1192. Application works inside cluster but not from outside; what would you check?
1193. Application works externally but not internally; what would you investigate?
1194. One availability zone becomes unavailable; how does your Kubernetes design respond?
1195. How would you investigate a production outage immediately after a deployment?
1196. How would you distinguish application failure from Kubernetes infrastructure failure?
1197. How would you perform root-cause analysis for a Kubernetes outage?
1198. What evidence would you collect before restarting or deleting anything?
1199. How would you avoid making an incident worse during troubleshooting?
1200. How would you design preventive controls after resolving a Kubernetes incident?

---

# 24. Senior-Level Kubernetes System Design

1201. Design a production Kubernetes platform for a high-traffic application.
1202. Design Kubernetes for a 24×7 financial application.
1203. Design Kubernetes for a stateless microservices platform.
1204. Design Kubernetes for a stateful application platform.
1205. Design Kubernetes for 100 microservices.
1206. Design Kubernetes for 1,000 microservices.
1207. Design Kubernetes for multiple teams sharing one cluster.
1208. Design Kubernetes for strict tenant isolation.
1209. Design Kubernetes for development, staging, and production workloads.
1210. Would you use one cluster or multiple clusters for multiple environments?
1211. What factors determine whether to use one cluster or multiple clusters?
1212. How would you isolate production workloads from development workloads?
1213. How would you isolate teams within the same cluster?
1214. How would you enforce namespace-level security?
1215. How would you enforce network isolation between teams?
1216. How would you enforce resource limits between teams?
1217. How would you prevent noisy-neighbor problems?
1218. How would you design node pools for different workload classes?
1219. How would you design Kubernetes for burst traffic?
1220. How would you design Kubernetes for predictable traffic?
1221. How would you design Kubernetes for GPU workloads?
1222. How would you design Kubernetes for high-memory workloads?
1223. How would you design Kubernetes for CPU-intensive workloads?
1224. How would you design Kubernetes for batch workloads?
1225. How would you design Kubernetes for latency-sensitive workloads?
1226. How would you design Kubernetes for stateful databases?
1227. How would you design storage for multi-AZ workloads?
1228. How would you design cluster networking at large scale?
1229. How would you design Service discovery at large scale?
1230. How would you design Ingress for hundreds of services?
1231. How would you design API server high availability?
1232. How would you design etcd high availability?
1233. How would you design node high availability?
1234. How would you design application high availability?
1235. How would you design Kubernetes disaster recovery?
1236. How would you design Kubernetes backup architecture?
1237. How would you design Kubernetes monitoring?
1238. How would you design centralized Kubernetes logging?
1239. How would you design Kubernetes security?
1240. How would you design Kubernetes access control for hundreds of engineers?
1241. How would you design Kubernetes RBAC for multiple teams?
1242. How would you design Secret management?
1243. How would you design NetworkPolicies for microservices?
1244. How would you design zero-downtime deployments?
1245. How would you design safe cluster upgrades?
1246. How would you design automated node replacement?
1247. How would you design Kubernetes capacity planning?
1248. How would you determine the right number of worker nodes?
1249. How would you determine Pod density per node?
1250. How would you prevent cluster overcommitment?

---

# 25. Kubernetes Cross-Questions

1251. Why is a Deployment preferred over a naked Pod?
1252. Why is a Service required when Pods already have IP addresses?
1253. Why is Ingress required when Services already expose applications?
1254. Why use ClusterIP behind Ingress?
1255. Why use LoadBalancer with Ingress?
1256. Why does Ingress normally route to a Service instead of directly to a Pod?
1257. Why use StatefulSet instead of Deployment for databases?
1258. Why use DaemonSet instead of Deployment for node agents?
1259. Why use Job instead of Deployment for batch processing?
1260. Why use CronJob instead of Job?
1261. Why use PVC instead of mounting hostPath?
1262. Why use StorageClass instead of manually creating PVs?
1263. Why use ConfigMap instead of hardcoding configuration?
1264. Why use Secret instead of ConfigMap for sensitive data?
1265. Why use readiness probe instead of only liveness probe?
1266. Why use startup probe if readiness already exists?
1267. Why use HPA instead of simply increasing replicas manually?
1268. Why use VPA if HPA already exists?
1269. Why use Cluster Autoscaler if HPA scales Pods?
1270. Why use node affinity when nodeSelector exists?
1271. Why use Pod anti-affinity when topology spread constraints exist?
1272. Why use taints when node affinity exists?
1273. Why use tolerations together with taints?
1274. Why use NetworkPolicy if RBAC already exists?
1275. Why use RBAC if NetworkPolicy already isolates traffic?
1276. Why use PDB if Deployment already maintains replicas?
1277. Why use multiple replicas if Kubernetes automatically restarts failed Pods?
1278. Why use multiple availability zones?
1279. Why use multiple control-plane nodes?
1280. Why use an odd number of etcd members?
1281. Why does Kubernetes use etcd instead of a relational database?
1282. Why does Kubernetes need controllers if users already define desired state?
1283. Why does Kubernetes need scheduler if kubelet already runs Pods?
1284. Why does kubelet need the API server?
1285. Why does kube-proxy need Services?
1286. Why does Kubernetes need CNI?
1287. Why does Kubernetes need CRI?
1288. Why is kube-apiserver the central communication point?
1289. Why should users not directly modify etcd?
1290. Why should Kubernetes resources be managed declaratively?

---

# 26. Architecture Flow Questions

1291. Walk through what happens when `kubectl create deployment nginx --image=nginx` is executed.
1292. Walk through what happens when a Deployment with three replicas is created.
1293. Which component receives the request first?
1294. Which component authenticates the request?
1295. Which component authorizes the request?
1296. Which component validates the object?
1297. Where is the Deployment stored?
1298. Who notices that the Deployment needs a ReplicaSet?
1299. Who creates the ReplicaSet?
1300. Who creates the Pods?
1301. Who notices that the Pods are unscheduled?
1302. Who assigns the Pods to nodes?
1303. Who notices the node assignment?
1304. Who asks the container runtime to start the containers?
1305. Who pulls the image?
1306. Where does the image come from?
1307. How does the Pod receive an IP?
1308. How does the Pod become Ready?
1309. How does the Service discover the Pod?
1310. How does external traffic eventually reach the Pod?
1311. What happens if the scheduler is down during Pod creation?
1312. What happens if controller-manager is down during Deployment creation?
1313. What happens if kubelet is down after scheduling?
1314. What happens if containerd is down after scheduling?
1315. What happens if CNI is down after scheduling?
1316. What happens if CoreDNS is down after the Pod starts?
1317. What happens if kube-proxy is down after the Service exists?
1318. What happens if API server goes down after Pods are running?
1319. What happens if etcd goes down after Pods are running?
1320. Which parts of the request flow are synchronous?
1321. Which parts of the Kubernetes control loop are asynchronous?
1322. Where does reconciliation occur?
1323. How does Kubernetes recover from temporary component failures?
1324. Why is eventual reconciliation important?
1325. What happens if the actual state differs from desired state for an extended period?

---

# 27. Kubernetes Command-Based Interview Questions

1326. How do you list all nodes?
1327. How do you list all Pods?
1328. How do you list Pods across all namespaces?
1329. How do you list all Deployments?
1330. How do you list all Services?
1331. How do you list all ReplicaSets?
1332. How do you list all StatefulSets?
1333. How do you list all DaemonSets?
1334. How do you list all Jobs?
1335. How do you list all CronJobs?
1336. How do you list all namespaces?
1337. How do you describe a Pod?
1338. How do you describe a node?
1339. How do you view Pod logs?
1340. How do you view logs from the previous container instance?
1341. How do you execute a command inside a Pod?
1342. How do you open an interactive shell inside a Pod?
1343. How do you copy files from a Pod?
1344. How do you copy files into a Pod?
1345. How do you inspect Pod YAML?
1346. How do you inspect Deployment YAML?
1347. How do you edit a Kubernetes resource?
1348. How do you delete a Pod?
1349. How do you delete a Deployment?
1350. How do you scale a Deployment?
1351. How do you restart a Deployment?
1352. How do you check Deployment rollout status?
1353. How do you check Deployment rollout history?
1354. How do you roll back a Deployment?
1355. How do you cordon a node?
1356. How do you drain a node?
1357. How do you uncordon a node?
1358. How do you label a node?
1359. How do you taint a node?
1360. How do you remove a taint?
1361. How do you check node labels?
1362. How do you check node taints?
1363. How do you check resource usage?
1364. How do you inspect Kubernetes events?
1365. How do you check API connectivity?
1366. How do you check current Kubernetes context?
1367. How do you switch Kubernetes context?
1368. How do you check your RBAC permissions?
1369. How do you check Service endpoints?
1370. How do you check EndpointSlices?
1371. How do you inspect a PVC?
1372. How do you inspect a PV?
1373. How do you inspect a StorageClass?
1374. How do you inspect a NetworkPolicy?
1375. How do you inspect an Ingress?
1376. How do you inspect HPA?
1377. How do you inspect ResourceQuota?
1378. How do you inspect LimitRange?
1379. How do you inspect PDB?
1380. How do you watch Kubernetes resources in real time?

---

# 28. Advanced Production Incident Questions

1381. Production traffic suddenly drops to zero; how do you investigate?
1382. Production traffic suddenly returns 503; how do you investigate?
1383. All Pods are Running but users receive errors; what could be wrong?
1384. All Pods are Ready but users receive timeouts; what could be wrong?
1385. Service has healthy endpoints but external traffic fails; what do you investigate?
1386. Ingress is healthy but backend Pods return errors; what do you investigate?
1387. Application latency increases after adding more replicas; why could that happen?
1388. Application latency increases after a node replacement; what could be wrong?
1389. Application latency increases after a CNI change; what could be wrong?
1390. Application latency increases after a Kubernetes upgrade; what do you investigate?
1391. All nodes are healthy but scheduling becomes slow; what do you investigate?
1392. API requests become slow only during deployments; why could this happen?
1393. Kubernetes API server CPU is high; what would you investigate?
1394. etcd CPU is high; what would you investigate?
1395. etcd disk latency is high; what impact could it have?
1396. Scheduler CPU is high; what would you investigate?
1397. Controller-manager CPU is high; what would you investigate?
1398. kubelet CPU is high on one node; what would you investigate?
1399. kube-proxy CPU is high; what would you investigate?
1400. CoreDNS CPU is high; what would you investigate?
1401. CoreDNS latency is high; what would you investigate?
1402. Pods intermittently fail DNS resolution; how would you investigate?
1403. Pods intermittently lose network connectivity; how would you investigate?
1404. Only cross-node traffic fails; how would you investigate?
1405. Only external traffic fails; how would you investigate?
1406. Only internal Service traffic fails; how would you investigate?
1407. Only one namespace experiences networking problems; what could explain it?
1408. Only one node experiences networking problems; what could explain it?
1409. Only newly created Pods have networking issues; what could explain it?
1410. Existing Pods work but newly scheduled Pods cannot communicate; what would you investigate?
1411. A node has plenty of CPU but Pods remain Pending; why?
1412. A node has plenty of memory but Pods remain Pending; why?
1413. A cluster has sufficient aggregate resources but Pods remain Pending; why?
1414. HPA shows unknown metrics; what would you investigate?
1415. HPA suddenly scales to maximum replicas; what would you investigate?
1416. HPA suddenly scales down to minimum; what would you investigate?
1417. Cluster Autoscaler does not remove unused nodes; what would you investigate?
1418. Cluster Autoscaler repeatedly adds and removes nodes; what could cause this?
1419. Pods are repeatedly evicted; what would you investigate?
1420. Nodes repeatedly become NotReady and Ready; what would you investigate?

---

# 29. Disaster Recovery

1421. What is Kubernetes disaster recovery?
1422. What Kubernetes data must be backed up?
1423. Why should etcd be backed up?
1424. What is an etcd snapshot?
1425. How do you verify an etcd backup?
1426. How do you restore etcd?
1427. What happens if etcd backup is corrupted?
1428. Should backups be stored on the same cluster?
1429. How would you protect backups from accidental deletion?
1430. How would you encrypt Kubernetes backups?
1431. How do you back up PV data?
1432. How do you restore PV data?
1433. How do you restore Kubernetes manifests?
1434. Can Git be used to reconstruct Kubernetes configuration?
1435. Is Git alone sufficient for disaster recovery of stateful applications?
1436. How would you design a multi-region Kubernetes recovery strategy?
1437. What is active-passive Kubernetes disaster recovery?
1438. What is active-active Kubernetes disaster recovery?
1439. What are the trade-offs between active-active and active-passive?
1440. How would you handle DNS during multi-region failover?
1441. How would you handle persistent data during multi-region failover?
1442. How would you prevent split-brain?
1443. How would you test a disaster recovery plan?
1444. How frequently should restore testing be performed?
1445. What is the difference between backup and disaster recovery?
1446. What is the difference between high availability and disaster recovery?
1447. Can a highly available cluster survive a complete region failure?
1448. What happens if the entire control plane is lost?
1449. How would you recover a cluster when etcd is lost?
1450. How would you recover application state after cluster recreation?

---

# 30. Expert-Level Kubernetes Questions

1451. Explain Kubernetes reconciliation architecture in depth.
1452. Explain the complete Kubernetes control loop.
1453. Explain how Kubernetes achieves eventual consistency.
1454. Explain how controllers use informers and watches.
1455. What is an informer?
1456. What is a work queue?
1457. Why do controllers use work queues?
1458. What is a Kubernetes finalizer?
1459. Why can a resource remain stuck in Terminating because of a finalizer?
1460. How do you troubleshoot a resource stuck because of a finalizer?
1461. What is garbage collection in Kubernetes?
1462. What are owner references?
1463. What is cascading deletion?
1464. What is foreground deletion?
1465. What is background deletion?
1466. What is orphan deletion?
1467. What is optimistic concurrency in Kubernetes?
1468. What is `resourceVersion`?
1469. What is `generation`?
1470. What is `observedGeneration`?
1471. Why does Kubernetes use resource versions?
1472. What causes a Kubernetes update conflict?
1473. How do you troubleshoot `the object has been modified` errors?
1474. What is server-side apply?
1475. What is client-side apply?
1476. What is field ownership?
1477. What is a managed field?
1478. How does Kubernetes handle conflicting field ownership?
1479. What is a mutating admission webhook?
1480. What is a validating admission webhook?
1481. What is the difference between mutating and validating admission?
1482. What happens if an admission webhook is unavailable?
1483. What is `failurePolicy` for admission webhooks?
1484. What are the risks of poorly designed admission webhooks?
1485. What is a Kubernetes operator?
1486. How does an operator use CRDs and controllers?
1487. What is a Custom Resource?
1488. What is a CustomResourceDefinition?
1489. How does Kubernetes API discovery work?
1490. What is API aggregation?
1491. What is an aggregated API server?
1492. What is a webhook-based admission controller?
1493. What is a dynamic admission controller?
1494. What is a static Pod?
1495. How are control-plane static Pods bootstrapped?
1496. What happens when kube-apiserver itself is a static Pod?
1497. How can kubelet start kube-apiserver if API server is not yet available?
1498. How does Kubernetes bootstrap its own control plane?
1499. How would you debug a control-plane bootstrap failure?
1500. Explain Kubernetes architecture as if you were designing it from scratch.
