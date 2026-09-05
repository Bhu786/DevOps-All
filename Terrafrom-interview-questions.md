# Terraform — 8 Years DevOps Engineer: Complete Interview Question Bank



## 1. Terraform Fundamentals

1. What is Terraform?
2. Why do we use Terraform?
3. What is Infrastructure as Code?
4. What are the advantages of IaC?
5. What is declarative infrastructure?
6. What is the difference between declarative and imperative approaches?
7. Why is Terraform called declarative?
8. What problem does Terraform solve?
9. What are the major components of Terraform?
10. What are the core concepts of Terraform?
11. What is HCL?
12. Why does Terraform use HCL?
13. What is the difference between HCL and JSON syntax in Terraform?
14. What is the difference between HCL and Bash in Terraform?
15. Is Terraform cloud-specific?
16. Which cloud providers does Terraform support?
17. Can Terraform manage on-premises infrastructure?
18. Can Terraform manage Kubernetes?
19. Can Terraform manage SaaS applications?
20. What is Terraform's architecture?
21. How does Terraform communicate with AWS?
22. How does Terraform communicate with Azure?
23. How does Terraform communicate with GCP?
24. What is a Terraform provider?
25. What is a Terraform resource?
26. What is a Terraform module?
27. What is Terraform state?
28. What is a Terraform backend?
29. What is a data source?
30. What is the difference between a resource and a data source?
31. What is the difference between Terraform and CloudFormation?
32. What is the difference between Terraform and Ansible?
33. What is the difference between Terraform and Pulumi?
34. What are Terraform's limitations?
35. What are the disadvantages of Terraform?
36. When would you not use Terraform?
37. Why would you choose Terraform over native cloud IaC?
38. Can Terraform manage resources that were not created by Terraform?
39. Can Terraform modify manually created infrastructure?
40. Can Terraform manage an existing environment?
41. What happens if someone manually changes infrastructure managed by Terraform?
42. What is configuration drift?
43. How does Terraform detect drift?
44. What does Terraform mean by desired state?
45. What is the difference between desired state, actual state, and Terraform state?
46. Why is state so important in Terraform?
47. What happens if the Terraform state file is deleted?
48. Can Terraform work without a state file?
49. Why shouldn't Terraform state normally be committed to Git?
50. What are the most important Terraform concepts you would expect an 8-year DevOps engineer to know?

---

# 2. Terraform Installation and CLI

51. How do you install Terraform?
52. How do you verify the Terraform version?
53. How do you upgrade Terraform?
54. How do you manage multiple Terraform versions?
55. What is `terraform --version`?
56. What does `terraform init` do?
57. What happens internally during `terraform init`?
58. When should you run `terraform init`?
59. What happens if you don't run `terraform init`?
60. What does `terraform validate` do?
61. What does `terraform fmt` do?
62. What is the difference between `terraform fmt` and `terraform validate`?
63. What does `terraform plan` do?
64. What does `terraform apply` do?
65. What does `terraform destroy` do?
66. What is the difference between `terraform plan` and `terraform apply`?
67. What is the difference between `terraform destroy` and deleting resources manually?
68. What is `terraform show`?
69. What is `terraform output`?
70. What is `terraform console`?
71. What is `terraform providers`?
72. What is `terraform graph`?
73. What is `terraform get`?
74. What is `terraform force-unlock`?
75. What is `terraform state`?
76. What is `terraform import`?
77. What is `terraform refresh`?
78. Why is the old `terraform refresh` workflow no longer preferred?
79. What is `terraform plan -refresh-only`?
80. What is `terraform apply -refresh-only`?
81. What is `terraform plan -out`?
82. Why would you save a Terraform plan to a file?
83. How do you apply a previously generated plan?
84. What is `terraform plan -destroy`?
85. What is `terraform plan -target`?
86. Why should `-target` generally not be used as a normal deployment strategy?
87. What is `terraform apply -auto-approve`?
88. When would you use `-auto-approve`?
89. What risks exist with `-auto-approve`?
90. What Terraform commands do you commonly use in production?

---

# 3. Terraform Configuration and HCL

91. What is the basic structure of a Terraform configuration?
92. What are Terraform configuration blocks?
93. What is a resource block?
94. What is a provider block?
95. What is a variable block?
96. What is an output block?
97. What is a module block?
98. What is a data block?
99. What is a locals block?
100. What is a terraform block?
101. What is a backend block?
102. What is a lifecycle block?
103. What is a `resource "type" "name"` declaration?
104. What does the resource type represent?
105. What does the resource name represent?
106. What is a Terraform resource address?
107. What is the difference between resource type and resource name?
108. What happens if two resources have the same Terraform name?
109. What are Terraform identifiers?
110. What are Terraform expressions?
111. What are Terraform arguments?
112. What are Terraform attributes?
113. What are Terraform blocks?
114. What are Terraform meta-arguments?
115. What is interpolation in Terraform?
116. Is `${}` still required for normal Terraform expressions?
117. What are Terraform comments?
118. What is the difference between single-line and multi-line comments in HCL?
119. Can Terraform configuration be written in JSON?
120. What is the difference between `.tf` and `.tf.json`?
121. How does Terraform load multiple `.tf` files?
122. Does Terraform care about the filename `main.tf`?
123. Does Terraform execute files in filename order?
124. Can provider configuration be in `main.tf`?
125. Can variables be defined in any `.tf` file?
126. Why do teams commonly separate `main.tf`, `variables.tf`, `outputs.tf`, and `providers.tf`?
127. Is this file structure mandatory?
128. How does Terraform combine multiple configuration files?
129. What happens if two `.tf` files contain conflicting configuration?
130. How do you organize a large Terraform repository?

---

# 4. Providers

131. What is a Terraform provider?
132. How does Terraform install a provider?
133. What is `required_providers`?
134. What is the difference between `required_providers` and the `provider` block?
135. Where should `required_providers` be defined?
136. Why should provider versions be pinned?
137. What is provider version constraint syntax?
138. What does `~>` mean in Terraform?
139. What is the difference between `>=`, `>`, `<`, `<=`, `=`, and `~>`?
140. What is `.terraform.lock.hcl`?
141. Why should `.terraform.lock.hcl` be committed to Git?
142. What does `terraform init -upgrade` do?
143. What happens when you change a provider version?
144. How do you safely upgrade a provider?
145. What happens if two modules require incompatible provider versions?
146. Can child modules define provider configurations?
147. How are provider configurations passed to child modules?
148. What is provider aliasing?
149. Why would you use multiple AWS provider configurations?
150. How do you deploy resources into multiple AWS regions using Terraform?
151. How do you deploy resources into multiple AWS accounts using Terraform?
152. How do provider aliases work with modules?
153. What happens if a module requires a provider alias?
154. What is an implicit provider configuration?
155. What is an explicit provider configuration?
156. How does Terraform know which provider a resource should use?
157. Can one Terraform configuration use multiple versions of the same provider?
158. Can two modules use different provider aliases?
159. What happens if a provider configuration is removed while resources still exist in state?
160. How would you troubleshoot a provider initialization error?

---

# 5. Resources

161. What is a Terraform resource?
162. How does Terraform identify a resource?
163. What is a resource address?
164. What is the difference between resource configuration and resource state?
165. What happens when a resource is added to configuration?
166. What happens when a resource is removed from configuration?
167. What happens when a resource attribute changes?
168. What does Terraform mean by `+`, `~`, and `-` in a plan?
169. What does `-/+` mean in Terraform plan output?
170. Why does Terraform sometimes replace instead of update a resource?
171. What determines whether an attribute causes replacement?
172. What does `ForceNew` mean in a provider schema?
173. How do you identify why Terraform wants to replace a resource?
174. How do you prevent an accidental replacement?
175. What happens if someone manually deletes a Terraform-managed resource?
176. What happens if someone manually creates a resource with the same name?
177. Can two Terraform resources manage the same cloud resource?
178. What happens if two resources point to the same infrastructure object?
179. How do you avoid duplicate resource ownership?
180. How do you safely remove a resource from Terraform management without deleting the actual resource?

---

# 6. Data Sources

181. What is a Terraform data source?
182. Why would you use a data source?
183. What is the difference between a data source and a resource?
184. Can a data source create infrastructure?
185. How does Terraform refresh a data source?
186. Can a data source depend on a resource?
187. Can you use a resource output as input to a data source?
188. What happens if a data source cannot find the requested object?
189. What is the difference between querying an existing AMI using a data source and hard-coding its ID?
190. How would you use AWS data sources to discover VPC information?
191. How would you use data sources across modules?
192. What happens when a data source value is unknown during planning?
193. Can data sources cause Terraform plan-time errors?
194. When should you prefer a data source over a variable?
195. What are common mistakes when using data sources?

---

# 7. Variables

196. What are Terraform input variables?
197. Why do we use variables?
198. What is the difference between a variable and a local?
199. What are variable types in Terraform?
200. What is a string variable?
201. What is a number variable?
202. What is a bool variable?
203. What is a list variable?
204. What is a set variable?
205. What is a map variable?
206. What is an object variable?
207. What is a tuple variable?
208. What is `any` type?
209. What is variable type validation?
210. How do you define variable validation rules?
211. What is a variable default?
212. What happens if a variable has no default value?
213. What is the precedence of Terraform variable values?
214. What is `terraform.tfvars`?
215. What is `terraform.tfvars.json`?
216. What is `*.auto.tfvars`?
217. What is the difference between `terraform.tfvars` and `*.auto.tfvars`?
218. How do environment variables provide Terraform variables?
219. What does the `TF_VAR_` prefix mean?
220. How do you pass a variable from the command line?
221. How do you pass variables in CI/CD?
222. How do you handle environment-specific variables?
223. How do you protect sensitive variable values?
224. What does `sensitive = true` do?
225. Does `sensitive = true` encrypt the value?
226. Does marking a variable sensitive prevent the value from entering state?
227. What happens to sensitive values in Terraform state?
228. How would you design variables for a reusable production module?
229. What makes a Terraform variable interface good or bad?
230. How do you validate an AWS region variable?
231. How do you validate an environment variable such as `dev`, `stage`, or `prod`?

---

# 8. Locals

232. What are Terraform locals?
233. Why would you use locals?
234. What is the difference between variables and locals?
235. Can locals be overridden?
236. Can locals reference variables?
237. Can locals reference resources?
238. Can locals reference data sources?
239. Can locals reference other locals?
240. When should you use locals instead of variables?
241. How would you create common tags using locals?
242. How do locals improve maintainability?
243. Can excessive use of locals make Terraform harder to understand?

---

# 9. Outputs

244. What are Terraform outputs?
245. Why are outputs useful?
246. How do you define an output?
247. How do you access an output from the CLI?
248. How do you expose a child module output to the root module?
249. Can one module consume another module's output?
250. How do module outputs establish dependencies?
251. Can outputs contain sensitive information?
252. What happens if an output is marked sensitive?
253. Where are Terraform outputs stored?
254. How do you use Terraform outputs in CI/CD?
255. What is the difference between an output and a variable?
256. What is the difference between an output and a local?
257. How do you output the private IP of an EC2 instance?
258. How do you output a list of resource IDs?
259. How would you expose only required information from a module?

---

# 10. Terraform Expressions and Functions

260. What are Terraform expressions?
261. What are Terraform operators?
262. What are conditional expressions?
263. What is the syntax of a Terraform conditional expression?
264. What are `for` expressions?
265. What is a `for` expression used for?
266. What is the difference between `for` expressions and `for_each`?
267. What is the splat expression?
268. When would you use a splat expression?
269. What are Terraform functions?
270. What are commonly used Terraform functions?
271. What does `lookup()` do?
272. What does `try()` do?
273. What does `can()` do?
274. What does `merge()` do?
275. What does `concat()` do?
276. What does `flatten()` do?
277. What does `toset()` do?
278. What does `tolist()` do?
279. What does `tomap()` do?
280. What does `distinct()` do?
281. What does `compact()` do?
282. What does `join()` do?
283. What does `split()` do?
284. What does `replace()` do?
285. What does `format()` do?
286. What does `coalesce()` do?
287. What does `length()` do?
288. What does `contains()` do?
289. What does `element()` do?
290. What does `keys()` do?
291. What does `values()` do?
292. What does `zipmap()` do?
293. What does `jsonencode()` do?
294. What does `jsondecode()` do?
295. What does `yamldecode()` do?
296. What does `yamlencode()` do?
297. How do you handle optional values in Terraform?
298. How do you handle null values?
299. What is the difference between `null` and an empty string?
300. What is an unknown value in Terraform?
301. What is a known value versus an unknown value?
302. Why can Terraform sometimes not determine a value during plan?
303. How do unknown values affect `for_each`?
304. How do unknown values affect `count`?
305. How do you troubleshoot an expression evaluation error?

---

# 11. count and for_each

306. What is the `count` meta-argument?
307. What is the `for_each` meta-argument?
308. What is the difference between `count` and `for_each`?
309. When would you choose `count`?
310. When would you choose `for_each`?
311. Why is `for_each` generally safer when resources have unique identities?
312. How are `count` resources addressed?
313. How are `for_each` resources addressed?
314. What happens if you remove an item from a list used with `count`?
315. What happens if you remove an item from a map used with `for_each`?
316. Why can changing a list order with `count` cause unexpected replacements?
317. Can you use both `count` and `for_each` on the same resource?
318. Can modules use `count`?
319. Can modules use `for_each`?
320. Can data sources use `count`?
321. Can data sources use `for_each`?
322. Can you use `for_each` with a set?
323. Why must `for_each` keys be known during planning?
324. Why can't you use sensitive values as `for_each` keys?
325. How do you migrate a resource from `count` to `for_each` safely?
326. How do you migrate from `for_each` to `count`?
327. How would you troubleshoot Terraform destroying resources after changing `count` to `for_each`?
328. What happens to Terraform addresses when converting a single resource to `for_each`?
329. How would you use `for_each` with a complex object map?
330. How would you create multiple AWS EC2 instances with different instance types using `for_each`?

---

# 12. Dynamic Blocks

331. What is a dynamic block?
332. Why would you use a dynamic block?
333. What is the difference between `dynamic` and `for_each`?
334. Can dynamic blocks create resources?
335. What can dynamic blocks generate?
336. Can dynamic blocks generate lifecycle blocks?
337. Can dynamic blocks generate provisioner blocks?
338. What is the `content` block inside a dynamic block?
339. What is the iterator variable in a dynamic block?
340. How do you use `for_each` inside a dynamic block?
341. When should you avoid dynamic blocks?
342. How can overusing dynamic blocks make Terraform code difficult to maintain?

---

# 13. Dependencies and Dependency Graph

343. How does Terraform determine resource dependencies?
344. What is an implicit dependency?
345. What is an explicit dependency?
346. What is `depends_on`?
347. When should you use `depends_on`?
348. When should you avoid `depends_on`?
349. What is the difference between implicit dependency and `depends_on`?
350. How does Terraform build its dependency graph?
351. What is a dependency graph?
352. How does Terraform use the dependency graph during plan?
353. How does Terraform use the dependency graph during apply?
354. Does Terraform create resources strictly sequentially?
355. How does Terraform achieve parallelism?
356. What happens if resource A depends on resource B?
357. Can Terraform detect circular dependencies?
358. What happens when Terraform detects a dependency cycle?
359. How do you troubleshoot a dependency cycle?
360. What is `terraform graph`?
361. How would you visualize Terraform dependencies?
362. How can excessive `depends_on` reduce Terraform parallelism?
363. How can `depends_on` create unnecessary dependencies?
364. Can a module have `depends_on`?
365. What happens when a module depends on another module?

---

# 14. Modules

366. What is a Terraform module?
367. What is the root module?
368. What is a child module?
369. What is the difference between root and child modules?
370. Why should we use modules?
371. What are the advantages of Terraform modules?
372. What are the disadvantages of Terraform modules?
373. How do you design a reusable Terraform module?
374. What should a good Terraform module contain?
375. What should a module expose through variables?
376. What should a module expose through outputs?
377. What should not be hard-coded inside a reusable module?
378. How do you structure Terraform modules?
379. What is a local module?
380. What is a registry module?
381. What is a Git-based module?
382. How do you reference a module from Git?
383. How do you version Terraform modules?
384. Why should module versions be pinned?
385. What is semantic versioning for Terraform modules?
386. How do you upgrade a module safely?
387. How do you roll back a module version?
388. Can modules contain providers?
389. How should provider configuration be handled in reusable modules?
390. How do you pass provider aliases into modules?
391. Can one module call another module?
392. How deeply can modules be nested?
393. What are module outputs?
394. What are module inputs?
395. How do you pass variables from root module to child module?
396. How do you pass outputs from child module to root module?
397. How do you pass output from one module into another module?
398. What happens if a module input is missing?
399. How do you make a module input optional?
400. How do you create multiple module instances?
401. How do `count` and `for_each` work on modules?
402. What is a module registry?
403. How do you publish a module?
404. What are Terraform Registry naming conventions?
405. How do you test a reusable module?
406. How do you handle breaking changes in a module?
407. What is module composition?
408. What is module abstraction?
409. How much abstraction is too much in Terraform?
410. How would you design networking, compute, and database modules?
411. Should one module create an entire application stack?
412. How do you decide module boundaries?
413. How do you prevent modules from becoming tightly coupled?
414. How do you handle module ownership in a large organization?
415. How do you manage hundreds of Terraform modules?
416. How do you prevent module version sprawl?
417. How do you deprecate an old module?
418. How do you safely refactor a production module?

---

# 15. Terraform State

419. What is Terraform state?
420. Why does Terraform need state?
421. What information does Terraform state contain?
422. How does Terraform map configuration to real infrastructure?
423. Why can't Terraform simply query AWS every time instead of using state?
424. What is `terraform.tfstate`?
425. What is `terraform.tfstate.backup`?
426. What happens during a Terraform refresh?
427. When does Terraform refresh state?
428. Does `terraform plan` refresh state?
429. Does `terraform apply` refresh state?
430. What is refresh-only mode?
431. What happens if Terraform state is out of sync with infrastructure?
432. What is state drift?
433. How do you detect state drift?
434. How do you fix state drift?
435. What happens if a resource is deleted manually?
436. What happens if a resource is modified manually?
437. What happens if a resource is created manually?
438. What happens if the state file is corrupted?
439. What happens if the state file is accidentally deleted?
440. How do you recover deleted Terraform state?
441. How do you restore Terraform state from backup?
442. How do you inspect state?
443. What does `terraform state list` do?
444. What does `terraform state show` do?
445. What does `terraform state mv` do?
446. What does `terraform state rm` do?
447. What does `terraform state pull` do?
448. What does `terraform state push` do?
449. When would you use `terraform state mv`?
450. When would you use `terraform state rm`?
451. Why is manually editing `terraform.tfstate` dangerous?
452. How do you safely manipulate Terraform state?
453. How do you remove a resource from Terraform state without deleting it?
454. How do you move a resource from one module to another?
455. How do you rename a Terraform resource without destroying infrastructure?
456. What is a state migration?
457. What is a state lineage?
458. What is a state serial?
459. What is Terraform state locking?
460. Why is state locking required?
461. Which operations require state locking?
462. What happens if state locking fails?
463. What is `terraform force-unlock`?
464. When should you use `terraform force-unlock`?
465. What are the risks of force-unlocking?
466. What happens if two engineers run `terraform apply` simultaneously?
467. What happens if CI/CD runs Terraform while another engineer is applying?
468. How do you troubleshoot a stuck Terraform state lock?
469. How do you identify who owns a state lock?
470. What happens if Terraform crashes while holding a lock?
471. How do you recover after a failed Terraform apply?
472. Can Terraform partially apply resources?
473. What happens to state after a partial apply?
474. How do you recover from a partial apply?
475. What happens if Terraform crashes halfway through an apply?
476. What happens if the cloud API succeeds but Terraform crashes before updating state?
477. How would you reconcile state after such a failure?

---

# 16. Remote State and Backends

478. What is a Terraform backend?
479. Why do we need a backend?
480. What is the default Terraform backend?
481. What is local state?
482. What is remote state?
483. Why should production Terraform use remote state?
484. What are the advantages of remote backends?
485. What are the disadvantages of remote backends?
486. Which remote backends have you used?
487. How does the S3 backend work?
488. How do you configure an S3 backend?
489. What are the bucket, key, and region in an S3 backend?
490. How do you organize state keys for multiple environments?
491. How do you isolate dev, stage, and prod state?
492. How do you enable state locking for your backend?
493. How do you secure an S3 Terraform state bucket?
494. How do you encrypt Terraform state?
495. How do you control access to Terraform state?
496. How do you enable versioning on Terraform state?
497. Why is state bucket versioning important?
498. How do you recover a previous version of Terraform state?
499. How do you protect Terraform state from accidental deletion?
500. How do you audit access to Terraform state?
501. How do you handle cross-account access to Terraform state?
502. How do you manage backend credentials?
503. Should backend credentials be hard-coded?
504. What is partial backend configuration?
505. What is `-backend-config`?
506. What risks exist when using `-backend-config` for credentials?
507. What happens during `terraform init` when the backend changes?
508. What does `terraform init -migrate-state` do?
509. What does `terraform init -reconfigure` do?
510. What is the difference between `-migrate-state` and `-reconfigure`?
511. How do you migrate local state to S3?
512. How do you migrate from one backend to another?
513. What happens if backend configuration changes?
514. Can Terraform use different backends for different environments?
515. How do you design backend architecture for hundreds of AWS accounts?
516. How do you separate state between teams?
517. How do you separate state between applications?
518. How do you prevent one team from accessing another team's state?
519. What is `terraform_remote_state`?
520. How does `terraform_remote_state` work?
521. When should you use `terraform_remote_state`?
522. What are the security concerns of `terraform_remote_state`?
523. What are alternatives to `terraform_remote_state`?
524. How do you share infrastructure information between independent Terraform states?

---

# 17. Workspaces and Environments

525. What are Terraform workspaces?
526. What problem do Terraform workspaces solve?
527. How do Terraform CLI workspaces work?
528. What is the default workspace?
529. How do you create a workspace?
530. How do you switch workspaces?
531. How do you list Terraform workspaces?
532. How does workspace state isolation work?
533. What is `terraform.workspace`?
534. Can different workspaces have different state?
535. Should you use workspaces for dev, stage, and prod?
536. What are the limitations of Terraform workspaces?
537. When should you avoid workspaces?
538. What is the difference between workspaces and separate directories?
539. What is the difference between workspaces and separate repositories?
540. How would you design Terraform environments for dev, stage, and prod?
541. How would you isolate production credentials from development credentials?
542. Can workspaces provide security isolation?
543. Can workspaces provide different IAM permissions?
544. How do you manage environment-specific variables?
545. How do you prevent developers from accidentally applying to production?
546. What is your preferred multi-environment Terraform architecture and why?

---

# 18. Lifecycle

547. What is the Terraform `lifecycle` block?
548. What is `create_before_destroy`?
549. When would you use `create_before_destroy`?
550. What problems can `create_before_destroy` cause?
551. What happens if the resource name must be unique?
552. What happens to cost when using `create_before_destroy`?
553. What is `prevent_destroy`?
554. When should you use `prevent_destroy`?
555. What happens if Terraform tries to destroy a resource with `prevent_destroy`?
556. What is `ignore_changes`?
557. When should you use `ignore_changes`?
558. What are the dangers of `ignore_changes`?
559. What does `ignore_changes = all` mean?
560. Why can `ignore_changes` hide drift?
561. What is `replace_triggered_by`?
562. When would you use `replace_triggered_by`?
563. How can you rebuild an EC2 instance automatically when an AMI changes?
564. What is immutable infrastructure?
565. How does Terraform support immutable infrastructure?
566. What is the difference between update-in-place and replacement?
567. How do you protect a production database from accidental Terraform destruction?
568. How do you achieve zero-downtime resource replacement?
569. Can lifecycle rules be used on modules?
570. Can lifecycle rules be used on data sources?
571. What lifecycle settings would you use for a production database?
572. What lifecycle settings would you use for EC2?
573. How would you troubleshoot an unexpected replacement?
574. Why is Terraform planning to destroy and recreate a resource?
575. How do you determine which attribute caused replacement?

---

# 19. Import and Existing Infrastructure

576. How do you import existing infrastructure into Terraform?
577. What is `terraform import`?
578. What is an `import` block?
579. What is the difference between CLI import and configuration-driven import?
580. Why doesn't import automatically create perfect Terraform configuration?
581. What steps do you follow after importing a resource?
582. How do you import an existing EC2 instance?
583. How do you import an existing VPC?
584. How do you import an existing S3 bucket?
585. How do you import a resource into a module?
586. How do you import resources managed by `for_each`?
587. How do you import resources managed by `count`?
588. How do you import multiple resources?
589. What happens if you import a resource into the wrong address?
590. How do you correct an incorrect import?
591. What happens if an imported resource does not match configuration?
592. Why does Terraform show changes immediately after import?
593. How do you achieve a clean plan after import?
594. How do you import resources without downtime?
595. What is generated configuration during Terraform import?
596. How do you safely migrate manually created production infrastructure to Terraform?

---

# 20. Moved Blocks and Refactoring

597. What is a `moved` block?
598. Why do we need `moved` blocks?
599. How do you rename a Terraform resource without destroying it?
600. How do you move a resource into a module?
601. How do you move a resource from one module to another?
602. What is the difference between `moved` and `terraform state mv`?
603. When would you use a `moved` block?
604. When would you use `terraform state mv`?
605. How do you refactor a production Terraform codebase safely?
606. What happens if you rename a resource without a `moved` block?
607. Why can Terraform plan a destroy/create after a simple resource rename?
608. How do you migrate from a single resource to `for_each`?
609. How do you migrate from `count` to `for_each` without destroying resources?
610. How do you move a resource from root module to child module?
611. How do you split one module into multiple modules safely?
612. How do you rename a module?
613. What happens if a `moved` block is removed?
614. How do you preserve backward compatibility in a reusable module?
615. How would you refactor a large production Terraform repository without downtime?

---

# 21. State Drift

616. What is infrastructure drift?
617. What is Terraform state drift?
618. What causes drift?
619. How do you detect drift?
620. How does `terraform plan` reveal drift?
621. What happens if someone manually changes an EC2 instance?
622. What happens if someone manually changes security groups?
623. What happens if someone manually changes tags?
624. What happens if an autoscaling system modifies an attribute managed by Terraform?
625. When would you use `ignore_changes` for drift?
626. Why is `ignore_changes` not a true drift-remediation mechanism?
627. How do you remediate drift?
628. How do you detect drift without modifying infrastructure?
629. How do you perform a refresh-only plan?
630. How do you handle drift in production without downtime?
631. How would you handle drift caused by an emergency manual change?
632. How would you handle drift when the manual change is intentional?
633. How would you handle drift when the manual change is unauthorized?
634. How do you prevent drift from happening?
635. How can CI/CD automatically detect Terraform drift?
636. How would you build a drift-detection pipeline?

---

# 22. Terraform Security

637. How do you secure Terraform?
638. How do you manage AWS credentials securely in Terraform?
639. Should AWS access keys be stored in `.tf` files?
640. Should secrets be stored in `terraform.tfvars`?
641. Should `terraform.tfvars` be committed to Git?
642. What is the difference between sensitive variables and secret management?
643. Does `sensitive = true` encrypt secrets?
644. Can secrets still appear in Terraform state?
645. Can secrets appear in Terraform plan files?
646. How do you secure Terraform state?
647. How do you encrypt remote state?
648. How do you restrict access to Terraform state?
649. How do you audit state access?
650. How do you manage secrets using AWS Secrets Manager?
651. How do you integrate Vault with Terraform?
652. How do you use environment variables for secrets?
653. What are the risks of using `TF_VAR_*` for secrets?
654. What are the risks of using backend credentials in Terraform configuration?
655. How do you prevent credentials from leaking through CI logs?
656. How do you prevent secrets from appearing in Terraform outputs?
657. What happens when you use `terraform output -raw` on a sensitive value?
658. What is an ephemeral value in Terraform?
659. When should you use ephemeral variables?
660. How do write-only resource arguments help with secret management?
661. How do you secure Terraform Cloud/HCP Terraform variables?
662. How do you implement least privilege for Terraform IAM?
663. Should Terraform use administrator permissions?
664. How do you separate Terraform permissions by environment?
665. How do you prevent developers from modifying production infrastructure?
666. How do you implement approval controls for Terraform production changes?

---

# 23. Terraform CI/CD

667. How do you integrate Terraform with Jenkins?
668. How do you integrate Terraform with GitHub Actions?
669. How do you integrate Terraform with GitLab CI?
670. How do you integrate Terraform with Azure DevOps?
671. What should a Terraform CI/CD pipeline look like?
672. What stages would you include in a production Terraform pipeline?
673. Where should `terraform fmt` run?
674. Where should `terraform validate` run?
675. Where should security scanning run?
676. Where should `terraform plan` run?
677. Where should `terraform apply` run?
678. Should `terraform apply` run automatically for production?
679. How do you implement manual approval before production apply?
680. How do you save and review a Terraform plan in CI?
681. Why is applying a previously generated plan safer?
682. What happens if the configuration changes after the plan is generated?
683. How do you prevent someone from applying a different configuration than the one reviewed?
684. How do you authenticate CI/CD to AWS securely?
685. Should CI/CD use long-lived AWS access keys?
686. How would you use AWS IAM roles/OIDC for Terraform CI/CD?
687. How do you isolate Terraform state per environment in CI?
688. How do you prevent concurrent Terraform pipelines?
689. How do you handle Terraform state locking in CI/CD?
690. How do you handle a failed Terraform apply in Jenkins?
691. How do you handle Terraform approval gates?
692. How do you detect destructive Terraform plans automatically?
693. How would you fail a pipeline if Terraform plans to destroy production resources?
694. How do you implement policy checks before Terraform apply?
695. How do you integrate Checkov with Terraform?
696. How do you integrate tfsec with Terraform?
697. How do you integrate TFLint with Terraform?
698. How do you integrate OPA with Terraform?
699. How do you implement Terraform plan artifact retention?
700. How do you secure Terraform plan artifacts?
701. Can Terraform plan files contain secrets?
702. How would you design a production-grade Terraform CI/CD pipeline?

---

# 24. Terraform Troubleshooting

703. `terraform init` is failing; how do you troubleshoot it?
704. Provider installation is failing; what do you check?
705. Terraform cannot download a provider; what do you check?
706. Terraform provider checksum verification is failing; what do you check?
707. Terraform says the provider version is incompatible; how do you resolve it?
708. Terraform says the dependency lock file is inconsistent; what do you do?
709. `terraform validate` fails; how do you troubleshoot it?
710. `terraform plan` fails; how do you troubleshoot it?
711. `terraform apply` fails; what is your troubleshooting approach?
712. Terraform is stuck during apply; what do you check?
713. Terraform is stuck waiting for a state lock; what do you do?
714. Terraform says state is locked by another process; how do you determine whether it is safe to unlock?
715. Terraform state lock cannot be released; what do you do?
716. Terraform reports "Error acquiring the state lock"; how do you resolve it?
717. Terraform wants to destroy a production database; what do you do?
718. Terraform wants to replace an EC2 instance unexpectedly; how do you investigate?
719. Terraform plan shows thousands of changes unexpectedly; what do you check?
720. Terraform plan shows no changes but infrastructure is incorrect; how do you investigate?
721. Terraform plan shows changes every time even though you did not change code; why?
722. Terraform keeps changing tags on every apply; how do you troubleshoot it?
723. Terraform keeps recreating a resource; how do you troubleshoot it?
724. Terraform creates duplicate resources; how do you troubleshoot it?
725. Terraform cannot find a resource that exists in AWS; what do you check?
726. Terraform says a resource already exists; how do you resolve it?
727. Terraform says a resource is missing from state; what do you do?
728. Terraform state contains a resource that no longer exists; what do you do?
729. Terraform configuration exists but the resource is not in state; how do you fix it?
730. A resource exists in AWS but Terraform wants to create it; why?
731. Terraform wants to delete an imported resource; why?
732. Terraform import succeeded but plan shows many changes; why?
733. Terraform state is corrupted; how do you recover?
734. Terraform state was accidentally deleted; how do you recover?
735. Terraform apply failed halfway through; what is your recovery procedure?
736. Terraform crashed during apply; what do you do?
737. Terraform process was killed during apply; what do you do?
738. AWS resource was created but Terraform says creation failed; how do you reconcile it?
739. Terraform says "resource already exists"; what is the safest approach?
740. Terraform has a dependency cycle; how do you troubleshoot it?
741. Terraform plan hangs indefinitely; what do you investigate?
742. Terraform apply takes hours; how do you troubleshoot performance?
743. Terraform is making resources sequentially instead of parallelly; why?
744. Terraform is consuming excessive memory; how do you investigate?
745. Terraform CI pipeline is intermittently failing; how do you troubleshoot it?
746. Terraform works locally but fails in Jenkins; what do you check?
747. Terraform works in dev but fails in production; what do you investigate?
748. Terraform works on one engineer's machine but not another's; what do you check?
749. Terraform works before provider upgrade but fails after upgrade; how do you troubleshoot?
750. Terraform plan changes after `terraform init -upgrade`; why?
751. Terraform cannot authenticate to AWS; what do you check?
752. Terraform is using the wrong AWS account; how do you troubleshoot it?
753. Terraform is deploying to the wrong AWS region; what do you check?
754. Terraform is using the wrong provider alias; how do you troubleshoot it?
755. Terraform cannot assume an IAM role; what do you check?
756. Terraform backend initialization is failing; how do you troubleshoot it?
757. Terraform cannot access the remote state bucket; what do you check?
758. Terraform state locking is not working; what do you investigate?
759. Terraform backend configuration changed unexpectedly; what do you do?
760. Terraform reports "Backend configuration changed"; how do you resolve it?
761. Terraform says "Failed to load state"; how do you troubleshoot it?
762. Terraform output is unexpectedly sensitive; what do you check?
763. Terraform is exposing secrets in logs; how do you stop it?
764. Terraform has an unexpected drift; how do you determine who changed the resource?
765. Terraform keeps planning changes after every successful apply; what are the likely causes?

---

# 25. Production Scenarios

766. You have 500 AWS resources managed by Terraform and one developer accidentally changes a production resource manually; what do you do?
767. Your production state is locked by a terminated Jenkins job; how do you recover?
768. A production apply fails after creating 70% of the resources; what is your recovery strategy?
769. Terraform wants to destroy a production database because of a configuration change; how do you handle it?
770. A developer changed `count` to `for_each` and Terraform wants to destroy 100 resources; how do you fix it?
771. A module rename causes Terraform to destroy production resources; how do you prevent it?
772. You need to move resources from the root module into a reusable module without downtime; how do you do it?
773. Your organization has 100 AWS accounts and wants centralized Terraform management; how would you design it?
774. Your organization has dev, QA, staging, and production; how would you structure Terraform?
775. Multiple teams need to manage the same AWS environment; how would you divide state?
776. Two teams need outputs from each other's Terraform stacks; how would you design that dependency?
777. One Terraform state contains 5,000 resources and plans are extremely slow; how would you redesign it?
778. A Terraform repository has become unmaintainable; how would you refactor it?
779. A module is used by 50 teams and you need to introduce a breaking change; how would you roll it out?
780. A provider upgrade changes behavior across hundreds of resources; how would you safely roll it out?
781. Terraform state contains secrets and is currently stored locally; how would you secure it?
782. Developers can currently run `terraform apply` against production from their laptops; how would you redesign the process?
783. A production deployment requires manual approval; how would you implement it?
784. Terraform plan shows an unexpected destroy of a load balancer; what would you investigate first?
785. Terraform is continuously fighting with an autoscaling controller; how would you resolve it?
786. Terraform and Kubernetes controllers are both modifying the same resource; how would you design ownership?
787. A resource must be modified manually during an incident; how do you bring that change back under Terraform management?
788. Someone manually deleted a resource that Terraform manages; what happens next?
789. Someone manually changed an IAM policy managed by Terraform; what happens on the next plan?
790. Your state backend becomes unavailable during a production deployment; what happens?
791. Your Terraform provider registry is temporarily unavailable; how would you keep CI/CD reliable?
792. Your Terraform state bucket is accidentally deleted; what is your recovery plan?
793. Your Terraform state bucket is compromised; what is your incident response?
794. A developer commits AWS credentials inside Terraform code; what do you do?
795. Terraform plan contains sensitive values; how would you secure plan artifacts?
796. You need to deploy the same infrastructure into 20 regions; how would you design Terraform?
797. You need to deploy the same module into 100 AWS accounts; how would you design provider aliases and orchestration?
798. You need zero downtime while replacing EC2 instances; how would you approach it?
799. You need to prevent accidental deletion of a production RDS database; what Terraform controls would you use?
800. You need Terraform to rebuild infrastructure whenever an AMI changes; how would you design it?

---

# 26. Advanced Terraform State Scenarios

801. What happens internally when Terraform refreshes state?
802. What happens internally during `terraform plan`?
803. What happens internally during `terraform apply`?
804. What is the sequence of operations during `terraform apply`?
805. How does Terraform compare configuration, state, and real infrastructure?
806. How does Terraform determine whether a resource should be created?
807. How does Terraform determine whether a resource should be updated?
808. How does Terraform determine whether a resource should be replaced?
809. How does Terraform determine resource dependencies?
810. How does Terraform decide the order of resource creation?
811. How does Terraform perform parallel resource creation?
812. What happens if a dependency fails?
813. What happens to dependent resources when an upstream resource fails?
814. How does Terraform recover from partial execution?
815. How does Terraform maintain state consistency after an apply?
816. What happens between provider API calls and state updates?
817. What is the relationship between state and provider configuration?
818. Why does Terraform state retain provider configuration information?
819. What happens if the provider configuration used by a resource is removed?
820. How would you recover resources whose provider configuration was removed?

---

# 27. Advanced Module Design

821. How would you design a reusable VPC module?
822. How would you design a reusable EKS module?
823. How would you design a reusable EC2 module?
824. How would you design a reusable RDS module?
825. How would you design a reusable IAM module?
826. How would you design a reusable security-group module?
827. How would you design a module that supports multiple AWS regions?
828. How would you design a module that supports multiple environments?
829. How would you design a module that supports optional resources?
830. How would you conditionally create resources inside a module?
831. How do you avoid creating resources when a feature is disabled?
832. How do you expose only necessary outputs from a module?
833. How do you prevent a child module from creating unnecessary dependencies?
834. How do you handle provider aliases in reusable modules?
835. How do you design modules for backward compatibility?
836. How do you version module interfaces?
837. How do you test module backward compatibility?
838. How do you publish modules internally?
839. How do you enforce module standards across an organization?
840. How do you prevent teams from bypassing approved modules?
841. How do you design a Terraform module catalog?
842. How do you handle module ownership?
843. How do you document Terraform modules?
844. How do you prevent modules from becoming overly generic?
845. How do you decide whether logic belongs in a module or root configuration?

---

# 28. Terraform Testing and Validation

846. How do you test Terraform code?
847. What is `terraform test`?
848. What are `.tftest.hcl` files?
849. Where should Terraform test files be stored?
850. What is unit testing in Terraform?
851. What is integration testing in Terraform?
852. How do you test Terraform modules?
853. How do you validate Terraform configuration before apply?
854. What is `terraform validate`?
855. What is TFLint?
856. What is Checkov?
857. What is tfsec?
858. What is Terratest?
859. What is OPA?
860. What is Sentinel?
861. How do you combine Terraform validation and security scanning?
862. How do you test Terraform without creating real AWS resources?
863. How do you test a reusable Terraform module?
864. How do you test negative scenarios?
865. How do you test Terraform policy compliance?
866. How do you prevent insecure Terraform from reaching production?
867. How would you build a Terraform quality gate?

---

# 29. Terraform Security and Compliance at Enterprise Scale

868. How would you implement Terraform governance across an enterprise?
869. How would you enforce tagging standards?
870. How would you enforce mandatory encryption?
871. How would you prevent public S3 buckets through Terraform policy?
872. How would you prevent public security groups?
873. How would you prevent unencrypted EBS volumes?
874. How would you enforce approved AWS regions?
875. How would you enforce approved instance types?
876. How would you enforce mandatory cost-center tags?
877. How would you enforce naming conventions?
878. How would you prevent developers from creating expensive resources?
879. How would you implement policy-as-code?
880. What is the difference between Sentinel and OPA?
881. How would you integrate policy checks into Terraform CI/CD?
882. How would you implement least privilege for Terraform?
883. How would you separate Terraform execution roles by environment?
884. How would you audit Terraform changes?
885. How would you provide Terraform change traceability?
886. How would you implement approval workflows?
887. How would you manage break-glass access?
888. How would you implement separation of duties?
889. How would you secure the Terraform state lifecycle?
890. How would you respond if Terraform state credentials were compromised?

---

# 30. Terraform and AWS

891. How do you configure the AWS provider in Terraform?
892. How do you authenticate Terraform to AWS?
893. How do you use AWS IAM roles with Terraform?
894. How do you use AWS STS AssumeRole with Terraform?
895. How do you deploy Terraform into multiple AWS accounts?
896. How do you deploy Terraform into multiple AWS regions?
897. How do you configure provider aliases for AWS?
898. How do you create a VPC using Terraform?
899. How do you create public and private subnets?
900. How do you create route tables?
901. How do you create an Internet Gateway?
902. How do you create a NAT Gateway?
903. How do you create an Application Load Balancer?
904. How do you create an Auto Scaling Group?
905. How do you create an EC2 instance?
906. How do you create an RDS instance?
907. How do you create an S3 bucket?
908. How do you create IAM roles using Terraform?
909. How do you create IAM policies using Terraform?
910. How do you manage security groups using Terraform?
911. How do you manage Route 53 records using Terraform?
912. How do you manage CloudFront using Terraform?
913. How do you manage EKS using Terraform?
914. How do you manage Lambda using Terraform?
915. How do you manage Secrets Manager using Terraform?
916. How do you manage KMS keys using Terraform?
917. How do you manage CloudWatch resources using Terraform?
918. How do you manage AWS Organizations using Terraform?
919. How do you manage cross-account resources?
920. How do you handle AWS eventual consistency in Terraform?
921. How do you handle AWS API throttling?
922. How do you troubleshoot AWS provider errors?
923. How do you troubleshoot IAM `AccessDenied` errors from Terraform?
924. How do you troubleshoot an AWS resource that Terraform cannot find?
925. How do you prevent Terraform from accidentally deleting critical AWS resources?

---

# 31. Terraform and Kubernetes

926. Can Terraform manage Kubernetes resources?
927. What is the Kubernetes provider?
928. What is the difference between Terraform and kubectl?
929. What is the difference between Terraform and Helm?
930. When would you use Terraform to manage Kubernetes?
931. When would you use Helm instead?
932. Can Terraform deploy Helm charts?
933. What is the Helm provider?
934. How do you manage EKS and Kubernetes resources with Terraform?
935. How do you handle dependency between EKS creation and Kubernetes provider initialization?
936. What happens if Terraform tries to use the Kubernetes provider before EKS is available?
937. How do you manage Kubernetes namespaces with Terraform?
938. How do you manage ConfigMaps with Terraform?
939. How do you manage Secrets with Terraform?
940. What are the security concerns of managing Kubernetes Secrets with Terraform?
941. How do you prevent Terraform from fighting Kubernetes controllers?
942. How do you decide which Kubernetes resources should be managed by Terraform and which by GitOps?

---

# 32. Provisioners

943. What are Terraform provisioners?
944. What is a `local-exec` provisioner?
945. What is a `remote-exec` provisioner?
946. What is a file provisioner?
947. Why are provisioners generally discouraged?
948. When would you use a provisioner?
949. What problems can provisioners create?
950. What happens if a provisioner fails?
951. What is `when = destroy`?
952. What is the difference between provisioners and cloud-init?
953. Why is cloud-init often preferred over Terraform provisioners?
954. How do you troubleshoot a failing remote-exec provisioner?
955. How do you make provisioners idempotent?
956. How do provisioners affect Terraform dependency graphs?
957. Can provisioners cause non-repeatable infrastructure?
958. What alternatives exist to provisioners?

---

# 33. Advanced Meta-Arguments

959. What are Terraform meta-arguments?
960. What is `count`?
961. What is `for_each`?
962. What is `depends_on`?
963. What is `provider` meta-argument?
964. What is `lifecycle`?
965. How do meta-arguments affect Terraform's dependency graph?
966. Which meta-arguments can be used with modules?
967. Which meta-arguments can be used with data sources?
968. Which meta-arguments can be used with resources?
969. Can you use `count` and `for_each` together?
970. Can `depends_on` be used with modules?
971. Can `provider` be selected dynamically?
972. How do you choose a provider configuration for a resource?
973. How do you choose a provider configuration for a module?

---

# 34. Version Management and Upgrades

974. How do you manage Terraform versions in an organization?
975. What is `required_version`?
976. Where is `required_version` configured?
977. What happens if Terraform version doesn't satisfy `required_version`?
978. How do you pin Terraform versions?
979. How do you upgrade Terraform safely?
980. How do you upgrade Terraform from an old major version?
981. How do you upgrade providers safely?
982. What is the dependency lock file?
983. Why should `.terraform.lock.hcl` be committed?
984. What happens during `terraform init -upgrade`?
985. How do you test provider upgrades?
986. How do you test Terraform upgrades?
987. How do you roll back a Terraform upgrade?
988. How do you roll back a provider upgrade?
989. What problems can provider upgrades cause?
990. How do you identify breaking changes in providers?
991. How do you manage Terraform version compatibility across modules?
992. How do you handle modules requiring different Terraform versions?
993. How would you perform a Terraform upgrade across 100 repositories?

---

# 35. Terraform Cloud / HCP Terraform / Enterprise

994. What is HCP Terraform?
995. What is Terraform Enterprise?
996. What is the difference between Terraform CLI and HCP Terraform?
997. What are Terraform Cloud workspaces?
998. How are HCP Terraform workspaces different from CLI workspaces?
999. What is remote execution?
1000. What is a remote backend in HCP Terraform?
1001. How does HCP Terraform store state?
1002. How does HCP Terraform handle state security?
1003. How does HCP Terraform handle concurrent runs?
1004. How do you implement approvals in HCP Terraform?
1005. What are run triggers?
1006. What are variable sets?
1007. How do variable sets help enterprise Terraform?
1008. What is a private module registry?
1009. How do you publish private Terraform modules?
1010. How do you implement RBAC in HCP Terraform?
1011. How do you separate teams and environments?
1012. How do you integrate HCP Terraform with GitHub?
1013. How do you integrate HCP Terraform with GitLab?
1014. How do you implement policy checks in HCP Terraform?
1015. What is Sentinel?
1016. How do Sentinel policies work with Terraform?
1017. What is the difference between Sentinel and OPA?
1018. How do you audit Terraform runs?
1019. How do you troubleshoot a failed HCP Terraform run?
1020. How do you migrate from local Terraform execution to HCP Terraform?

---

# 36. Advanced Terraform Internals

1021. How does Terraform work internally?
1022. What happens between `terraform init` and `terraform apply`?
1023. How does Terraform construct the execution graph?
1024. What is Terraform's dependency graph?
1025. How does Terraform determine dependencies from expressions?
1026. What is an implicit dependency internally?
1027. What is an explicit dependency internally?
1028. How does Terraform determine resource creation order?
1029. How does Terraform perform parallel execution?
1030. How does Terraform communicate with providers?
1031. What is the Terraform provider plugin architecture?
1032. What happens when Terraform starts a provider?
1033. How does Terraform know which provider version to install?
1034. What role does `.terraform.lock.hcl` play internally?
1035. How does Terraform determine whether a resource requires replacement?
1036. How does Terraform compare configuration with state?
1037. How does Terraform compare state with real infrastructure?
1038. What are unknown values?
1039. What are sensitive values?
1040. What are ephemeral values?
1041. How does Terraform handle computed attributes?
1042. What is a planned value?
1043. What is an execution plan?
1044. What happens when a provider returns an error?
1045. How does Terraform recover from provider API failures?
1046. How does Terraform maintain state consistency?
1047. How does Terraform handle resource dependencies during destroy?
1048. Why is Terraform destroy order different from creation order?
1049. How does Terraform detect cycles?
1050. How would you use `terraform graph` to troubleshoot dependencies?

---

# 37. Terraform Performance

1051. Why can Terraform plan become slow?
1052. Why can Terraform apply become slow?
1053. How do you optimize Terraform performance?
1054. How does Terraform parallelism work?
1055. What does the `-parallelism` flag do?
1056. When would you reduce Terraform parallelism?
1057. When would you increase Terraform parallelism?
1058. What risks exist when increasing parallelism?
1059. How does provider API throttling affect Terraform?
1060. How do you handle AWS API throttling?
1061. How does state size affect Terraform performance?
1062. How does a large dependency graph affect performance?
1063. How do large modules affect plan performance?
1064. How would you optimize a Terraform state containing thousands of resources?
1065. When should you split Terraform state?
1066. How do you decide Terraform state boundaries?
1067. What is the trade-off between one large state and many small states?
1068. How do you optimize CI Terraform execution?
1069. How do you reduce unnecessary provider calls?
1070. How do you troubleshoot a Terraform plan that takes 30 minutes?

---

# 38. Terraform Architecture Design

1071. How would you design Terraform for a large enterprise?
1072. How would you structure Terraform repositories?
1073. Monorepo vs multirepo for Terraform?
1074. What are the advantages of a Terraform monorepo?
1075. What are the disadvantages of a Terraform monorepo?
1076. How would you organize infrastructure by environment?
1077. How would you organize infrastructure by application?
1078. How would you organize infrastructure by AWS account?
1079. How would you organize infrastructure by region?
1080. How would you design Terraform state boundaries?
1081. How would you separate networking and application infrastructure?
1082. How would you separate platform and application Terraform?
1083. How would you manage shared infrastructure?
1084. How would you manage dependencies between Terraform stacks?
1085. How would you manage outputs between stacks?
1086. How would you prevent circular dependencies between stacks?
1087. How would you design Terraform for multi-account AWS?
1088. How would you design Terraform for multi-region AWS?
1089. How would you design Terraform for disaster recovery?
1090. How would you design Terraform for high availability?
1091. How would you design Terraform for zero-downtime deployments?
1092. How would you design Terraform for regulated environments?
1093. How would you design Terraform for hundreds of engineers?
1094. How would you design Terraform for thousands of resources?
1095. How would you design Terraform ownership between DevOps and application teams?

---

# 39. Real Senior-Level Design Questions

1096. Design a Terraform architecture for 50 AWS accounts.
1097. Design a Terraform architecture for 500 AWS accounts.
1098. Design Terraform for multiple organizations and business units.
1099. Design Terraform for dev/stage/prod with strict production isolation.
1100. Design Terraform where developers cannot directly access production AWS.
1101. Design Terraform with centralized state and decentralized application ownership.
1102. Design Terraform with separate networking, security, platform, and application states.
1103. Design a reusable VPC module used by 100 teams.
1104. Design a reusable EKS module used by multiple business units.
1105. Design Terraform CI/CD with pull-request plans and production approvals.
1106. Design Terraform drift detection.
1107. Design Terraform disaster recovery.
1108. Design Terraform state backup and recovery.
1109. Design Terraform state locking for a large team.
1110. Design Terraform secrets management.
1111. Design Terraform provider upgrade management.
1112. Design Terraform module version management.
1113. Design Terraform governance.
1114. Design Terraform policy-as-code.
1115. Design Terraform security controls.
1116. Design Terraform cost controls.
1117. Design Terraform tagging governance.
1118. Design Terraform compliance controls.
1119. Design Terraform for multi-region disaster recovery.
1120. Design Terraform for blue-green infrastructure.
1121. Design Terraform for immutable infrastructure.
1122. Design Terraform for ephemeral environments.
1123. Design Terraform for preview environments per pull request.
1124. Design Terraform for self-service infrastructure provisioning.
1125. Design an internal Terraform platform for 500 developers.

---

# 40. Terraform Coding Questions

1126. Write Terraform code to create an EC2 instance.
1127. Write Terraform code to create an S3 bucket.
1128. Write Terraform code to create a VPC.
1129. Write Terraform code to create public and private subnets.
1130. Write Terraform code to create an Internet Gateway.
1131. Write Terraform code to create a NAT Gateway.
1132. Write Terraform code to create an Application Load Balancer.
1133. Write Terraform code to create an Auto Scaling Group.
1134. Write Terraform code to create an RDS instance.
1135. Write Terraform code to create an IAM role.
1136. Write Terraform code to create an IAM policy.
1137. Write Terraform code to create a security group.
1138. Write Terraform code using variables.
1139. Write Terraform code using locals.
1140. Write Terraform code using outputs.
1141. Write Terraform code using data sources.
1142. Write Terraform code using `count`.
1143. Write Terraform code using `for_each`.
1144. Write Terraform code using a map of objects.
1145. Write Terraform code using a list of objects.
1146. Write Terraform code using conditional expressions.
1147. Write Terraform code using a `for` expression.
1148. Write Terraform code using a dynamic block.
1149. Write Terraform code using `depends_on`.
1150. Write Terraform code using `create_before_destroy`.
1151. Write Terraform code using `prevent_destroy`.
1152. Write Terraform code using `ignore_changes`.
1153. Write Terraform code using `replace_triggered_by`.
1154. Write Terraform code using multiple AWS provider aliases.
1155. Write Terraform code to deploy resources into two AWS regions.
1156. Write Terraform code to deploy resources into two AWS accounts.
1157. Write Terraform code to create a reusable module.
1158. Write Terraform code to consume a module.
1159. Write Terraform code to expose a module output.
1160. Write Terraform code to use one module's output as another module's input.
1161. Write Terraform code to configure an S3 backend.
1162. Write Terraform code to configure provider version constraints.
1163. Write Terraform code to configure Terraform version constraints.
1164. Write Terraform code for variable validation.
1165. Write Terraform code for sensitive variables.
1166. Write Terraform code for preconditions.
1167. Write Terraform code for postconditions.
1168. Write Terraform code for check blocks.
1169. Write Terraform code for import blocks.
1170. Write Terraform code for moved blocks.

---

# 41. "What Happens If..." Questions

1171. What happens if Terraform state is deleted?
1172. What happens if Terraform state is corrupted?
1173. What happens if someone manually deletes an EC2 instance?
1174. What happens if someone manually modifies an EC2 instance?
1175. What happens if someone manually creates an AWS resource?
1176. What happens if Terraform state and AWS infrastructure disagree?
1177. What happens if two engineers run `terraform apply` simultaneously?
1178. What happens if Terraform loses the state lock?
1179. What happens if a Terraform apply fails halfway?
1180. What happens if the Terraform process crashes?
1181. What happens if the AWS API times out?
1182. What happens if a provider API call succeeds but Terraform receives an error?
1183. What happens if `terraform plan` shows a replacement?
1184. What happens if you change a resource name?
1185. What happens if you change a resource type?
1186. What happens if you remove a resource block?
1187. What happens if you rename a module?
1188. What happens if you move a resource into a module?
1189. What happens if you change `count` to `for_each`?
1190. What happens if you change `for_each` keys?
1191. What happens if you change the provider version?
1192. What happens if `.terraform.lock.hcl` is deleted?
1193. What happens if `terraform.tfvars` is missing?
1194. What happens if a required variable has no value?
1195. What happens if a provider alias is missing?
1196. What happens if the backend is unavailable?
1197. What happens if the state bucket is deleted?
1198. What happens if state locking fails?
1199. What happens if a module version disappears?
1200. What happens if two modules require incompatible provider versions?
1201. What happens if Terraform cannot reach the provider registry?
1202. What happens if a sensitive value is used in state?
1203. What happens if a production resource has `prevent_destroy`?
1204. What happens if `ignore_changes = all` is configured?
1205. What happens if Terraform is using the wrong AWS account?
1206. What happens if Terraform is using the wrong region?
1207. What happens if an imported resource doesn't match configuration?
1208. What happens if a `moved` block is missing?
1209. What happens if a `moved` block is removed?
1210. What happens if a dependency cycle exists?

---

# 42. Senior Follow-Up / Cross-Question Round

1211. Why does Terraform need state if AWS already knows the resources?
1212. Why is remote state not enough without locking?
1213. Why is locking not the same as state versioning?
1214. Why isn't `ignore_changes` a proper drift solution?
1215. Why isn't `terraform import` enough to manage an existing resource?
1216. Why can `count` be dangerous for long-lived resources?
1217. Why is `for_each` often better for named infrastructure?
1218. Why should provider versions be constrained?
1219. Why should `.terraform.lock.hcl` be committed?
1220. Why shouldn't `.terraform` be committed?
1221. Why shouldn't Terraform state be committed?
1222. Why shouldn't secrets be hard-coded in Terraform?
1223. Why can sensitive values still be exposed?
1224. Why can Terraform plan contain secrets?
1225. Why should Terraform plan artifacts be protected?
1226. Why should production Terraform apply be controlled?
1227. Why shouldn't `-target` be used routinely?
1228. Why shouldn't `-lock=false` normally be used?
1229. Why are provisioners discouraged?
1230. Why should modules avoid hard-coded provider configurations?
1231. Why should module versions be pinned?
1232. Why should production state be separated from development state?
1233. Why should large Terraform states be split?
1234. Why can too many modules become problematic?
1235. Why can too many `depends_on` declarations be problematic?
1236. Why can excessive `ignore_changes` be dangerous?
1237. Why can excessive dynamic blocks make Terraform difficult to maintain?
1238. Why can workspace-based environment isolation be insufficient?
1239. Why can manually editing state be dangerous?
1240. Why can changing a resource address cause destruction?
1241. Why are `moved` blocks important in production refactoring?
1242. Why can provider upgrades cause unexpected replacements?
1243. Why should Terraform upgrades be tested before production?
1244. Why is state considered the most critical Terraform artifact?
1245. Why is Terraform state effectively a security-sensitive asset?

---

# 43. Rapid-Fire Questions Interviewers Can Throw at 8-Year Engineers

1246. What is Terraform?
1247. What is HCL?
1248. What is IaC?
1249. What is a provider?
1250. What is a resource?
1251. What is a module?
1252. What is a data source?
1253. What is state?
1254. What is a backend?
1255. What is remote state?
1256. What is state locking?
1257. What is drift?
1258. What is import?
1259. What is a moved block?
1260. What is `count`?
1261. What is `for_each`?
1262. What is `depends_on`?
1263. What is lifecycle?
1264. What is `create_before_destroy`?
1265. What is `prevent_destroy`?
1266. What is `ignore_changes`?
1267. What is `replace_triggered_by`?
1268. What is a variable?
1269. What is a local?
1270. What is an output?
1271. What is a data source?
1272. What is a dynamic block?
1273. What is a provider alias?
1274. What is `.terraform.lock.hcl`?
1275. What is `required_providers`?
1276. What is `required_version`?
1277. What is `terraform init`?
1278. What is `terraform validate`?
1279. What is `terraform plan`?
1280. What is `terraform apply`?
1281. What is `terraform destroy`?
1282. What is `terraform state list`?
1283. What is `terraform state show`?
1284. What is `terraform state mv`?
1285. What is `terraform state rm`?
1286. What is `terraform force-unlock`?
1287. What is `terraform import`?
1288. What is `terraform graph`?
1289. What is `terraform console`?
1290. What is `terraform test`?
1291. What is Terraform Cloud?
1292. What is HCP Terraform?
1293. What is Terraform Enterprise?
1294. What is Sentinel?
1295. What is policy-as-code?
1296. What is Terraform drift detection?
1297. What is immutable infrastructure?
1298. What is infrastructure refactoring?
1299. What is Terraform module versioning?
1300. What is Terraform state recovery?

---

# 44. Highest-Probability 8-Year DevOps Questions

1301. Explain your real-world Terraform architecture.
1302. How have you structured Terraform repositories in production?
1303. How have you structured Terraform state in production?
1304. How many resources were managed by your Terraform setup?
1305. How many AWS accounts and regions did you manage?
1306. How did you manage dev, stage, and production?
1307. How did you prevent accidental production changes?
1308. How did you implement Terraform CI/CD?
1309. How did you handle Terraform state locking?
1310. Have you ever recovered a stuck Terraform state lock?
1311. Have you ever recovered from a failed Terraform apply?
1312. Have you ever restored Terraform state?
1313. Have you ever dealt with Terraform drift?
1314. Have you ever imported existing infrastructure?
1315. Have you ever migrated Terraform state?
1316. Have you ever moved resources between modules?
1317. Have you ever used `moved` blocks?
1318. Have you ever migrated from `count` to `for_each`?
1319. Have you ever handled an unexpected Terraform destroy plan?
1320. How did you prevent production database deletion?
1321. How did you implement zero-downtime Terraform changes?
1322. How did you manage Terraform secrets?
1323. How did you manage AWS credentials for Terraform?
1324. How did you handle Terraform provider upgrades?
1325. How did you manage Terraform module versions?
1326. How did you enforce Terraform coding standards?
1327. How did you enforce security standards?
1328. How did you implement policy-as-code?
1329. How did you detect Terraform drift automatically?
1330. How did you handle Terraform failures in Jenkins?
1331. How did you handle concurrent Terraform pipelines?
1332. How did you design Terraform for multiple AWS accounts?
1333. How did you design Terraform for multiple AWS regions?
1334. How did you separate Terraform state between teams?
1335. How did you share outputs between Terraform stacks?
1336. How did you handle large Terraform states?
1337. How did you optimize slow Terraform plans?
1338. How did you troubleshoot Terraform provider failures?
1339. How did you troubleshoot Terraform authentication failures?
1340. How did you troubleshoot Terraform dependency cycles?
1341. How did you troubleshoot unexpected resource replacements?
1342. How did you troubleshoot repeated Terraform changes?
1343. How did you troubleshoot drift?
1344. How did you troubleshoot state corruption?
1345. How did you recover after Terraform crashed during apply?
1346. How did you handle a provider upgrade breaking production?
1347. How did you design reusable Terraform modules?
1348. How did you handle module backward compatibility?
1349. How did you test Terraform modules?
1350. What Terraform best practices did you enforce across your organization?

---

# 45. Very Deep "Explain Internally" Questions

1351. What exactly happens internally when you execute `terraform init`?
1352. What exactly happens internally when you execute `terraform plan`?
1353. What exactly happens internally when you execute `terraform apply`?
1354. What exactly happens internally when you execute `terraform destroy`?
1355. How does Terraform construct its dependency graph?
1356. How does Terraform determine whether a change is in-place or replacement?
1357. How does Terraform communicate with a provider?
1358. How does a provider communicate with AWS?
1359. How does Terraform maintain resource identity?
1360. How does Terraform map a resource address to a cloud object?
1361. How does Terraform use state during planning?
1362. How does Terraform refresh state?
1363. How does Terraform handle unknown values?
1364. How does Terraform handle computed values?
1365. How does Terraform handle sensitive values?
1366. How does Terraform determine execution order?
1367. How does Terraform execute independent resources in parallel?
1368. How does Terraform handle failures during graph execution?
1369. How does Terraform update state after successful operations?
1370. What happens when the provider reports success but state persistence fails?
1371. What happens when state persistence succeeds but the provider operation fails?
1372. How does Terraform locking protect state?
1373. How does Terraform prevent two writers from modifying state simultaneously?
1374. How does Terraform recover after an interrupted operation?
1375. How does Terraform identify drift?
1376. How does Terraform decide which resources need replacement?
1377. How do provider schemas influence Terraform planning?
1378. How do provider version changes affect planning?
1379. How does Terraform process modules?
1380. How does Terraform flatten module resources into its dependency graph?
1381. How does Terraform represent module/resource addresses?
1382. How does Terraform handle `count` instances internally?
1383. How does Terraform handle `for_each` instances internally?
1384. How does Terraform handle moved resource addresses?
1385. How does Terraform handle imports?
1386. How does Terraform handle remote state?
1387. How does Terraform handle backend initialization?
1388. How does Terraform handle provider installation?
1389. How does `.terraform.lock.hcl` influence provider installation?
1390. How does Terraform determine which provider version to install?

---

# 46. Ultimate Production Troubleshooting Round

1391. Terraform says the state is locked, but nobody is running Terraform; what do you check?
1392. Terraform says it will destroy 200 resources after a harmless variable change; what do you investigate?
1393. Terraform wants to replace an RDS database after a provider upgrade; what do you do?
1394. Terraform wants to replace every resource after changing a module version; how do you debug it?
1395. Terraform plan is clean but the application is broken; how do you investigate?
1396. Terraform plan shows drift on 1,000 resources; how do you handle it?
1397. Terraform apply fails after creating infrastructure but before state is updated; how do you recover?
1398. Terraform state exists but all resources appear missing; what could have happened?
1399. Terraform state points to the wrong AWS account; how do you recover?
1400. Terraform is creating resources in the wrong region; how do you debug provider configuration?
1401. Terraform is using the wrong IAM role; how do you troubleshoot provider authentication?
1402. Terraform suddenly starts recreating resources after `terraform init -upgrade`; how do you investigate?
1403. Terraform plan differs between developer laptop and CI; why?
1404. Terraform plan differs between two CI runners; why?
1405. Terraform succeeds locally but fails in CI with provider errors; what do you check?
1406. Terraform CI succeeds but production infrastructure is wrong; how do you investigate?
1407. Terraform keeps changing the same security group every run; what do you investigate?
1408. Terraform keeps changing tags every run; what do you investigate?
1409. Terraform keeps changing IAM policies every run; what do you investigate?
1410. Terraform keeps replacing an EC2 instance every run; what do you investigate?
1411. Terraform takes 45 minutes to plan; how do you troubleshoot it?
1412. Terraform apply takes hours; how do you troubleshoot it?
1413. Terraform cannot acquire the backend lock; what is your safe recovery process?
1414. Terraform state backend becomes unavailable during deployment; what do you do?
1415. Terraform state is accidentally exposed publicly; what is your incident response?
1416. Terraform state contains leaked credentials; what do you do?
1417. A Terraform plan artifact containing secrets was uploaded to an accessible CI artifact store; what do you do?
1418. A developer manually modified production infrastructure and refuses to revert it; how do you reconcile it with Terraform?
1419. An emergency production change was made manually; how do you bring it back under Terraform?
1420. Terraform is fighting an external autoscaler; how do you design ownership correctly?
1421. Terraform is fighting Kubernetes controllers; how do you resolve ownership conflicts?
1422. Two Terraform modules are trying to manage the same resource; how do you fix the architecture?
1423. Two teams require the same shared infrastructure; how do you establish ownership?
1424. A Terraform module has become a 5,000-line monolith; how do you refactor it?
1425. A Terraform state contains 10,000 resources; how would you split it safely?
1426. You must migrate Terraform from one AWS account to another; how do you do it?
1427. You must migrate Terraform from one backend to another; how do you do it?
1428. You must migrate Terraform from local execution to HCP Terraform; how do you do it?
1429. You must migrate Terraform from one provider to another; how would you approach it?
1430. You must upgrade Terraform across 200 repositories; how would you automate and control it?

---

# 47. Final "Interviewer Keeps Digging" Questions

1431. Why?
1432. What happens internally?
1433. What happens to state?
1434. What happens to the real infrastructure?
1435. What happens if the operation fails halfway?
1436. What happens if two engineers do it simultaneously?
1437. How would you do this safely in production?
1438. How would you do this without downtime?
1439. How would you roll this back?
1440. How would you detect failure?
1441. How would you detect drift afterward?
1442. How would you prove that Terraform is managing the correct resource?
1443. How would you prevent this from happening again?
1444. What are the risks of your approach?
1445. What are the alternatives?
1446. Why did you choose this approach over the alternatives?
1447. What happens when the state is unavailable?
1448. What happens when the provider is unavailable?
1449. What happens when the AWS API is throttled?
1450. What happens when the CI/CD pipeline crashes?
1451. What happens when the engineer loses access?
1452. What happens when credentials expire?
1453. What happens when the provider version changes?
1454. What happens when the module version changes?
1455. What happens when the resource is manually changed?
1456. What happens when the resource is manually deleted?
1457. What happens when the resource is moved?
1458. What happens when the resource address changes?
1459. What happens when the state is corrupted?
1460. What happens when the state lock is stale?
1461. What happens when the plan wants a destructive change?
1462. How do you verify the plan before applying?
1463. How do you make production Terraform safe?
1464. How do you make Terraform scalable?
1465. How do you make Terraform reusable?
1466. How do you make Terraform secure?
1467. How do you make Terraform auditable?
1468. How do you make Terraform compliant?
1469. How do you make Terraform highly available?
1470. How do you make Terraform enterprise-ready?

**This is the level I would use for an 8-year DevOps interview:** the uploaded material covers the fundamentals through state, modules, backends, lifecycle, best practices and AWS hands-on work, while current senior-interview patterns heavily emphasize state, locking, drift, imports, refactoring, `count`/`for_each`, provider/version management, CI/CD, security, and production troubleshooting.  ([interviewchamp.ai][1])

[1]: https://interviewchamp.ai/learn/terraform-interview-questions-2026?utm_source=chatgpt.com "Terraform Interview Questions for 2026: 40+ Questions on State, Modules, Providers, Drift, and the Scenarios Interviewers Actually Ask — InterviewChamp.AI"
