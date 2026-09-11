Yes. I analyzed **both uploaded documents**, including the 7-page PATHNEX PDF and the expanded interview notes. The material covers the Docker fundamentals, commands, networking, volumes, registry, Compose, Swarm/Kubernetes, and cleanup commands. 

But because you have **8 years of development experience**, I would **not prepare only the questions directly present in the PDF**. An interviewer will usually move from:

> **Basic → Concept → Why → How → Troubleshooting → Production → Design → Security → CI/CD → Kubernetes**

The PDF gives a good foundation, but it is **not sufficient for an 8-year-level Docker interview**.

Below is the **master Docker interview question bank** I would use.

---

# Docker Interview Master Question Bank

### For 8 Years Experience

## 0. First understand what your PDF covers

The PDF essentially gives this lifecycle:

```text
Dockerfile
    ↓
docker build
    ↓
Image
    ↓
docker run
    ↓
Container
    ↓
Network + Volume + Port
    ↓
Logs + Inspect + Exec
    ↓
Registry
    ↓
Push / Pull
    ↓
Compose / Swarm / Kubernetes
```

This same relationship is explicitly summarized in your notes. 

So interview preparation should follow exactly this flow.

---

# LEVEL 1 — Docker Fundamentals

### Must know

### 1. What is Docker?
docker is a open source and automation tools which ours application run on conatainer and easily shift and easily deploy.

### 2. Why do we use Docker?
 bocz it share host kernel resources and it is lighweight.

### 3. What problem does Docker solve?
Docker solves the “works on my machine” problem.

It packages application + dependencies + runtime into a container so it runs consistently across development, testing, and production.

👉 In short: Build once, run anywhere.

### 4. What is a container?
a running instance is container.
A container is a lightweight, isolated environment that contains an application and everything it needs to run.
### 5. Why are containers lightweight?
Containers are lightweight because they share the host OS kernel instead of running a complete guest OS like a VM.

👉 VM: App + Full OS → Heavy
👉 Container: App + Dependencies → Lightweight

Interview answer:
“Containers are lightweight because they share the host machine’s OS kernel and don't require a full operating system for each application.”

### 6. Container vs Virtual Machine?
| Container              | VM                         |
| ---------------------- | -------------------------- |
| Shares host OS kernel  | Has its own full OS        |
| Lightweight            | Heavy                      |
| Starts in seconds      | Takes longer to start      |
| Uses less CPU/RAM      | Uses more CPU/RAM          |
| Good for microservices | Good for full OS isolation |

### 7. Why does a container start faster than a VM?
A container starts faster because it doesn't need to boot a full operating system.

Container: Starts the application/process directly → seconds or less
VM: Boots a complete OS first → takes longer
### 8. What does container isolation mean?
**Container isolation** means each container runs in its **own isolated environment**, so processes, files, network, and resources are separated from other containers.

**Example:**
Container A can't normally see or interfere with Container B's files or processes.

👉 **Interview answer:** “Container isolation prevents applications running in different containers from interfering with each other.”

### 9. Do containers have their own OS?
**No, containers don't have their own full OS.**

They **share the host OS kernel**, but have their own:

* Filesystem
* Libraries/dependencies
* Processes
* Network environment

👉 **Interview line:** “Containers share the host OS kernel, unlike VMs, which have their own complete guest OS.”

### 10. Do containers share the host kernel?
yes
### 11. Can Linux containers run on Windows?
**Yes.** Linux containers can run on Windows using **WSL 2 or a lightweight Linux VM** underneath.

👉 **Simple:** Windows → Linux VM/WSL2 → Linux Container

**Interview line:** “Linux containers can run on Windows, but they need a Linux kernel, typically provided through WSL 2 or a VM.”

### 12. What makes containers portable?
Containers are **portable** because the application and its **dependencies are packaged together into a container image**.

So the same image can run on different environments that support containers.

👉 **Interview line:** “Container images package the application and its dependencies, making them portable across environments.”

### 13. What is containerization?
**Containerization** is the process of packaging an **application + its dependencies** into a **container** so it can run consistently across different environments.

👉 **Interview line:** “Containerization packages an application and its dependencies into an isolated, portable container.”

### 14. What are the advantages of Docker?
### Advantages of Docker

1. **Portable** – Run the same container anywhere.
2. **Lightweight** – Uses fewer resources than VMs.
3. **Fast startup** – Containers start quickly.
4. **Isolation** – Applications don't interfere with each other.
5. **Consistency** – Same environment in Dev, Test, and Prod.
6. **Easy deployment** – Package once and deploy easily.
7. **Scalable** – Easily create multiple container instances.
8. **Dependency management** – Application dependencies are packaged together.

👉 **Interview line:** **“Docker provides portability, consistency, isolation, fast deployment, and efficient resource utilization.”**

### 15. What are the disadvantages of Docker?
### Disadvantages of Docker

1. **Security risk** – Misconfigured containers can create security vulnerabilities.
2. **Persistent data** – Containers are temporary; data needs **volumes** or external storage.
3. **Networking complexity** – Networking becomes harder with many containers.
4. **Management complexity** – Hundreds/thousands of containers need tools like **Kubernetes**.
5. **Not a full VM** – Containers share the host kernel, so isolation isn't as strong as a VM.
6. **Debugging can be harder** – Distributed containerized applications can be difficult to troubleshoot.
7. **Image size** – Poorly built images can consume significant disk space.

👉 **Interview line:** **“Docker is lightweight and portable, but introduces challenges around security, networking, persistent storage, debugging, and managing large numbers of containers.”**

### 16. When would you NOT use Docker?
### When would you NOT use Docker?

* **Need a full OS** → Use a **VM**.
* **Very strict isolation/security requirements** → VM may be better.
* **Simple small application** → Docker may add unnecessary complexity.
* **GUI-heavy desktop applications** → Containers aren't ideal.
* **Application requires a specific kernel/OS** → Use a VM or bare metal.
* **Legacy applications** that don't work well in containers.

👉 **Interview line:** **“I wouldn't use Docker when I need a full OS, stronger isolation, specific kernel requirements, or when containerization adds more complexity than value.”**

### 17. Docker vs traditional deployment?
| Traditional Deployment            | Docker Deployment              |
| --------------------------------- | ------------------------------ |
| Install app directly on server    | Run app inside container       |
| Manually install dependencies     | Dependencies packaged in image |
| Environment differences can occur | Same environment everywhere    |
| Deployment can be slower          | Fast deployment                |
| Dependency conflicts possible     | Isolated dependencies          |
| Harder to reproduce               | Easy to reproduce              |

### 18. Docker vs VM?
yes
### 19. Docker vs bare-metal deployment?
### Docker vs Bare-Metal Deployment

| Docker                      | Bare Metal                           |
| --------------------------- | ------------------------------------ |
| App runs inside a container | App runs directly on physical server |
| Lightweight isolation       | No container isolation               |
| Easy to deploy/replace      | More manual setup                    |
| Portable                    | Less portable                        |
| Better resource sharing     | Direct hardware access               |
| Slight overhead             | Maximum performance                  |
| Easy scaling                | Scaling requires more infrastructure |

**Simple:**

`Docker → Server → Container → App`

`Bare Metal → Physical Server → App`

👉 **Interview line:** **“Docker provides portability and isolation, while bare metal provides direct hardware access and maximum performance.”**

### 20. What is immutable infrastructure?
**Immutable Infrastructure** means **you don't modify an existing server after deployment**. If you need a change, you **create a new server/container with the updated version and replace the old one**.

**Example:**

❌ Traditional:
`Server → Update application → Restart`

✅ Immutable:
`Old Container → Remove ❌`
`New Container → Deploy ✅`

👉 **Interview line:** **“Immutable infrastructure means replacing infrastructure instead of modifying it in place.”**


The PDF specifically emphasizes isolation, portability and sharing the host OS kernel. 

---

# LEVEL 2 — Image / Container / Dockerfile

### Extremely important

### 21. What is a Docker image?
read only template and immutable and blueprint/template and containing dependencies,libraries, and instructions.
### 22. What is a Docker container?
runnind instnace 
### 23. Image vs container?
u know 
### 24. Is a Docker image mutable?
no
### 25. Is a container mutable?
**Yes, a running container is mutable.**

You can change files, install packages, or modify things **inside a running container**. But these changes are usually **lost when the container is removed** unless stored in a volume or committed to a new image.

👉 **Simple:**
**Image = Immutable (read-only)**
**Container = Mutable (writable layer)**

### 26. Can multiple containers be created from one image?
yes
### 27. Can multiple containers use the same image?
yes
### 28. What happens internally when `docker run` executes?
When you run:

```bash
docker run nginx
```

Docker roughly does this:

1. **Checks for the image** `nginx` locally.
2. If not found → **pulls the image** from Docker Registry.
3. **Creates a container** from the image.
4. Adds a **writable container layer** on top of the read-only image.
5. Sets up **networking, filesystem, namespaces, and resource limits**.
6. Starts the container's **main process** (`nginx`).
7. Docker **attaches your terminal** to the container if required.

### Simple flow

```text
docker run
    ↓
Find/Pull Image
    ↓
Create Container
    ↓
Setup Isolation + Network + Filesystem
    ↓
Start Main Process
    ↓
Running Container
```

👉 **Interview line:**
**“`docker run` pulls the image if needed, creates a container from it, configures its isolation and resources, and starts its main process.”**

### 29. What happens if the image doesn't exist locally?

### 30. What is a base image?

### 31. What is a custom image?

### 32. What is Docker Hub?

### 33. What is a Docker registry?

### 34. Registry vs repository?

### 35. Image vs repository?

### 36. Tag vs image?

### 37. What is an image digest?

### 38. Tag vs digest?

### 39. Why should production deployments prefer immutable image references?

### 40. What is `latest`?

### 41. Should we use `latest` in production?

### 42. How do you version Docker images?

Your notes summarize the critical relationship as:

```text
Dockerfile → Build → Image → Run → Container
```

and describe the image as a read-only template. 

---

# LEVEL 3 — Dockerfile

### Very high probability

Your PDF contains:

```dockerfile
FROM node:14
WORKDIR /user/pathnex
COPY . .
RUN npm install
EXPOSE 3000
CMD ["npm", "start"]
```

The notes explain the purpose of each instruction. 

Interviewers can ask:

### 43. What is a Dockerfile?

### 44. What is `FROM`?

### 45. What is `WORKDIR`?

### 46. What is `COPY`?

### 47. What is `ADD`?

### 48. COPY vs ADD?

### 49. What is `RUN`?

### 50. What is `CMD`?

### 51. What is `ENTRYPOINT`?

### 52. CMD vs ENTRYPOINT?

### 53. What is `EXPOSE`?

### 54. Does `EXPOSE` actually publish a port?

### 55. `EXPOSE` vs `-p`?

### 56. What is `ENV`?

### 57. What is `ARG`?

### 58. ARG vs ENV?

### 59. What is `USER`?

### 60. What is `VOLUME`?

### 61. What is `HEALTHCHECK`?

### 62. What is `SHELL`?

### 63. What is `LABEL`?

### 64. What is `ONBUILD`?

### 65. What is `STOPSIGNAL`?

### 66. What is `MAINTAINER` and why isn't it generally used?

### 67. Which Dockerfile instructions create layers?

### 68. What is Docker build context?

### 69. What does `.` mean in `docker build -t app .`?

### 70. What is `.dockerignore`?

### 71. Why should we use `.dockerignore`?

### 72. What happens if `.dockerignore` is missing?

### 73. How do you reduce Docker image size?

### 74. How do you optimize a Dockerfile?

### 75. Why should dependencies be copied before application source?

### 76. How does Docker build cache work?

### 77. What invalidates Docker cache?

### 78. How do you debug a failed Docker build?

### 79. How do you make Docker builds reproducible?

### 80. How do you build a production-grade Dockerfile?

---

# LEVEL 4 — CMD vs ENTRYPOINT

### VERY important for your experience

Expect these.

### 81. Difference between CMD and ENTRYPOINT?

Simple:

```text
CMD        → Default command/arguments
ENTRYPOINT → Main executable
```

Example:

```dockerfile
ENTRYPOINT ["python"]
CMD ["app.py"]
```

Running:

```bash
docker run myimage
```

means:

```text
python app.py
```

Now:

```bash
docker run myimage test.py
```

becomes:

```text
python test.py
```

### Follow-up questions

### 82. Can CMD be overridden?

### 83. Can ENTRYPOINT be overridden?

### 84. What does `docker run --entrypoint` do?

### 85. Shell form vs exec form?

### 86. Why is exec form preferred?

### 87. How does signal handling differ between shell and exec form?

### 88. Why does PID 1 matter inside a container?

### 89. What happens when PID 1 doesn't handle SIGTERM correctly?

### 90. Why can an application fail to shut down gracefully inside Docker?

---

# LEVEL 5 — Docker Image Internals

### Senior-level

### 91. How is a Docker image constructed?

### 92. What are image layers?

### 93. Why does Docker use layers?

### 94. Are Docker image layers mutable?

### 95. What is a writable container layer?

### 96. What happens when a container modifies a file from an image layer?

### 97. What is copy-on-write?

### 98. Why do two containers from the same image save disk space?

### 99. What happens when you delete a file in a lower image layer?

### 100. Does deleting a file reduce image size?

### 101. What is an image manifest?

### 102. What is an image digest?

### 103. What is a multi-platform image?

### 104. How does Docker select an image for ARM vs AMD64?

### 105. What is a manifest list/index?

### 106. How do you inspect image layers?

### 107. `docker history` vs `docker inspect`?

### 108. How do you find why an image is 2 GB?

### 109. How do you reduce image size from 2 GB to 200 MB?

---

# LEVEL 6 — Multi-stage Builds

### Very likely at 8 years

### 110. What is a multi-stage Docker build?

### 111. Why do we use multi-stage builds?

### 112. How does multi-stage build reduce image size?

### 113. Build image vs runtime image?

### 114. Can you copy files from one stage to another?

### 115. How do you name build stages?

### 116. Example for Java?

### 117. Example for Node.js?

### 118. Example for Go?

### 119. Why shouldn't compilers/build tools be present in production images?

### 120. How would you containerize a Java Spring Boot application?

### 121. How would you containerize a Node.js application?

### 122. How would you containerize a React frontend?

---

# LEVEL 7 — Docker Networking

Your source explicitly covers:

```text
Bridge
Host
Overlay
None
```

with Bridge as default, Host sharing host networking, Overlay for multi-host/Swarm, and None providing no network interface. 

Interview questions:

### 123. What is Docker networking?

### 124. Why do containers need networking?

### 125. What is bridge networking?

### 126. What is host networking?

### 127. What is overlay networking?

### 128. What is none networking?

### 129. Bridge vs host?

### 130. Bridge vs overlay?

### 131. What is the default Docker network?

### 132. How do two containers communicate?

### 133. Can containers communicate using container IP?

### 134. Why shouldn't application configuration depend on container IP?

### 135. How does Docker DNS work?

### 136. Can one container resolve another by container name?

### 137. What is a user-defined bridge network?

### 138. Default bridge vs user-defined bridge?

### 139. How do you create a Docker network?

### 140. How do you connect a running container to a network?

### 141. How do you disconnect a container?

### 142. How do you inspect a Docker network?

### 143. What happens if two containers are on different networks?

### 144. Can a container belong to multiple networks?

### 145. How does container-to-container traffic work?

### 146. How does container access the internet?

### 147. How does outside traffic reach a container?

### 148. What is NAT in Docker networking?

### 149. What is port publishing?

### 150. `-p 8080:80` means what?

Remember:

```text
HOST       : CONTAINER
8080       : 80
```

The uploaded notes explicitly emphasize **left = host, right = container**. 

---

# LEVEL 8 — Networking Troubleshooting

### 151. Container cannot access internet. How troubleshoot?

### 152. Container A cannot connect to Container B. What do you check?

### 153. Container can ping IP but cannot resolve hostname. Why?

### 154. Port is exposed but application isn't reachable. Why?

### 155. `curl localhost:8080` from host fails. What do you check?

### 156. Application works inside container but not from browser. Why?

### 157. Application listens on `127.0.0.1` inside container. What's wrong?

### 158. Application listens on port 8080 but Docker maps `8080:80`. What's wrong?

### 159. Two containers use the same host port. What happens?

### 160. How do you identify which container owns a port?

### 161. How do you inspect container networking?

### 162. How do you troubleshoot DNS inside a container?

---

# LEVEL 9 — Volumes & Storage

Your PDF correctly identifies the important problem:

```text
Container removed
      ↓
Container filesystem gone
      ↓
Data can be lost
```

Volumes provide persistence. 

Questions:

### 163. Why do we need Docker volumes?

### 164. What happens to container data when container is removed?

### 165. What is a Docker volume?

### 166. Volume vs container filesystem?

### 167. What is bind mount?

### 168. Volume vs bind mount?

### 169. What is tmpfs mount?

### 170. When would you use bind mount?

### 171. When would you use named volume?

### 172. Can multiple containers share a volume?

### 173. How do you create a volume?

### 174. How do you inspect a volume?

### 175. How do you remove a volume?

### 176. What happens if a container is deleted but volume remains?

### 177. How do you backup Docker volumes?

### 178. How do you restore a Docker volume?

### 179. Why should databases use persistent storage?

### 180. Should we store database data inside the container filesystem?

---

# LEVEL 10 — Docker Compose

The source describes Compose as the tool for defining/running multi-container applications through YAML, including services, networks, relationships and volumes. 

Questions:

### 181. What is Docker Compose?

### 182. Why do we need Compose?

### 183. What is `docker-compose.yml`?

### 184. What is a service in Compose?

### 185. How do containers communicate in Compose?

### 186. How are networks created in Compose?

### 187. How are volumes defined in Compose?

### 188. How do you pass environment variables?

### 189. How do you expose ports?

### 190. How do you build an image in Compose?

### 191. `image` vs `build`?

### 192. What is `depends_on`?

### 193. Does `depends_on` mean application readiness?

### 194. How do you implement health checks?

### 195. How do you scale a Compose service?

### 196. How do you restart a Compose service?

### 197. How do you see Compose logs?

### 198. How do you enter a Compose container?

### 199. How do you rebuild Compose images?

### 200. How do you run Compose in background?

### 201. Docker Compose vs Kubernetes?

### 202. When would you use Compose instead of Kubernetes?

---

# LEVEL 11 — Registry / Docker Hub

Your source describes registry as image storage and the basic:

```text
Local → push → Registry
Registry → pull → Local
```

flow. 

Questions:

### 203. What is a Docker registry?

### 204. Docker Hub vs private registry?

### 205. Repository vs registry?

### 206. What is image tagging?

### 207. What does this mean?

```text
repo/nginx:v1
```

### 208. What is `docker tag`?

### 209. What is `docker push`?

### 210. What is `docker pull`?

### 211. What is `docker login`?

### 212. How do you push an image to a private registry?

### 213. How do you secure a private registry?

### 214. What is image immutability?

### 215. Why shouldn't we overwrite production tags?

### 216. Tag vs digest?

### 217. How would CI/CD authenticate to a registry?

### 218. What happens when `docker pull` gets denied?

### 219. How do you troubleshoot image pull failures?

---

# LEVEL 12 — Docker Engine / containerd / Runtime

Your PDF has a point that needs special attention.

It says:

> "`dockerd` is not being used nowadays... now we are using Containerd."

The expanded notes themselves warn not to overstate this as a complete replacement. 

For an interview, **do not answer "dockerd is obsolete."**

Know:

```text
Docker CLI
    ↓
Docker Engine / API
    ↓
dockerd
    ↓
containerd
    ↓
containerd-shim
    ↓
runc
    ↓
Container
```

Questions:

### 220. What is Docker Engine?

### 221. What is Docker daemon?

### 222. What is `dockerd`?

### 223. What is containerd?

### 224. What is runc?

### 225. containerd vs runc?

### 226. Docker Engine vs container runtime?

### 227. Why did Kubernetes move away from dockershim?

### 228. Does Docker require containerd?

### 229. What happens internally when `docker run` executes?

### 230. What role does OCI play?

### 231. What is an OCI image?

### 232. What is an OCI runtime?

---

# LEVEL 13 — Docker Lifecycle

### 233. Explain complete Docker lifecycle.

Strong answer:

```text
Dockerfile
    ↓
docker build
    ↓
Image
    ↓
Registry
    ↓
docker pull
    ↓
docker run
    ↓
Container
    ↓
Network / Volume
    ↓
Application
    ↓
Logs / Inspect / Exec
    ↓
Stop
    ↓
Remove
```

Your notes contain essentially this complete lifecycle. 

Follow-ups:

### 234. Difference between create and start?

### 235. What exactly does `docker run` do?

### 236. What happens when container exits?

### 237. Can a stopped container be restarted?

### 238. Can you start a removed container?

### 239. What happens when PID 1 exits?

### 240. What is container restart policy?

### 241. `restart: always` vs `unless-stopped`?

### 242. How do you automatically restart failed containers?

---

# LEVEL 14 — Docker Commands

Your source includes the basic operational commands such as `build`, `run`, `ps`, `stop`, `rm`, `pull`, and `push`. 

You should know:

### 243. `docker ps`

### 244. `docker ps -a`

### 245. `docker images`

### 246. `docker pull`

### 247. `docker push`

### 248. `docker build`

### 249. `docker run`

### 250. `docker create`

### 251. `docker start`

### 252. `docker stop`

### 253. `docker restart`

### 254. `docker kill`

### 255. `docker rm`

### 256. `docker rmi`

### 257. `docker exec`

### 258. `docker logs`

### 259. `docker inspect`

### 260. `docker stats`

### 261. `docker top`

### 262. `docker cp`

### 263. `docker rename`

### 264. `docker diff`

### 265. `docker history`

### 266. `docker info`

### 267. `docker version`

### 268. `docker events`

---

# LEVEL 15 — `docker run` Deep Questions

### 269. Explain:

```bash
docker run -d --name app -p 8080:8080 image
```

### 270. What does `-d` mean?

### 271. What does `-it` mean?

### 272. What does `--name` mean?

### 273. What does `-p` mean?

### 274. What does `-v` mean?

### 275. What does `-e` mean?

### 276. What does `--env-file` do?

### 277. What does `--restart` do?

### 278. What does `--network` do?

### 279. What does `--cpus` do?

### 280. What does `--memory` do?

### 281. What does `--read-only` do?

### 282. What does `--user` do?

### 283. What does `--rm` do?

### 284. What does `--entrypoint` do?

---

# LEVEL 16 — Troubleshooting

## VERY IMPORTANT for 8 years

This is where your interview will become senior-level.

### Scenario 1

**Container exits immediately. What will you do?**

Answer pattern:

```text
docker ps -a
      ↓
docker logs <container>
      ↓
docker inspect <container>
      ↓
check CMD / ENTRYPOINT
      ↓
check application error
```

Your notes specifically identify `logs`, `inspect`, and `exec` as the main operational tools. 

---

### 285. Container starts and immediately exits. Why?

### 286. Container is running but application isn't responding.

### 287. Container is restarting continuously.

### 288. Container is consuming 100% CPU.

### 289. Container is consuming too much memory.

### 290. Container gets OOMKilled.

### 291. Container cannot access another container.

### 292. Container cannot access internet.

### 293. Host cannot access container.

### 294. Application works locally but not inside Docker.

### 295. Application works inside Docker but fails in Kubernetes.

### 296. Image build is very slow.

### 297. Image size suddenly increased.

### 298. Docker host disk is full.

### 299. Docker daemon isn't running.

### 300. `docker ps` returns daemon connection error.

### 301. Image pull fails.

### 302. Image push fails.

### 303. Permission denied while running Docker.

### 304. Container can't write to mounted volume.

### 305. Container cannot resolve DNS.

### 306. Port already allocated.

### 307. Docker network doesn't work.

### 308. Container health check is failing.

### 309. Logs are empty.

### 310. `docker exec` doesn't work.

### 311. Container is stuck in stopping state.

### 312. Docker storage is consuming the entire disk.

---

# LEVEL 17 — Docker Security

### Missing from the PDF — MUST ADD for 8 years

### 313. How do you secure Docker containers?

### 314. Why shouldn't containers run as root?

### 315. How do you run a container as non-root?

### 316. What is Docker rootless mode?

### 317. What is a privileged container?

### 318. Why is `--privileged` dangerous?

### 319. What are Linux capabilities?

### 320. How do you drop capabilities?

### 321. What is seccomp?

### 322. What is AppArmor?

### 323. What is SELinux?

### 324. How do you scan Docker images for vulnerabilities?

### 325. Where should secrets be stored?

### 326. Should passwords be put in Dockerfile?

### 327. Why is this dangerous?

```dockerfile
ENV DB_PASSWORD=password
```

### 328. Can secrets remain in image layers?

### 329. How do you prevent secrets from entering image layers?

### 330. What is Docker Content Trust?

### 331. What is image signing?

### 332. How do you ensure only trusted images run?

### 333. How do you minimize container attack surface?

### 334. Why use minimal base images?

### 335. Alpine vs distroless?

### 336. What security checks would you add to CI/CD?

---

# LEVEL 18 — Docker Resource Management

### 337. How do you limit container CPU?

### 338. How do you limit container memory?

### 339. What happens when a container exceeds memory limit?

### 340. CPU limit vs CPU shares?

### 341. What is CPU throttling?

### 342. How do you monitor container resources?

### 343. `docker stats`?

### 344. How do you investigate high CPU?

### 345. How do you investigate high memory?

### 346. How do you identify a memory leak?

### 347. What happens when Docker host runs out of disk?

### 348. How do you clean unused Docker resources?

---

# LEVEL 19 — Docker Cleanup

Your uploaded PDF's final page is dedicated to prune operations. The notes cover system, container, image, volume, network and builder cleanup. 

Questions:

### 349. What is `docker system prune`?

### 350. What does `docker system prune -a` do?

### 351. Difference between `docker image prune` and `docker image prune -a`?

### 352. What does `docker container prune` remove?

### 353. What does `docker volume prune` remove?

### 354. What does `docker network prune` remove?

### 355. What does `docker builder prune` remove?

### 356. What is a dangling image?

### 357. What is an unused image?

### 358. Is `docker system prune -a` safe in production?

### 359. Docker disk is full. How do you safely clean it?

The notes correctly warn that `system prune -a` is more aggressive. 

---

# LEVEL 20 — Docker Logging & Monitoring

### 360. How does Docker logging work?

### 361. What is the default logging driver?

### 362. How do you view container logs?

### 363. How do you follow logs in real time?

### 364. How do you limit Docker log size?

### 365. Why can Docker logs fill disk?

### 366. What logging drivers are available?

### 367. How would you send Docker logs to centralized logging?

### 368. How do you monitor Docker containers?

### 369. What metrics would you monitor?

### 370. CPU?

### 371. Memory?

### 372. Network?

### 373. Disk?

### 374. Restart count?

### 375. Health status?

---

# LEVEL 21 — Health Checks

### 376. What is Docker HEALTHCHECK?

### 377. Why do we need health checks?

### 378. Difference between container running and application healthy?

### 379. How do you define HEALTHCHECK?

### 380. What happens when health check fails?

### 381. Does Docker automatically restart an unhealthy container?

### 382. How does health check differ from restart policy?

### 383. How would you health-check a REST API?

---

# LEVEL 22 — CI/CD + Docker

### Very important for senior developer

### 384. How do you use Docker in CI/CD?

### 385. Explain your Docker CI/CD pipeline.

### 386. Where do you build the image?

### 387. Where do you scan the image?

### 388. Where do you tag the image?

### 389. Where do you push the image?

### 390. How do you deploy the image?

### 391. How do you roll back?

### 392. How do you ensure the same image reaches production?

### 393. Why shouldn't you rebuild the image for production?

### 394. What is immutable deployment?

### 395. How do you cache Docker builds in CI?

### 396. How do you speed up Docker builds?

### 397. How do you secure registry credentials in CI?

### 398. How do you handle secrets in pipelines?

### 399. How do you implement vulnerability scanning?

### 400. What happens if vulnerability scan fails?

### 401. Would you allow a critical vulnerability into production?

### 402. How do you implement image promotion from dev → staging → prod?

---

# LEVEL 23 — Docker + Kubernetes

### MUST KNOW for modern interviews

Your source introduces Kubernetes only at a high level, describing it as a container orchestration platform for deployment, scaling and operations. 

For 8 years, interviewers can go much deeper.

### 403. Docker vs Kubernetes?

### 404. Why do we need Kubernetes if Docker already exists?

### 405. What does Kubernetes do?

### 406. What is a container runtime?

### 407. Does Kubernetes require Docker?

### 408. What is containerd?

### 409. What is CRI?

### 410. What is a Pod?

### 411. Why does Kubernetes use Pods instead of directly managing containers?

### 412. Docker container vs Kubernetes Pod?

### 413. Deployment vs container?

### 414. Service vs container networking?

### 415. How does Kubernetes pull a Docker image?

### 416. What happens when a Pod starts?

### 417. How does Kubernetes restart a failed container?

### 418. How does Kubernetes perform rolling updates?

### 419. How does Kubernetes perform rollback?

### 420. Docker Compose vs Kubernetes?

---

# LEVEL 24 — Production Design Questions

This is where an **8-year developer** should be strong.

### 421. Design Docker architecture for 20 microservices.

### 422. How would you containerize a monolith?

### 423. How would you break a monolith into containers?

### 424. How many containers should one application have?

### 425. Should one container run multiple processes?

### 426. How would you design Docker networking for microservices?

### 427. How would services discover each other?

### 428. How would you persist database data?

### 429. How would you handle secrets?

### 430. How would you implement logging?

### 431. How would you implement monitoring?

### 432. How would you implement health checks?

### 433. How would you implement zero-downtime deployment?

### 434. How would you rollback a bad image?

### 435. How would you handle image vulnerabilities?

### 436. How would you reduce Docker infrastructure cost?

### 437. How would you optimize startup time?

### 438. How would you optimize image size?

### 439. How would you handle 1000 containers?

### 440. Docker Swarm or Kubernetes for production? Why?

---

# LEVEL 25 — Scenario-Based Senior Questions

These are **very important**.

## Scenario 1

> Your Docker image is 3 GB. Production deployment is slow. What will you do?

Expected thinking:

```text
docker history
       ↓
Find large layers
       ↓
Multi-stage build
       ↓
Minimal runtime image
       ↓
.dockerignore
       ↓
Dependency optimization
       ↓
Build cache
```

---

## Scenario 2

> Container is using 100% CPU.

Ask/check:

```text
docker stats
     ↓
docker top
     ↓
application metrics
     ↓
logs
     ↓
thread/process analysis
```

---

## Scenario 3

> Container keeps restarting.

Think:

```text
docker ps -a
      ↓
docker logs
      ↓
docker inspect
      ↓
exit code
      ↓
CMD / ENTRYPOINT
      ↓
application failure
      ↓
healthcheck / restart policy
```

---

## Scenario 4

> Application works on developer laptop but not in Docker.

Possible investigation:

```text
Environment variables
Dependencies
OS libraries
File paths
Permissions
Network
Port
Architecture
Application binding address
```

---

## Scenario 5

> Docker host disk is 100% full.

What do you check?

```bash
docker system df
docker images
docker ps -a
docker volume ls
docker system prune
```

Then identify **what is actually consuming space** before deleting anything.

---

# LEVEL 26 — Tricky Interview Questions

These separate someone who has **used Docker** from someone who **understands Docker**.

### 441. Is a container a VM?

### 442. Does every container have its own kernel?

### 443. Does `docker stop` delete the container?

### 444. Does `docker rm` delete the image?

### 445. Does `docker rmi` delete containers?

### 446. Does `EXPOSE` expose a port?

### 447. Does restarting a container create a new container?

### 448. Does `docker run` create a new container every time?

### 449. Can two containers use the same image?

### 450. Can two containers use the same host port?

### 451. Can containers share a volume?

### 452. Can a stopped container retain its filesystem changes?

### 453. What happens to a container's writable layer after removal?

### 454. What happens to a named volume after container removal?

### 455. Can you change a Docker image after it is built?

### 456. Why is container IP not stable?

### 457. Why should applications not depend on container IP?

### 458. Why should secrets not be baked into images?

### 459. Why is `latest` dangerous?

### 460. Why is running as root dangerous?

---

# LEVEL 27 — Commands You Should Be Able to Write Without Thinking

The PDF's practical section includes installation, pulling, running, stopping, starting, building, tagging, pushing, inspecting, logs, volumes, ports and exec. 

You should be comfortable writing:

```bash
docker build -t myapp:v1 .
```

```bash
docker run -d --name myapp -p 8080:8080 myapp:v1
```

```bash
docker ps
```

```bash
docker ps -a
```

```bash
docker logs myapp
```

```bash
docker logs -f myapp
```

```bash
docker exec -it myapp /bin/bash
```

```bash
docker inspect myapp
```

```bash
docker stats
```

```bash
docker stop myapp
```

```bash
docker start myapp
```

```bash
docker restart myapp
```

```bash
docker rm myapp
```

```bash
docker rmi myapp:v1
```

```bash
docker tag myapp:v1 repo/myapp:v1
```

```bash
docker push repo/myapp:v1
```

```bash
docker pull repo/myapp:v1
```

```bash
docker network ls
```

```bash
docker network inspect mynetwork
```

```bash
docker volume ls
```

```bash
docker volume inspect myvolume
```

---

# The Most Important 30 Questions

If the interviewer gives you only 30–40 minutes, **these are the questions I'd prioritize**:

1. What is Docker?
2. Why Docker?
3. Container vs VM?
4. How does Docker provide isolation?
5. Image vs container?
6. Dockerfile vs image vs container?
7. Explain `docker run`.
8. What happens internally during `docker run`?
9. Explain Dockerfile instructions.
10. `RUN` vs `CMD`.
11. `CMD` vs `ENTRYPOINT`.
12. `COPY` vs `ADD`.
13. `ARG` vs `ENV`.
14. What is Docker build context?
15. What is `.dockerignore`?
16. What are Docker image layers?
17. How does Docker caching work?
18. How do you reduce image size?
19. What is a multi-stage build?
20. Explain Docker networking.
21. Bridge vs host vs overlay.
22. How do containers communicate?
23. What does `-p 8080:80` mean?
24. Volume vs bind mount.
25. How do you persist database data?
26. What is Docker Compose?
27. Docker Compose vs Kubernetes.
28. What is containerd?
29. How do you troubleshoot a container that keeps restarting?
30. How do you troubleshoot a container with high CPU/memory?
31. How do you secure a Docker container?
32. Why shouldn't containers run as root?
33. How do you handle secrets?
34. How do you scan images?
35. Explain Docker CI/CD pipeline.
36. How do you achieve zero-downtime deployment?
37. How do you rollback?
38. How do you troubleshoot a full Docker disk?
39. Docker Swarm vs Kubernetes.
40. Design a production Docker architecture.

---

# ⚠️ Important Analysis of Your PDF

Your PDF is **good for beginner → intermediate Docker**, but there are some things you should **not stop at** if you're interviewing with 8 years experience.

### PDF covers well

```text
Docker
Containers
Images
Dockerfile
Engine
Compose
Registry
Networking
Volumes
Swarm
Kubernetes introduction
Commands
Port mapping
Volume mapping
Logs
Inspect
Exec
Cleanup
```

This matches the source coverage list in the expanded notes. 

### PDF does NOT go deep enough into

```text
❌ CMD vs ENTRYPOINT
❌ COPY vs ADD
❌ ARG vs ENV
❌ Multi-stage builds
❌ BuildKit
❌ Docker layer internals
❌ Build cache optimization
❌ .dockerignore
❌ Container PID 1
❌ Signal handling
❌ HEALTHCHECK
❌ Resource limits
❌ OOM
❌ Docker security
❌ Rootless containers
❌ Linux capabilities
❌ seccomp
❌ Image vulnerability scanning
❌ Secrets management
❌ Advanced networking
❌ DNS
❌ iptables/NAT
❌ Logging drivers
❌ Production monitoring
❌ CI/CD image promotion
❌ Immutable images
❌ containerd/runc/OCI internals
❌ Advanced troubleshooting
❌ Production architecture
```

**These are exactly the areas I'd add for an 8-year profile.**

---

# One Important Correction in Your Notes

Your source says:

> `dockerd` is not being used nowadays and Containerd is now being used.

Don't say this blindly in an interview.

A better answer is:

> **"Docker Engine uses dockerd as its daemon, and containerd is used underneath for container lifecycle management. Kubernetes itself no longer requires Docker Engine; it uses a CRI-compatible runtime such as containerd or CRI-O."**

Your own expanded notes actually flag this point and say not to treat containerd as a complete replacement for the Docker Engine architecture. 

That distinction can matter in a senior interview.

---

# Your 8-Year Interview Preparation Strategy

Don't memorize 460 answers individually.

Use this pattern:

```text
WHAT?
   ↓
WHY?
   ↓
HOW?
   ↓
INTERNAL WORKING?
   ↓
PROBLEM?
   ↓
TROUBLESHOOT?
   ↓
PRODUCTION?
   ↓
SECURITY?
   ↓
DESIGN?
```

For example:

### Topic = Docker Volume

Don't only learn:

> "Volume provides persistent storage."

Learn:

```text
What is volume?
       ↓
Why volume?
       ↓
Volume vs bind mount?
       ↓
How does Docker mount it?
       ↓
What happens if container dies?
       ↓
How do I backup it?
       ↓
What if permission denied?
       ↓
How do I monitor storage?
       ↓
How would I use it for DB?
       ↓
What would I use in Kubernetes?
```

That's the **8-year-level thinking pattern**.

Your source itself gives the core memory model:

> Dockerfile builds the image → image creates the container → container runs the application → network connects it → volume preserves data → registry stores the image → orchestration manages multiple containers. 

### Best way to prepare

I would divide your Docker preparation into **8 interview rounds**:

```text
ROUND 1 → Docker Fundamentals
ROUND 2 → Dockerfile + Images
ROUND 3 → Networking + Volumes
ROUND 4 → Commands + Troubleshooting
ROUND 5 → Compose + Registry
ROUND 6 → Security + Performance
ROUND 7 → Docker + Kubernetes + CI/CD
ROUND 8 → Production Scenarios + Architecture
```

**For your 8-year profile, Round 4–8 are more important than simply memorizing the basic definitions.**
