# CI/CD Fundamentals — What should an 8-year DevOps engineer be able to answer? 

1. What is CI/CD?
2. What is Continuous Integration?
3. What is Continuous Delivery?
4. What is Continuous Deployment?
5. What is the difference between Continuous Delivery and Continuous Deployment?
6. What problems does CI solve?
7. What problems does CD solve?
8. Why is CI/CD important in DevOps?
9. What is the difference between CI, Continuous Delivery, Continuous Deployment, and Continuous Release?
10. What is a CI/CD pipeline?
11. What are the typical stages of a CI/CD pipeline?
12. What happens from developer commit to production deployment?
13. What is the difference between a pipeline, stage, job, task, and step?
14. What is a build artifact?
15. Why should artifacts be immutable?
16. What is artifact promotion?
17. Why should the same artifact be promoted across environments?
18. What is the difference between source deployment and artifact deployment?
19. What is a build once, deploy many strategy?
20. What is pipeline-as-code?
21. Why should CI/CD configuration be stored in Git?
22. What is the role of Git in CI/CD?
23. How does a Git push trigger a CI/CD pipeline?
24. What is a webhook?
25. How does a webhook differ from polling?
26. What is the difference between pull-based and push-based CI/CD?
27. What is trunk-based development?
28. What is GitFlow?
29. How would you design CI/CD for GitFlow?
30. How would you design CI/CD for trunk-based development?
31. How should feature branches be handled in CI/CD?
32. How should pull requests be handled in CI/CD?
33. What should run on every pull request?
34. What should run only after merging to the main branch?
35. What should run before production deployment?
36. How would you design a CI/CD pipeline for development, staging, and production?
37. How would you prevent broken code from reaching production?
38. What is a quality gate?
39. What is a deployment gate?
40. What is an approval gate?
41. What is a manual gate?
42. What is automated promotion?
43. When should manual approval be used?
44. When should manual approval be avoided?
45. What is pipeline orchestration?
46. What is pipeline idempotency?
47. Why should deployment pipelines be idempotent?
48. What is pipeline reproducibility?
49. How do you make a build reproducible?
50. What is environment parity?
51. How do you prevent "works on my machine" problems?
52. What is shift-left testing?
53. What is shift-left security?
54. Where should unit testing occur in a CI/CD pipeline?
55. Where should integration testing occur?
56. Where should security scanning occur?
57. Where should DAST occur?
58. Where should container scanning occur?
59. Where should infrastructure validation occur?
60. How do you decide the order of pipeline stages?
61. How do you reduce CI/CD feedback time?
62. What are the characteristics of a good CI/CD pipeline?
63. What are common CI/CD anti-patterns?
64. How do you measure CI/CD maturity?
65. What are DORA metrics?
66. What is deployment frequency?
67. What is lead time for changes?
68. What is change failure rate?
69. What is mean time to restore?
70. How would you improve DORA metrics?
71. How do you measure pipeline efficiency?
72. How do you calculate CI/CD pipeline success rate?
73. How do you calculate deployment failure rate?
74. How do you identify the slowest stage in a pipeline?
75. How would you design a pipeline for hundreds of microservices?
76. How would you design CI/CD for a monolithic application?
77. How would you design CI/CD for microservices?
78. How would you design CI/CD for a monorepo?
79. How would you design CI/CD for multiple repositories?
80. How would you handle dependencies between multiple repositories?
81. How do you handle versioning in CI/CD?
82. What is semantic versioning?
83. How should Git tags be used in CI/CD?
84. How would you automatically generate release versions?
85. How would you prevent two pipelines from deploying conflicting versions?
86. How would you implement rollback in CI/CD?
87. What is rollback versus roll-forward?
88. When would you choose rollback over roll-forward?
89. How would you design zero-downtime deployments?
90. What is blue-green deployment?
91. What is canary deployment?
92. What is rolling deployment?
93. What is recreate deployment?
94. What is feature-flag-based deployment?
95. How do blue-green and canary deployments differ?
96. How would you integrate feature flags into CI/CD?
97. How would you deploy database changes safely?
98. How do you handle backward-compatible database migrations?
99. How do you handle database rollback?
100. How would you deploy an application when database changes are not backward compatible?

# Jenkins Architecture — What Jenkins questions should an experienced DevOps engineer expect? ([Jenkins][1])

101. What is Jenkins?
102. Why is Jenkins used in CI/CD?
103. What are the major components of Jenkins?
104. What is a Jenkins controller?
105. What is a Jenkins agent?
106. What is an executor?
107. What is the difference between a node and an executor?
108. How does Jenkins distribute jobs to agents?
109. What happens when all Jenkins executors are busy?
110. What happens when no suitable Jenkins agent is available?
111. What is the Jenkins built-in node?
112. Why should production builds generally not run on the Jenkins controller?
113. How would you design a Jenkins controller-agent architecture?
114. How would you scale Jenkins horizontally?
115. How would you handle 500 concurrent Jenkins builds?
116. How do you decide how many executors an agent should have?
117. What is the relationship between CPU, memory, executors, and build performance?
118. What happens if you configure too many executors on one agent?
119. What happens if you configure too few executors?
120. How would you isolate workloads between Jenkins agents?
121. How would you create dedicated agents for Docker builds?
122. How would you create dedicated agents for Terraform?
123. How would you create dedicated agents for Kubernetes?
124. How would you create dedicated agents for Windows builds?
125. How would you dynamically provision Jenkins agents?
126. How would you integrate Jenkins with Kubernetes?
127. What are ephemeral Jenkins agents?
128. What are the advantages of ephemeral agents?
129. What are the disadvantages of ephemeral agents?
130. How would you implement Jenkins agents using Kubernetes pods?
131. What happens if a Jenkins agent dies during a build?
132. How would you recover a failed Jenkins agent?
133. How would you troubleshoot a Jenkins agent that is offline?
134. How would you troubleshoot an agent that connects but cannot execute jobs?
135. What is the difference between inbound and outbound Jenkins agents?
136. What is WebSocket-based Jenkins agent communication?
137. When would you use WebSocket agents?
138. How would you secure Jenkins agent communication?
139. How would you isolate untrusted builds from trusted builds?
140. How would you prevent one Jenkins job from affecting another job?

# Jenkins Jobs and Pipeline — What Jenkins pipeline questions should you master? ([Jenkins][1])

141. What is a Jenkins job?
142. What is a Freestyle project?
143. What is a Pipeline job?
144. What is a Multibranch Pipeline?
145. What is an Organization Folder?
146. What is the difference between Freestyle and Pipeline?
147. What is a Jenkinsfile?
148. Why should a Jenkinsfile be stored in Git?
149. What is Pipeline as Code?
150. What is Declarative Pipeline?
151. What is Scripted Pipeline?
152. What is the difference between Declarative and Scripted Pipeline?
153. When would you choose Declarative Pipeline?
154. When would you choose Scripted Pipeline?
155. Can Declarative Pipeline contain Scripted Pipeline code?
156. What is the `pipeline` block?
157. What is an `agent`?
158. What is `agent any`?
159. What is a stage?
160. What is a step?
161. What is the difference between stage and step?
162. What is `stages`?
163. What is `steps`?
164. What is `post`?
165. What are the different conditions available inside `post`?
166. What is `always` in Jenkins?
167. What is `success` in Jenkins?
168. What is `failure` in Jenkins?
169. What is `unstable`?
170. What is `changed`?
171. What is `aborted`?
172. What is `cleanup`?
173. What is the `when` directive?
174. How do you execute a stage only on a specific branch?
175. How do you execute a stage only when a tag is created?
176. How do you execute a stage only for pull requests?
177. How do you execute a stage only when a condition is true?
178. What is the `input` directive?
179. How does manual approval work in Jenkins?
180. How do you implement production approval in Jenkins?
181. How do you restrict who can approve a production deployment?
182. What happens to the pipeline while it is waiting for `input`?
183. How do you implement timeout for manual approval?
184. What happens if approval is rejected?
185. What is the `environment` block?
186. What is the difference between global and stage-level environment variables?
187. How do you define environment variables dynamically?
188. How do you pass values between Jenkins stages?
189. What is `params` in Jenkins?
190. What is a parameterized Jenkins build?
191. What is the difference between parameters and environment variables?
192. How do you pass a parameter from Jenkins UI into a pipeline?
193. How do you validate Jenkins parameters?
194. What is `options` in Declarative Pipeline?
195. What is `timeout`?
196. What is `retry`?
197. What is `timestamps()`?
198. What is `disableConcurrentBuilds()`?
199. What is `buildDiscarder()`?
200. What is `skipDefaultCheckout()`?
201. What is `preserveStashes()`?
202. What is `quietPeriod`?
203. What is `retry` versus rerunning the entire Jenkins build?
204. How would you retry only a failed deployment step?
205. How would you prevent overlapping production deployments?
206. How would you cancel an older deployment when a newer deployment starts?
207. How would you prevent duplicate builds?
208. What is Jenkins `parallel`?
209. How do you run multiple stages in parallel?
210. What are the advantages of parallel stages?
211. What are the risks of parallel stages?
212. What is `failFast`?
213. How would you run unit tests, security scans, and linting in parallel?
214. How would you run tests across multiple versions of Node.js in parallel?
215. What is a Jenkins matrix?
216. How is matrix execution different from parallel execution?
217. How would you build a Jenkins pipeline for multiple environments?
218. How would you make a Jenkins pipeline reusable across 100 repositories?
219. What are Jenkins Shared Libraries?
220. Why would you use Shared Libraries?
221. How do you create a Shared Library?
222. How do you version a Jenkins Shared Library?
223. How do you prevent breaking changes in a Shared Library?
224. How do you test a Jenkins Shared Library?
225. What is the difference between global and folder-level Shared Libraries?
226. How would you migrate duplicated Jenkinsfiles into a Shared Library?
227. What are the risks of Jenkins Shared Libraries?
228. How would you secure a Shared Library?
229. How would you debug a Shared Library?
230. How would you design a centralized CI/CD framework using Jenkins Shared Libraries?

# Jenkins SCM and Git Integration — What Git/Jenkins integration questions can be asked?

231. How do you integrate Jenkins with GitHub?
232. How do you integrate Jenkins with GitLab?
233. How do you integrate Jenkins with Bitbucket?
234. How does Jenkins detect a Git change?
235. What is a Jenkins webhook?
236. What is SCM polling?
237. Webhook versus polling: which would you choose and why?
238. How do you configure a GitHub webhook for Jenkins?
239. What happens when a GitHub webhook reaches Jenkins?
240. How do you prevent duplicate builds caused by multiple webhook events?
241. How do you trigger Jenkins only for specific branches?
242. How do you trigger Jenkins only for pull requests?
243. How does Multibranch Pipeline discover branches?
244. How does Multibranch Pipeline discover pull requests?
245. What is branch indexing?
246. What happens if Jenkins branch indexing fails?
247. How would you troubleshoot Jenkins not detecting a new branch?
248. How would you troubleshoot Jenkins not detecting a pull request?
249. How do you authenticate Jenkins to GitHub?
250. SSH key versus HTTPS token for Jenkins Git authentication?
251. How do you securely store Git credentials in Jenkins?
252. How would you configure Jenkins to checkout a private repository?
253. What is shallow clone?
254. When would you use shallow clone in Jenkins?
255. How do you optimize Git checkout performance?
256. How would you handle Git submodules in Jenkins?
257. How would you handle Git LFS in Jenkins?
258. How would you build only the services changed in a monorepo?
259. How would you detect changed files in Jenkins?
260. How would you trigger different pipelines based on changed directories?

# Jenkins Credentials and Secrets — What security questions should an 8-year engineer expect? ([Jenkins][2])

261. How does Jenkins manage credentials?
262. What types of credentials can Jenkins store?
263. Where should passwords be stored in Jenkins?
264. How do you store SSH private keys in Jenkins?
265. How do you store AWS credentials in Jenkins?
266. How do you store Kubernetes credentials in Jenkins?
267. How do you use credentials inside a Jenkinsfile?
268. What is `credentials()` in Jenkins?
269. What is `withCredentials`?
270. What is credential binding?
271. How does Jenkins mask secrets in console logs?
272. Can Jenkins guarantee that a secret can never be exposed in logs?
273. How can shell commands accidentally leak Jenkins secrets?
274. How would you prevent secrets from appearing in `set -x` output?
275. How would you rotate Jenkins credentials?
276. How do you restrict credentials to a specific folder?
277. How do you restrict credentials to a specific pipeline?
278. What is the principle of least privilege for Jenkins credentials?
279. What happens if a Jenkins administrator credential is compromised?
280. How would you respond to a leaked Jenkins credential?
281. How would you audit Jenkins credential usage?
282. How would you integrate Jenkins with HashiCorp Vault?
283. How would you integrate Jenkins with AWS Secrets Manager?
284. How would you avoid long-lived cloud credentials in Jenkins?
285. How would you implement short-lived credentials in Jenkins?
286. How would you secure credentials on ephemeral agents?
287. Can credentials be exposed through malicious pull requests?
288. How would you secure Jenkins pipelines for untrusted pull requests?
289. How would you prevent a developer from accessing production credentials through Jenkins?
290. How would you separate development, staging, and production credentials?

# Jenkins Security and Administration — What advanced Jenkins security questions can be asked? ([Jenkins][3])

291. How do you secure Jenkins?
292. What is Jenkins RBAC?
293. What is Matrix-based authorization?
294. What is Role-Based Authorization Strategy?
295. Authentication versus authorization in Jenkins?
296. What is a Jenkins Security Realm?
297. How would you integrate Jenkins with LDAP?
298. How would you integrate Jenkins with Active Directory?
299. How would you integrate Jenkins with SSO?
300. How would you integrate Jenkins with OAuth?
301. What is CSRF protection in Jenkins?
302. What is a Jenkins crumb?
303. Why can Jenkins API calls fail because of CSRF protection?
304. How would you troubleshoot a Jenkins API call returning a 403 crumb error?
305. How do you secure Jenkins behind a reverse proxy?
306. How do you expose Jenkins securely over HTTPS?
307. Which Jenkins ports need to be exposed?
308. How would you restrict Jenkins network access?
309. How would you secure Jenkins from the public internet?
310. How do you harden the Jenkins controller?
311. Why should Jenkins plugins be regularly updated?
312. How do you handle a vulnerable Jenkins plugin?
313. How would you identify vulnerable Jenkins plugins?
314. How would you safely upgrade Jenkins?
315. How do you handle Jenkins LTS upgrades?
316. How would you test a Jenkins upgrade before production?
317. How would you roll back a Jenkins upgrade?
318. What is Jenkins Configuration as Code?
319. How would you manage Jenkins configuration as code?
320. How would you manage Jenkins plugins as code?
321. How would you automate Jenkins installation?
322. How would you provision Jenkins using Terraform?
323. How would you provision Jenkins using Ansible?
324. How would you manage Jenkins configuration across environments?
325. How would you prevent configuration drift in Jenkins?
326. How would you secure Jenkins Script Console?
327. Why is Jenkins Script Console dangerous?
328. What permissions should be given to Jenkins administrators?
329. What is the security risk of allowing users to configure jobs?
330. How would you isolate Jenkins controllers for different teams?

# Jenkins Artifacts, Workspace and Storage — What artifact-management questions should you know?

331. What is a Jenkins workspace?
332. How is a workspace created?
333. Where is the Jenkins workspace stored?
334. What happens to the workspace after a build?
335. What is `cleanWs()`?
336. Why would you clean a Jenkins workspace?
337. What is workspace pollution?
338. How would you troubleshoot a build that works on one Jenkins agent but fails on another?
339. What is `archiveArtifacts`?
340. Why do we archive artifacts?
341. What is the difference between archived artifacts and workspace files?
342. What is an artifact repository?
343. Jenkins artifact archive versus Nexus?
344. Jenkins artifact archive versus JFrog Artifactory?
345. How would you integrate Jenkins with Nexus?
346. How would you integrate Jenkins with Artifactory?
347. How would you publish a Docker image from Jenkins?
348. How would you publish a Maven artifact from Jenkins?
349. How would you publish an npm package from Jenkins?
350. How would you promote artifacts between environments?
351. How do you prevent rebuilding an artifact for production?
352. How do you retain artifacts for compliance?
353. How do you automatically delete old artifacts?
354. How would you handle a Jenkins controller running out of disk space?
355. How would you handle a Jenkins agent running out of disk space?
356. How would you optimize Jenkins workspace storage?
357. What is `stash` in Jenkins?
358. What is `unstash` in Jenkins?
359. What is the difference between `stash`, `archiveArtifacts`, and an artifact repository?
360. When should you avoid using Jenkins `stash` for large artifacts?

# Jenkins Notifications and Observability — What operational questions can be asked?

361. How do you send Jenkins notifications to Slack?
362. How do you send Jenkins notifications to email?
363. How do you send Jenkins notifications to Microsoft Teams?
364. How do you notify developers only when a pipeline fails?
365. How do you notify only when a previously successful build becomes failed?
366. How do you notify the deployment team after production deployment?
367. How would you integrate Jenkins with PagerDuty?
368. How would you monitor Jenkins?
369. What Jenkins metrics should be monitored?
370. How do you monitor executor utilization?
371. How do you monitor queue length?
372. How do you monitor build duration?
373. How do you monitor failed builds?
374. How do you monitor agent availability?
375. How do you monitor Jenkins disk usage?
376. How do you monitor Jenkins JVM memory?
377. How do you monitor Jenkins CPU?
378. How do you monitor Jenkins thread usage?
379. How would you integrate Jenkins with Prometheus?
380. How would you integrate Jenkins with Grafana?
381. How would you detect a Jenkins performance bottleneck?
382. How would you troubleshoot Jenkins becoming slow?
383. How would you troubleshoot Jenkins UI becoming unresponsive?
384. How would you troubleshoot Jenkins builds getting stuck in queue?
385. How would you troubleshoot Jenkins builds taking twice as long as before?

# Jenkins Failure and Troubleshooting — What real-world troubleshooting scenarios should you prepare for?

386. A Jenkins job is stuck in the queue; how would you troubleshoot it?
387. A Jenkins job says "Waiting for next available executor"; what would you check?
388. Jenkins cannot find an available agent; how would you troubleshoot it?
389. A Jenkins agent suddenly goes offline; what would you check?
390. A Jenkins agent is online but the build never starts; how would you troubleshoot it?
391. Jenkins can connect to GitHub but checkout fails; how would you troubleshoot it?
392. Jenkins cannot authenticate to GitHub; how would you troubleshoot it?
393. Jenkins webhook is configured but builds are not triggering; how would you troubleshoot it?
394. Jenkins is triggering the same build multiple times; how would you troubleshoot it?
395. Jenkins is triggering builds for the wrong branch; how would you troubleshoot it?
396. Jenkins Multibranch Pipeline is not discovering a branch; how would you troubleshoot it?
397. Jenkins Multibranch Pipeline is not discovering a pull request; how would you troubleshoot it?
398. Jenkinsfile is present but Jenkins says it cannot find it; how would you troubleshoot it?
399. Jenkinsfile syntax validation fails; how would you troubleshoot it?
400. A pipeline fails only on Jenkins but works locally; how would you troubleshoot it?
401. A pipeline works on one agent but fails on another; how would you troubleshoot it?
402. A pipeline suddenly starts failing after a plugin update; how would you troubleshoot it?
403. A pipeline suddenly starts failing after a Java update; how would you troubleshoot it?
404. Jenkins controller CPU is at 100%; how would you troubleshoot it?
405. Jenkins controller memory is exhausted; how would you troubleshoot it?
406. Jenkins disk is full; how would you recover the system?
407. Jenkins build logs are extremely slow; how would you troubleshoot them?
408. Jenkins builds are randomly failing; how would you identify the root cause?
409. Jenkins builds are hanging indefinitely; how would you troubleshoot them?
410. Jenkins pipeline is stuck at an `input` step; how would you investigate it?
411. Jenkins pipeline fails during credential binding; what would you check?
412. Jenkins credentials are not available to a pipeline; how would you troubleshoot it?
413. Jenkins secret is appearing in logs; how would you fix it?
414. Jenkins cannot connect to an SSH deployment server; how would you troubleshoot it?
415. Jenkins SSH deployment works manually but fails in the pipeline; why could that happen?
416. Jenkins Docker build fails with permission denied; how would you troubleshoot it?
417. Jenkins Docker agent cannot start; how would you troubleshoot it?
418. Jenkins Kubernetes agent remains pending; how would you troubleshoot it?
419. Jenkins Kubernetes agent starts and immediately terminates; how would you troubleshoot it?
420. Jenkins pipeline fails after a node restart; how would you investigate it?
421. Jenkins loses pipeline state after restart; what would you check?
422. Jenkins controller crashes during a production deployment; how would you recover?
423. A production deployment succeeds but Jenkins reports failure; how would you investigate?
424. Jenkins reports success but the application was not deployed; how would you investigate?
425. Jenkins deployment partially succeeds; how would you recover safely?
426. Two Jenkins pipelines deploy to production simultaneously; how would you prevent this?
427. Jenkins pipeline is consuming excessive disk space; how would you optimize it?
428. Jenkins queue is continuously growing; how would you identify the bottleneck?
429. Jenkins agents are underutilized but builds remain queued; what could cause this?
430. Jenkins agents have capacity but jobs still cannot run; what would you check?

# Jenkins Production Architecture — What senior-level Jenkins design questions can be asked?

431. How would you design a highly available Jenkins architecture?
432. Is Jenkins controller itself highly available by default?
433. How would you protect Jenkins from controller failure?
434. How would you back up Jenkins?
435. What should be backed up from Jenkins?
436. What is `JENKINS_HOME`?
437. How would you restore Jenkins from backup?
438. How would you perform Jenkins disaster recovery?
439. What is your Jenkins RTO?
440. What is your Jenkins RPO?
441. How would you design Jenkins for disaster recovery across regions?
442. How would you migrate Jenkins from one server to another?
443. How would you migrate Jenkins from VM to Kubernetes?
444. How would you migrate a large Jenkins instance with thousands of jobs?
445. How would you reduce Jenkins controller load?
446. How would you scale Jenkins agents dynamically?
447. How would you isolate teams in a shared Jenkins environment?
448. How would you implement multi-tenant Jenkins?
449. When would you use multiple Jenkins controllers?
450. When would you use one centralized Jenkins controller?
451. How would you handle 1,000 repositories in Jenkins?
452. How would you manage thousands of Jenkins jobs?
453. How would you standardize Jenkins pipelines across hundreds of applications?
454. How would you manage plugin sprawl?
455. How would you minimize Jenkins plugin dependencies?
456. How would you design Jenkins for regulated environments?
457. How would you audit Jenkins deployments?
458. How would you implement separation of duties in Jenkins?
459. How would you prevent developers from deploying directly to production?
460. How would you design Jenkins for zero-downtime upgrades?

# GitHub Actions Fundamentals — What GitHub Actions questions should an experienced engineer know? ([GitHub Docs][4])

461. What is GitHub Actions?
462. How is GitHub Actions different from Jenkins?
463. What are the main components of GitHub Actions?
464. What is a workflow?
465. What is a job?
466. What is a step?
467. What is an action?
468. What is a runner?
469. What is the difference between a workflow, job, step, and action?
470. Where are GitHub Actions workflow files stored?
471. What is `.github/workflows`?
472. What is YAML used for in GitHub Actions?
473. How is a GitHub Actions workflow triggered?
474. What is the `on` keyword?
475. What is the `push` event?
476. What is the `pull_request` event?
477. What is `workflow_dispatch`?
478. What is `workflow_call`?
479. What is `workflow_run`?
480. What is `repository_dispatch`?
481. What is `schedule`?
482. What is a GitHub Actions event filter?
483. How do you trigger a workflow only for specific branches?
484. How do you trigger a workflow only for specific paths?
485. How do you trigger a workflow only when specific files change?
486. How do you trigger a workflow manually?
487. How do you pass inputs to a manually triggered workflow?
488. How do you trigger one workflow after another workflow finishes?
489. What limitations exist when chaining workflows?
490. How would you design a GitHub Actions workflow for PR validation?
491. How would you design a GitHub Actions workflow for production deployment?
492. How would you create separate workflows for CI and CD?
493. How would you combine CI and CD in a single workflow?
494. When should CI and CD be separate workflows?
495. How do you prevent a pull request workflow from deploying to production?

# GitHub Actions Jobs, Steps and Dependencies — What workflow-design questions can be asked? ([GitHub Docs][4])

496. How does a GitHub Actions job execute?
497. Do GitHub Actions jobs run sequentially or in parallel by default?
498. How do you make one job depend on another?
499. What is `needs`?
500. How do you create a dependency graph between jobs?
501. What happens when a job in `needs` fails?
502. How do you run a job even if a previous job fails?
503. What is `if:` in GitHub Actions?
504. How do you conditionally execute a step?
505. How do you conditionally execute a job?
506. What is `always()`?
507. What is `success()`?
508. What is `failure()`?
509. What is `cancelled()`?
510. How do you run cleanup after a failed job?
511. How do you make jobs execute in parallel?
512. How do you make jobs execute sequentially?
513. How do you pass data between jobs?
514. How do you pass outputs from one job to another?
515. What are job outputs?
516. What are step outputs?
517. How do you set environment variables in GitHub Actions?
518. What is `$GITHUB_ENV`?
519. What is `$GITHUB_OUTPUT`?
520. What is `$GITHUB_PATH`?
521. What are GitHub Actions contexts?
522. What is the `github` context?
523. What is the `env` context?
524. What is the `vars` context?
525. What is the `secrets` context?
526. What is the `runner` context?
527. What is the `job` context?
528. What is the `steps` context?
529. What is the `needs` context?
530. What is the `inputs` context?
531. What is the difference between `${{ env.X }}` and `$X`?
532. Where can GitHub Actions expressions be evaluated?
533. How do you use expressions in `if:` conditions?
534. How do you compare strings and numbers in GitHub Actions expressions?
535. How do you handle empty or undefined variables?

# GitHub Actions Runners — What runner architecture questions can be asked? ([GitHub Docs][5])

536. What is a GitHub-hosted runner?
537. What is a self-hosted runner?
538. GitHub-hosted versus self-hosted runners: what are the differences?
539. When would you use self-hosted runners?
540. When would you use GitHub-hosted runners?
541. What are the security risks of self-hosted runners?
542. How do you register a self-hosted runner?
543. How does GitHub assign jobs to runners?
544. What is `runs-on`?
545. What are runner labels?
546. How do custom runner labels work?
547. How do multiple labels affect runner selection?
548. What are runner groups?
549. How do runner groups improve security?
550. How do you restrict which repositories can use a runner?
551. How do you route production deployment jobs to dedicated runners?
552. How would you create separate runners for development and production?
553. How would you isolate runners for different teams?
554. How do you secure a self-hosted runner?
555. Why are self-hosted runners risky for public repositories?
556. How could a malicious pull request compromise a self-hosted runner?
557. How would you protect secrets when using self-hosted runners?
558. How do you clean a self-hosted runner after every job?
559. How do you make self-hosted runners ephemeral?
560. How do you autoscale GitHub Actions runners?
561. What is Actions Runner Controller?
562. How would you run GitHub Actions runners on Kubernetes?
563. How would you design an autoscaling runner architecture?
564. What happens if no GitHub Actions runner matches `runs-on`?
565. What happens if a self-hosted runner goes offline?
566. How would you troubleshoot a GitHub Actions job stuck waiting for a runner?
567. How would you troubleshoot a runner that is online but not accepting jobs?
568. How would you troubleshoot a self-hosted runner with high CPU usage?
569. How would you troubleshoot a self-hosted runner with disk exhaustion?
570. How would you troubleshoot a runner registration failure?

# GitHub Actions Matrix and Parallelism — What advanced workflow questions should you prepare?

571. What is a GitHub Actions matrix strategy?
572. Why would you use a matrix strategy?
573. How do you test an application against multiple versions?
574. How do you test across multiple operating systems?
575. How do you combine OS and application-version matrices?
576. What is `strategy.matrix`?
577. What is `include` in a matrix?
578. What is `exclude` in a matrix?
579. What is `fail-fast` in a matrix?
580. What is `continue-on-error`?
581. How do you allow one matrix combination to fail without failing the entire workflow?
582. How would you dynamically generate a matrix?
583. How would you pass matrix values between jobs?
584. How would you control matrix size?
585. What problems can an excessively large matrix create?
586. How would you optimize a matrix-based CI pipeline?
587. How would you run tests in parallel without overloading infrastructure?

# GitHub Actions Artifacts, Cache and Dependencies — What artifact questions can be asked? ([GitHub Docs][6])

588. What is a GitHub Actions artifact?
589. Why would you upload an artifact?
590. How do you download an artifact in another job?
591. What is the difference between artifacts and cache?
592. When should you use cache?
593. When should you use artifacts?
594. Why should a cache miss not break a build?
595. How do you cache npm dependencies?
596. How do you cache Maven dependencies?
597. How do you cache Gradle dependencies?
598. How do you cache Docker layers?
599. How do you invalidate a GitHub Actions cache?
600. What is a cache key?
601. What is a cache restore key?
602. How would you design a good cache key?
603. How do you prevent stale cache from causing incorrect builds?
604. How would you transfer a Docker image between jobs?
605. How would you transfer a compiled binary between jobs?
606. How would you publish build artifacts to Artifactory?
607. How would you publish build artifacts to Nexus?
608. How would you publish Docker images to GHCR?
609. How would you publish packages to GitHub Packages?
610. How would you implement artifact retention?
611. How would you verify artifact integrity?
612. How would you implement artifact provenance?

# GitHub Actions Reusable Workflows and Actions — What advanced reusability questions can be asked? ([GitHub Docs][4])

613. What is a reusable workflow?
614. What is `workflow_call`?
615. What is the difference between a reusable workflow and a composite action?
616. What is a composite action?
617. When would you create a custom GitHub Action?
618. When would you create a reusable workflow?
619. How do you pass inputs to a reusable workflow?
620. How do you pass secrets to a reusable workflow?
621. How do you return outputs from a reusable workflow?
622. How do you version reusable workflows?
623. How do you prevent breaking changes in reusable workflows?
624. How would you create a centralized CI workflow for 100 repositories?
625. How would you standardize security scanning across all repositories?
626. How would you standardize Docker builds across repositories?
627. How would you create an organization-wide deployment workflow?
628. How do you securely consume third-party GitHub Actions?
629. Why should GitHub Actions be pinned to commit SHAs?
630. What are the risks of using `@main` for third-party actions?
631. How would you manage versions of internal GitHub Actions?
632. How would you test a custom action?
633. How would you troubleshoot a reusable workflow?
634. How would you troubleshoot a composite action?

# GitHub Actions Secrets and Security — What security questions should you expect? ([GitHub Docs][7])

635. What are GitHub Actions secrets?
636. Where can GitHub Actions secrets be configured?
637. What are repository secrets?
638. What are organization secrets?
639. What are environment secrets?
640. What is the difference between secrets and variables?
641. How are GitHub Actions secrets protected?
642. How do you use secrets in a workflow?
643. Can secrets be directly accessed from a forked pull request?
644. What security risks exist with `pull_request` workflows?
645. What is `pull_request_target`?
646. Why can `pull_request_target` be dangerous?
647. How would you safely handle secrets in pull-request workflows?
648. What is the `GITHUB_TOKEN`?
649. What permissions does `GITHUB_TOKEN` have?
650. How do you restrict `GITHUB_TOKEN` permissions?
651. What is the principle of least privilege for `GITHUB_TOKEN`?
652. What is OIDC in GitHub Actions?
653. Why use OIDC instead of long-lived cloud credentials?
654. How does GitHub Actions OIDC authentication work?
655. What is the purpose of `id-token: write`?
656. How would you configure GitHub Actions to authenticate to AWS using OIDC?
657. How would you configure GitHub Actions to authenticate to Azure using OIDC?
658. How would you configure GitHub Actions to authenticate to GCP using OIDC?
659. How would you restrict an AWS IAM role to a specific GitHub repository?
660. How would you restrict cloud access to a specific branch?
661. How would you restrict cloud access to a specific GitHub environment?
662. How would you prevent a GitHub Actions workflow from accessing production credentials?
663. How would you rotate GitHub Actions secrets?
664. What happens when a secret is printed in logs?
665. Can secret masking be bypassed?
666. How would you prevent secrets from being exposed through shell commands?
667. How would you scan repositories for accidentally committed secrets?
668. How would you integrate secret scanning into CI/CD?
669. How would you secure third-party GitHub Actions?
670. How would you audit GitHub Actions security?
671. How would you secure self-hosted runners?
672. How would you isolate production deployment runners?
673. How would you prevent malicious workflow modifications from deploying to production?

# GitHub Actions Environments and Deployment — What production deployment questions can be asked?

674. What is a GitHub Actions environment?
675. Why are environments useful?
676. How do environment-specific secrets work?
677. How do environment protection rules work?
678. How do you require approval before production deployment?
679. How do you restrict production deployment to specific users?
680. How would you implement dev, staging, and production environments?
681. How would you implement automatic deployment to development?
682. How would you implement approval-based deployment to production?
683. How would you implement deployment gates?
684. How would you prevent direct production deployment from feature branches?
685. How would you allow production deployment only from tags?
686. How would you implement semantic-version-based releases?
687. How would you implement rollback using GitHub Actions?
688. How would you implement blue-green deployment using GitHub Actions?
689. How would you implement canary deployment using GitHub Actions?
690. How would you integrate GitHub Actions with Kubernetes deployments?
691. How would you integrate GitHub Actions with Argo CD?
692. GitHub Actions versus Argo CD: what belongs in CI and what belongs in CD?
693. How would you implement GitOps using GitHub Actions?
694. How would you update a Helm chart repository from GitHub Actions?
695. How would you deploy Terraform using GitHub Actions?
696. How would you prevent accidental `terraform apply` from CI?
697. How would you implement approval before Terraform production apply?
698. How would you safely manage Terraform state from GitHub Actions?

# GitHub Actions Concurrency and Reliability — What senior questions should you prepare?

699. What is concurrency in GitHub Actions?
700. How do you prevent two deployments from running simultaneously?
701. How do you cancel an older workflow when a newer commit arrives?
702. What is `cancel-in-progress`?
703. How would you prevent concurrent production deployments?
704. How would you prevent duplicate deployments from multiple workflows?
705. How do you implement deployment locking?
706. How would you design a workflow that is safe to retry?
707. How do you handle transient failures?
708. How do you implement retries in GitHub Actions?
709. When should a workflow step be retried?
710. When should a workflow not be retried?
711. How do you set job timeouts?
712. How do you prevent a workflow from hanging forever?
713. How do you handle partial deployment failure?
714. How do you recover from a failed production deployment?
715. How would you design an idempotent GitHub Actions deployment?
716. How would you design a disaster-recovery deployment workflow?

# Jenkins vs GitHub Actions — What comparison questions can an interviewer ask?

717. Jenkins versus GitHub Actions: which would you choose?
718. What are the advantages of Jenkins over GitHub Actions?
719. What are the advantages of GitHub Actions over Jenkins?
720. Jenkins controller-agent architecture versus GitHub Actions runner architecture?
721. Jenkins agents versus GitHub-hosted runners?
722. Jenkins credentials versus GitHub secrets?
723. Jenkins Shared Libraries versus reusable GitHub workflows?
724. Jenkins plugins versus GitHub Actions marketplace?
725. Jenkins Pipeline versus GitHub Actions workflow?
726. Jenkins `input` versus GitHub environment approvals?
727. Jenkins `parallel` versus GitHub matrix?
728. Jenkins `stash/unstash` versus GitHub artifacts?
729. Jenkins credentials binding versus GitHub OIDC?
730. Jenkins webhook triggers versus GitHub-native events?
731. Jenkins Multibranch Pipeline versus GitHub workflow branch filters?
732. Jenkins self-hosted agents versus GitHub self-hosted runners?
733. Jenkins scalability versus GitHub Actions scalability?
734. Jenkins security model versus GitHub Actions security model?
735. Jenkins backup and disaster recovery versus GitHub Actions?
736. Jenkins versus GitHub Actions for enterprise CI/CD?
737. Jenkins versus GitHub Actions for Kubernetes?
738. Jenkins versus GitHub Actions for Terraform?
739. Jenkins versus GitHub Actions for monorepos?
740. Jenkins versus GitHub Actions for microservices?
741. Jenkins versus GitHub Actions for regulated environments?
742. When would you keep Jenkins even if the organization uses GitHub?
743. When would you migrate Jenkins to GitHub Actions?
744. What challenges would you expect while migrating Jenkins to GitHub Actions?
745. How would you migrate 500 Jenkins pipelines to GitHub Actions?
746. How would you validate that the migrated GitHub Actions pipeline behaves exactly like Jenkins?
747. How would you run Jenkins and GitHub Actions in parallel during migration?
748. How would you perform a gradual CI/CD migration from Jenkins to GitHub Actions?
749. How would you roll back a migration from Jenkins to GitHub Actions?
750. How would you convince management to migrate from Jenkins to GitHub Actions?

# CI/CD with Docker — What containerized pipeline questions can be asked?

751. How do you build a Docker image in Jenkins?
752. How do you build a Docker image in GitHub Actions?
753. How do you authenticate CI/CD to a container registry?
754. How do you securely push Docker images?
755. How do you tag Docker images in CI/CD?
756. What Docker image tagging strategy would you use?
757. Why should you avoid using only `latest`?
758. How would you tag an image using Git commit SHA?
759. How would you tag an image using semantic versioning?
760. How would you promote the same image across environments?
761. How would you scan Docker images during CI?
762. Where should container scanning occur?
763. How would you fail a pipeline when a critical vulnerability is detected?
764. How would you handle false positives in container scanning?
765. How would you optimize Docker build time?
766. How would you cache Docker layers in Jenkins?
767. How would you cache Docker layers in GitHub Actions?
768. What is Docker BuildKit?
769. How would you build multi-architecture images?
770. How would you build ARM64 and AMD64 images simultaneously?
771. How would you publish multi-platform images?
772. How would you sign Docker images?
773. How would you verify image signatures during deployment?
774. How would you implement SBOM generation in CI/CD?
775. How would you implement container provenance?
776. How would you prevent unauthorized images from reaching production?

# CI/CD with Kubernetes — What Kubernetes pipeline questions can be asked?

777. How would you deploy Kubernetes applications through Jenkins?
778. How would you deploy Kubernetes applications through GitHub Actions?
779. Jenkins versus Argo CD for Kubernetes deployment?
780. GitHub Actions versus Argo CD for Kubernetes deployment?
781. What should CI do and what should CD do in a Kubernetes GitOps architecture?
782. How would Jenkins update a Helm chart?
783. How would GitHub Actions update a Helm chart?
784. How would you deploy Helm charts from Jenkins?
785. How would you deploy Helm charts from GitHub Actions?
786. How would you handle Kubernetes credentials in Jenkins?
787. How would you handle Kubernetes credentials in GitHub Actions?
788. How would you avoid storing Kubernetes admin credentials in CI/CD?
789. How would you use cloud identity instead of static Kubernetes credentials?
790. How would you implement namespace-based environment isolation?
791. How would you implement promotion from staging to production?
792. How would you implement rollback of a Kubernetes deployment through CI/CD?
793. How would you detect a failed Kubernetes rollout in CI/CD?
794. What should happen in the pipeline if `kubectl rollout status` fails?
795. How would you automatically collect Kubernetes logs after a deployment failure?
796. How would you automatically run smoke tests after Kubernetes deployment?
797. How would you implement post-deployment health checks?
798. How would you stop a pipeline if Kubernetes readiness checks fail?
799. How would you implement canary deployment through CI/CD?
800. How would you implement blue-green deployment through CI/CD?

# CI/CD with Terraform and Infrastructure — What infrastructure pipeline questions should you know?

801. How would you design a Terraform CI/CD pipeline?
802. What stages should exist in a Terraform pipeline?
803. Where should `terraform fmt` run?
804. Where should `terraform validate` run?
805. Where should `terraform plan` run?
806. Where should `terraform apply` run?
807. Why should Terraform plan and apply be separated?
808. Why should production Terraform apply require approval?
809. How would you store Terraform state securely?
810. How would CI/CD authenticate to the cloud for Terraform?
811. How would you avoid static AWS credentials in Jenkins?
812. How would you avoid static AWS credentials in GitHub Actions?
813. How would you use OIDC for Terraform deployments?
814. How would you prevent concurrent Terraform applies?
815. What happens if two Terraform pipelines run simultaneously?
816. How would you implement Terraform state locking?
817. How would you handle a failed Terraform apply?
818. How would you recover from Terraform state corruption?
819. How would you prevent Terraform from modifying production accidentally?
820. How would you separate Terraform pipelines for dev, staging, and production?
821. How would you implement Terraform policy checks in CI?
822. How would you integrate Checkov into CI/CD?
823. How would you integrate tfsec into CI/CD?
824. How would you integrate OPA/Conftest into CI/CD?
825. How would you implement Terraform drift detection?
826. How would you schedule Terraform drift detection?
827. How would you handle Terraform plan output as a pipeline artifact?
828. How would you review Terraform plan during pull requests?
829. How would you prevent secrets from appearing in Terraform plan output?
830. How would you implement automatic Terraform deployment for non-production and approval for production?

# CI/CD Security and DevSecOps — What advanced security questions can be asked?

831. Where should security scanning be placed in a CI/CD pipeline?
832. What is SAST?
833. What is SCA?
834. What is DAST?
835. What is IaC scanning?
836. What is container scanning?
837. What is secret scanning?
838. What is dependency scanning?
839. What is license scanning?
840. How do SAST and DAST differ?
841. How do SCA and SAST differ?
842. How do SCA and container scanning differ?
843. How would you implement a DevSecOps pipeline?
844. How would you prevent security vulnerabilities from reaching production?
845. What is a security quality gate?
846. How would you define vulnerability severity thresholds?
847. Should every vulnerability fail the pipeline?
848. How would you handle false positives?
849. How would you handle accepted risks?
850. How would you implement security exceptions?
851. How would you prevent developers from bypassing security gates?
852. How would you secure CI/CD infrastructure itself?
853. How would you secure Jenkins from supply-chain attacks?
854. How would you secure GitHub Actions from supply-chain attacks?
855. What is software supply-chain security?
856. What is dependency confusion?
857. What is dependency poisoning?
858. What is a malicious CI/CD action?
859. How would you verify third-party GitHub Actions?
860. Why should GitHub Actions be pinned to SHA?
861. How would you secure Jenkins plugins?
862. How would you prevent compromised dependencies from entering builds?
863. What is SBOM?
864. How would you generate an SBOM in CI/CD?
865. How would you validate an SBOM?
866. What is artifact signing?
867. How would you sign build artifacts?
868. How would you verify artifact signatures?
869. What is SLSA?
870. How would you implement build provenance?
871. How would you secure the software supply chain end-to-end?
872. How would you detect a compromised CI/CD pipeline?
873. What would you do if your CI/CD system was compromised?

# CI/CD Troubleshooting Scenarios — What "production incident" questions could an interviewer ask?

874. Your pipeline suddenly became 40 minutes slower; how would you troubleshoot it?
875. Your pipeline was previously green but every build now fails; how would you investigate?
876. Only production deployments are failing; how would you isolate the problem?
877. Only pull-request builds are failing; what would you check?
878. Only builds from feature branches are failing; what would you check?
879. Builds are queued for hours; how would you diagnose the bottleneck?
880. Builds are randomly assigned to the wrong environment; how would you investigate?
881. Two releases are deployed simultaneously; how would you prevent it?
882. A developer accidentally deployed to production; how would you prevent it in the future?
883. A pipeline succeeds but the application is unhealthy; what should the pipeline have checked?
884. Deployment succeeds but smoke tests fail; what should happen automatically?
885. Smoke tests pass but users report failures; how would you investigate the pipeline?
886. A deployment succeeds but the previous version cannot be restored; how would you improve the pipeline?
887. A rollback itself fails; how would you design recovery?
888. Your artifact repository is unavailable during deployment; what should happen?
889. GitHub is temporarily unavailable during deployment; what should happen?
890. Jenkins controller becomes unavailable during deployment; what should happen?
891. Your self-hosted GitHub Actions runner becomes unavailable during deployment; what should happen?
892. Your cloud provider becomes unavailable during deployment; how should CI/CD behave?
893. A pipeline has a flaky integration test; how would you handle it?
894. A test passes locally but fails in CI; what would you investigate?
895. A test passes on Jenkins but fails on GitHub Actions; what would you compare?
896. Docker builds work locally but fail in CI; what would you investigate?
897. Kubernetes deployment works manually but fails from CI; what would you investigate?
898. Terraform works locally but fails in CI; what would you investigate?
899. A secret works locally but is unavailable in CI; what would you investigate?
900. A GitHub Actions secret is not available in a pull request; why might that happen?
901. A Jenkins credential exists but the pipeline cannot access it; what would you investigate?
902. GitHub Actions says a runner is unavailable; how would you troubleshoot it?
903. Jenkins says no executor is available; how would you troubleshoot it?
904. A GitHub Actions matrix suddenly creates hundreds of jobs; how would you stop it?
905. Jenkins parallel execution overloads your infrastructure; how would you control it?
906. CI/CD costs doubled this month; how would you identify why?
907. Pipeline duration increased after enabling security scans; how would you optimize it?
908. Developers complain that CI feedback is too slow; how would you redesign the pipeline?
909. Production deployment requires 20 manual steps; how would you automate it safely?
910. Multiple teams have copied the same Jenkinsfile with small differences; how would you fix the architecture?
911. Multiple GitHub repositories contain almost identical workflows; how would you standardize them?
912. A shared pipeline change breaks 200 repositories; how would you prevent this?
913. A third-party GitHub Action is compromised; how would you respond?
914. A Jenkins plugin is found to contain a critical vulnerability; what would you do?
915. A cloud access key is leaked through CI logs; what would you do immediately?
916. A production deployment credential is accidentally committed to Git; what is your response?
917. A malicious pull request attempts to exfiltrate CI secrets; how would you prevent it?
918. A compromised self-hosted runner is detected; what would you do?
919. A developer modifies the deployment workflow to bypass approval; how would you prevent it?
920. An attacker obtains write access to the CI/CD repository; what would you do?

# CI/CD Architecture and System Design — What questions would test your 8-year-level design skills?

921. Design an enterprise CI/CD platform for 100 development teams.
922. Design a CI/CD platform supporting 1,000 microservices.
923. Design a highly available Jenkins platform for an enterprise.
924. Design a GitHub Actions platform using self-hosted runners.
925. Design a CI/CD platform for multiple AWS accounts.
926. Design a CI/CD platform for multiple Kubernetes clusters.
927. Design a multi-region CI/CD platform.
928. Design a CI/CD platform with strict production segregation.
929. Design a zero-trust CI/CD architecture.
930. Design a secure CI/CD platform for a financial organization.
931. Design a CI/CD platform for a healthcare organization.
932. Design a CI/CD platform supporting both Jenkins and GitHub Actions.
933. Design a hybrid Jenkins + GitHub Actions architecture.
934. Design CI/CD where GitHub Actions performs CI and Argo CD performs CD.
935. Design CI/CD where Jenkins performs CI and Argo CD performs CD.
936. Design a GitOps-based CI/CD architecture.
937. Design a monorepo CI/CD architecture.
938. Design a polyrepo CI/CD architecture.
939. Design CI/CD for microservices with independent deployments.
940. Design CI/CD for applications requiring coordinated releases.
941. Design CI/CD for applications requiring zero downtime.
942. Design CI/CD with automatic rollback.
943. Design CI/CD with progressive delivery.
944. Design CI/CD with automated security gates.
945. Design CI/CD with artifact immutability.
946. Design CI/CD with complete auditability.
947. Design CI/CD with short-lived cloud credentials.
948. Design CI/CD with ephemeral runners.
949. Design CI/CD with automatic runner scaling.
950. Design CI/CD with disaster recovery.
951. Design CI/CD with cross-region disaster recovery.
952. Design CI/CD where no CI/CD system has permanent production credentials.
953. Design CI/CD where every production deployment is traceable to a Git commit.
954. Design CI/CD where every production artifact can be reproduced.
955. Design CI/CD where developers cannot modify production deployment controls.
956. Design CI/CD where the same artifact moves from dev to staging to production.
957. Design CI/CD with automated compliance evidence collection.
958. Design CI/CD with complete deployment observability.

# Senior/Lead DevOps CI/CD Questions — What leadership and decision-making questions can be asked?

959. How would you assess the maturity of an organization's CI/CD platform?
960. What would you improve first in a poorly designed CI/CD pipeline?
961. How would you identify the biggest bottleneck in an organization's delivery process?
962. How would you reduce deployment lead time?
963. How would you improve deployment frequency without increasing failures?
964. How would you reduce change failure rate?
965. How would you improve MTTR through CI/CD?
966. How would you convince developers to adopt CI/CD best practices?
967. How would you enforce CI/CD standards without blocking developers?
968. How would you create CI/CD governance for multiple teams?
969. How would you balance developer freedom and platform standardization?
970. How would you handle a team that refuses to adopt centralized CI/CD standards?
971. How would you handle a team that wants production access through Jenkins?
972. How would you establish separation of duties?
973. How would you establish production deployment ownership?
974. How would you define CI/CD SLAs?
975. What CI/CD KPIs would you present to leadership?
976. How would you calculate the ROI of CI/CD automation?
977. How would you estimate the cost of running Jenkins?
978. How would you estimate the cost of GitHub Actions?
979. How would you reduce CI/CD infrastructure costs?
980. How would you reduce unnecessary pipeline executions?
981. How would you reduce flaky tests across the organization?
982. How would you introduce pipeline standards gradually?
983. How would you migrate legacy manual deployments to CI/CD?
984. How would you migrate shell-script-based deployments to Jenkins?
985. How would you migrate Jenkins pipelines to GitHub Actions?
986. How would you migrate GitLab CI pipelines to GitHub Actions?
987. How would you evaluate Jenkins versus GitHub Actions for a new organization?
988. What factors would determine your CI/CD platform choice?
989. How would you handle disagreement between development and security teams about pipeline gates?
990. How would you design a CI/CD platform that developers actually want to use?

# Real Pipeline Coding Questions — What Jenkinsfile and GitHub Actions coding questions should you expect?

991. Write a Jenkinsfile with Build, Test, and Deploy stages.
992. Write a Declarative Jenkinsfile for a Node.js application.
993. Write a Jenkinsfile for a Java Maven application.
994. Write a Jenkinsfile for a Python application.
995. Write a Jenkinsfile for a Dockerized application.
996. Write a Jenkinsfile that builds and pushes a Docker image.
997. Write a Jenkinsfile that deploys to Kubernetes.
998. Write a Jenkinsfile that deploys to staging automatically and production after approval.
999. Write a Jenkinsfile that runs tests in parallel.
1000. Write a Jenkinsfile that runs different stages based on branch.
1001. Write a Jenkinsfile that runs deployment only for Git tags.
1002. Write a Jenkinsfile that automatically creates Git tags.
1003. Write a Jenkinsfile that archives build artifacts.
1004. Write a Jenkinsfile that publishes artifacts to Nexus.
1005. Write a Jenkinsfile that publishes Docker images to a registry.
1006. Write a Jenkinsfile using Jenkins credentials.
1007. Write a Jenkinsfile using `withCredentials`.
1008. Write a Jenkinsfile using a Shared Library.
1009. Write a Jenkinsfile with retry and timeout.
1010. Write a Jenkinsfile with manual production approval.
1011. Write a Jenkinsfile with post-build notifications.
1012. Write a Jenkinsfile with automatic cleanup.
1013. Write a Jenkinsfile that prevents concurrent deployments.
1014. Write a Jenkinsfile that performs a health check after deployment.
1015. Write a Jenkinsfile that automatically rolls back after a failed health check.
1016. Write a Jenkinsfile that builds multiple Docker architectures.
1017. Write a Jenkinsfile that executes Terraform fmt, validate, plan, and apply.
1018. Write a Jenkinsfile that requires manual approval before Terraform apply.
1019. Write a Jenkinsfile that performs Terraform plan on pull requests.
1020. Write a Jenkinsfile that uses ephemeral Kubernetes agents.
1021. Write a GitHub Actions workflow for Node.js CI.
1022. Write a GitHub Actions workflow for Java Maven CI.
1023. Write a GitHub Actions workflow for Python CI.
1024. Write a GitHub Actions workflow for Docker build and push.
1025. Write a GitHub Actions workflow for Kubernetes deployment.
1026. Write a GitHub Actions workflow for Terraform.
1027. Write a GitHub Actions workflow with PR validation.
1028. Write a GitHub Actions workflow with manual deployment.
1029. Write a GitHub Actions workflow with production approval.
1030. Write a GitHub Actions workflow using environments.
1031. Write a GitHub Actions workflow using secrets.
1032. Write a GitHub Actions workflow using OIDC.
1033. Write a GitHub Actions workflow using a matrix.
1034. Write a GitHub Actions workflow using reusable workflows.
1035. Write a GitHub Actions workflow using artifacts.
1036. Write a GitHub Actions workflow using dependency caching.
1037. Write a GitHub Actions workflow using self-hosted runners.
1038. Write a GitHub Actions workflow with concurrency control.
1039. Write a GitHub Actions workflow with automatic rollback.
1040. Write a GitHub Actions workflow that deploys only when a release tag is created.

# Final Senior-Level Scenarios — What questions separate an 8-year DevOps engineer from a junior/mid-level engineer?

1041. You inherit a Jenkins platform with 2,000 jobs and no documentation; what would you do first?
1042. You inherit 500 GitHub Actions workflows with duplicated YAML; how would you standardize them?
1043. Jenkins controller CPU reaches 100% every morning; how would you investigate?
1044. Jenkins queue reaches 500 jobs every morning; how would you redesign capacity?
1045. GitHub Actions runner demand suddenly increases 10x; how would you scale the platform?
1046. Production deployment must happen within five minutes; how would you design the pipeline?
1047. Your organization has 200 microservices and each has a different Jenkinsfile; how would you standardize them?
1048. Your organization wants zero manual deployment steps; how would you design the controls?
1049. Security requires manual production approval but developers want full automation; how would you reconcile the requirements?
1050. Your organization wants to move from Jenkins to GitHub Actions with zero downtime; how would you execute the migration?
1051. Jenkins and GitHub Actions must coexist for two years; how would you design the platform?
1052. A production deployment failed halfway through a database migration; how would you recover?
1053. A pipeline accidentally deployed the wrong Docker image to production; how would you identify the cause and prevent recurrence?
1054. A developer force-pushed a production tag; how would you prevent this?
1055. Someone modified the Jenkinsfile and bypassed the security scan; how would you prevent this?
1056. Someone modified the GitHub Actions workflow and removed the production approval; how would you prevent this?
1057. A compromised third-party GitHub Action has access to your production environment; how would you contain the risk?
1058. A compromised Jenkins plugin has access to production credentials; how would you respond?
1059. Your CI/CD platform itself becomes the target of an attack; how would you protect it?
1060. How would you design an end-to-end CI/CD platform where **Git → PR → CI → Security → Build → Artifact → Approval → CD → Deployment → Verification → Rollback → Monitoring** is fully automated and auditable?

[1]: https://www.jenkins.io/doc/book/pipeline/?utm_source=chatgpt.com "Pipeline"
[2]: https://www.jenkins.io/doc/book/security/credentials/?utm_source=chatgpt.com "Credentials"
[3]: https://www.jenkins.io/doc/book/security/?utm_source=chatgpt.com "Securing Jenkins"
[4]: https://docs.github.com/en/actions/reference/workflows-and-actions/workflow-syntax?utm_source=chatgpt.com "Workflow syntax for GitHub Actions - GitHub Docs"
[5]: https://docs.github.com/en/actions/reference/runners/self-hosted-runners?utm_source=chatgpt.com "Self-hosted runners reference - GitHub Docs"
[6]: https://docs.github.com/en/actions/concepts/workflows-and-actions/workflow-artifacts?utm_source=chatgpt.com "Workflow artifacts - GitHub Docs"
[7]: https://docs.github.com/en/actions/concepts/security/secrets?utm_source=chatgpt.com "Secrets - GitHub Docs"
