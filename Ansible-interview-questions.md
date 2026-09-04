Yes. Since you are preparing as an **8-year DevOps Engineer**, I would not limit the preparation to the basic Ansible questions in the PATHNEX document. The uploaded material covers the foundation—Ansible, agentless architecture, inventory, playbooks, modules, roles, workflow, cloud provisioning, patching and IaC. 

The second uploaded notes file reorganizes the same material into interview-friendly concepts such as **Control Node → Inventory → Playbook → Modules → Managed Nodes → Result**. 

For **8 years experience**, interviewers can go much deeper into architecture, troubleshooting, security, performance, CI/CD and real production scenarios.

# Ansible — 8 Years DevOps Interview Question Bank

## 1. Ansible Fundamentals

1. What is Ansible?
2. Why do you use Ansible in DevOps?
3. What problems does Ansible solve?
4. What are the major use cases of Ansible?
5. Why is Ansible called agentless?
6. How does Ansible communicate with Linux servers?
7. How does Ansible communicate with Windows servers?
8. What is the difference between Ansible and traditional configuration-management tools?
9. What are the advantages of Ansible?
10. What are the limitations of Ansible?
11. Where would you **not** use Ansible?
12. Is Ansible push-based or pull-based?
13. Explain Ansible architecture.
14. What is a Control Node?
15. What is a Managed Node?
16. What is the relationship between Control Node and Managed Node?
17. How does Ansible execute a task on a remote server?
18. Explain the complete Ansible execution flow.
19. What happens internally when you execute `ansible-playbook`?
20. Why doesn't Ansible require an agent?
21. What prerequisites are required on a Linux managed node?
22. What prerequisites are required on the control node?
23. Can Ansible manage thousands of servers?
24. How does Ansible scale?

---

# 2. Inventory

The source specifically introduces inventory as the list/grouping of machines Ansible manages. 

25. What is an Ansible inventory?
26. What is a static inventory?
27. What is a dynamic inventory?
28. Static inventory vs dynamic inventory?
29. How do you create an inventory file?
30. How do you define groups in inventory?
31. How do you create nested groups?
32. What are `group_vars` and `host_vars`?
33. How do you define variables inside inventory?
34. How do you specify a non-default SSH port?
35. How do you specify a different SSH user?
36. How do you specify an SSH private key?
37. How do you connect to a server using a bastion host?
38. How do you configure inventory for multiple environments?
39. How would you structure inventory for dev, QA, staging and production?
40. How does dynamic AWS inventory work?
41. How would you dynamically discover EC2 instances?
42. What are inventory plugins?
43. Inventory script vs inventory plugin?
44. How do you verify that Ansible can see your hosts?
45. What does `ansible-inventory --list` do?
46. What does `ansible-inventory --graph` do?
47. How would you troubleshoot a host missing from inventory?
48. How do you exclude a host/group during execution?

---

# 3. Playbooks

The source describes playbooks as YAML files containing plays/tasks and defining what actions should happen on which systems. 

49. What is an Ansible playbook?
50. What is a play?
51. Play vs playbook?
52. What is a task?
53. What is a handler?
54. What is a module?
55. What is a directive?
56. How do you write a basic playbook?
57. Explain the structure of a playbook.
58. What does `hosts` mean?
59. What does `tasks` mean?
60. What does `become` mean?
61. What is `become_user`?
62. What is `become_method`?
63. What is `remote_user`?
64. What is `gather_facts`?
65. How do you disable fact gathering?
66. When would you disable `gather_facts`?
67. How do you execute multiple plays from one playbook?
68. Can one playbook call another playbook?
69. How do you reuse a playbook?
70. `import_playbook` vs `include_tasks`?
71. `import_tasks` vs `include_tasks`?
72. Static import vs dynamic include?
73. How do you conditionally execute tasks?
74. How do you execute a task only when another task changes something?
75. How do you execute tasks only on specific hosts?
76. How do you execute a task only on Red Hat systems?
77. How do you execute a task only in production?
78. How do you skip a task?
79. How do you handle task failure?
80. How do you continue execution after a task failure?

---

# 4. Modules

The source identifies modules as the units that perform actual work, with `yum` and `copy` as examples. 

81. What is an Ansible module?
82. Which Ansible modules have you used in production?
83. Difference between `command` and `shell`?
84. Difference between `shell` and `raw`?
85. Why should you prefer modules over shell commands?
86. What is the `package` module?
87. `yum` vs `dnf` vs `package`?
88. What is the `apt` module?
89. What is the `service` module?
90. `service` vs `systemd`?
91. What is the `copy` module?
92. What is the `template` module?
93. `copy` vs `template`?
94. What is the `file` module?
95. How do you create a directory?
96. How do you change file permissions?
97. How do you change ownership?
98. How do you create a symbolic link?
99. What is the `lineinfile` module?
100. What is the `replace` module?
101. What is the `blockinfile` module?
102. When would you use `lineinfile` vs `template`?
103. What is the `user` module?
104. What is the `group` module?
105. How do you create users with SSH keys?
106. What is the `unarchive` module?
107. How do you download files using Ansible?
108. What is the `get_url` module?
109. What is the `uri` module?
110. What is the `stat` module?
111. What is the `find` module?
112. What is the `fetch` module?
113. `copy` vs `fetch`?
114. What is the `debug` module?
115. What is the `set_fact` module?
116. What is the `assert` module?
117. What is the `wait_for` module?
118. What is the `mount` module?
119. What is the `cron` module?
120. What is the `firewalld` module?
121. What is the `iptables` module?
122. What is the `docker_container` module?
123. What Kubernetes modules have you used?
124. How do you check whether a module is available?
125. What is FQCN in Ansible?

---

# 5. Idempotency — VERY IMPORTANT

126. What is idempotency in Ansible?
127. Why is idempotency important?
128. Give a real production example of idempotency.
129. How does Ansible achieve idempotency?
130. Are all Ansible modules idempotent?
131. Is the `command` module idempotent?
132. Is the `shell` module idempotent?
133. How would you make a shell command idempotent?
134. What is `creates`?
135. What is `removes`?
136. Why is your playbook showing `changed` every time?
137. How would you troubleshoot a non-idempotent task?
138. What is the difference between `changed`, `ok`, `failed`, `skipped`, and `unreachable`?

---

# 6. Variables

139. What are variables in Ansible?
140. Why do we use variables?
141. Where can variables be defined?
142. What is variable precedence?
143. Explain Ansible variable precedence.
144. Which has higher precedence: inventory variable or `extra_vars`?
145. What are `host_vars`?
146. What are `group_vars`?
147. What are registered variables?
148. What is `register`?
149. How do you use the output of one task in another task?
150. What is `set_fact`?
151. `set_fact` vs normal variable?
152. What are magic variables?
153. What is `inventory_hostname`?
154. What is `ansible_hostname`?
155. What is `hostvars`?
156. What is `groups`?
157. What is `group_names`?
158. What is `ansible_facts`?
159. What is the difference between `hostvars` and `vars`?
160. How do you access nested variables?
161. What happens if a variable is undefined?
162. How do you provide default values?
163. What is the `default()` filter?
164. How do you override variables at runtime?

---

# 7. Facts

165. What are Ansible facts?
166. How are facts collected?
167. What is `gather_facts`?
168. How do you disable fact gathering?
169. Why can fact gathering make playbooks slow?
170. How do you collect only specific facts?
171. What is `ansible_facts`?
172. How do you find OS information?
173. How do you find IP address using facts?
174. How do you determine whether a server is Red Hat or Ubuntu?
175. How do you troubleshoot missing facts?

---

# 8. Jinja2 / Templates

176. What is Jinja2?
177. Why is Jinja2 used in Ansible?
178. What is a template?
179. Difference between `.j2` template and normal file?
180. `copy` vs `template`?
181. How do you use variables inside templates?
182. What are Jinja2 filters?
183. What are Jinja2 tests?
184. What is `{% if %}`?
185. What is `{% for %}`?
186. How do you loop inside a template?
187. How do you provide default values in Jinja?
188. How do you perform string manipulation?
189. How do you convert a variable to JSON?
190. How do you parse JSON?
191. How do you use conditionals in Jinja?
192. How do you troubleshoot a template rendering error?

---

# 9. Loops

193. How do you loop over a list?
194. `loop` vs `with_items`?
195. Why is `loop` preferred?
196. How do you loop over dictionaries?
197. How do you loop over files?
198. How do you loop over users?
199. How do you register output from a loop?
200. How do you conditionally execute items inside a loop?
201. How do you loop over nested data?
202. How do you use `loop_control`?
203. What is `loop_var`?

---

# 10. Handlers

204. What is a handler?
205. Why do we use handlers?
206. When does a handler execute?
207. What does `notify` do?
208. Can multiple tasks notify the same handler?
209. When does the handler actually run?
210. What is `meta: flush_handlers`?
211. How do you force handlers to execute immediately?
212. What happens if a task changes but the play later fails?
213. How would you restart Nginx only when its configuration changes?

---

# 11. Roles

Roles are explicitly covered in your source as reusable organized units containing tasks, templates, files and variables. 

214. What is an Ansible role?
215. Why do we use roles?
216. What is the standard role directory structure?
217. Explain `tasks/main.yml`.
218. What is `handlers/main.yml`?
219. What is `templates/`?
220. What is `files/`?
221. What is `vars/`?
222. What is `defaults/`?
223. `vars` vs `defaults`?
224. What is `meta/main.yml`?
225. How do you create a role?
226. How do you call a role from a playbook?
227. How do you pass variables to a role?
228. How do you override role defaults?
229. How do role dependencies work?
230. What are role tags?
231. How do you test roles?
232. How do you reuse one role across multiple environments?
233. How do you version roles?
234. What is Ansible Galaxy?
235. How do you install a role from Galaxy?
236. How would you build your own internal Ansible Galaxy?
237. How do you structure roles for a large organization?

---

# 12. Ansible Vault / Security

238. What is Ansible Vault?
239. Why do we use Ansible Vault?
240. How do you encrypt a file?
241. How do you decrypt a file?
242. How do you edit an encrypted file?
243. How do you use Vault in CI/CD?
244. Where should Vault passwords be stored?
245. How do you rotate Vault passwords?
246. Can Vault encrypt individual variables?
247. How do you manage production secrets?
248. Ansible Vault vs AWS Secrets Manager?
249. Ansible Vault vs HashiCorp Vault?
250. How do you prevent secrets from appearing in logs?
251. What does `no_log: true` do?
252. How would you manage database credentials in Ansible?
253. How do you securely pass secrets from Jenkins to Ansible?
254. How do you integrate Ansible with a cloud secret manager?

---

# 13. SSH / Connectivity

255. How does Ansible connect to Linux?
256. How do you configure SSH authentication?
257. Password vs SSH key authentication?
258. How do you specify an SSH key?
259. What is `ansible_user`?
260. What is `ansible_port`?
261. What is `ansible_host`?
262. How do you use a bastion/jump server?
263. How do you troubleshoot SSH connectivity?
264. What if ping works but Ansible fails?
265. What if SSH works manually but Ansible fails?
266. What if you get `Permission denied`?
267. What if you get `UNREACHABLE`?
268. How do you troubleshoot host-key problems?
269. How do you configure ProxyJump?
270. How do you use `become` when SSH user doesn't have root access?

---

# 14. Privilege Escalation

271. What is `become`?
272. Why do we use `become: true`?
273. What is sudo?
274. `become` vs `sudo`?
275. How do you execute a task as root?
276. How do you execute a task as another user?
277. What is `become_user`?
278. How do you configure passwordless sudo?
279. How do you troubleshoot sudo failures?
280. How do you restrict Ansible's sudo privileges for security?

---

# 15. Error Handling

281. How do you handle failures in Ansible?
282. What is `ignore_errors`?
283. Why should `ignore_errors` be used carefully?
284. What is `failed_when`?
285. What is `changed_when`?
286. Difference between `failed_when` and `changed_when`?
287. What is `block`?
288. What is `rescue`?
289. What is `always`?
290. How do you implement try/catch-like behavior?
291. How do you rollback after a failed deployment?
292. How do you continue execution even if one host fails?
293. What is `any_errors_fatal`?
294. What is `max_fail_percentage`?
295. How do you stop deployment if validation fails?

---

# 16. Tags

296. What are Ansible tags?
297. Why are tags useful?
298. How do you run only selected tags?
299. How do you skip tags?
300. What are `--tags` and `--skip-tags`?
301. How do you use tags in roles?
302. How do you design tags for production deployments?

---

# 17. Ansible Configuration

303. What is `ansible.cfg`?
304. Where can `ansible.cfg` exist?
305. What is the precedence of Ansible configuration files?
306. How do you specify the inventory in `ansible.cfg`?
307. How do you configure remote user?
308. How do you configure SSH settings?
309. How do you increase forks?
310. What is `forks`?
311. How does `forks` affect performance?
312. What is `timeout`?
313. How do you configure logging?
314. How do you disable host-key checking?
315. What are the risks of disabling host-key checking?

---

# 18. Performance & Scalability — 8-Year Level

316. Your playbook takes 30 minutes. How would you optimize it?
317. How do you make Ansible execution faster?
318. What is `forks`?
319. What is `serial`?
320. `forks` vs `serial`?
321. What is `strategy: linear`?
322. What is `strategy: free`?
323. Linear vs free strategy?
324. How can fact gathering affect performance?
325. How do you optimize fact gathering?
326. How do you reduce unnecessary tasks?
327. How do you avoid repeated package installations?
328. How do you optimize large inventories?
329. How do you execute tasks in parallel?
330. How do you implement rolling deployments?
331. How do you deploy to 1,000 servers safely?
332. How would you deploy to production without impacting all servers?
333. What is `serial: 10%`?
334. How do you implement batch deployment?
335. How do you stop a rollout if failures cross a threshold?
336. How do you use `max_fail_percentage` in production?
337. How do you optimize SSH connections?
338. How would you troubleshoot slow Ansible execution?

---

# 19. CI/CD + Ansible

339. How do you integrate Ansible with Jenkins?
340. How do you integrate Ansible with GitLab CI?
341. How do you integrate Ansible with GitHub Actions?
342. Where does Ansible fit in a CI/CD pipeline?
343. Jenkins vs Ansible?
344. Terraform vs Ansible?
345. Why use Terraform + Ansible together?
346. How does Terraform provision infrastructure and Ansible configure it?
347. How do you pass Terraform outputs to Ansible?
348. How do you manage secrets in CI/CD?
349. How do you promote an application from dev → QA → staging → production?
350. How do you implement approval before production deployment?
351. How do you rollback through Ansible?
352. How do you version Ansible playbooks?
353. How do you perform code review for Ansible?
354. How do you validate Ansible before merging?
355. What is `ansible-lint`?
356. What is Molecule?
357. How do you test an Ansible role?

---

# 20. Ansible + AWS

Your source explicitly includes cloud provisioning and mentions AWS, GCP and Azure. 

358. How have you used Ansible with AWS?
359. Can Ansible create EC2 instances?
360. How do you configure AWS credentials for Ansible?
361. How do you avoid hardcoding AWS credentials?
362. How do you use IAM roles with Ansible?
363. How do you dynamically discover EC2 instances?
364. How do you configure security groups?
365. How do you create an EC2 instance using Ansible?
366. How do you configure an EC2 instance after creation?
367. How do you install software on newly created EC2 instances?
368. How do you manage multiple AWS accounts?
369. How do you manage dev/staging/prod AWS environments?
370. Ansible vs Terraform for AWS infrastructure?
371. When would you choose Terraform instead of Ansible?

---

# 21. Kubernetes + Ansible

372. Can Ansible manage Kubernetes?
373. Why use Ansible with Kubernetes?
374. Can Ansible deploy Kubernetes?
375. How can Ansible configure Kubernetes nodes?
376. How do you deploy an application to Kubernetes using Ansible?
377. Ansible vs Helm?
378. Ansible vs Kubernetes Operators?
379. How do you manage Kubernetes configuration with Ansible?
380. How would you automate Kubernetes cluster setup?
381. How would you troubleshoot an Ansible-based Kubernetes deployment?

---

# 22. Ansible + Docker

382. Can Ansible manage Docker?
383. How do you start/stop containers using Ansible?
384. How do you deploy a Docker application using Ansible?
385. Ansible vs Docker Compose?
386. Ansible vs Kubernetes?
387. How do you update a container image using Ansible?
388. How would you perform zero-downtime Docker deployment?

---

# 23. Production Scenario Questions ⭐

These are especially important for an **8-year engineer**.

389. You have 500 servers and need to install Java. How would you design the playbook?
390. You need to patch 1,000 production servers. How would you safely do it?
391. Your Ansible deployment failed on 10% of servers. What will you do?
392. Your playbook works in dev but fails in production. How do you troubleshoot?
393. Your playbook works manually but fails from Jenkins. Why?
394. Ansible says a host is unreachable. What do you check?
395. SSH works manually but Ansible cannot connect. What do you check?
396. A task keeps showing `changed` every time. Why?
397. A task fails on Ubuntu but works on RHEL. How do you handle it?
398. Your application deployment succeeded but the application is down. What next?
399. Nginx configuration changed. How do you restart Nginx only when necessary?
400. A deployment fails halfway. How do you rollback?
401. How would you deploy an application without downtime?
402. How would you implement blue-green deployment using Ansible?
403. How would you implement canary deployment using Ansible?
404. How would you implement rolling deployment?
405. How would you deploy to 100 servers in batches of 10?
406. What happens if server number 7 fails during deployment?
407. How do you prevent deployment to all servers if one batch fails?
408. How would you design an Ansible framework for 50+ applications?
409. How would you organize Ansible repositories for multiple teams?
410. How would you manage different configurations for 20 environments?
411. How would you manage secrets across those environments?
412. How would you make your playbooks reusable?
413. How would you prevent developers from modifying production configuration?
414. How would you audit who changed an Ansible configuration?
415. How would you integrate Ansible with Git?
416. How would you design Ansible for disaster recovery?
417. How would you recover if the Ansible control node is lost?
418. How do you make Ansible automation highly available?
419. How do you handle configuration drift?
420. How do you detect configuration drift?
421. How do you enforce desired state?
422. How do you safely make changes to thousands of machines?

---

# 24. Troubleshooting Scenarios ⭐⭐⭐

423. `UNREACHABLE!` — what does it mean?
424. `Permission denied` — how do you troubleshoot?
425. `sudo: password is required` — how do you fix it?
426. `module not found` — what do you check?
427. Python missing on target — what happens?
428. Python version incompatible — how do you troubleshoot?
429. YAML syntax error — how do you debug?
430. Template rendering failed — what do you check?
431. Variable undefined — how do you debug?
432. Wrong variable value — how do you find where it came from?
433. Role not found — how do you troubleshoot?
434. Handler not triggered — why?
435. Task unexpectedly skipped — why?
436. Task runs on the wrong server — how do you debug?
437. Dynamic inventory isn't returning instances — what do you check?
438. Playbook is extremely slow — troubleshooting approach?
439. Only one server is slow while others are fine — what do you investigate?
440. Jenkins execution fails but local execution succeeds — troubleshooting approach?
441. Vault decryption fails — what do you check?
442. Playbook changes every time — how do you make it idempotent?
443. Package installation fails on only some servers — what do you investigate?
444. File permissions are incorrect after deployment — where do you look?
445. Ansible is restarting services unnecessarily — how do you fix it?

---

# 25. Architecture / Design Questions ⭐⭐⭐

446. Design an enterprise Ansible architecture.
447. How would you structure Ansible for 5,000 servers?
448. How would you manage multiple teams using one Ansible platform?
449. How would you separate dev/staging/prod?
450. How would you design inventory architecture?
451. How would you design role architecture?
452. How would you manage secrets at enterprise scale?
453. How would you integrate Ansible with GitOps?
454. How would you implement RBAC around Ansible?
455. How would you implement audit logging?
456. How would you implement approval workflows?
457. How would you design a centralized Ansible control system?
458. What is Ansible Automation Platform?
459. What is Ansible Automation Controller?
460. What is Ansible AWX?
461. AWX vs Ansible Automation Controller?
462. How does Ansible Tower/Automation Controller work?
463. What is a Job Template?
464. What is an Inventory in Automation Controller?
465. What is a Credential?
466. What is a Project?
467. What is a Workflow Job Template?
468. How would you design an enterprise automation platform?
469. How would you control who can execute production playbooks?
470. How would you schedule automated patching?

---

# 26. Advanced Ansible Questions

471. What are action plugins?
472. What are callback plugins?
473. What are connection plugins?
474. What are lookup plugins?
475. What are filter plugins?
476. What are test plugins?
477. What are inventory plugins?
478. What are strategy plugins?
479. What are vars plugins?
480. What are cache plugins?
481. What are become plugins?
482. What are module plugins?
483. How do you write a custom Ansible module?
484. How do you write a custom filter?
485. How do you write a callback plugin?
486. What is an Ansible collection?
487. What is the difference between a role and a collection?
488. How do you install collections?
489. What is `ansible-galaxy`?
490. How do you publish an internal collection?
491. What is FQCN?
492. Why should FQCN be used?
493. How do you handle collection dependencies?
494. How do you pin collection versions?
495. How do you manage Ansible version compatibility?

---

# 27. Commands You Should Know for an 8-Year Interview

Be ready to explain these **without Googling**:

```bash
ansible --version

ansible all -i inventory -m ping

ansible all -i inventory -m setup

ansible-inventory --list

ansible-inventory --graph

ansible-playbook playbook.yml

ansible-playbook -i inventory playbook.yml

ansible-playbook playbook.yml --check

ansible-playbook playbook.yml --diff

ansible-playbook playbook.yml -v

ansible-playbook playbook.yml -vv

ansible-playbook playbook.yml -vvv

ansible-playbook playbook.yml --limit server1

ansible-playbook playbook.yml --tags deploy

ansible-playbook playbook.yml --skip-tags config

ansible-playbook playbook.yml --start-at-task "Install nginx"

ansible-playbook playbook.yml --syntax-check

ansible-galaxy role init myrole

ansible-galaxy install <role>

ansible-galaxy collection install <collection>

ansible-vault create secrets.yml

ansible-vault encrypt secrets.yml

ansible-vault decrypt secrets.yml

ansible-vault edit secrets.yml

ansible-vault view secrets.yml
```

The basic execution pattern in your source is `ansible-playbook -i inventory_file webserver.yml`, followed by verification of task success/failure. 

---

# 28. Most Important Comparisons

These are **very commonly asked**:

| Question                          | Must Know                                                     |
| --------------------------------- | ------------------------------------------------------------- |
| Ansible vs Terraform              | Configuration/automation vs infrastructure provisioning       |
| Ansible vs Chef                   | Agentless vs agent-based model                                |
| Ansible vs Puppet                 | Push-oriented automation vs Puppet's typical agent/pull model |
| Ansible vs Jenkins                | Automation engine vs CI/CD orchestrator                       |
| Ansible vs Helm                   | Server/config automation vs Kubernetes package management     |
| Ansible vs Kubernetes             | Automation tool vs container orchestration platform           |
| Playbook vs Role                  | Instructions/orchestration vs reusable structure              |
| Play vs Playbook                  | One execution definition vs collection                        |
| Task vs Module                    | Unit of work vs implementation that performs it               |
| Inventory vs Playbook             | WHERE vs WHAT                                                 |
| `copy` vs `template`              | Static file vs dynamically rendered file                      |
| `command` vs `shell`              | Command execution vs shell features                           |
| `import_tasks` vs `include_tasks` | Static vs dynamic                                             |
| `vars` vs `defaults`              | Higher vs lower role-variable precedence                      |
| `forks` vs `serial`               | Parallelism vs rollout batching                               |
| `failed_when` vs `changed_when`   | Failure condition vs change detection                         |
| `ignore_errors` vs `rescue`       | Ignore failure vs structured recovery                         |
| Vault vs Secrets Manager          | Encrypted Ansible data vs external secret management          |

---

# 29. Questions Based Directly on Your Uploaded Material

Don't skip these because they are the foundation from the PATHNEX material:

1. What is Ansible?
2. Why is Ansible agentless?
3. What protocols does Ansible use?
4. What is a playbook?
5. What is inventory?
6. Static vs dynamic inventory?
7. What is a module?
8. What is the `yum` module?
9. What is the `copy` module?
10. What is a role?
11. Control Node vs Managed Node?
12. How does Ansible work?
13. Explain `Connect → Execute → Report`.
14. Explain `Write → Run → Verify`.
15. What are Ansible use cases?
16. How is Ansible used for system configuration?
17. How is Ansible used for application deployment?
18. How is Ansible used for cloud provisioning?
19. How is Ansible used for patch management?
20. How is Ansible related to IaC?
21. How would you install Nginx using Ansible?
22. How would you deploy a LAMP stack?
23. What is LAMP?
24. What is MEAN?
25. What are the benefits of Ansible?

These concepts map directly to the source's workflow and use-case sections.  

---

# 30. The 30 Questions I Would Expect Most for 8 Years

If the interviewer has only **30–45 minutes**, I'd prioritize these:

1. Explain your real-world Ansible architecture.
2. How does Ansible work internally?
3. Why is Ansible agentless?
4. Explain inventory architecture in your project.
5. Static vs dynamic inventory.
6. Explain roles and their directory structure.
7. Explain variable precedence.
8. `vars` vs `defaults`.
9. `copy` vs `template`.
10. `command` vs `shell`.
11. How do you achieve idempotency?
12. How do you handle failures?
13. `failed_when` vs `changed_when`.
14. Explain handlers.
15. Explain `register`.
16. Explain `set_fact`.
17. Explain Ansible Vault.
18. How do you manage secrets?
19. How do you integrate Ansible with Jenkins?
20. How do you implement rolling deployment?
21. How do you deploy to 1,000 servers safely?
22. How do you optimize a slow playbook?
23. Explain `forks`, `serial`, and `strategy`.
24. How do you troubleshoot `UNREACHABLE`?
25. SSH works manually but Ansible fails—why?
26. How do you handle configuration drift?
27. How do you design Ansible for multiple environments?
28. Ansible vs Terraform?
29. Ansible vs Helm?
30. **Walk me through one production automation you personally designed and the problems you solved.**

### The key difference at 8 years

Don't prepare only:

> **"What is Ansible?"**

Prepare to answer:

> **"You have 2,000 production servers, four environments, multiple application teams, secrets, rolling deployment requirements, and a failed deployment in the middle. Design the complete Ansible solution and explain how you would troubleshoot and operate it."**

That is the level where an **8-year DevOps interview** usually moves from *tool knowledge* to **architecture + production experience + troubleshooting + decision making**.
