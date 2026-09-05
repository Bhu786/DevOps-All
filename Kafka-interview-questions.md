# Kafka — 8-Year DevOps Engineer Master Interview Question Bank

## Questions Only

### 1. Kafka Fundamentals & Architecture ([Apache Kafka][1]) 

1. What is Apache Kafka?
2. Why is Kafka called a distributed event-streaming platform?
3. Why is Kafka also described as a distributed commit log?
4. What problem does Kafka solve compared with traditional messaging systems?
5. Explain Kafka architecture end-to-end.
6. What are the major components of Kafka?
7. What is a Kafka cluster?
8. What is a Kafka broker?
9. Why do we need multiple brokers?
10. What happens inside Kafka when a producer sends a message?
11. What happens inside Kafka when a consumer reads a message?
12. What is a Kafka topic?
13. What is a Kafka partition?
14. Why does Kafka use partitions?
15. Why is a partition considered an ordered append-only log?
16. What is an offset?
17. Is an offset unique across the entire Kafka cluster?
18. Is an offset unique across partitions?
19. What is the difference between a topic, partition, and offset?
20. What is a record in Kafka?
21. What is the difference between a Kafka message and a Kafka record?
22. What is a record key?
23. What is a record value?
24. What are Kafka record headers?
25. What is a producer?
26. What is a consumer?
27. What is a consumer group?
28. What is the relationship between producers, brokers, topics, partitions, and consumers?
29. How does Kafka achieve scalability?
30. How does Kafka achieve fault tolerance?
31. How does Kafka achieve high throughput?
32. How does Kafka achieve durability?
33. How does Kafka differ from RabbitMQ?
34. How does Kafka differ from ActiveMQ?
35. How does Kafka differ from traditional JMS messaging?
36. Kafka vs RabbitMQ — when would you choose each?
37. Kafka vs Redis Streams — when would you choose each?
38. Kafka vs Amazon Kinesis — what are the major differences?
39. Kafka vs Pulsar — what are the major differences?
40. When should Kafka not be used?
41. What are the biggest limitations of Kafka?
42. What makes Kafka suitable for event-driven architecture?
43. What makes Kafka suitable for log aggregation?
44. What makes Kafka suitable for real-time analytics?
45. What is event sourcing and how can Kafka be used for it?
46. Can Kafka be used as a database?
47. Can Kafka be used as a queue?
48. Can Kafka be used as a pub/sub system?
49. Can Kafka be used as an event store?
50. What is the difference between Kafka messaging and Kafka event streaming?

---

# 2. Topics, Partitions & Offsets 

51. How do you create a Kafka topic?
52. How do you list Kafka topics?
53. How do you describe a Kafka topic?
54. How do you delete a Kafka topic?
55. How do you increase the number of partitions of a topic?
56. Can you decrease the number of partitions of a Kafka topic?
57. What happens when you increase partitions?
58. What happens to message ordering when partitions are increased?
59. How do you decide the number of partitions for a topic?
60. How do you calculate the required number of partitions?
61. What factors influence partition count?
62. How does partition count affect consumer parallelism?
63. How does partition count affect throughput?
64. How does partition count affect storage?
65. How does partition count affect metadata?
66. How many partitions can a Kafka cluster handle?
67. What happens if a topic has too many partitions?
68. What is partition skew?
69. What causes hot partitions?
70. How do you detect a hot partition?
71. How do you fix a hot partition?
72. What is partition assignment?
73. How does Kafka decide which partition receives a record?
74. What happens when a producer sends a record without a key?
75. What happens when a producer sends a record with a key?
76. What is key-based partitioning?
77. What is the default partitioning strategy?
78. What is a custom partitioner?
79. When would you use a custom partitioner?
80. How do you guarantee ordering for a particular customer?
81. How do you guarantee ordering for a particular order ID?
82. How do you guarantee global ordering?
83. Why can't Kafka guarantee ordering across partitions?
84. What is an offset?
85. What is the difference between current offset and committed offset?
86. What is log-end offset?
87. What is high watermark?
88. What is the relationship between offset and consumer lag?
89. Where are consumer offsets stored?
90. What is `__consumer_offsets`?
91. How is `__consumer_offsets` partitioned?
92. What happens if `__consumer_offsets` becomes unavailable?
93. How can you reset consumer offsets?
94. How do you reset offsets to the earliest record?
95. How do you reset offsets to the latest record?
96. How do you reset offsets to a specific timestamp?
97. How do you reset offsets for a specific partition?
98. What happens if the committed offset no longer exists?
99. What is `auto.offset.reset`?
100. What is the difference between `earliest`, `latest`, and `none`?
101. What happens when a consumer starts for the first time?
102. What happens when a consumer group has no committed offset?
103. Can two consumer groups read the same Kafka records?
104. Can the same consumer group read the same partition simultaneously?
105. What happens when a partition reaches its maximum offset range?
106. How does Kafka handle offset overflow?
107. What is offset retention?
108. What happens to offsets when a consumer group becomes inactive?

---

# 3. Producers ([Apache Kafka][2])

109. Explain the Kafka producer architecture.
110. How does a Kafka producer communicate with brokers?
111. What happens when `send()` is called?
112. Is Kafka producer `send()` synchronous or asynchronous?
113. What is the producer buffer?
114. What is `buffer.memory`?
115. What is `batch.size`?
116. What is `linger.ms`?
117. How do `batch.size` and `linger.ms` work together?
118. What is `acks` in Kafka?
119. What does `acks=0` mean?
120. What does `acks=1` mean?
121. What does `acks=all` mean?
122. Which `acks` setting would you use in production?
123. What is `min.insync.replicas`?
124. How does `acks=all` work with `min.insync.replicas`?
125. What happens if `acks=all` is configured but ISR is smaller than `min.insync.replicas`?
126. What is producer retry?
127. What causes producer retries?
128. Can producer retries create duplicate messages?
129. What is idempotent producer?
130. How does `enable.idempotence=true` work?
131. What is the difference between idempotence and exactly-once processing?
132. What is a producer sequence number?
133. What is a producer ID?
134. What is an epoch in Kafka producer protocol?
135. What is `max.in.flight.requests.per.connection`?
136. Why is `max.in.flight.requests.per.connection` important?
137. What happens if multiple requests are in flight and one fails?
138. How can producer retries affect ordering?
139. What is `compression.type`?
140. Which Kafka compression algorithm would you choose and why?
141. What are the trade-offs of compression?
142. How does compression affect CPU?
143. How does compression affect network bandwidth?
144. How do you tune Kafka producer throughput?
145. How do you tune Kafka producer latency?
146. How do you troubleshoot slow producer performance?
147. What causes `TimeoutException` on the producer?
148. What causes `RecordTooLargeException`?
149. What is `message.max.bytes`?
150. What is `max.request.size`?
151. What is the relationship between `message.max.bytes` and `max.request.size`?
152. What is `replica.fetch.max.bytes`?
153. What happens when producer request size exceeds broker limits?
154. How would you safely increase Kafka message size limits?
155. What is producer backpressure?
156. How would you handle producer buffer exhaustion?
157. What is `BufferExhaustedException`?
158. How do you troubleshoot producer request timeouts?
159. How do you troubleshoot producer retries continuously increasing?
160. How do you guarantee producer-side ordering?
161. How do transactions work with producers?
162. What is `transactional.id`?
163. What is producer fencing?
164. What happens if two producers use the same `transactional.id`?
165. What is `transaction.timeout.ms`?
166. How do you configure a producer for maximum durability?
167. How do you configure a producer for maximum throughput?
168. How do you configure a producer for minimum latency?
169. How would you choose producer settings for a financial transaction system?

---

# 4. Consumers & Consumer Groups 

170. Explain Kafka consumer architecture.
171. What is a Kafka consumer group?
172. Why do we use consumer groups?
173. How does Kafka distribute partitions among consumers?
174. What happens when there are fewer consumers than partitions?
175. What happens when consumers equal partitions?
176. What happens when consumers exceed partitions?
177. Can two consumers in the same group consume the same partition?
178. Can consumers from different groups consume the same partition?
179. How does Kafka provide parallelism using consumer groups?
180. What is group coordination?
181. What is the group coordinator?
182. How is a group coordinator selected?
183. What is consumer membership?
184. What happens when a consumer joins a group?
185. What happens when a consumer leaves a group?
186. What happens when a consumer crashes?
187. What happens when a consumer becomes slow?
188. What is consumer heartbeat?
189. What is `session.timeout.ms`?
190. What is `heartbeat.interval.ms`?
191. What is `max.poll.interval.ms`?
192. What is `max.poll.records`?
193. What is the difference between `session.timeout.ms` and `max.poll.interval.ms`?
194. Why can a consumer be alive but still trigger a rebalance?
195. What is consumer rebalancing?
196. What triggers a consumer rebalance?
197. What happens internally during a rebalance?
198. What is eager rebalancing?
199. What is cooperative rebalancing?
200. What is cooperative-sticky assignment?
201. What is the difference between eager and cooperative rebalancing?
202. What is static consumer group membership?
203. What is `group.instance.id`?
204. How does static membership reduce unnecessary rebalances?
205. What is the broker-coordinated consumer rebalance protocol?
206. What is KIP-848?
207. How does the newer consumer rebalance protocol differ from the traditional protocol?
208. What is a partition assignor?
209. What is RangeAssignor?
210. What is RoundRobinAssignor?
211. What is StickyAssignor?
212. What is CooperativeStickyAssignor?
213. When would you choose each assignment strategy?
214. How does partition assignment change during scaling?
215. How would you perform a zero/minimal-downtime consumer deployment?
216. How do you avoid rebalance storms during Kubernetes rolling deployments?
217. How do you troubleshoot continuous consumer rebalances?
218. How do you identify which consumer owns a partition?
219. How do you inspect consumer group state?
220. How do you delete a consumer group?
221. When should you not delete a consumer group?
222. What happens if a consumer group is deleted while consumers are running?
223. What happens if two applications accidentally use the same `group.id`?
224. What happens if two applications use different `group.id`s?
225. How do you design consumer groups for multiple independent applications?

---

# 5. Consumer Offset Management

226. What is auto-commit?
227. How does `enable.auto.commit` work?
228. What is manual offset commit?
229. What is synchronous offset commit?
230. What is asynchronous offset commit?
231. What is the difference between `commitSync()` and `commitAsync()`?
232. When would you use manual commits?
233. When would you use auto-commit?
234. What happens if a consumer crashes before committing an offset?
235. What happens if a consumer commits before processing a record?
236. What happens if a consumer commits after processing a record?
237. How can incorrect commit timing cause message loss?
238. How can incorrect commit timing cause duplicate processing?
239. How do you implement at-most-once processing?
240. How do you implement at-least-once processing?
241. How do you implement exactly-once processing?
242. What is offset commit ordering?
243. What happens when asynchronous commits complete out of order?
244. How do you handle offset commits during consumer shutdown?
245. How do you commit offsets for individual partitions?
246. How do you pause and resume partitions?
247. Why would you pause a consumer partition?
248. How do you handle a poison message without blocking the entire partition?
249. How do you implement retry topics?
250. How do you implement a dead-letter topic?
251. How do you prevent infinite retries?
252. How do you replay failed Kafka messages?
253. How do you replay a topic safely in production?

---

# 6. Replication, Leader, Follower & ISR 

254. What is Kafka replication?
255. What is replication factor?
256. What does replication factor 1 mean?
257. What does replication factor 3 mean?
258. Why is replication factor 3 commonly used in production?
259. What is a leader replica?
260. What is a follower replica?
261. What does the partition leader do?
262. What does a follower do?
263. Does a follower serve normal client reads?
264. What is ISR?
265. What is the in-sync replica set?
266. How does a replica enter the ISR?
267. How does a replica leave the ISR?
268. What causes ISR shrinkage?
269. What causes ISR expansion?
270. Why is ISR important for durability?
271. What is an out-of-sync replica?
272. What is `min.insync.replicas`?
273. How does `min.insync.replicas=2` work with replication factor 3?
274. What happens when ISR falls below `min.insync.replicas`?
275. What is unclean leader election?
276. What are the risks of unclean leader election?
277. When would you enable unclean leader election?
278. What is preferred leader?
279. What is preferred replica election?
280. What causes uneven leader distribution?
281. How do you rebalance partition leadership?
282. What happens when a partition leader broker goes down?
283. How is a new partition leader selected?
284. What happens if all ISR replicas fail?
285. What happens if the leader is unavailable but a non-ISR replica exists?
286. What is leader epoch?
287. What is leader epoch fencing?
288. What is replica lag?
289. How do you detect replica lag?
290. How do you troubleshoot ISR constantly shrinking?
291. How do you troubleshoot under-replicated partitions?
292. What is an under-replicated partition?
293. What is an offline partition?
294. What is the difference between under-replicated and offline partitions?
295. How do you recover from under-replicated partitions?
296. How do you recover from offline partitions?
297. What happens if a broker loses its disk?
298. How does Kafka recover replicas after broker restart?

---

# 7. Kafka Storage & Log Internals

299. How does Kafka store messages on disk?
300. What is a Kafka log segment?
301. Why does Kafka use log segments?
302. What is `log.segment.bytes`?
303. What is `log.segment.ms`?
304. What happens when a log segment rolls?
305. What is log retention?
306. What is time-based retention?
307. What is size-based retention?
308. Can Kafka delete messages individually?
309. Why does Kafka delete records based on segments?
310. What is log compaction?
311. How does log compaction work?
312. What is a compacted topic?
313. When would you use log compaction?
314. What is the difference between retention and compaction?
315. Can a compacted topic still contain old records?
316. What is a tombstone record?
317. How does Kafka handle tombstones?
318. What happens to tombstones during compaction?
319. What is `cleanup.policy=delete`?
320. What is `cleanup.policy=compact`?
321. What is `cleanup.policy=compact,delete`?
322. How would you configure a topic for both compaction and retention?
323. What is `log.dirs`?
324. What happens if Kafka has multiple log directories?
325. How does Kafka distribute partitions across log directories?
326. What happens when one Kafka disk becomes full?
327. How do you recover a Kafka broker from disk-full condition?
328. What happens when the Kafka filesystem reaches 100% usage?
329. How does filesystem page cache affect Kafka performance?
330. Why is Kafka heavily dependent on filesystem page cache?
331. Why is Kafka often deployed on local disks?
332. HDD vs SSD for Kafka — what would you choose?
333. What is the impact of disk IOPS on Kafka?
334. What is the impact of disk throughput on Kafka?
335. What is the impact of disk latency on Kafka?
336. How would you design Kafka storage for a high-throughput cluster?
337. How would you estimate Kafka storage requirements?

---

# 8. Kafka KRaft & ZooKeeper ([Apache Kafka][3]) 

338. What is ZooKeeper's role in older Kafka architectures?
339. What metadata did Kafka store/manage through ZooKeeper?
340. What is KRaft?
341. Why was KRaft introduced?
342. What problem does KRaft solve?
343. What is the difference between ZooKeeper mode and KRaft mode?
344. How does KRaft manage cluster metadata?
345. What is the KRaft metadata quorum?
346. What is a KRaft controller?
347. What is an active controller?
348. What is a standby controller?
349. What is `process.roles`?
350. What is a broker-only KRaft node?
351. What is a controller-only KRaft node?
352. What is a combined broker/controller node?
353. Why is combined mode not preferred for critical production environments?
354. How many KRaft controllers should you run in production?
355. Why are 3 or 5 controllers commonly used?
356. How many KRaft controller failures can a 3-controller quorum tolerate?
357. How many can a 5-controller quorum tolerate?
358. What happens if KRaft loses quorum?
359. Can Kafka brokers continue serving data if the controller quorum is unavailable?
360. What is the KRaft metadata log?
361. What is the relationship between KRaft and Raft consensus?
362. What is `node.id` in KRaft?
363. What replaced `broker.id` in KRaft configurations?
364. What is `controller.quorum.voters`?
365. What is `controller.quorum.bootstrap.servers`?
366. What is the difference between static and dynamic KRaft quorum?
367. How do you add a KRaft controller?
368. How do you remove a KRaft controller?
369. How do you check KRaft quorum health?
370. How do you troubleshoot a KRaft controller failure?
371. How do you troubleshoot KRaft metadata quorum loss?
372. How do you migrate ZooKeeper-based Kafka to KRaft?
373. What is the bridge release for ZooKeeper-to-KRaft migration?
374. What should you verify before migrating ZooKeeper to KRaft?
375. How would you plan a production ZooKeeper-to-KRaft migration?
376. How would you roll back a failed KRaft migration?
377. How do you monitor KRaft controller health?
378. What are the operational advantages of KRaft?
379. What are the operational risks of KRaft?
380. How would you explain KRaft architecture on a whiteboard?

---

# 9. Kafka Networking, Listeners & Connectivity 

381. What are Kafka listeners?
382. What are `listeners`?
383. What are `advertised.listeners`?
384. What is the difference between `listeners` and `advertised.listeners`?
385. Why is `advertised.listeners` one of the most common Kafka connectivity problems?
386. What happens if `advertised.listeners` points to an unreachable hostname?
387. How does Kafka client bootstrap work?
388. What is `bootstrap.servers`?
389. Does a Kafka client communicate only with the bootstrap broker?
390. What happens after the client receives metadata?
391. How does a producer discover the partition leader?
392. How does a consumer discover its partition leader?
393. What is a listener protocol?
394. What is `PLAINTEXT`?
395. What is `SSL`?
396. What is `SASL_PLAINTEXT`?
397. What is `SASL_SSL`?
398. How do you configure multiple Kafka listeners?
399. Why would you configure INTERNAL and EXTERNAL listeners?
400. How would you configure Kafka listeners in Kubernetes?
401. How would you expose Kafka outside Kubernetes?
402. Why does a Kubernetes LoadBalancer configuration often require special Kafka listener configuration?
403. How would you expose a Kafka cluster to applications in another network?
404. How would you troubleshoot DNS problems with Kafka?
405. How would you troubleshoot firewall problems with Kafka?
406. How would you troubleshoot `Connection refused`?
407. How would you troubleshoot `Connection timed out`?
408. How would you troubleshoot `UnknownHostException`?
409. How would you troubleshoot `NetworkException`?
410. How would you troubleshoot `NotLeaderOrFollowerException`?
411. How would you troubleshoot `LeaderNotAvailableException`?
412. How would you troubleshoot `Failed to update metadata`?
413. How would you troubleshoot Kafka connectivity from a Docker container?
414. How would you troubleshoot Kafka connectivity from Kubernetes?
415. How would you troubleshoot Kafka connectivity across regions?
416. How would you troubleshoot intermittent broker connectivity?

---

# 10. Kafka Security — Authentication & Authorization ([Apache Kafka][4]) 

417. What is Kafka authentication?
418. What is Kafka authorization?
419. What is the difference between authentication and authorization?
420. What security mechanisms does Kafka support?
421. What is SSL/TLS authentication?
422. What is SASL?
423. What is SASL/PLAIN?
424. What is SASL/SCRAM?
425. What is SASL/GSSAPI?
426. What is Kerberos?
427. What is SASL/OAUTHBEARER?
428. When would you use SASL/SCRAM?
429. When would you use Kerberos?
430. When would you use mTLS?
431. What is SASL_SSL?
432. What is SASL_PLAINTEXT?
433. What is the difference between SASL_SSL and SSL?
434. How do you enable TLS encryption for Kafka?
435. How do you configure Kafka SSL certificates?
436. What is a keystore?
437. What is a truststore?
438. What is the difference between a keystore and truststore?
439. What is a CA certificate?
440. How does Kafka certificate validation work?
441. How do you rotate Kafka TLS certificates?
442. How do you rotate certificates without downtime?
443. How do you troubleshoot Kafka SSL handshake failures?
444. How do you troubleshoot `SSLHandshakeException`?
445. What causes hostname verification failures?
446. What is Kafka ACL?
447. How do Kafka ACLs work?
448. How do you grant producer access to a topic?
449. How do you grant consumer access to a topic?
450. How do you grant consumer-group access?
451. What permissions are required to consume from a secured Kafka topic?
452. What permissions are required to produce to a secured Kafka topic?
453. How do you troubleshoot `TopicAuthorizationException`?
454. How do you troubleshoot `GroupAuthorizationException`?
455. How do you implement least privilege in Kafka?
456. How do you secure internal Kafka topics?
457. How do you secure `__consumer_offsets`?
458. How do you secure Kafka Connect internal topics?
459. How do you secure Kafka Streams internal topics?
460. How do you audit Kafka access?
461. How would you secure Kafka in a production enterprise environment?

---

# 11. JAAS, LDAP, Active Directory & Enterprise Security 

462. What is JAAS?
463. Why does Kafka use JAAS?
464. What is a JAAS login module?
465. What is `ScramLoginModule`?
466. What is `PlainLoginModule`?
467. How does JAAS authentication work in Kafka?
468. What is `KAFKA_OPTS`?
469. What are `required`, `requisite`, `sufficient`, and `optional` in JAAS?
470. How would you integrate Kafka with LDAP?
471. How would you integrate Kafka with Active Directory?
472. LDAP vs Active Directory — what is the difference?
473. How would you authenticate Kafka users against enterprise AD?
474. How would you combine LDAP authentication with Kafka ACLs?
475. How would you troubleshoot Kafka LDAP authentication failures?
476. How would you troubleshoot Kerberos authentication failures?
477. What is a Kerberos principal?
478. What is a keytab?
479. What is SPNEGO?
480. How would you rotate Kafka service credentials?
481. How would you avoid storing Kafka passwords in plaintext configuration files?
482. How would you integrate Kafka security with Kubernetes Secrets?
483. How would you integrate Kafka security with Vault?
484. How would you design Kafka security for multiple teams?

---

# 12. Kafka Delivery Semantics & Reliability ([Apache Kafka][5])

485. What is at-most-once delivery?
486. What is at-least-once delivery?
487. What is exactly-once processing?
488. What is the difference between at-most-once and at-least-once?
489. What is the difference between at-least-once and exactly-once?
490. How can Kafka provide at-least-once processing?
491. How can Kafka provide exactly-once processing?
492. What is idempotent processing?
493. What is an idempotent producer?
494. Is idempotent producer the same as exactly-once?
495. What are Kafka transactions?
496. What is a transactional producer?
497. What is `transactional.id`?
498. What is a transaction coordinator?
499. How does Kafka transaction coordination work?
500. What happens when a Kafka transaction aborts?
501. What is `read_committed`?
502. What is `read_uncommitted`?
503. What is the difference between `read_committed` and `read_uncommitted`?
504. What happens to aborted records?
505. What is transaction timeout?
506. What is transaction fencing?
507. How does Kafka guarantee atomicity between output records and consumer offsets?
508. How would you implement exactly-once consume-process-produce?
509. What are the limitations of exactly-once semantics?
510. Does Kafka guarantee exactly-once side effects in an external database?
511. How would you achieve exactly-once behavior between Kafka and a database?
512. What is the dual-write problem?
513. How can the Outbox Pattern solve the dual-write problem?
514. Kafka EOS vs database transaction — what is the difference?
515. What happens to transactions when a broker fails?
516. What happens if a producer crashes during a transaction?
517. What happens if a consumer crashes during a transaction?
518. How do you troubleshoot `ProducerFencedException`?
519. How do you troubleshoot transaction timeouts?
520. When should you avoid Kafka transactions?

---

# 13. Consumer Lag & Performance Troubleshooting ([TechPrep][6]) 

521. What is consumer lag?
522. How is consumer lag calculated?
523. What is the difference between offset lag and time lag?
524. How do you check consumer lag from CLI?
525. How do you monitor consumer lag in production?
526. What causes consumer lag?
527. How do you troubleshoot continuously increasing consumer lag?
528. How do you troubleshoot lag on only one partition?
529. How do you troubleshoot lag on all partitions?
530. What is a hot partition?
531. How can a hot partition cause consumer lag?
532. How can slow downstream APIs cause consumer lag?
533. How can slow database calls cause consumer lag?
534. How can garbage collection cause consumer lag?
535. How can CPU saturation cause consumer lag?
536. How can memory pressure cause consumer lag?
537. How can network latency cause consumer lag?
538. How can broker disk latency cause consumer lag?
539. How can frequent rebalances cause consumer lag?
540. How can `max.poll.interval.ms` cause lag?
541. How can `max.poll.records` affect lag?
542. How can fetch size affect consumer throughput?
543. How does `fetch.min.bytes` affect consumer performance?
544. How does `fetch.max.wait.ms` affect latency?
545. How do you increase consumer throughput?
546. When should you add more consumers?
547. When does adding consumers not help?
548. When should you increase partitions?
549. What is the relationship between partitions and consumer parallelism?
550. How do you troubleshoot a consumer that is active but making no progress?
551. How do you troubleshoot one consumer that is much slower than others?
552. How do you troubleshoot consumer lag after a deployment?
553. How do you troubleshoot consumer lag after increasing producer traffic?
554. How do you troubleshoot lag caused by a poison message?
555. How would you design alerting for consumer lag?
556. What lag threshold would you use for a critical Kafka workload?
557. How would you distinguish normal lag from dangerous lag?

---

# 14. Broker Performance & Cluster Troubleshooting

558. How do you troubleshoot a slow Kafka broker?
559. What Kafka broker metrics do you monitor?
560. How do you identify broker CPU bottlenecks?
561. How do you identify broker memory bottlenecks?
562. How do you identify broker disk bottlenecks?
563. How do you identify broker network bottlenecks?
564. What happens when Kafka broker CPU reaches 100%?
565. What happens when Kafka broker disk reaches 100%?
566. What happens when Kafka broker network bandwidth is saturated?
567. How do you identify slow disk I/O?
568. How do you identify excessive garbage collection?
569. How do you identify request queue saturation?
570. What is request latency in Kafka?
571. What is request queue time?
572. What is request processing time?
573. How do you troubleshoot high produce latency?
574. How do you troubleshoot high fetch latency?
575. How do you troubleshoot high request latency?
576. What is broker throttling?
577. Why would you throttle replication?
578. Why would you throttle reassignment?
579. How do you safely rebalance a large Kafka cluster?
580. How do you prevent cluster overload during partition reassignment?
581. How do you troubleshoot broker disk imbalance?
582. How do you troubleshoot uneven partition distribution?
583. How do you troubleshoot uneven leader distribution?
584. How do you troubleshoot high network utilization?
585. How do you troubleshoot Kafka JVM GC pauses?
586. What JVM settings are important for Kafka?
587. How does Kafka use heap memory?
588. Why should Kafka not simply be given a huge JVM heap?
589. What is the role of OS page cache in Kafka?
590. How do you perform Kafka capacity planning?

---

# 15. Kafka Broker Configuration

591. What are the most important Kafka broker configurations?
592. What is `num.network.threads`?
593. What is `num.io.threads`?
594. What is `socket.send.buffer.bytes`?
595. What is `socket.receive.buffer.bytes`?
596. What is `socket.request.max.bytes`?
597. What is `message.max.bytes`?
598. What is `replica.fetch.max.bytes`?
599. What is `replica.fetch.response.max.bytes`?
600. What is `num.replica.fetchers`?
601. What is `replica.lag.time.max.ms`?
602. What is `log.retention.ms`?
603. What is `log.retention.bytes`?
604. What is `log.segment.bytes`?
605. What is `log.segment.ms`?
606. What is `log.cleanup.policy`?
607. What is `auto.create.topics.enable`?
608. Would you enable automatic topic creation in production?
609. What is `default.replication.factor`?
610. What is `num.partitions`?
611. What is `unclean.leader.election.enable`?
612. What is `delete.topic.enable`?
613. What is `controlled.shutdown.enable`?
614. Which broker settings should be changed cautiously?
615. Which Kafka settings can be changed dynamically?
616. Which settings require a broker restart?
617. How do you change broker configuration without downtime?
618. How do you validate Kafka configuration changes?
619. How do you roll back a bad Kafka configuration?

---

# 16. Kafka CLI & Administration

620. What Kafka CLI tools do you use regularly?
621. How do you create a topic using CLI?
622. How do you describe a topic?
623. How do you alter topic configuration?
624. How do you list consumer groups?
625. How do you describe a consumer group?
626. How do you reset consumer offsets?
627. How do you delete a consumer group?
628. How do you produce test messages from CLI?
629. How do you consume messages from CLI?
630. How do you consume from the beginning?
631. How do you consume only the latest messages?
632. How do you consume from a specific partition?
633. How do you consume from a specific offset?
634. How do you consume from a specific timestamp?
635. How do you inspect topic configuration?
636. How do you inspect partition assignment?
637. How do you inspect broker configuration?
638. How do you inspect log directories?
639. How do you inspect partition replica distribution?
640. How do you perform partition reassignment?
641. How do you verify partition reassignment?
642. How do you cancel or modify a reassignment?
643. How do you elect preferred leaders?
644. How do you identify under-replicated partitions?
645. How do you identify offline partitions?
646. How do you identify the controller?
647. What Kafka CLI commands would you use first during an incident?

---

# 17. Kafka Monitoring & Observability ([Apache Kafka][7])

648. What Kafka metrics should be monitored in production?
649. Which broker metrics are critical?
650. Which producer metrics are critical?
651. Which consumer metrics are critical?
652. Which replication metrics are critical?
653. Which controller metrics are critical?
654. Which KRaft metrics are critical?
655. What is JMX in Kafka?
656. How do you expose Kafka JMX metrics?
657. How do you integrate Kafka with Prometheus?
658. How do you integrate Kafka with Grafana?
659. How would you monitor Kafka using Datadog?
660. How would you monitor Kafka using Splunk?
661. How would you monitor Kafka using ELK?
662. What alerts would you configure for Kafka?
663. What alert would you configure for under-replicated partitions?
664. What alert would you configure for offline partitions?
665. What alert would you configure for consumer lag?
666. What alert would you configure for disk utilization?
667. What alert would you configure for broker availability?
668. What alert would you configure for ISR shrink?
669. What alert would you configure for controller changes?
670. What alert would you configure for KRaft quorum health?
671. What alert would you configure for failed authentication?
672. What alert would you configure for producer error rate?
673. What alert would you configure for consumer error rate?
674. How do you correlate Kafka metrics with application metrics?
675. How do you build an end-to-end Kafka observability strategy?
676. How would you distinguish application problems from Kafka cluster problems?

---

# 18. Kafka Connect ([Apache Kafka][8]) 

677. What is Kafka Connect?
678. Why would you use Kafka Connect instead of writing a custom Kafka application?
679. What is a source connector?
680. What is a sink connector?
681. What is the difference between source and sink connectors?
682. What is a Kafka Connect worker?
683. What is standalone Kafka Connect?
684. What is distributed Kafka Connect?
685. What is the difference between standalone and distributed mode?
686. What is a connector?
687. What is a task?
688. What is the relationship between connector and task?
689. How does Kafka Connect scale?
690. How do you increase Kafka Connect tasks?
691. What determines the maximum useful number of connector tasks?
692. What are Kafka Connect internal topics?
693. What is the config topic?
694. What is the offsets topic?
695. What is the status topic?
696. How should Kafka Connect internal topics be replicated?
697. How do you deploy Kafka Connect in production?
698. How do you configure Kafka Connect for high availability?
699. How does Kafka Connect rebalance tasks?
700. What happens when a Kafka Connect worker fails?
701. How does another worker recover its tasks?
702. How do you troubleshoot a failed connector?
703. How do you restart a connector?
704. How do you pause a connector?
705. How do you resume a connector?
706. How do you inspect connector status?
707. How do you inspect connector tasks?
708. What is a dead-letter queue in Kafka Connect?
709. How do you configure error handling in Kafka Connect?
710. What is `errors.tolerance`?
711. What is `errors.retry.timeout`?
712. What is `errors.deadletterqueue.topic.name`?
713. How do you handle poison records in Kafka Connect?
714. What are SMTs in Kafka Connect?
715. What are Single Message Transforms?
716. When should you use SMTs?
717. When should you avoid SMTs?
718. How do you secure Kafka Connect?
719. How do you monitor Kafka Connect?
720. How do you upgrade Kafka Connect without downtime?
721. How do you troubleshoot Kafka Connect worker crashes?
722. How do you troubleshoot a connector stuck in RUNNING state?
723. How do you troubleshoot connector task failures?
724. How do you troubleshoot connector throughput issues?
725. How do you achieve exactly-once semantics in Kafka Connect?

---

# 19. Kafka Connect Production Scenarios

726. How would you stream MySQL changes into Kafka?
727. How would you stream PostgreSQL changes into Kafka?
728. How would you stream Kafka data into Elasticsearch?
729. How would you stream Kafka data into S3?
730. How would you stream Kafka data into a relational database?
731. How would you handle database schema changes with Kafka Connect?
732. How would you handle connector credential rotation?
733. How would you handle connector version upgrades?
734. How would you deploy connectors using Kubernetes?
735. How would you manage connector configurations using GitOps?
736. How would you prevent duplicate data from a source connector?
737. How would you troubleshoot CDC connector lag?
738. How would you troubleshoot a source connector that stopped reading?
739. How would you troubleshoot a sink connector that stopped writing?
740. How would you troubleshoot a sink connector with increasing lag?
741. How would you recover a corrupted Connect internal topic?
742. How would you recover a failed Connect worker?
743. How would you design a highly available Kafka Connect cluster?
744. How would you isolate connectors belonging to different teams?
745. How would you design Kafka Connect for hundreds of connectors?

---

# 20. MirrorMaker 2 & Multi-Cluster Kafka ([Apache Kafka][9]) 

746. What is MirrorMaker?
747. What is MirrorMaker 2?
748. What is the difference between MirrorMaker 1 and MirrorMaker 2?
749. Why is MirrorMaker 2 based on Kafka Connect?
750. How does MirrorMaker 2 replicate data?
751. What components does MirrorMaker 2 use?
752. What are heartbeat connectors?
753. What are checkpoint connectors?
754. What are MirrorMaker 2 internal topics?
755. How does MirrorMaker 2 synchronize consumer offsets?
756. What is offset translation in MirrorMaker 2?
757. What is `offset-syncs`?
758. What is the checkpoint topic?
759. How do you configure Cluster A → Cluster B replication?
760. How do you configure bidirectional replication?
761. What is active-active Kafka replication?
762. What is active-passive Kafka replication?
763. When would you choose active-active?
764. When would you choose active-passive?
765. How do you prevent replication loops?
766. How does topic naming work with MirrorMaker 2?
767. How do you filter topics in MirrorMaker 2?
768. How do you filter consumer groups?
769. How do you secure MirrorMaker 2?
770. How do you monitor MirrorMaker 2?
771. How do you measure replication lag?
772. How do you troubleshoot MirrorMaker 2 replication lag?
773. How do you troubleshoot MirrorMaker 2 authentication failures?
774. How do you troubleshoot MirrorMaker 2 authorization failures?
775. How do you perform disaster recovery using MirrorMaker 2?
776. How do you perform failover from Cluster A to Cluster B?
777. How do you perform failback?
778. How do you prevent duplicate processing during failover?
779. How do you handle consumer offsets during DR?
780. How would you design Kafka DR across two regions?
781. How would you design Kafka DR across two data centers?
782. How would you design Kafka replication for zero/low RPO?
783. How would you calculate RPO/RTO for Kafka?
784. How would you test Kafka disaster recovery?

---

# 21. Kafka Streams

785. What is Kafka Streams?
786. Kafka Streams vs Kafka Connect — what is the difference?
787. Kafka Streams vs Apache Flink — what is the difference?
788. Kafka Streams vs Spark Streaming — what is the difference?
789. What is a Kafka Streams application?
790. What is a topology?
791. What is a stream?
792. What is a table?
793. What is a KStream?
794. What is a KTable?
795. What is a GlobalKTable?
796. What is stream processing?
797. What is a stateless transformation?
798. What is a stateful transformation?
799. What is a state store?
800. What is a changelog topic?
801. What is a repartition topic?
802. Why does Kafka Streams create repartition topics?
803. What is windowing?
804. What is tumbling window?
805. What is hopping window?
806. What is sliding window?
807. What is session window?
808. What is event time?
809. What is processing time?
810. What are stream-table joins?
811. What are stream-stream joins?
812. What are table-table joins?
813. How does Kafka Streams scale?
814. How does Kafka Streams handle failures?
815. How does Kafka Streams achieve exactly-once processing?
816. What is `application.id`?
817. Why must `application.id` be unique?
818. How does Kafka Streams use consumer groups?
819. What happens when a Kafka Streams instance crashes?
820. How does state restoration work?
821. How do you monitor Kafka Streams?
822. How do you troubleshoot a Kafka Streams application?
823. How do you troubleshoot Kafka Streams rebalance?
824. How do you troubleshoot a Kafka Streams state-store issue?

---

# 22. Schema Registry & Serialization

825. What is serialization in Kafka?
826. What is deserialization?
827. What is Avro?
828. What is JSON serialization?
829. What is Protobuf?
830. What is JSON Schema?
831. What is Schema Registry?
832. Why do we need Schema Registry?
833. Kafka vs Schema Registry — what is the difference?
834. Where is the schema stored?
835. What is a schema ID?
836. How does a Kafka consumer retrieve the schema?
837. What is schema evolution?
838. What is backward compatibility?
839. What is forward compatibility?
840. What is full compatibility?
841. What is backward-transitive compatibility?
842. What happens if a producer sends an incompatible schema?
843. How do you manage schema versions in production?
844. How do you prevent breaking Kafka consumers?
845. How do you handle schema evolution across multiple teams?
846. How would you secure Schema Registry?
847. How would you monitor Schema Registry?
848. How would you troubleshoot serialization errors?
849. How would you troubleshoot deserialization errors?
850. How would you handle schema compatibility failures during deployment?

---

# 23. Kafka on Kubernetes

851. Would you deploy Kafka on Kubernetes?
852. What are the advantages of running Kafka on Kubernetes?
853. What are the disadvantages of running Kafka on Kubernetes?
854. What is Strimzi?
855. How does Strimzi deploy Kafka?
856. What is a Kafka custom resource?
857. How does Strimzi manage Kafka brokers?
858. How does Strimzi manage Kafka users?
859. How does Strimzi manage Kafka topics?
860. How does Strimzi manage Kafka Connect?
861. How does Strimzi manage Kafka MirrorMaker 2?
862. How would you deploy a 3-broker Kafka cluster on Kubernetes?
863. How would you configure persistent storage for Kafka?
864. Which Kubernetes storage class would you choose for Kafka?
865. Why is local persistent storage important for Kafka?
866. How do StatefulSets help Kafka?
867. Why does Kafka require stable broker identity?
868. How do you expose Kafka internally in Kubernetes?
869. How do you expose Kafka externally?
870. How do you configure Kafka advertised listeners in Kubernetes?
871. How do you handle Kafka TLS certificates in Kubernetes?
872. How do you manage Kafka credentials using Kubernetes Secrets?
873. How do you perform Kafka rolling upgrades on Kubernetes?
874. How do you scale Kafka brokers on Kubernetes?
875. What happens when a Kafka pod is rescheduled?
876. How do you handle node failure?
877. How do you spread Kafka brokers across Kubernetes nodes?
878. What is pod anti-affinity for Kafka?
879. What is topology spread constraint for Kafka?
880. How do you prevent two Kafka brokers from running on the same node?
881. How would you configure PodDisruptionBudget for Kafka?
882. How would you perform Kubernetes node maintenance without Kafka downtime?
883. How do you troubleshoot a Kafka pod stuck in Pending?
884. How do you troubleshoot Kafka PVC issues?
885. How do you troubleshoot Kafka CrashLoopBackOff?
886. How do you troubleshoot Kafka readiness failures?
887. How do you troubleshoot Kafka liveness failures?
888. How do you troubleshoot Kafka networking inside Kubernetes?
889. How do you monitor Kafka running on Kubernetes?
890. How would you design production-grade Kafka on Kubernetes?

---

# 24. Kafka High Availability & Production Design

891. How would you design a production Kafka cluster?
892. How many brokers would you use for a production cluster?
893. How do you decide replication factor?
894. How do you decide controller count?
895. How do you decide partition count?
896. How do you decide broker count?
897. How do you decide disk size?
898. How do you decide disk IOPS requirements?
899. How do you decide network bandwidth?
900. How do you decide CPU requirements?
901. How do you decide memory requirements?
902. How do you design Kafka across availability zones?
903. How do you distribute replicas across AZs?
904. What is rack awareness in Kafka?
905. Why is rack awareness important?
906. How do you configure `broker.rack`?
907. How does rack-aware replica assignment work?
908. What happens if an entire availability zone fails?
909. How many AZ failures can your Kafka design tolerate?
910. How would you design Kafka for zero data loss?
911. How would you design Kafka for maximum throughput?
912. How would you design Kafka for minimum latency?
913. How would you design Kafka for millions of events per second?
914. How would you design Kafka for very large messages?
915. How would you design Kafka for millions of partitions?
916. How would you design Kafka for hundreds of consumer groups?
917. How would you design Kafka for multi-tenancy?
918. How would you isolate tenants?
919. How would you implement Kafka quotas?
920. How would you prevent one application from overwhelming Kafka?
921. How would you design Kafka for financial transactions?
922. How would you design Kafka for order processing?
923. How would you design Kafka for IoT workloads?
924. How would you design Kafka for log ingestion?
925. How would you design Kafka for real-time analytics?
926. How would you design Kafka for event-driven microservices?

---

# 25. Kafka Capacity Planning & Scaling

927. How do you perform Kafka capacity planning?
928. How do you calculate required broker throughput?
929. How do you calculate storage requirements?
930. How do you calculate replication storage overhead?
931. How do you calculate network bandwidth?
932. How do you calculate expected consumer throughput?
933. How do you estimate partition count from throughput?
934. How do you estimate partition count from consumer parallelism?
935. What happens when Kafka traffic doubles?
936. How do you scale Kafka horizontally?
937. How do you add a new broker?
938. Does adding a broker automatically rebalance existing data?
939. How do you move partitions to a new broker?
940. How do you rebalance a Kafka cluster?
941. How do you avoid overloading brokers during rebalancing?
942. How do you scale consumers?
943. How do you scale producers?
944. How do you scale Kafka Connect?
945. How do you scale MirrorMaker 2?
946. How do you identify the current Kafka bottleneck?
947. How do you perform Kafka load testing?
948. Which metrics do you collect during load testing?
949. How do you establish Kafka performance baselines?
950. How do you plan capacity for future traffic growth?

---

# 26. Kafka Partition Reassignment & Broker Operations

951. What is partition reassignment?
952. Why would you perform partition reassignment?
953. How do you move partitions from one broker to another?
954. How do you add replicas to partitions?
955. How do you remove replicas from partitions?
956. How do you rebalance a cluster after adding brokers?
957. What is replica movement throttling?
958. Why should partition reassignment be throttled?
959. How do you monitor reassignment progress?
960. What happens if a broker fails during reassignment?
961. What happens if reassignment gets stuck?
962. How do you cancel reassignment?
963. How do you verify data after reassignment?
964. What is preferred replica election?
965. How do you rebalance leaders after broker maintenance?
966. How would you decommission a Kafka broker?
967. What steps would you follow before shutting down a broker?
968. How do you safely remove a broker from a production cluster?
969. What happens to its partitions?
970. How do you verify that no replicas remain on the broker?
971. How would you replace a failed Kafka broker?
972. How would you recover a broker with a corrupted disk?
973. How would you replace a disk without losing Kafka data?

---

# 27. Kafka Upgrades & Migration ([Apache Kafka][10])

974. How do you upgrade Kafka in production?
975. What is a rolling Kafka upgrade?
976. How do you perform a zero-downtime Kafka upgrade?
977. What should you verify before upgrading Kafka?
978. How do you verify client compatibility before a Kafka upgrade?
979. How do you upgrade brokers one by one?
980. What is inter-broker protocol version?
981. What is metadata version?
982. How do you handle Kafka protocol compatibility during upgrades?
983. What is the difference between Kafka broker version and client version?
984. Can an older Kafka client connect to a newer broker?
985. Can a newer Kafka client connect to an older broker?
986. How do you upgrade Kafka clients?
987. How do you upgrade Kafka Connect?
988. How do you upgrade MirrorMaker 2?
989. How do you upgrade Kafka Streams applications?
990. How do you perform ZooKeeper-to-KRaft migration?
991. How do you validate a Kafka upgrade?
992. What metrics should be watched during an upgrade?
993. What would cause an upgrade to fail?
994. How do you roll back a Kafka upgrade?
995. How do you handle deprecated Kafka configurations?
996. How do you perform a major-version upgrade with minimal risk?
997. How would you design an upgrade plan for a 50-broker Kafka cluster?

---

# 28. Kafka Failure Scenarios

998. What happens when one Kafka broker goes down?
999. What happens when two brokers go down?
1000. What happens when three brokers go down in a replication-factor-3 cluster?
1001. What happens when the partition leader goes down?
1002. What happens when all ISR replicas go down?
1003. What happens when a follower becomes unavailable?
1004. What happens when a broker loses network connectivity?
1005. What happens when a broker loses its disk?
1006. What happens when a broker runs out of disk space?
1007. What happens when a controller goes down?
1008. What happens when the active KRaft controller goes down?
1009. What happens when the KRaft controller quorum loses majority?
1010. What happens when all Kafka controllers go down?
1011. What happens when ZooKeeper goes down in an older Kafka cluster?
1012. What happens when a consumer goes down?
1013. What happens when all consumers in a group go down?
1014. What happens when a producer goes down?
1015. What happens when a producer crashes after sending a message?
1016. What happens when a producer crashes before receiving an acknowledgement?
1017. What happens when a consumer crashes after processing but before committing?
1018. What happens when a consumer crashes after committing but before processing?
1019. What happens when `__consumer_offsets` is unavailable?
1020. What happens when a topic leader election takes place?
1021. What happens during a network partition?
1022. What happens during a split-brain scenario?
1023. How does Kafka prevent stale leaders from writing data?
1024. How does Kafka handle broker recovery?
1025. How would you recover Kafka after a complete cluster outage?

---

# 29. Kafka Troubleshooting — Real Production Scenarios

1026. A producer cannot connect to Kafka; how would you troubleshoot it?
1027. A consumer cannot connect to Kafka; how would you troubleshoot it?
1028. Kafka clients report `Failed to update metadata`; what would you check?
1029. Kafka clients report timeout errors; how would you troubleshoot them?
1030. Kafka clients report `LeaderNotAvailableException`; what would you check?
1031. Kafka clients report `NotLeaderOrFollowerException`; what would you check?
1032. Kafka clients report `UnknownTopicOrPartitionException`; what would you check?
1033. Kafka clients report `RecordTooLargeException`; how would you fix it?
1034. Kafka clients report `MessageSizeTooLarge`; what would you check?
1035. Producers are timing out; how would you investigate?
1036. Producers are retrying continuously; how would you investigate?
1037. Producer throughput suddenly drops; how would you troubleshoot it?
1038. Producer latency suddenly increases; how would you troubleshoot it?
1039. Consumers suddenly stop consuming; what would you check?
1040. Consumers are alive but lag is increasing; how would you troubleshoot it?
1041. One partition has huge lag; what could be the cause?
1042. All partitions have huge lag; what could be the cause?
1043. Consumer rebalances happen continuously; how would you troubleshoot them?
1044. Consumer group is stuck in `PreparingRebalance`; what would you investigate?
1045. Consumer group is stuck in `CompletingRebalance`; what would you investigate?
1046. Consumer group has no active members; how would you investigate?
1047. Consumers are constantly joining and leaving; what would you check?
1048. Consumer processing takes longer than expected; which configurations would you inspect?
1049. A consumer gets kicked out despite sending heartbeats; why could that happen?
1050. A consumer gets kicked out because of `max.poll.interval.ms`; how would you fix it?
1051. Kafka has high CPU usage; how would you troubleshoot it?
1052. Kafka has high memory usage; how would you troubleshoot it?
1053. Kafka has high disk utilization; how would you troubleshoot it?
1054. Kafka disk I/O latency is high; how would you troubleshoot it?
1055. Kafka network traffic is saturated; how would you troubleshoot it?
1056. ISR keeps shrinking; how would you troubleshoot it?
1057. Under-replicated partitions keep increasing; how would you troubleshoot them?
1058. Offline partitions appear; what would you do?
1059. Partition leadership is heavily skewed; how would you fix it?
1060. One broker has much more data than others; how would you troubleshoot it?
1061. One broker has much higher traffic than others; what could cause it?
1062. Kafka broker repeatedly restarts; how would you investigate?
1063. Kafka broker is OOM-killed; how would you investigate?
1064. Kafka broker has long GC pauses; how would you investigate?
1065. Kafka pod is CrashLoopBackOff; how would you troubleshoot it?
1066. Kafka PVC is full; what would you do?
1067. Kafka pod is Pending; how would you troubleshoot it?
1068. Kafka TLS handshake is failing; how would you troubleshoot it?
1069. SASL authentication is failing; how would you troubleshoot it?
1070. Kafka ACL authorization is failing; how would you troubleshoot it?
1071. Kafka Connect task is failing; how would you troubleshoot it?
1072. MirrorMaker 2 replication has stopped; how would you troubleshoot it?
1073. MirrorMaker 2 replication lag is increasing; how would you troubleshoot it?
1074. Kafka Streams application is continuously rebalancing; how would you troubleshoot it?
1075. Kafka cluster becomes unavailable after a configuration change; how would you recover it?
1076. Kafka cluster has high latency immediately after increasing partitions; what would you investigate?
1077. Kafka performance degraded after enabling TLS; how would you investigate?
1078. Kafka performance degraded after enabling compression; how would you investigate?
1079. Kafka performance degraded after increasing replication factor; how would you investigate?
1080. Kafka performance degraded after adding a consumer group; how would you investigate?
1081. Kafka works inside the cluster but not from outside; how would you troubleshoot it?
1082. Kafka works from one Kubernetes pod but not another; how would you troubleshoot it?
1083. Kafka works through IP but not hostname; how would you troubleshoot it?
1084. Kafka works with `localhost` but not with the broker DNS name; what would you check?
1085. Kafka clients connect to bootstrap server but then fail; what is the likely troubleshooting path?

---

# 30. Advanced Kafka Debugging

1086. How would you troubleshoot Kafka using broker logs?
1087. Which Kafka log messages indicate controller problems?
1088. Which Kafka log messages indicate replication problems?
1089. Which Kafka log messages indicate consumer-group problems?
1090. Which Kafka log messages indicate authentication problems?
1091. Which Kafka log messages indicate authorization problems?
1092. How would you correlate Kafka logs with JMX metrics?
1093. How would you correlate broker metrics with consumer lag?
1094. How would you identify whether a problem is producer-side or broker-side?
1095. How would you identify whether a problem is consumer-side or broker-side?
1096. How would you identify whether lag is caused by Kafka or the downstream database?
1097. How would you troubleshoot Kafka without restarting anything?
1098. When is restarting a Kafka broker justified?
1099. Why can blindly restarting Kafka brokers make an incident worse?
1100. How would you troubleshoot a production Kafka incident under pressure?
1101. What information would you collect before making a Kafka production change?
1102. How would you perform a Kafka root-cause analysis?
1103. How would you differentiate symptoms from root cause in a Kafka incident?
1104. What Kafka metrics would you capture before and after remediation?
1105. How would you prove that your Kafka fix actually worked?

---

# 31. Kafka Disaster Recovery

1106. What is RPO?
1107. What is RTO?
1108. How do you define RPO for Kafka?
1109. How do you define RTO for Kafka?
1110. How would you design Kafka for disaster recovery?
1111. Same-region vs cross-region Kafka replication — what would you choose?
1112. How would you replicate Kafka between two regions?
1113. How would you use MirrorMaker 2 for DR?
1114. How would you handle consumer offsets during DR?
1115. How would you fail over producers to another Kafka cluster?
1116. How would you fail over consumers to another Kafka cluster?
1117. How would you avoid duplicate processing during DR failover?
1118. How would you avoid data loss during DR failover?
1119. How would you handle DNS during Kafka failover?
1120. How would you handle application configuration during Kafka failover?
1121. How would you test Kafka DR without impacting production?
1122. How often should Kafka DR be tested?
1123. What is active-active Kafka DR?
1124. What is active-passive Kafka DR?
1125. What are the risks of active-active Kafka?
1126. How would you design a multi-region Kafka architecture?
1127. How would you handle regional network partition?
1128. How would you handle split-brain between Kafka regions?
1129. How would you calculate expected replication lag during DR?
1130. What would your Kafka DR runbook contain?

---

# 32. Kafka Security Production Scenarios

1131. How would you secure a Kafka cluster exposed to multiple applications?
1132. How would you isolate teams using Kafka ACLs?
1133. How would you implement least-privilege Kafka access?
1134. How would you rotate SASL credentials without downtime?
1135. How would you rotate TLS certificates without downtime?
1136. How would you migrate from PLAINTEXT to TLS?
1137. How would you migrate from SASL/PLAIN to SASL/SCRAM?
1138. How would you migrate from one authentication mechanism to another?
1139. How would you troubleshoot expired certificates?
1140. How would you troubleshoot certificate trust issues?
1141. How would you troubleshoot incorrect Kafka principals?
1142. How would you troubleshoot ACL mismatches?
1143. How would you secure Kafka-to-Kafka replication?
1144. How would you secure Kafka Connect?
1145. How would you secure MirrorMaker 2?
1146. How would you secure Kafka running in Kubernetes?
1147. How would you prevent credentials from appearing in logs?
1148. How would you integrate Kafka with enterprise IAM?
1149. How would you audit Kafka security events?
1150. How would you detect unauthorized Kafka access?

---

# 33. Kafka Multi-Tenancy & Quotas ([Apache Kafka][7])

1151. What is Kafka multi-tenancy?
1152. How would you host multiple teams on one Kafka cluster?
1153. How would you isolate teams using ACLs?
1154. How would you isolate teams using quotas?
1155. What are Kafka client quotas?
1156. What is a producer quota?
1157. What is a consumer quota?
1158. What is a request quota?
1159. What happens when a client exceeds its quota?
1160. How would you prevent one producer from overwhelming Kafka?
1161. How would you prevent one consumer from overwhelming a broker?
1162. How would you monitor quota throttling?
1163. How would you design Kafka for hundreds of tenants?
1164. When should you use separate Kafka clusters instead of multi-tenancy?
1165. How would you implement topic naming standards across teams?

---

# 34. Kafka Tiered Storage & Large-Scale Retention ([Apache Kafka][11])

1166. What is Kafka tiered storage?
1167. Why was tiered storage introduced?
1168. What is local tier storage?
1169. What is remote tier storage?
1170. What types of external storage can be used for Kafka tiered storage?
1171. How does tiered storage change Kafka retention architecture?
1172. What are the benefits of tiered storage?
1173. What are the disadvantages of tiered storage?
1174. How does tiered storage affect broker disk requirements?
1175. How does tiered storage affect recovery?
1176. How does tiered storage affect backfills?
1177. How would you design Kafka for months or years of retention?
1178. When would you choose tiered storage over simply increasing broker disks?
1179. How would you troubleshoot remote storage access failures?
1180. How would you monitor tiered storage?

---

# 35. Kafka Performance Engineering

1181. How would you optimize Kafka for throughput?
1182. How would you optimize Kafka for latency?
1183. What is the throughput-vs-latency trade-off in Kafka?
1184. How do batching and compression improve Kafka throughput?
1185. How does `linger.ms` affect throughput and latency?
1186. How does `batch.size` affect throughput?
1187. How does compression affect throughput?
1188. How does replication affect throughput?
1189. How does partition count affect throughput?
1190. How does consumer count affect throughput?
1191. How does network bandwidth limit Kafka?
1192. How does disk throughput limit Kafka?
1193. How does CPU limit Kafka?
1194. How does page cache affect Kafka?
1195. How does TLS affect Kafka performance?
1196. How does SASL affect Kafka performance?
1197. How would you benchmark Kafka?
1198. How would you benchmark producer throughput?
1199. How would you benchmark consumer throughput?
1200. How would you benchmark end-to-end latency?
1201. How would you identify the bottleneck in a Kafka pipeline?
1202. What is the difference between broker throughput and end-to-end throughput?
1203. How would you optimize a Kafka cluster processing 1 million messages per second?
1204. How would you optimize a Kafka cluster for low-latency financial transactions?
1205. How would you optimize Kafka for very large batch ingestion?

---

# 36. Kafka Architecture Design Questions — 8-Year Level

1206. Design a Kafka cluster for 100K messages/sec.
1207. Design a Kafka cluster for 1M messages/sec.
1208. Design Kafka for 10M messages/sec.
1209. Design Kafka for 100 TB of retained data.
1210. Design Kafka for multi-region deployment.
1211. Design Kafka for multi-AZ high availability.
1212. Design Kafka for zero data loss.
1213. Design Kafka for near-zero downtime.
1214. Design Kafka for extremely low latency.
1215. Design Kafka for maximum throughput.
1216. Design Kafka for thousands of producers.
1217. Design Kafka for thousands of consumers.
1218. Design Kafka for hundreds of consumer groups.
1219. Design Kafka for high-volume IoT telemetry.
1220. Design Kafka for e-commerce order processing.
1221. Design Kafka for payment transactions.
1222. Design Kafka for fraud detection.
1223. Design Kafka for log aggregation.
1224. Design Kafka for real-time analytics.
1225. Design Kafka for microservices event communication.
1226. Design Kafka for CDC from multiple databases.
1227. Design Kafka for a centralized enterprise event bus.
1228. Design Kafka for cross-region disaster recovery.
1229. Design Kafka for active-active applications.
1230. Design Kafka for active-passive disaster recovery.
1231. Design Kafka with strict per-customer ordering.
1232. Design Kafka with strict global ordering.
1233. Design Kafka where consumers can replay data for 30 days.
1234. Design Kafka where consumers can replay data for one year.
1235. Design Kafka with exactly-once processing requirements.
1236. Design Kafka with at-least-once requirements.
1237. Design Kafka for schema evolution across 100 teams.
1238. Design Kafka for secure enterprise workloads.
1239. Design Kafka on Kubernetes for production.
1240. Design Kafka with separate controller and broker nodes.
1241. Design Kafka using KRaft from scratch.
1242. Design Kafka with MirrorMaker 2 between two regions.
1243. Design Kafka with Kafka Connect and CDC.
1244. Design Kafka with Schema Registry.
1245. Design a complete Kafka platform including monitoring, security, DR, Connect, and GitOps.

---

# 37. Scenario-Based Senior/Lead Interview Questions

1246. You inherit a 20-broker Kafka cluster with poor documentation; how would you assess it?
1247. You inherit a Kafka cluster with 10,000 partitions; what would you investigate?
1248. You inherit a Kafka cluster running PLAINTEXT in production; how would you secure it?
1249. You inherit a ZooKeeper-based Kafka cluster; how would you plan KRaft migration?
1250. You inherit a Kafka cluster with replication factor 1; how would you remediate it?
1251. You inherit a cluster with constant ISR shrinkage; how would you investigate?
1252. You inherit a cluster with frequent leader elections; what would you investigate?
1253. You inherit a cluster with increasing consumer lag every evening; how would you troubleshoot it?
1254. You inherit a cluster where one broker is always overloaded; how would you investigate?
1255. You inherit a cluster with uneven partition distribution; how would you fix it?
1256. You inherit a cluster with uneven leader distribution; how would you fix it?
1257. You inherit a cluster with full disks; what would you do first?
1258. You inherit a Kafka cluster with no monitoring; what would you implement?
1259. You inherit a Kafka cluster with no authentication; what would you implement first?
1260. You inherit a Kafka platform with hundreds of manually created topics; how would you standardize it?
1261. You inherit a Kafka platform with no retention policy; how would you fix it?
1262. You inherit a Kafka platform with uncontrolled topic creation; how would you govern it?
1263. You inherit a Kafka platform where every application uses a different serialization format; how would you standardize it?
1264. You inherit a Kafka platform with frequent consumer rebalances; how would you fix the architecture?
1265. You inherit a Kafka platform where every deployment causes a rebalance storm; how would you redesign deployment?
1266. You inherit a Kafka platform where producers frequently get `TimeoutException`; how would you investigate?
1267. You inherit a Kafka platform where consumers frequently get `CommitFailedException`; how would you investigate?
1268. You inherit a Kafka platform where MirrorMaker 2 is continuously falling behind; how would you troubleshoot it?
1269. You inherit a Kafka Connect cluster with hundreds of connectors; how would you operate it safely?
1270. You inherit a Kafka cluster running on Kubernetes with unstable pods; how would you stabilize it?
1271. You inherit a Kafka cluster where TLS certificates expire every month; how would you automate certificate management?
1272. You inherit a Kafka cluster with no disaster-recovery plan; how would you build one?
1273. You inherit a Kafka cluster that must support a 10x traffic increase; how would you capacity-plan it?
1274. You inherit a Kafka cluster that must support zero data loss; which configurations would you review?
1275. You inherit a Kafka cluster that must reduce latency by 50%; how would you approach it?

---

# 38. DevOps / CI-CD / Kafka

1276. How would you manage Kafka infrastructure using Terraform?
1277. What Kafka resources would you manage through Terraform?
1278. How would you manage Kafka topics as code?
1279. How would you manage Kafka ACLs as code?
1280. How would you manage Kafka users as code?
1281. How would you manage Kafka Connect connectors through GitOps?
1282. How would you deploy Kafka using Helm?
1283. How would you deploy Kafka using Argo CD?
1284. How would you implement Kafka configuration promotion across environments?
1285. How would you manage dev, staging, and production Kafka clusters?
1286. How would you prevent production topic changes from being made manually?
1287. How would you implement Kafka configuration drift detection?
1288. How would you perform Kafka upgrades through CI/CD?
1289. How would you validate Kafka configuration in CI?
1290. How would you test Kafka connectivity during deployment?
1291. How would you automate Kafka topic creation?
1292. How would you automate Kafka ACL creation?
1293. How would you automate Kafka user creation?
1294. How would you automate Kafka Connect deployment?
1295. How would you implement rollback for Kafka configuration?
1296. How would you implement policy-as-code for Kafka?
1297. How would you prevent developers from creating unlimited partitions?
1298. How would you enforce replication-factor standards automatically?
1299. How would you enforce retention policies automatically?
1300. How would you integrate Kafka platform operations into a DevOps pipeline?

---

# 39. Kafka + Terraform / Infrastructure-as-Code

1301. How would you provision Kafka infrastructure using Terraform?
1302. How would you provision Kafka on AWS using Terraform?
1303. How would you provision Kafka on Azure using Terraform?
1304. How would you provision Kafka on GCP using Terraform?
1305. Managed Kafka vs self-managed Kafka — what would you choose?
1306. Apache Kafka vs Amazon MSK — what are the operational differences?
1307. How would you manage MSK using Terraform?
1308. How would you manage Kafka topics using Terraform?
1309. How would you manage Kafka ACLs using Terraform?
1310. How would you prevent Terraform from accidentally deleting production topics?
1311. How would you manage Kafka secrets with Terraform safely?
1312. How would you handle Kafka configuration drift?
1313. How would you perform Kafka infrastructure changes without downtime?
1314. How would you design reusable Terraform modules for Kafka?
1315. How would you separate Kafka infrastructure state across environments?

---

# 40. Cloud Kafka / Managed Kafka

1316. What is Amazon MSK?
1317. What is Confluent Cloud?
1318. Managed Kafka vs self-managed Kafka — what are the trade-offs?
1319. What Kafka responsibilities remain with you in a managed Kafka service?
1320. What Kafka responsibilities are handled by the cloud provider?
1321. How would you migrate self-managed Kafka to MSK?
1322. How would you migrate MSK to self-managed Kafka?
1323. How would you migrate between two Kafka providers?
1324. How would you migrate Kafka without losing messages?
1325. How would you migrate Kafka consumers without duplicate processing?
1326. How would you migrate Kafka producers with minimal downtime?
1327. How would you perform a cross-cloud Kafka migration?
1328. How would you use MirrorMaker 2 for cloud migration?
1329. What are the cost drivers for managed Kafka?
1330. How would you optimize managed Kafka costs?

---

# 41. Advanced Kafka Internals

1331. Explain Kafka's request processing pipeline.
1332. Explain the Kafka network thread model.
1333. Explain the Kafka I/O thread model.
1334. Explain Kafka's log append path.
1335. Explain Kafka's fetch path.
1336. Explain how a producer request reaches the partition leader.
1337. Explain how a consumer fetch request reaches the partition leader.
1338. Explain how replication fetches work.
1339. What is a replica fetcher?
1340. What is the high watermark?
1341. What is the log end offset?
1342. What is the last stable offset?
1343. What is the difference between high watermark and last stable offset?
1344. What is a leader epoch?
1345. What is an epoch checkpoint?
1346. How does Kafka prevent stale replica writes?
1347. How does Kafka detect stale leaders?
1348. What is fencing in Kafka?
1349. What is the transaction coordinator?
1350. What is the group coordinator?
1351. How are group coordinators selected?
1352. How are transaction coordinators selected?
1353. What internal Kafka topics exist?
1354. What is `__consumer_offsets`?
1355. What is `__transaction_state`?
1356. What internal topics are created by Kafka Streams?
1357. What internal topics are created by Kafka Connect?
1358. What happens if an internal Kafka topic becomes unavailable?
1359. How does Kafka recover metadata after broker restart?
1360. How does KRaft persist metadata?
1361. How does KRaft recover after controller failure?
1362. How does Kafka recover a replica after broker restart?

---

# 42. Extreme Troubleshooting Questions

1363. Kafka cluster is healthy, but application latency is high — how do you isolate the issue?
1364. Kafka has zero broker errors, but consumer lag is increasing — what do you check?
1365. Kafka has zero consumer errors, but messages are not being processed — what do you check?
1366. Producer acknowledgements are successful, but consumers don't see messages — how do you troubleshoot?
1367. Consumers see duplicate messages — how do you identify the cause?
1368. Consumers miss messages — how do you identify the cause?
1369. Messages appear out of order — how do you investigate?
1370. Only messages for one customer are out of order — how do you investigate?
1371. Only one partition is overloaded — how do you fix it?
1372. Increasing consumers does not reduce lag — what would you investigate?
1373. Increasing partitions does not improve throughput — what would you investigate?
1374. Increasing broker count does not improve performance — why might that happen?
1375. Kafka has plenty of CPU but poor throughput — what could be wrong?
1376. Kafka has plenty of disk space but poor performance — what could be wrong?
1377. Kafka has low network usage but high producer latency — what could be wrong?
1378. Kafka has high network usage but low disk usage — what could be happening?
1379. Consumer lag appears only after deployments — what could be wrong?
1380. Consumer lag appears only during peak hours — how would you investigate?
1381. ISR shrinks only during peak traffic — what would you investigate?
1382. Broker disk usage grows unexpectedly — what would you investigate?
1383. Topic size is growing despite retention — what would you investigate?
1384. Compacted topic is not shrinking — what would you investigate?
1385. Kafka Connect is RUNNING but data is not moving — what would you investigate?
1386. MirrorMaker 2 is RUNNING but target topic is not receiving data — what would you investigate?
1387. KRaft controllers are alive but metadata operations fail — how would you investigate?
1388. Kafka clients work from one subnet but not another — how would you troubleshoot?
1389. Kafka TLS works for one client but fails for another — how would you troubleshoot?
1390. Kafka authentication succeeds but authorization fails — what would you check?
1391. Kafka authorization succeeds but consumption fails — what would you check?
1392. Kafka works after restart but fails again after several hours — how would you investigate?
1393. Kafka performance slowly degrades over days — what would you investigate?
1394. Kafka brokers are healthy individually but the cluster is unstable — how would you troubleshoot?
1395. How would you troubleshoot Kafka when you have only 15 minutes before business impact becomes critical?

---

# 43. Final Senior/Architect-Level Questions

1396. Explain Kafka as if you were designing the platform for a Fortune-500 company.
1397. What are the top five Kafka production risks you would identify before going live?
1398. What Kafka architecture would you recommend for a business-critical platform and why?
1399. What Kafka configurations would you never change without a maintenance plan?
1400. What Kafka configurations are commonly misunderstood by engineers?
1401. What Kafka concepts are most important for preventing data loss?
1402. What Kafka concepts are most important for preventing duplicate processing?
1403. What Kafka concepts are most important for maintaining ordering?
1404. What Kafka concepts are most important for achieving high throughput?
1405. What Kafka concepts are most important for achieving low latency?
1406. How would you prove that a Kafka cluster is production-ready?
1407. What production readiness checklist would you use for Kafka?
1408. What disaster-recovery checklist would you use for Kafka?
1409. What security checklist would you use for Kafka?
1410. What monitoring checklist would you use for Kafka?
1411. What capacity-planning checklist would you use for Kafka?
1412. What Kafka SLOs would you define?
1413. What Kafka SLIs would you monitor?
1414. How would you define Kafka availability?
1415. How would you define Kafka durability?
1416. How would you define Kafka consumer reliability?
1417. How would you define Kafka replication health?
1418. How would you define Kafka platform health?
1419. How would you perform a Kafka architecture review?
1420. How would you challenge a Kafka architecture proposed by another engineer?
1421. When would you reject Kafka as the solution?
1422. What is the most dangerous Kafka configuration mistake you have seen?
1423. What is the most common Kafka production mistake?
1424. What is the hardest Kafka incident you would expect to troubleshoot?
1425. If you were made the Kafka platform owner tomorrow, what would you inspect first?
1426. If the interviewer gives you an unknown Kafka production issue, what systematic troubleshooting framework would you follow?
1427. How would you explain Kafka's complete architecture, failure handling, security, scaling, monitoring, and DR strategy on a whiteboard in 15 minutes?
1428. How would you defend your Kafka architecture decisions to a principal engineer or architect?
1429. How would you design a Kafka platform that can survive broker failures, AZ failures, application failures, network failures, disk failures, and regional failures?
1430. What would your complete end-to-end Kafka production architecture look like for an 8-year DevOps/SRE engineer?

[1]: https://kafka.apache.org/intro/?utm_source=chatgpt.com "Introduction | Apache Kafka"
[2]: https://kafka.apache.org/26/configuration/producer-configs/?utm_source=chatgpt.com "Producer Configs | Apache Kafka"
[3]: https://kafka.apache.org/42/operations/kraft/?utm_source=chatgpt.com "KRaft | Apache Kafka"
[4]: https://kafka.apache.org/42/security/security-overview/?utm_source=chatgpt.com "Security Overview | Apache Kafka"
[5]: https://kafka.apache.org/41/design/design/?utm_source=chatgpt.com "Design | Apache Kafka"
[6]: https://www.techprep.app/blog/kafka-interview-questions?utm_source=chatgpt.com "182 Kafka Interview Questions and Answers (2026) | TechPrep"
[7]: https://kafka.apache.org/42/operations/multi-tenancy/?utm_source=chatgpt.com "Multi-Tenancy | Apache Kafka"
[8]: https://kafka.apache.org/42/kafka-connect/user-guide/?utm_source=chatgpt.com "User Guide | Apache Kafka"
[9]: https://kafka.apache.org/42/configuration/mirrormaker-configs/?utm_source=chatgpt.com "MirrorMaker Configs | Apache Kafka"
[10]: https://kafka.apache.org/42/getting-started/upgrade/?utm_source=chatgpt.com "Upgrading | Apache Kafka"
[11]: https://kafka.apache.org/42/operations/tiered-storage/?utm_source=chatgpt.com "Tiered Storage | Apache Kafka"
