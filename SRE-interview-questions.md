Absolutely. I’ll treat your **SRE-pathnex PDF as the primary source** and turn it into an **8-years-experienced DevOps/SRE interview question bank**—not just basic definitions, but the kind of **deep-dive, troubleshooting, architecture, incident, and scenario-based questions** an interviewer can ask.

The PDF covers SRE fundamentals, SLI/SLO/SLA, incident management, observability, toil, capacity planning, change management, chaos testing, tools, SRE culture, the 5 W's, hard/cold freeze, and error budgets. 

# SRE / DevOps — 8 Years Interview Question Bank

## 1. SRE Fundamentals

### Basic → Intermediate

1. What is Site Reliability Engineering?
2. Why was SRE introduced?
3. How is SRE different from traditional Operations?
4. How is SRE different from DevOps?
5. What are the primary goals of SRE?
6. What does reliability mean in a production system?
7. What is the role of an SRE in an organization?
8. What are the major responsibilities of an SRE?
9. How do you measure whether a service is reliable?
10. What is the difference between availability, reliability, and performance?
11. How does SRE balance development velocity and system stability?
12. What does an engineering-first approach mean in SRE?
13. Why should SREs write code instead of performing only operational activities?
14. What is automation's role in SRE?
15. What is resilience engineering?
16. What is toil?
17. How do you identify toil?
18. How do you reduce toil?
19. Give an example of operational toil you eliminated.
20. How do you decide whether an operational task should be automated?

The source explicitly defines SRE as applying software-engineering principles to infrastructure and operations problems, with goals around scalable and highly reliable systems. 

---

# 2. SLI, SLO and SLA

This is a **very important 8-year interview area**.

21. What is an SLI?
22. What is an SLO?
23. What is an SLA?
24. What is the difference between SLI, SLO and SLA?
25. Give a real-world example of SLI/SLO/SLA.
26. How do you define an SLI for an API?
27. How do you define an SLI for a database?
28. How do you define an SLI for Kubernetes?
29. What metrics can be used as SLIs?
30. How do you choose the right SLI?
31. What makes a good SLI?
32. How do you define an SLO?
33. Who should define the SLO—the development team or SRE team?
34. What happens if your SLO is too aggressive?
35. What happens if your SLO is too relaxed?
36. Can availability and latency both be SLOs?
37. Can you have multiple SLOs for the same service?
38. What happens when an SLO is violated?
39. How do you communicate SLO violations to stakeholders?
40. What is the relationship between SLO and error budget?
41. Why don't we simply target 100% availability?
42. Why is 99.9% availability different from 99.99%?
43. How would you calculate availability for a service?
44. How would you measure request success rate?
45. How would you measure latency as an SLI?

The PDF describes SLI as a reliability measurement, SLO as the target reliability level, and SLA as a formalized agreement that may include penalties. 

---

# 3. Error Budget — Deep Dive

This is one of the **highest-value topics from your PDF**.

46. What is an error budget?
47. Why do we need an error budget?
48. How is error budget calculated?
49. What is the formula for error budget?
50. If SLO is 99.9%, what is the error budget?
51. What does 0.1% error budget actually mean?
52. How much downtime does 99.9% availability allow in a 30-day month?
53. What happens when the error budget is exhausted?
54. What happens when the error budget is nearly exhausted?
55. What is error-budget burn?
56. What is burn rate?
57. What is fast error-budget burn?
58. What is slow error-budget burn?
59. How does burn rate influence deployment decisions?
60. When would you stop deployments because of the error budget?
61. Who decides whether feature development should continue?
62. How do you balance reliability versus feature delivery using error budgets?
63. Suppose your SLO is 99.9% and you already consumed most of the error budget. A developer wants to release a major feature. What would you do?
64. Your application has consumed 80% of the error budget but there is no active incident. Would you stop deployments?
65. Your error budget is burning very quickly. What actions would you take?
66. Your error budget is barely being consumed. What does that tell you?
67. How can error-budget policies be automated?
68. Can error budget be used as a deployment gate?
69. How would you integrate error-budget checks into CI/CD?
70. What is the difference between an SLO violation and error-budget exhaustion?

The source gives the formula **Error Budget = 100% − SLO** and uses 99.9% SLO → 0.1% budget → 43.2 minutes in a 30-day month.  

---

# 4. Scenario-Based Error Budget Questions

These are more appropriate for someone claiming **8 years of experience**.

71. Your service has a 99.9% SLO. It has already experienced 30 minutes of downtime in five days. What is your remaining budget?

72. A service has a 99.9% SLO, but users complain about latency even though availability is good. Is the service reliable?

73. Your error budget is being consumed rapidly because of a new deployment. What would you investigate?

74. Your deployment pipeline is healthy, but error-budget burn suddenly increases. How would you troubleshoot?

75. Product management says reliability is slowing down releases. How would you explain error budgets to them?

76. Developers want 100% availability as the SLO. Would you agree?

77. A service continuously violates its SLO. What long-term actions would you recommend?

78. Your SLO is being met, but customers are still unhappy. What could be wrong?

79. Your monitoring says 99.99% availability, but customers report outages. How would you investigate the mismatch?

80. How would you determine whether the SLO itself is incorrectly defined?

---

# 5. Incident Management

The PDF identifies incident management as detecting, responding to, and recovering from outages/service disruptions, followed by blameless postmortems and preventive actions. 

### Interview Questions

81. What is an incident?
82. What is incident management?
83. What is your incident-response process?
84. How do you detect an incident?
85. What is the first thing you do after receiving a production alert?
86. How do you determine incident severity?
87. How do you prioritize multiple incidents?
88. What is an incident commander?
89. What responsibilities should an incident commander have?
90. How do you coordinate developers, SREs and management during an incident?
91. How do you communicate during a major outage?
92. How do you avoid duplicate troubleshooting efforts?
93. What information should be captured during an incident?
94. How do you create an incident timeline?
95. What is root-cause analysis?
96. How do you perform RCA?
97. What is a blameless postmortem?
98. Why should postmortems be blameless?
99. What should a postmortem contain?
100. How do you ensure an incident does not happen again?
101. What is the difference between immediate mitigation and permanent remediation?
102. How do you identify recurring incidents?
103. How do you measure incident-management effectiveness?
104. What metrics would you track for incident response?
105. What is MTTR?
106. What is MTTD?
107. What is MTBF?
108. How would you reduce MTTR?
109. How would you reduce MTTD?
110. How do you handle an incident when the root cause is unknown?

---

# 6. Production Incident Scenarios

For an 8-year engineer, expect questions like:

111. Production is completely down. Walk me through your first 15 minutes.

112. CPU suddenly reaches 100% across production servers. What do you check?

113. Application latency suddenly increases. How do you troubleshoot?

114. Error rate suddenly increases after deployment. What do you do?

115. Monitoring says everything is healthy, but customers report failures. How do you investigate?

116. Only one region is affected. How would you isolate the issue?

117. Only one Kubernetes node is affected. What would you check?

118. Only one microservice is failing. How would you determine whether the problem is inside the service or downstream?

119. Database latency suddenly increases. How would you approach the incident?

120. Traffic suddenly increases by 10x. What would you do?

121. A deployment caused an outage. Would you rollback or troubleshoot forward?

122. Rollback itself fails. What is your next step?

123. Multiple teams are blaming each other during an incident. How do you handle it?

124. Management asks for an ETA while you don't know the root cause. What do you communicate?

125. After restoring service, what do you do next?

---

# 7. Monitoring & Observability

The source emphasizes dashboards, alerts and logs and specifically calls out **actionable alerts** and reducing alert fatigue. 

126. What is monitoring?
127. What is observability?
128. Monitoring vs observability?
129. Why do we need observability?
130. What are the three pillars of observability?
131. What metrics do you monitor for production?
132. What application-level metrics do you monitor?
133. What infrastructure-level metrics do you monitor?
134. What Kubernetes metrics do you monitor?
135. What is an actionable alert?
136. What is alert fatigue?
137. How do you reduce alert fatigue?
138. What should trigger an alert?
139. What should not trigger an alert?
140. What is the difference between an alert and a dashboard?
141. How do you design production dashboards?
142. How do you decide alert thresholds?
143. Static threshold vs dynamic threshold?
144. How do you prevent duplicate alerts?
145. How do you handle noisy alerts?
146. How do you troubleshoot when monitoring itself is unavailable?
147. How do you monitor monitoring systems?

---

# 8. Monitoring Tools

The source specifically lists Prometheus, Grafana, Datadog and New Relic for monitoring; ELK, Fluentd and Loki for logging. 

148. What is Prometheus?
149. Why is Prometheus commonly used in SRE?
150. How does Prometheus collect metrics?
151. What is a Prometheus exporter?
152. What is PromQL?
153. What is Grafana?
154. Prometheus vs Grafana?
155. How do you create a production dashboard?
156. How do you monitor Kubernetes using Prometheus?
157. How would you monitor API availability?
158. How would you monitor API latency?
159. How would you monitor HTTP error rate?
160. What is Datadog?
161. Prometheus vs Datadog?
162. When would you choose New Relic?
163. How do you decide between monitoring platforms?

---

# 9. Logging

164. Why is logging important for SRE?
165. What is centralized logging?
166. Why shouldn't every server maintain isolated logs?
167. What is ELK?
168. Explain Elasticsearch, Logstash and Kibana.
169. What is Fluentd?
170. What is Loki?
171. ELK vs Loki?
172. How do you collect logs from Kubernetes?
173. How do you troubleshoot an application using logs?
174. How do you correlate logs with metrics?
175. How do you search logs during an incident?
176. How do you prevent excessive logging?
177. What happens if logs suddenly increase 100x?
178. How do you handle log retention?
179. How do you protect sensitive information in logs?

---

# 10. Automation & Toil

The PDF defines toil as manual, repetitive work that scales with system growth and recommends automating deployment, monitoring and incident-response activities. 

180. What is toil?
181. How do you identify toil?
182. What percentage of your time should be spent on toil?
183. Give examples of toil in DevOps.
184. Give examples of toil in SRE.
185. How would you automate manual deployments?
186. How would you automate monitoring?
187. How would you automate incident response?
188. How do you calculate ROI of automation?
189. When should you NOT automate something?
190. How do you prioritize automation work?
191. What is the difference between automation and engineering?
192. How do you measure toil reduction?
193. Tell me about the biggest manual process you automated.
194. What happens if automation itself fails?
195. How do you make automation safe?

---

# 11. Capacity Planning & Performance

The source includes forecasting future infrastructure requirements and optimizing for speed, scale and cost-efficiency. 

196. What is capacity planning?
197. Why is capacity planning important?
198. How do you forecast infrastructure requirements?
199. What metrics do you use for capacity planning?
200. How do you plan capacity for a rapidly growing application?
201. How do you estimate future traffic?
202. How do you determine whether to scale vertically or horizontally?
203. What is over-provisioning?
204. What is under-provisioning?
205. How do you balance performance and cost?
206. How do you identify infrastructure bottlenecks?
207. How do you perform performance testing?
208. How do you perform load testing?
209. How do you plan for traffic spikes?
210. What happens if capacity planning is wrong?
211. How would you capacity-plan Kubernetes?
212. How would you capacity-plan a database?
213. How would you plan infrastructure for Black Friday-level traffic?

---

# 12. Change Management

The PDF emphasizes safe production changes using CI/CD, canary releases and rollbacks, with the goal of making deployments quick, reliable and reversible. 

214. What is change management?
215. Why is change management important?
216. How do you safely deploy changes to production?
217. What makes a deployment reliable?
218. What makes a deployment reversible?
219. What is a rollback?
220. Rollback vs roll-forward?
221. What is a canary deployment?
222. Why use canary deployment?
223. How do you decide canary success criteria?
224. How do you automatically rollback a canary?
225. What metrics would you monitor during canary deployment?
226. How does SLO influence deployment decisions?
227. How do you reduce deployment risk?
228. What is progressive delivery?
229. Blue-green vs canary deployment?
230. How do you handle database changes during rollback?
231. What if the application rollback succeeds but database rollback isn't possible?
232. How do you make deployments reversible?

---

# 13. CI/CD + SRE

The source specifically lists Jenkins, GitLab CI and ArgoCD under CI/CD tools. 

233. How does CI/CD support SRE?
234. How can CI/CD improve reliability?
235. How can CI/CD introduce reliability problems?
236. How would you build a production-grade CI/CD pipeline?
237. Where would you add automated testing?
238. Where would you add security scanning?
239. Where would you add deployment validation?
240. How would you implement automated rollback?
241. How would you integrate SLO checks into CI/CD?
242. How would you prevent risky deployments?
243. Jenkins vs GitLab CI?
244. What is GitOps?
245. How does ArgoCD support reliability?
246. What happens if ArgoCD deploys a bad configuration?
247. How do you detect failed deployments automatically?

---

# 14. Chaos Engineering / Reliability

The source describes reliability engineering as designing systems to gracefully handle failures and chaos testing as introducing controlled failures to test resilience. 

248. What is chaos engineering?
249. Why do we need chaos testing?
250. What is resilience?
251. Reliability vs resilience?
252. What types of failures can you introduce?
253. How would you perform chaos testing in production?
254. Would you perform chaos testing directly in production?
255. What safeguards are required?
256. How do you define success criteria for a chaos experiment?
257. What happens if a chaos experiment causes a real outage?
258. How would you test failure of a Kubernetes node?
259. How would you test failure of a service?
260. How would you test network failure?
261. How would you test dependency failure?
262. How does chaos engineering improve SLO confidence?
263. What is the difference between disaster recovery testing and chaos testing?

---

# 15. Hard Freeze vs Cold Freeze

This is explicitly covered in your PDF, so it is a likely direct interview question.

264. What is a hard freeze?
265. What is a cold freeze?
266. What is the difference between hard freeze and cold freeze?
267. When would you implement a hard freeze?
268. When would you implement a cold freeze?
269. Why would an organization freeze deployments?
270. Can security patches be deployed during a cold freeze?
271. Can security patches be deployed during a hard freeze according to the given model?
272. How is error budget related to a deployment freeze?
273. What would you do if the error budget exceeds the predefined threshold?
274. Should every production change be blocked during a freeze?
275. How would you communicate a production freeze to development teams?

The PDF describes hard freeze as a complete freeze on changes and cold freeze as a partial freeze where essential changes such as security patches are allowed. 

---

# 16. SRE 5 W's

The document explicitly presents the **5 W's** as a way to understand and solve reliability problems. 

276. What are the 5 W's in SRE?
277. What does "What" mean in incident analysis?
278. What does "Why" mean?
279. What does "Where" mean?
280. What does "When" mean?
281. What does "Who" mean?
282. How do the 5 W's help during RCA?
283. How would you use the 5 W's during a production outage?
284. Give an example of applying all 5 W's to an incident.
285. Why is the timeline important during incident investigation?
286. How do you identify affected users?
287. How do you determine which teams should investigate an incident?

---

# 17. SRE Tools

From the source's tool list: 

288. Which monitoring tools have you used?
289. Which logging tools have you used?
290. Which automation tools have you used?
291. Which CI/CD tools have you used?
292. Which incident-management tools have you used?
293. Prometheus vs Datadog?
294. Grafana vs Datadog?
295. ELK vs Loki?
296. Terraform vs Ansible?
297. Jenkins vs GitLab CI?
298. Jenkins vs ArgoCD?
299. How does Terraform contribute to SRE?
300. How does Ansible contribute to SRE?
301. How does ArgoCD contribute to SRE?
302. How does PagerDuty help incident response?
303. How would you integrate Slack with incident management?

---

# 18. SRE Culture

The PDF emphasizes **blameless culture, collaboration with developers, and engineering-first thinking**. 

304. What is a blameless culture?
305. Why are blameless postmortems important?
306. Does blameless mean nobody is accountable?
307. How do you handle an engineer who repeatedly causes incidents?
308. How do you work with developers during production incidents?
309. What should the relationship between Dev and SRE look like?
310. How do you convince developers to improve reliability?
311. What if developers prioritize features over reliability?
312. What if management prioritizes feature delivery over SLO?
313. How do you create a reliability culture?
314. How do you measure whether your SRE culture is improving?
315. How do you handle disagreements between SRE and development teams?

---

# 19. Very Deep 8-Year Scenario Questions

These are the questions I would especially prepare for a **Senior/Lead DevOps/SRE interview**.

### Scenario 1

316. **Your production system has an SLO of 99.9%. Error budget is almost exhausted. Product wants to deploy a critical business feature tonight. What do you do?**

### Scenario 2

317. **A deployment has completed successfully from the CI/CD perspective, but error-budget burn rate has increased sharply. How do you investigate?**

### Scenario 3

318. **Your monitoring dashboard shows green, but customers are reporting failures. Explain your investigation strategy.**

### Scenario 4

319. **You receive 1,000 alerts during an outage. How do you identify the real issue and reduce alert fatigue afterward?**

### Scenario 5

320. **A production outage happens immediately after a deployment. Explain your first 30 minutes.**

### Scenario 6

321. **The application is available but extremely slow. Your availability SLO is still satisfied. Is this a reliability problem?**

### Scenario 7

322. **You have repeated incidents caused by manual operational tasks. How would you identify and eliminate the toil?**

### Scenario 8

323. **Your infrastructure is constantly running at 20% utilization but costs are very high. How would you approach capacity optimization?**

### Scenario 9

324. **Traffic is growing 30% every month. How would you perform capacity planning?**

### Scenario 10

325. **Black Friday is tomorrow. Would you allow production deployments? Explain hard freeze vs cold freeze and your decision.**

### Scenario 11

326. **A critical security vulnerability is discovered during a hard freeze. What would you do?**

### Scenario 12

327. **Your canary deployment shows increased latency but no increase in errors. Would you continue rollout?**

### Scenario 13

328. **A rollback fixes the application but creates a database compatibility issue. How would you recover?**

### Scenario 14

329. **Management asks why you need an error budget when the goal should simply be maximum reliability. How would you explain it?**

### Scenario 15

330. **You have 99.99% availability but developers complain that releases are too slow. How would you balance reliability and delivery velocity?**

---

# 20. Architecture-Level Questions

For an 8-year engineer, interviewers may move from "What is SRE?" to **"Design it."**

331. Design a highly reliable production architecture.

332. How would you design an SLO-driven architecture?

333. How would you design monitoring for 100+ microservices?

334. How would you design centralized logging?

335. How would you design an incident-management platform?

336. How would you design automated alerting?

337. How would you design an automated rollback mechanism?

338. How would you design a canary deployment system?

339. How would you design a system to reduce operational toil?

340. How would you design capacity planning for a rapidly growing platform?

341. How would you design a production system that can tolerate infrastructure failures?

342. How would you introduce chaos engineering into an existing production environment?

343. How would you design an SRE platform for multiple Kubernetes clusters?

344. How would you define SLOs across multiple microservices?

345. How would you calculate overall reliability when one service depends on five downstream services?

---

# 21. "Tell Me About Your Experience" Questions

At **8 years**, expect experience-based questions rather than only definitions.

346. Tell me about your SRE/DevOps experience.

347. Tell me about the most serious production outage you handled.

348. What was the root cause?

349. What was your role during the incident?

350. How did you restore service?

351. What did you change afterward?

352. Tell me about a major automation you implemented.

353. Tell me about a major toil-reduction project.

354. Tell me about a time you improved reliability.

355. Tell me about a time you reduced MTTR.

356. Tell me about a time you reduced alert noise.

357. Tell me about a failed deployment.

358. Tell me about a rollback you performed.

359. Tell me about a difficult production incident.

360. Tell me about a disagreement with developers.

361. Tell me about a situation where you chose reliability over feature delivery.

362. Tell me about a situation where you chose feature delivery over reliability.

363. Tell me about a major performance problem you solved.

364. Tell me about a capacity-planning challenge.

365. Tell me about a time automation failed.

---

# 22. Rapid-Fire Questions

These are excellent for final interview rounds.

366. SLI vs SLO?
367. SLO vs SLA?
368. SLO vs error budget?
369. Reliability vs availability?
370. Monitoring vs observability?
371. Alert vs notification?
372. Toil vs automation?
373. Incident vs problem?
374. RCA vs postmortem?
375. Blameless vs accountability?
376. Hard freeze vs cold freeze?
377. Canary vs rollback?
378. Capacity vs performance?
379. Reliability vs resilience?
380. MTTR vs MTTD?
381. Prometheus vs Grafana?
382. ELK vs Loki?
383. Terraform vs Ansible?
384. Jenkins vs ArgoCD?
385. Deployment failure vs application failure?

---

## ⭐ Most Important 25 to Master First

If you don't have unlimited preparation time, prioritize these:

1. **What is SRE?**
2. **DevOps vs SRE**
3. **SLI vs SLO vs SLA**
4. **How do you define an SLO?**
5. **What is an error budget?**
6. **Calculate error budget for 99.9% SLO**
7. **What is error-budget burn rate?**
8. **What happens when error budget is exhausted?**
9. **How do you handle a production incident?**
10. **Explain RCA and blameless postmortem**
11. **How do you reduce MTTR?**
12. **Monitoring vs observability**
13. **How do you design actionable alerts?**
14. **How do you reduce alert fatigue?**
15. **What is toil and how do you eliminate it?**
16. **How do you perform capacity planning?**
17. **How do you safely deploy to production?**
18. **Explain canary deployment**
19. **How would you automatically rollback a bad deployment?**
20. **What is chaos engineering?**
21. **Hard freeze vs cold freeze**
22. **How does error budget influence deployments?**
23. **Explain SRE's 5 W's**
24. **Explain your biggest production incident**
25. **Design a highly reliable production platform**

### One important point

Your PDF is only **5 pages**, so it gives the SRE foundation rather than covering every implementation detail of tools such as Prometheus, Kubernetes, Terraform, Jenkins, ArgoCD, etc. The question bank above therefore **extracts and expands interview questions from the concepts actually present in the PDF** rather than pretending the PDF contains material it doesn't. The document's summary itself identifies the core SRE focus as **reliability, automation and resilience**, core practices as **monitoring, incident management and change control**, and core metrics as **SLIs, SLOs and SLAs**. 

If you're preparing for an **8-year interview**, the next best step is to take these questions **one by one like a real interviewer**, where I ask the question, you answer, and I evaluate your answer at **Senior/8-year level** and then give you the ideal answer.
