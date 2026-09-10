Yes. For an **8-year developer**, I would not prepare Docker as isolated questions. Interviewers often start with a Docker problem and then move into **Linux, networking, CI/CD, Kubernetes, AWS, security, observability, Git, databases, and system design**.

Your uploaded material gives the core chain:

**Dockerfile → Build → Image → Registry → Run → Container → Network/Port/Volume → Logs/Inspect/Exec → Stop/Start/Remove → Cleanup → Compose/Orchestration/CI-CD**. 

The original PDF specifically covers Docker Engine, Compose, registry, bridge/host/overlay/none networking, volumes, Swarm/Kubernetes, commands and cleanup. 

I also cross-checked the current Docker documentation for daemon troubleshooting, networking/DNS, resource limits, logging, security, Compose, BuildKit and multi-platform builds. Docker's own troubleshooting guide specifically includes daemon connectivity, OOM, kernel/cgroup issues, IP forwarding, DNS and volume problems. ([Docker Docs][1])

# 🔥 MASTER DOCKER SCENARIO + TROUBLESHOOTING INTERVIEW BANK

**Legend**

* 🔴 = very important for 8 years
* ⭐ = frequently asked
* 🧠 = tricky interviewer question
* 🛠️ = practical/live troubleshooting
* `[K8s: ...]` = same concept exists in Kubernetes
* `[Linux: ...]` = Linux connection
* `[AWS: ...]` = AWS connection
* `[CI/CD: ...]` = CI/CD connection
* `[Network: ...]` = networking connection
* `[Security: ...]` = security connection
* `[Git: ...]` = Git connection
* `[DB: ...]` = database connection
* `[Observability: ...]` = monitoring/logging connection

---

# 1. CONTAINER IS RUNNING BUT APPLICATION IS NOT WORKING

### 🔴 1

Container shows:

```text
Up 2 minutes
```

but browser cannot access application.

**How do you troubleshoot?**

`[K8s: Pod Running but application unavailable] [Network]`

### 🔴 2

Container is running but:

```bash
curl localhost:8080
```

fails.

What do you check first?

`[Network]`

### 🔴 3

Application works inside container but not from host.

What could be wrong?

`[Network: port publishing]`

### 🔴 4

Application works with:

```bash
docker exec -it app sh
curl localhost:8080
```

but:

```bash
curl localhost:8080
```

from host fails.

Explain the complete reason.

### 🔴 5

You started:

```bash
docker run -d nginx
```

Why can't you access it from:

```text
http://localhost
```

?

### 🔴 6

You start:

```bash
docker run -d -p 8080:80 nginx
```

Explain exactly:

```text
Host 8080
      ↓
Container 80
      ↓
Nginx
```

### 7

Container listens on port 3000 but you mapped:

```bash
-p 8080:80
```

What happens?

### 8

Application listens only on:

```text
127.0.0.1:8080
```

inside container.

Will `-p 8080:8080` necessarily make it accessible?

Why?

`[Network]`

### 9

Application listens on:

```text
0.0.0.0:8080
```

Why is this generally different?

---

# 2. CONTAINER IMMEDIATELY EXITS

### 🔴 10

You run:

```bash
docker run myapp
```

Container immediately exits.

What commands do you run?

Expected investigation:

```bash
docker ps -a
docker logs <container>
docker inspect <container>
```

`[K8s: CrashLoopBackOff]`

### 🔴 11

Container status is:

```text
Exited (1)
```

What does exit code 1 tell you?

### 🔴 12

Container status:

```text
Exited (0)
```

but interviewer says "application isn't running."

What's your explanation?

### 🔴 13

Container exits immediately even though Dockerfile has:

```dockerfile
CMD ["npm", "start"]
```

What could be wrong?

### 🔴 14

Your Dockerfile has:

```dockerfile
CMD ["npm", "start"]
```

but container exits.

How do you prove whether the issue is Docker or the application?

### 15

Container starts manually using:

```bash
docker run -it image sh
```

but exits when run normally.

Why?

### 🔴 16

Application needs environment variable:

```text
DATABASE_URL
```

Container exits because it is missing.

How do you diagnose?

`[12-factor] [K8s: ConfigMap/Secret]`

### 17

Container starts locally but exits in CI.

What differences do you investigate?

`[CI/CD]`

---

# 3. RESTART LOOP

### 🔴 18

Container keeps restarting every few seconds.

How do you troubleshoot?

`[K8s: CrashLoopBackOff]`

### 🔴 19

You configured:

```bash
--restart=always
```

and now debugging becomes difficult.

Why?

### 20

Container is repeatedly restarting because application exits with code 1.

Would changing Docker restart policy solve the root cause?

### 🔴 21

How do you determine whether restart is caused by:

* application crash
* OOM
* health check
* Docker daemon
* host reboot?

`[K8s: restartPolicy]`

### 22

Container was stable for 2 hours and suddenly enters restart loop.

What changed?

### 23

How would you distinguish:

```text
Application crash
vs
OOM kill
vs
manual restart
```

?

---

# 4. OOM / MEMORY PROBLEMS

Docker officially supports memory limits and CPU constraints, and an unrestricted container can consume host resources until the host itself becomes unstable. ([Docker Docs][2])

### 🔴 24

Container suddenly dies.

Logs show nothing useful.

How do you check whether it was OOM killed?

`[Linux: OOM Killer] [K8s: OOMKilled]`

### 🔴 25

Container uses 100% memory.

What commands do you run?

```bash
docker stats
docker inspect
```

What else would you check on Linux?

`[Linux: free/top/ps/cgroups]`

### 🔴 26

You configured:

```bash
--memory=512m
```

Application requires 700 MB.

What happens?

### 🔴 27

Host has 16 GB RAM but container is configured with:

```text
--memory=512m
```

Why can't it consume all host memory?

### 🔴 28

Five containers together consume almost all RAM.

How do you find which container is responsible?

### 🔴 29

Docker host itself becomes slow when one container consumes huge memory.

Explain the relationship.

### 30

How would you set memory limits for:

* Java
* Node.js
* Python

applications?

`[JVM] [Linux]`

### 🔴 31

Java container has:

```text
-Xmx2g
```

but Docker memory limit is:

```text
1g
```

What problem can happen?

`[Java/JVM]`

### 32

Container's memory usage keeps increasing.

How do you determine:

```text
Docker problem
vs
application memory leak
```

?

`[Observability]`

---

# 5. CPU PROBLEMS

### 🔴 33

One container is consuming 100% CPU.

How do you identify it?

### 🔴 34

How do you limit CPU?

```bash
--cpus
```

What does it actually control?

### 35

Application became slower after setting:

```bash
--cpus=0.5
```

Why?

### 36

CPU is 100%, but application throughput is low.

What would you investigate?

`[Linux: CPU saturation] [Observability]`

### 37

One container is starving other containers.

How would you design resource limits?

`[K8s: requests/limits]`

---

# 6. PORT CONFLICT

### 🔴 38

You execute:

```bash
docker run -p 8080:80 nginx
```

and get:

```text
port is already allocated
```

How do you troubleshoot?

`[Network]`

### 🔴 39

How do you find which container is already using port 8080?

### 40

How do you find which Linux process owns port 8080?

```bash
ss -lntp
```

`[Linux: networking]`

### 41

Two applications both require host port 8080.

How would you solve it?

### 42

Can two containers listen on port 8080 internally?

Can both publish it as host port 8080?

Explain.

---

# 7. DNS PROBLEMS

Docker's networking documentation explicitly covers container DNS and network connectivity. ([Docker Docs][3])

### 🔴 43

Container can access:

```text
8.8.8.8
```

but cannot access:

```text
google.com
```

What's likely wrong?

`[Network: DNS] [K8s: CoreDNS]`

### 🔴 44

Container A cannot resolve Container B by name.

What do you check?

### 🔴 45

Two containers are running but:

```bash
ping backend
```

fails.

What are your steps?

### 🔴 46

Why does communication work on a user-defined Docker network but behave differently on the default bridge?

### 🔴 47

Container can resolve DNS but cannot connect to the resolved IP.

What does that tell you?

`[Network: DNS vs TCP]`

### 48

How would you troubleshoot:

```text
DNS failure
vs
routing failure
vs
port failure
vs
application failure
```

?

### 🔴 49

Container DNS works on one server but not another.

What host-level configuration do you investigate?

`[Linux] [DNS]`

---

# 8. CONTAINER-TO-CONTAINER COMMUNICATION

### 🔴 50

You have:

```text
frontend
backend
database
```

How should they communicate?

### 🔴 51

Frontend cannot connect to backend using:

```text
backend:8080
```

What do you check?

### 🔴 52

Containers are on different Docker networks.

Can they communicate?

How would you connect them?

### 53

Can one container belong to multiple Docker networks?

Why would you do it?

### 🔴 54

Backend can reach database but frontend cannot reach backend.

How do you isolate the problem?

### 55

Database container is listening on 5432.

Does backend need:

```yaml
ports:
  - "5432:5432"
```

to communicate with it?

**Very common trick question.**

`[K8s: Service]`

---

# 9. HOST NETWORKING

### 56

What happens when:

```bash
docker run --network host nginx
```

?

### 57

Application behaves differently under:

```text
bridge
vs
host
```

networking.

How would you investigate?

### 58

Why can host networking create port conflicts?

### 59

When would you deliberately use host networking?

### 60

Why is host networking a security consideration?

`[Security]`

---

# 10. NONE NETWORK

### 61

Container has no network connectivity.

You discover:

```bash
--network none
```

What does it mean?

### 62

When would you intentionally use a container with no network?

`[Security]`

---

# 11. OVERLAY / MULTI-HOST

The supplied PDF associates Overlay networking with multi-host Swarm networking. 

### 🔴 63

Container A is on Docker host 1 and Container B is on Docker host 2.

How can they communicate?

`[Swarm] [Network]`

### 64

Why doesn't a normal local bridge network solve multi-host communication?

### 65

Overlay network exists but services cannot communicate.

What do you troubleshoot?

### 66

What host-level network/firewall issues could break overlay networking?

`[Linux: firewall] [Network]`

---

# 12. DOCKERFILE BUILD FAILURES

### 🔴 67

Build fails at:

```dockerfile
RUN npm install
```

What do you check?

### 68

Build cannot download packages.

Application runtime network works.

What is different?

`[Network] [Proxy] [CI/CD]`

### 69

Build works on developer laptop but fails in Jenkins.

What do you compare?

### 🔴 70

Build says:

```text
COPY failed
```

What are possible reasons?

### 71

Dockerfile is in:

```text
docker/Dockerfile
```

but source code is in parent directory.

Why can `COPY ../` fail?

`[Build Context]`

### 🔴 72

A developer says:

> "Docker can't see my source code."

What is your first question?

### 🔴 73

What is Docker build context?

### 74

Why can a huge build context make builds slow?

---

# 13. DOCKER BUILD CACHE

Docker's current documentation explains that Dockerfile instructions form layers and when a layer changes, downstream layers may need rebuilding. ([Docker Docs][4])

### 🔴 75

This Dockerfile is slow:

```dockerfile
COPY . .
RUN npm install
```

How would you optimize it?

### 🔴 76

Why is this usually better?

```dockerfile
COPY package*.json .
RUN npm install
COPY . .
```

### 🔴 77

Developer changes one source file.

Why does `npm install` suddenly execute again in a badly ordered Dockerfile?

### 78

How would you identify which Docker layer invalidated the cache?

### 🔴 79

Build takes 15 minutes after every small code change.

How do you troubleshoot?

### 80

`docker build --no-cache` makes the build work.

What does that tell you?

### 🧠 81

Can Docker cache cause a **wrong application version** to appear in an image?

How would you prove it?

---

# 14. MULTI-STAGE BUILD

### 🔴 82

Your Node application image is 1.2 GB.

How would you reduce it?

### 🔴 83

Build requires:

```text
gcc
make
npm
```

but runtime doesn't.

How do you design Dockerfile?

### 84

Why shouldn't build tools necessarily be present in production image?

`[Security]`

### 🔴 85

Write a multi-stage Dockerfile for:

```text
React → Nginx
```

### 🔴 86

Write a multi-stage Dockerfile for:

```text
Go application
```

### 🔴 87

Write a multi-stage Dockerfile for:

```text
Java/Spring Boot
```

### 88

Build stage succeeds but runtime stage cannot find binary.

How do you debug `COPY --from`?

### 89

Why does a multi-stage build improve security?

---

# 15. IMAGE SIZE

### 🔴 90

Image is 2 GB.

How do you find what's consuming space?

```bash
docker history image
docker system df
```

### 91

How do you determine which layer is huge?

### 92

Why is this bad?

```dockerfile
RUN apt-get update
RUN apt-get install ...
```

versus combining related operations appropriately?

### 93

Why doesn't deleting a large file in a later layer necessarily reduce image size as expected?

`[Filesystem layers]`

### 🔴 94

How would you reduce an image without changing application behavior?

---

# 16. IMAGE SECURITY / VULNERABILITY

### 🔴 95

Security scan reports 200 CVEs.

Does that automatically mean your application is vulnerable?

### 96

How do you determine whether a CVE comes from:

```text
application dependency
vs
OS package
vs
base image
```

`[Security] [Supply Chain]`

### 🔴 97

Production image contains:

```text
curl
bash
gcc
git
```

Would you remove them?

Why?

### 98

Why use a minimal/distroless runtime image?

### 99

What are the disadvantages of extremely minimal images?

### 100

Production container has no shell.

How do you troubleshoot it?

`[Observability]`

Current Docker documentation also highlights debugging challenges with minimal hardened images where shells/package managers may intentionally be absent. ([Docker Docs][5])

---

# 17. SECRETS

### 🔴 101

Developer puts:

```dockerfile
ENV DB_PASSWORD=secret123
```

What's wrong?

`[Security] [CI/CD]`

### 🔴 102

Developer puts secret in:

```dockerfile
RUN echo $TOKEN
```

Can it leak into build history/layers?

How would you redesign?

### 🔴 103

Application requires AWS credentials.

Would you bake them into the image?

**No. Explain why.**

`[AWS IAM] [Security]`

### 🔴 104

How should runtime secrets be injected?

### 🔴 105

How should build-time secrets be handled?

Current BuildKit/buildx supports build secrets rather than requiring credentials to be baked into image layers. ([Docker Docs][6])

---

# 18. ARG vs ENV

### 🔴 106

What's the difference between:

```dockerfile
ARG VERSION
ENV VERSION=$VERSION
```

?

### 107

Which one exists during build?

### 108

Which one is available at runtime?

### 109

Can `ARG` safely be used for passwords?

### 🧠 110

Why can build arguments still be a bad place for secrets?

---

# 19. CMD vs ENTRYPOINT

### 🔴 111

Dockerfile:

```dockerfile
ENTRYPOINT ["java","-jar","app.jar"]
CMD ["--server.port=8080"]
```

What happens?

### 🔴 112

Run:

```bash
docker run image --server.port=9090
```

What changes?

### 113

Difference between:

```dockerfile
CMD ["npm","start"]
```

and:

```dockerfile
ENTRYPOINT ["npm","start"]
```

### 🔴 114

Why can ENTRYPOINT cause debugging problems?

### 115

How would you override ENTRYPOINT?

### 116

Shell form vs exec form.

Why does it matter?

`[Linux: PID 1 / signals]`

---

# 20. PID 1 / GRACEFUL SHUTDOWN

### 🔴 117

Application doesn't shut down gracefully when Docker stops it.

What do you investigate?

`[Linux: signals] [K8s: termination]`

### 🔴 118

Why is PID 1 special inside a container?

### 119

Application doesn't receive SIGTERM.

What could be wrong?

### 120

What happens if your Dockerfile uses:

```dockerfile
CMD npm start
```

instead of exec form?

### 🔴 121

How would you ensure graceful shutdown for:

* Node
* Java
* Python
* Go

applications?

### 122

Why might you use an init process such as `tini`?

`[Linux] [K8s]`

---

# 21. HEALTHCHECK

### 🔴 123

Container status is:

```text
Up
```

but application is actually broken.

Why?

### 🔴 124

What's the difference between:

```text
running
healthy
unhealthy
```

?

### 125

Write a Docker `HEALTHCHECK`.

### 🔴 126

Healthcheck keeps failing but application works manually.

How do you debug?

### 127

Should healthcheck use:

```text
ping
```

or actual application endpoint?

Why?

### 128

Healthcheck itself consumes significant CPU.

What would you change?

### 🔴 129

Does `HEALTHCHECK` automatically restart a container?

**Very important trick question.**

---

# 22. DOCKER COMPOSE SCENARIOS

The current Compose documentation specifically covers startup order, healthchecks, dependencies, volumes, debugging and profiles. ([Docker Docs][7])

### 🔴 130

You have:

```text
frontend
backend
postgres
redis
```

Design `compose.yaml`.

### 🔴 131

Backend starts before Postgres is ready.

Application crashes.

How do you fix it?

`[K8s: readinessProbe/initContainer]`

### 🔴 132

Why is:

```yaml
depends_on:
  - db
```

not always enough?

### 🔴 133

How would you use:

```yaml
condition: service_healthy
```

?

### 🔴 134

Compose services can resolve each other by what name?

### 🔴 135

Backend cannot connect to Postgres.

What commands do you run?

```bash
docker compose ps
docker compose logs
docker compose exec
docker network inspect
```

### 136

Frontend needs backend but backend isn't externally exposed.

Can frontend still connect?

### 🔴 137

Why don't you necessarily publish database ports to the host?

### 138

How do you expose only frontend to host while keeping backend/database internal?

### 🔴 139

How do you persist PostgreSQL data in Compose?

### 140

`docker compose down` was executed.

Database data disappeared.

Why?

### 🔴 141

How do you make database data survive Compose recreation?

### 142

Difference:

```bash
docker compose stop
docker compose down
```

### 143

Difference:

```bash
docker compose down
docker compose down -v
```

### 🔴 144

Developer says:

> "I changed environment variable but container still has old value."

What do you investigate?

---

# 23. COMPOSE ENVIRONMENT PROBLEMS

### 145

`.env` contains:

```text
DB_HOST=postgres
```

but application gets:

```text
DB_HOST=localhost
```

Why?

### 🔴 146

Why is `localhost` inside a container often misunderstood?

`[Network] [K8s: localhost]`

### 147

Backend uses:

```text
localhost:5432
```

to connect to Postgres.

Postgres is another container.

Why does it fail?

### 🔴 148

How do you fix it?

---

# 24. VOLUME / DATA LOSS

Your supplied document explicitly emphasizes that container data is ephemeral and volumes provide persistence across restarts/removal. 

### 🔴 149

PostgreSQL container was deleted.

All data disappeared.

Why?

### 🔴 150

How do you prevent this?

### 🔴 151

Difference:

```text
named volume
bind mount
tmpfs
```

### 152

When would you use bind mount?

### 153

When would you use named volume?

### 154

Application gets:

```text
Permission denied
```

on mounted volume.

How do you troubleshoot?

`[Linux: UID/GID]`

### 🔴 155

Host user is UID 1000.

Container process is UID 1001.

Volume permissions fail.

How do you solve it?

### 156

Container runs as root and creates files owned by root on host.

How do you prevent this?

`[Security] [Linux]`

---

# 25. VOLUME BACKUP / RESTORE

### 🔴 157

How do you backup a Docker volume?

### 🔴 158

How do you restore it?

### 159

How do you migrate a volume from one Docker host to another?

### 160

How would you backup production database data from a container?

`[DB: pg_dump/mysqldump]`

### 🔴 161

Why isn't copying `/var/lib/docker/volumes/...` always the best application-level backup strategy?

---

# 26. DISK FULL

### 🔴 162

Docker host disk reaches 100%.

Application starts failing.

What do you check?

`[Linux: df/du]`

### 🔴 163

How do you determine whether disk usage is from:

```text
images
containers
volumes
logs
build cache
```

?

### 🔴 164

What does:

```bash
docker system df
```

help you determine?

### 🔴 165

How would you safely clean unused Docker resources?

### 🧠 166

Would you blindly run:

```bash
docker system prune -a --volumes
```

in production?

Why not?

---

# 27. LOGGING

Docker captures container stdout/stderr using its logging system; the default `json-file` driver can consume significant disk space if log rotation isn't configured. ([Docker Docs][8])

### 🔴 167

Application logs are not visible using:

```bash
docker logs
```

What do you check?

### 168

Application writes logs to:

```text
/app/logs/app.log
```

instead of stdout.

What issue can that create?

### 🔴 169

Docker host disk keeps filling because of container logs.

How do you solve it?

### 🔴 170

How do you configure log rotation?

### 171

What happens if log rotation is not configured?

### 🔴 172

Which logging driver is being used?

How do you determine it?

### 173

How would you ship Docker logs to:

```text
CloudWatch
ELK
Splunk
Fluentd
```

?

`[AWS] [Observability]`

### 174

Container generates millions of logs per minute.

What architectural changes would you make?

---

# 28. DOCKER DAEMON

### 🔴 175

You execute:

```bash
docker ps
```

and get:

```text
Cannot connect to the Docker daemon
```

How do you troubleshoot?

`[Linux: systemd]`

### 🔴 176

What do you check?

```bash
systemctl status docker
journalctl -u docker
docker info
```

### 🔴 177

Docker daemon is running but CLI still cannot connect.

What else?

### 178

How does Docker CLI communicate with Docker daemon?

### 179

What is Docker socket?

### 🔴 180

Why is:

```text
/var/run/docker.sock
```

security-sensitive?

`[Security] [Linux]`

---

# 29. DOCKER ENGINE INTERNALS

The official Docker Engine documentation describes Docker Engine as a client-server architecture involving `dockerd`, API and CLI. ([Docker Docs][9])

### 🔴 181

Explain:

```text
docker CLI
   ↓
Docker API
   ↓
dockerd
   ↓
containerd
   ↓
runc
   ↓
container
```

### 🔴 182

What does `dockerd` do?

### 183

What does containerd do?

### 184

What does runc do?

### 185

What is OCI?

### 🔴 186

Why did Kubernetes move away from requiring Docker Engine as its container runtime?

`[K8s: CRI]`

### 🧠 187

Interviewer says:

> "dockerd is obsolete."

How do you respond accurately?

---

# 30. CONTAINER RUNTIME

### 🔴 188

What is a container runtime?

### 189

Difference:

```text
Docker Engine
containerd
CRI-O
runc
```

### 🔴 190

Why can Kubernetes run containers without Docker Engine?

### 191

What is CRI?

`[K8s]`

### 192

What happens from:

```bash
kubectl run
```

to actual container creation?

`[K8s: control plane → kubelet → CRI → runtime]`

---

# 31. DOCKER NETWORK TROUBLESHOOTING DEEP DIVE

### 🔴 193

Container cannot access internet.

Give your exact troubleshooting sequence.

### 194

What commands would you use inside container?

```bash
ip addr
ip route
cat /etc/resolv.conf
curl
wget
nc
```

`[Linux: networking]`

### 🔴 195

Container has IP but no default route.

What does that indicate?

### 196

Container has route but DNS fails.

What layer is broken?

### 197

DNS resolves correctly but TCP connection fails.

What layer is broken?

### 198

TCP connection works but HTTP returns 500.

Is this a Docker network issue?

Why not necessarily?

### 🔴 199

How do you distinguish:

```text
Layer 3 problem
Layer 4 problem
Layer 7 problem
```

?

`[Network]`

---

# 32. NETWORK PACKET FLOW

### 🔴 200

Explain packet flow:

```text
Browser
 ↓
Host port
 ↓
Docker NAT
 ↓
Container IP
 ↓
Application
```

### 🔴 201

What happens when container connects to internet?

### 202

What is NAT doing in Docker networking?

`[Linux: iptables/nftables]`

### 203

What is bridge interface?

### 204

What is `docker0`?

### 205

What is veth pair?

`[Linux networking]`

### 🔴 206

Explain:

```text
Container namespace
        ↓
veth pair
        ↓
Docker bridge
        ↓
Host network
```

---

# 33. KUBERNETES CONNECTION QUESTIONS

This is **very important for your interview** because Docker troubleshooting maps strongly to Kubernetes.

### 🔴 207

Docker container exits.

What is the equivalent Kubernetes problem?

`[K8s: CrashLoopBackOff]`

### 🔴 208

Docker container is running but application unavailable.

Equivalent K8s problems?

`[K8s: Service / Ingress / readinessProbe]`

### 🔴 209

Docker container has wrong environment variable.

Kubernetes equivalent?

`[K8s: ConfigMap/Secret]`

### 🔴 210

Docker volume permission problem.

Kubernetes equivalent?

`[K8s: PV/PVC/securityContext/fsGroup]`

### 🔴 211

Docker container consumes too much memory.

Kubernetes equivalent?

`[K8s: resources.limits / OOMKilled]`

### 🔴 212

Docker application takes 60 seconds to start.

Kubernetes equivalent?

`[K8s: startupProbe/readinessProbe]`

### 🔴 213

Docker container listens on 8080.

How does this map to:

```text
containerPort
Service port
targetPort
Ingress
```

?

### 🔴 214

Docker Compose service discovery:

```text
backend:8080
```

What is the Kubernetes equivalent?

`[K8s: Service DNS]`

### 🔴 215

Docker network isolates services.

What is the Kubernetes equivalent?

`[K8s: NetworkPolicy]`

### 🔴 216

Docker restart policy vs Kubernetes restart behavior.

Compare them.

### 🔴 217

Docker healthcheck vs Kubernetes:

```text
livenessProbe
readinessProbe
startupProbe
```

### 🔴 218

Docker image tag changes.

How does Kubernetes decide which image to run?

### 219

Docker image exists locally but Kubernetes node can't run it.

What do you check?

`[K8s: imagePullSecrets/registry]`

---

# 34. DOCKER + CI/CD

### 🔴 220

Pipeline:

```text
Git push
 ↓
Build image
 ↓
Test
 ↓
Scan
 ↓
Push registry
 ↓
Deploy
```

Design it.

`[CI/CD]`

### 🔴 221

Build succeeds locally but fails in Jenkins.

What do you compare?

### 222

Docker image builds successfully but deployment fails.

Where can the problem be?

### 223

Image builds successfully but application crashes only in production.

What environment differences do you investigate?

### 🔴 224

How would you tag images?

Bad:

```text
latest
```

Better?

```text
1.2.3
commit-SHA
build-number
```

### 🔴 225

Why should production deployment use immutable image references?

`[DevOps]`

### 🔴 226

Deployment accidentally uses wrong image version.

How do you rollback?

`[K8s: Deployment rollback]`

### 🔴 227

How would you implement:

```text
build once
promote same image
dev → QA → staging → prod
```

?

### 🔴 228

Why shouldn't you rebuild the image separately for production?

---

# 35. REGISTRY PROBLEMS

The source explicitly covers registry push/pull and private registries. 

### 🔴 229

`docker push` fails with:

```text
denied
```

What do you check?

### 230

`docker pull` fails:

```text
unauthorized
```

Troubleshoot.

### 🔴 231

Image works locally but deployment server cannot pull it.

What do you check?

### 232

Private registry is accessible from laptop but not CI runner.

What could differ?

`[Network] [CI/CD]`

### 🔴 233

How do you authenticate a CI pipeline to registry securely?

### 234

Why should you avoid storing registry passwords directly in pipeline YAML?

`[Security]`

---

# 36. IMAGE TAG / DIGEST

### 🔴 235

What happens if you deploy:

```text
myapp:latest
```

and later someone pushes another image with same tag?

### 🔴 236

Difference:

```text
tag
digest
image ID
```

### 🔴 237

Why is digest-based deployment useful?

### 238

Two environments use:

```text
myapp:1.0
```

but apparently run different image contents.

How can this happen?

### 🔴 239

How would you prove two environments run exactly the same image?

---

# 37. DOCKER SAVE / LOAD / EXPORT / IMPORT

### 240

How do you move an image to a machine with no registry access?

### 241

Difference:

```bash
docker save
docker export
```

### 242

Difference:

```bash
docker load
docker import
```

### 243

When would you use `docker save`?

### 244

When would you use `docker export`?

### 🧠 245

Why does `docker export` not preserve the same image layer/history semantics?

---

# 38. CONTAINER FORENSICS

### 🔴 246

Container died 10 minutes ago.

How do you investigate?

### 247

Which commands give you:

```text
logs
environment
mounts
network
exit code
restart count
image
IP
```

?

### 248

What does:

```bash
docker inspect
```

give you that `docker ps` doesn't?

### 249

What is:

```bash
docker diff
```

useful for?

### 250

How can `docker diff` help diagnose an application changing files unexpectedly?

---

# 39. `docker exec` TROUBLESHOOTING

### 🔴 251

You execute:

```bash
docker exec -it app /bin/bash
```

and get:

```text
executable file not found
```

What does it mean?

### 252

Image has no Bash.

How do you troubleshoot?

```bash
docker exec -it app /bin/sh
```

### 253

Image has neither Bash nor Sh.

What options do you have?

### 254

Container is stopped.

Can you use `docker exec`?

Why not?

### 255

What is the difference between:

```bash
docker exec
docker attach
```

?

---

# 40. PRODUCTION SECURITY

Docker security involves namespaces, cgroups, daemon attack surface, capabilities and kernel security mechanisms. ([Docker Docs][10])

### 🔴 256

Would you run production containers as root?

Why/why not?

### 257

How do you run:

```bash
docker run --user 1000:1000 ...
```

?

### 🔴 258

What problem can occur when changing container user?

`[Linux: permissions]`

### 🔴 259

What is:

```bash
--privileged
```

?

Why is it dangerous?

### 260

Developer asks:

> "Give my container privileged mode because the application doesn't work."

Would you approve it?

### 🔴 261

What are Linux capabilities?

### 262

Difference:

```text
CAP_NET_ADMIN
CAP_SYS_ADMIN
CAP_NET_RAW
```

### 263

Why would you use:

```bash
--cap-drop=ALL
```

?

`[Security]`

### 264

What is seccomp?

### 265

What is AppArmor?

### 266

What is SELinux?

### 🔴 267

How do:

```text
namespaces
cgroups
capabilities
seccomp
AppArmor/SELinux
```

work together?

---

# 41. ROOTLESS DOCKER

Current Docker documentation describes rootless mode as running both the daemon and containers without root privileges, using user namespaces. ([Docker Docs][11])

### 268

What is rootless Docker?

### 269

Why use rootless Docker?

### 270

What problems can rootless Docker create?

### 271

Application cannot bind to low port under rootless mode.

Why?

### 272

Rootless container can't access something that works in rootful mode.

What do you investigate?

### 273

When would you prefer rootless Docker?

---

# 42. DOCKER SOCKET SECURITY

### 🔴 274

Why is mounting:

```bash
-v /var/run/docker.sock:/var/run/docker.sock
```

dangerous?

### 🔴 275

A CI container has Docker socket access.

What security risk does this introduce?

### 276

Why can Docker socket access effectively provide powerful control over the host?

`[Security] [Linux] [CI/CD]`

### 277

How would you build CI without directly exposing host Docker socket?

---

# 43. READ-ONLY CONTAINER

### 278

How would you run:

```bash
docker run --read-only ...
```

?

### 279

Application fails because it needs temporary files.

How would you solve it without making entire root filesystem writable?

`[Security]`

### 280

What is tmpfs useful for?

### 281

Why is read-only root filesystem a security hardening technique?

---

# 44. RESOURCE / PROCESS LIMITS

### 282

Container creates thousands of processes.

Host becomes unstable.

What do you investigate?

### 283

What is:

```text
--pids-limit
```

?

### 284

Why can process limits be useful?

`[Linux: fork bomb] [Security]`

### 285

Container requires larger shared memory.

What Docker option could matter?

```text
--shm-size
```

### 286

Application using `/dev/shm` fails inside container.

How do you troubleshoot?

`[Linux]`

---

# 45. DOCKER BUILDx / BUILDKIT

Modern Docker uses BuildKit for builds, and Buildx exposes extended build functionality including cache export/import, secrets and multi-platform builds. ([Docker Docs][12])

### 🔴 287

What is BuildKit?

### 288

What is Buildx?

### 289

Difference:

```text
docker build
docker buildx build
```

### 🔴 290

Why is BuildKit faster?

### 291

How do you inspect builders?

```bash
docker buildx ls
docker buildx inspect
```

### 292

How do you create a custom builder?

### 🔴 293

Build works on AMD64 but fails on ARM64.

Why?

`[Architecture]`

### 🔴 294

How would you build:

```text
linux/amd64
linux/arm64
```

from one machine?

Docker supports multi-platform builds through Buildx/BuildKit. ([Docker Docs][13])

### 295

What is QEMU doing in multi-platform builds?

### 296

What is cross-compilation?

### 🔴 297

Why can an image built for `linux/amd64` fail on ARM?

---

# 46. BUILD CACHE IN CI

### 🔴 298

Every CI build starts from zero and takes 20 minutes.

How do you improve it?

### 299

How can BuildKit external cache help?

### 300

What is:

```text
--cache-from
--cache-to
```

?

### 301

Where can build cache be stored?

### 302

How would you design Docker build caching in GitHub Actions/Jenkins?

`[CI/CD]`

---

# 47. MULTI-ARCH PRODUCTION

### 🔴 303

Your developers use Mac ARM but production is Linux AMD64.

What problems can happen?

### 304

Developer says:

> "It works on my Mac."

Docker image runs on ARM locally but fails in x86 production.

Diagnose.

### 305

How would you create a multi-platform image?

### 306

How would you verify which architectures an image supports?

`[Registry] [Architecture]`

---

# 48. APPLICATION-SPECIFIC SCENARIOS

## Node.js

### 307

Node application works locally but exits in Docker.

What do you check?

### 308

Node app cannot connect to database.

What Docker-specific things do you check?

### 309

Node container consumes excessive memory.

How do you determine whether it's Node heap or Docker limit?

### 310

Node application receives SIGTERM but doesn't shut down.

What do you investigate?

---

## Java/Spring Boot

### 🔴 311

Spring Boot container starts slowly.

How would you design healthchecks/probes?

`[K8s: startupProbe]`

### 312

JVM gets OOM inside container even though host has enough RAM.

Explain.

### 313

JVM heap is larger than container memory limit.

What happens?

### 314

Spring Boot application listens on `localhost`.

Container cannot receive traffic.

Why?

### 315

Java image is 1 GB.

How would you reduce it?

---

## Python

### 316

Python application runs as root.

Would you keep it?

### 317

Python app writes files to `/app`.

Container runs as non-root and gets permission denied.

Fix?

### 318

Python app can't resolve database hostname.

Troubleshoot.

---

## Nginx

### 319

Nginx container is running but browser gets connection refused.

Troubleshoot.

### 320

Nginx returns `502 Bad Gateway`.

Is Docker necessarily broken?

`[Network] [Reverse Proxy]`

### 321

Nginx can resolve backend but connection is refused.

Where do you investigate?

---

# 49. DATABASE + DOCKER

### 🔴 322

Postgres runs in Docker.

Container is deleted.

How do you ensure database data survives?

### 323

Database container starts but application gets connection refused.

What sequence do you investigate?

### 324

Database is "running" but not ready.

How do you detect readiness?

### 325

Why shouldn't database storage normally be treated as disposable container filesystem?

### 326

How would you backup a production DB running inside Docker?

### 327

Database volume becomes full.

How do you investigate?

`[DB] [Linux: disk]`

---

# 50. PROXY / CORPORATE NETWORK

### 328

Docker build works at home but fails inside corporate network.

Why?

### 329

`apt-get`/`npm`/`pip` cannot reach internet during build.

What proxy settings might matter?

### 330

Docker daemon has internet access but build doesn't.

How do you distinguish daemon networking from build networking?

### 331

Containers can access internal services but not external internet.

What would you inspect?

`[Network] [Proxy] [Firewall]`

---

# 51. TIME / CERTIFICATE PROBLEMS

### 332

Docker application gets:

```text
certificate has expired
```

but certificate is valid.

What do you check?

### 333

Container time differs from expected environment.

Could this cause TLS/authentication problems?

### 334

Application works outside Docker but TLS fails inside Docker.

What dependencies/configuration do you investigate?

`[Linux] [Security]`

---

# 52. FILE PERMISSIONS

### 🔴 335

Application:

```text
Permission denied
```

inside container.

Give a systematic troubleshooting process.

### 336

Check:

```bash
id
ls -l
ls -ln
```

Why?

`[Linux: UID/GID]`

### 337

Host directory owned by:

```text
1000:1000
```

container runs:

```text
2000:2000
```

What happens?

### 338

How do you solve UID mismatch without running container as root?

---

# 53. "WORKS ON MY MACHINE"

### 🔴 339

Developer says:

> "Application works on my laptop but Docker doesn't."

What do you compare?

### 🔴 340

Docker application works locally but not staging.

Compare:

```text
image
environment
network
secrets
volume
CPU/memory
architecture
DNS
external dependencies
```

### 341

Docker image is identical between environments, but behavior differs.

What does that tell you?

`[DevOps]`

### 342

How do you prove that image is identical?

`[Registry: digest]`

---

# 54. DEPLOYMENT ROLLBACK

### 🔴 343

Production deployment introduces errors.

How do you rollback?

### 344

Image tag `latest` points to new image.

How do you safely recover previous version?

### 345

How would you design image versioning to make rollback easy?

### 346

How does this compare to:

```text
Kubernetes Deployment rollout/rollback
```

`[K8s]`

---

# 55. ZERO-DOWNTIME DEPLOYMENT

### 🔴 347

You need to deploy a new Docker image without downtime.

How would you design it?

`[CI/CD] [Load Balancer] [K8s]`

### 348

New container starts but takes 60 seconds to become ready.

How do you prevent traffic from reaching it too early?

### 349

Old container is killed before new container is ready.

What architectural mistake exists?

### 350

How would you implement:

```text
old container
      ↓
new container
      ↓
health check
      ↓
traffic switch
```

?

---

# 56. LOAD BALANCER + DOCKER

### 🔴 351

You have:

```text
Internet
 ↓
Load Balancer
 ↓
Docker host
 ↓
Container
```

Container is healthy but user gets 502.

Troubleshoot all layers.

`[AWS ALB] [Network]`

### 352

Load balancer healthcheck fails but direct localhost works.

Why?

### 353

Application binds to:

```text
127.0.0.1
```

Would external load balancer reach it?

### 354

Application binds to:

```text
0.0.0.0
```

Why is this generally required for containerized services?

---

# 57. AWS + DOCKER

### 355

Docker container runs on EC2 but cannot access S3.

What do you check?

`[AWS IAM] [Network]`

### 356

Should you put AWS access keys inside Docker image?

### 357

EC2 host can access AWS service but container cannot.

Troubleshoot.

### 358

Container needs AWS permissions.

How would you design credentials?

`[AWS IAM] [Security]`

### 359

Docker application runs behind:

```text
ALB → EC2 → Docker
```

What ports/security groups must be considered?

`[AWS SG] [Network]`

### 360

Container cannot pull private ECR image.

What do you check?

`[AWS ECR/IAM]`

---

# 58. DOCKER + TERRAFORM

### 361

Terraform creates an EC2 instance that must run Docker.

How would you bootstrap Docker?

`[Terraform] [AWS EC2]`

### 362

Terraform deployment succeeds but Docker application isn't running.

Where does Terraform responsibility end?

### 363

How would you separate:

```text
Infrastructure
vs
Application deployment
```

?

`[Terraform vs CI/CD]`

### 364

Terraform creates Docker network/container directly.

What are potential production limitations?

---

# 59. DOCKER + GIT

### 365

Developer commits:

```text
.env
```

containing production password.

What do you do?

`[Git] [Security]`

### 366

Secret was deleted in next commit.

Is it safe?

Why not?

### 367

Docker build copies `.git` into image.

Why might this be undesirable?

### 368

How would `.dockerignore` help?

---

# 60. DOCKER + MONITORING

### 🔴 369

Application is slow.

Docker container shows:

```text
CPU 20%
Memory 30%
```

Could Docker still be the problem?

### 370

What metrics would you monitor?

```text
CPU
memory
network
disk
restart count
container health
logs
```

### 371

Container restarts increased from 0 to 100/hour.

How would you investigate?

### 372

How do you correlate:

```text
container restart
application error
CPU spike
memory spike
deployment
```

?

`[Observability]`

---

# 61. DOCKER EVENTS

### 373

A production container disappeared.

How do you determine what happened?

### 374

How can:

```bash
docker events
```

help?

### 375

How would you correlate Docker events with CI/CD deployment logs?

---

# 62. DOCKER CLEANUP

### 376

Host has hundreds of stopped containers.

How do you clean them?

### 377

Unused images consume 100 GB.

How do you safely clean them?

### 378

Build cache consumes huge disk.

How do you clean it?

### 379

Unused volumes consume disk.

Would you delete all of them?

Why dangerous?

### 🔴 380

Production host is almost full.

Give a **safe cleanup sequence**, not a destructive command immediately.

---

# 63. PRODUCTION INCIDENT — COMPLETE QUESTIONS

These are the questions I'd practice **verbally**, because an 8-year interview can become an incident-management discussion.

### 🔴 381

**Production website is down. Docker containers are running.**

Walk me through your investigation.

### 🔴 382

**All containers suddenly stopped.**

What do you check?

### 🔴 383

**Only one container stopped.**

What do you check?

### 🔴 384

**All containers are restarting.**

What common dependency might be broken?

### 🔴 385

**Containers are healthy but users receive 502.**

Investigate from:

```text
Client
→ LB
→ host
→ Docker
→ network
→ container
→ application
```

### 🔴 386

**Application returns 500 only in production.**

How do you compare environments?

### 🔴 387

**Application is extremely slow after deployment.**

What metrics/logs do you check?

### 🔴 388

**Disk is 100%.**

What Docker resources might consume it?

### 🔴 389

**Memory is 100%.**

How do you identify the process/container?

### 🔴 390

**CPU is 100%.**

How do you isolate Docker vs application vs host?

---

# 64. THE "INTERVIEWER KEEPS GOING DEEPER" QUESTIONS

These are particularly useful for your 8-year level.

### 🔴 391

Interviewer:

> Container cannot connect to database.

You say:

> Check networking.

Interviewer:

> **What exactly?**

What do you answer?

---

### 🔴 392

Interviewer:

> DNS doesn't work.

You say:

> Check DNS.

Interviewer:

> **How do you prove it's DNS?**

---

### 🔴 393

Interviewer:

> Container crashed.

You say:

> Check logs.

Interviewer:

> **Logs are empty. Now what?**

---

### 🔴 394

Interviewer:

> Container is running.

Interviewer:

> **Does that prove application is healthy?**

---

### 🔴 395

Interviewer:

> Healthcheck is failing.

Interviewer:

> **Does Docker restart the container automatically?**

---

### 🔴 396

Interviewer:

> Container is OOM killed.

Interviewer:

> **How do you determine whether the application's memory requirement is wrong or Docker's limit is wrong?**

---

### 🔴 397

Interviewer:

> Image is 2 GB.

Interviewer:

> **How would you reduce it without randomly changing the application?**

---

### 🔴 398

Interviewer:

> Docker build is slow.

Interviewer:

> **Which exact Dockerfile instruction is causing cache invalidation?**

---

### 🔴 399

Interviewer:

> Docker works on AMD64 but not ARM.

Interviewer:

> **How would you build one image supporting both?**

---

### 🔴 400

Interviewer:

> Container needs a secret.

Interviewer:

> **Where exactly would you put it?**

---

# 65. THE MOST IMPORTANT CROSS-CONNECTION MAP

This is what I strongly recommend you memorize.

| Docker Problem          | Same/Similar Concept                        |
| ----------------------- | ------------------------------------------- |
| Container exits         | `[K8s: CrashLoopBackOff]`                   |
| Restart loop            | `[K8s: restartPolicy/CrashLoopBackOff]`     |
| OOM                     | `[Linux: OOM Killer] [K8s: OOMKilled]`      |
| CPU high                | `[Linux: CPU saturation] [K8s: CPU limits]` |
| Port conflict           | `[Network: ports/NAT] [K8s: Service]`       |
| DNS failure             | `[Network: DNS] [K8s: CoreDNS]`             |
| Container-to-container  | `[K8s: Pod/Service networking]`             |
| Docker network          | `[K8s: CNI]`                                |
| Network isolation       | `[K8s: NetworkPolicy]`                      |
| Volume                  | `[K8s: PV/PVC]`                             |
| Volume permission       | `[Linux: UID/GID] [K8s: securityContext]`   |
| Environment variables   | `[K8s: ConfigMap]`                          |
| Secrets                 | `[K8s: Secret] [AWS: Secrets Manager]`      |
| Healthcheck             | `[K8s: probes]`                             |
| Startup dependency      | `[K8s: readiness/startupProbe]`             |
| Registry                | `[AWS: ECR] [K8s: imagePullSecrets]`        |
| Image tag               | `[CI/CD: artifact versioning]`              |
| Image digest            | `[Supply Chain]`                            |
| Dockerfile              | `[CI/CD: build stage]`                      |
| Build cache             | `[CI/CD: pipeline optimization]`            |
| Docker daemon           | `[Linux: systemd]`                          |
| Docker socket           | `[Security] [Linux]`                        |
| Container user          | `[Linux: UID/GID]`                          |
| Privileged container    | `[Security: capabilities]`                  |
| seccomp                 | `[Linux Security]`                          |
| AppArmor                | `[Linux Security]`                          |
| Disk full               | `[Linux: df/du]`                            |
| Container logs          | `[Observability]`                           |
| Log rotation            | `[Linux/Observability]`                     |
| Docker stats            | `[Monitoring]`                              |
| Docker events           | `[Observability]`                           |
| Container restart       | `[Monitoring/Alerting]`                     |
| Multi-stage build       | `[Security + optimization]`                 |
| Multi-platform image    | `[CI/CD + architecture]`                    |
| Docker Compose          | `[K8s manifests/Helm]`                      |
| Compose depends_on      | `[K8s dependency/readiness]`                |
| Compose service DNS     | `[K8s Service DNS]`                         |
| Docker Swarm            | `[K8s orchestration]`                       |
| Docker on EC2           | `[AWS EC2]`                                 |
| Docker + ALB            | `[AWS ALB]`                                 |
| Docker + ECR            | `[AWS ECR/IAM]`                             |
| Docker + S3             | `[AWS IAM]`                                 |
| Docker + Terraform      | `[IaC]`                                     |
| Docker + Jenkins        | `[CI/CD]`                                   |
| Docker + GitHub Actions | `[CI/CD]`                                   |
| `.dockerignore`         | `[Git/build context]`                       |
| Secret committed to Git | `[Git Security]`                            |
| Image vulnerability     | `[DevSecOps/Supply Chain]`                  |

---

# 66. YOUR MASTER TROUBLESHOOTING TREE

This is the **single most useful pattern** for your interview.

When interviewer gives you **ANY Docker problem**, don't randomly throw commands.

Think:

```text
                    DOCKER PROBLEM
                          |
          +---------------+---------------+
          |               |               |
       BUILD           START/RUN       RUNNING
          |               |               |
     Dockerfile        Exit?          App works?
     Context           Logs?              |
     Cache             Inspect?           |
     Network           Exit code?         |
     Dependencies      Env?               |
                         |                 |
                    +----+----+       +----+----+
                    |         |       |         |
                  APP       DOCKER  NETWORK   STORAGE
                    |         |       |         |
                  logs      daemon    DNS       volume
                  env       runtime   port      perms
                  deps      resource  route     disk
```

Then go deeper:

```text
APPLICATION
    ↓
logs
    ↓
exit code
    ↓
environment
    ↓
dependencies
    ↓
filesystem
```

```text
NETWORK
    ↓
container IP
    ↓
route
    ↓
DNS
    ↓
TCP port
    ↓
HTTP
    ↓
application
```

```text
RESOURCE
    ↓
docker stats
    ↓
CPU
    ↓
memory
    ↓
disk
    ↓
network
    ↓
host cgroups
```

```text
STORAGE
    ↓
mount
    ↓
volume
    ↓
permissions
    ↓
UID/GID
    ↓
disk capacity
```

This is much stronger than saying:

> "I will run `docker logs`."

---

# 67. THE 30 SCENARIOS I WOULD ABSOLUTELY MASTER FIRST

If your interview is soon, prioritize these:

1. 🔴 Container exits immediately `[K8s: CrashLoopBackOff]`
2. 🔴 Container restart loop `[K8s]`
3. 🔴 Container running but application inaccessible
4. 🔴 Port mapping problem `[Network]`
5. 🔴 Port already allocated `[Network/Linux]`
6. 🔴 Container-to-container communication failure `[K8s Service]`
7. 🔴 DNS failure `[K8s CoreDNS]`
8. 🔴 Container cannot access internet `[Network]`
9. 🔴 Application binds to localhost `[Network]`
10. 🔴 OOMKilled `[Linux/K8s]`
11. 🔴 CPU 100% `[Linux/K8s]`
12. 🔴 Disk full `[Linux]`
13. 🔴 Docker daemon unavailable `[Linux/systemd]`
14. 🔴 Docker socket security `[Security]`
15. 🔴 Volume data disappeared `[K8s PV/PVC]`
16. 🔴 Volume permission denied `[Linux UID/GID]`
17. 🔴 Docker logs consuming disk `[Observability]`
18. 🔴 Healthcheck failing `[K8s probes]`
19. 🔴 Build cache not working `[CI/CD]`
20. 🔴 Build context problem `[CI/CD]`
21. 🔴 Image too large `[Optimization/Security]`
22. 🔴 Multi-stage build `[Optimization]`
23. 🔴 Secret inside Dockerfile `[DevSecOps]`
24. 🔴 Registry authentication failure `[CI/CD/AWS ECR]`
25. 🔴 Image works locally but not production `[DevOps]`
26. 🔴 AMD64 vs ARM64 `[Architecture]`
27. 🔴 Compose dependency/startup race `[K8s readiness]`
28. 🔴 Production 502 `[ALB/Network/Reverse Proxy]`
29. 🔴 Zero-downtime Docker deployment `[CI/CD/K8s]`
30. 🔴 Full production incident: **Docker + Linux + Network + Registry + Application + Monitoring**

---

## The key connection you should build

Don't memorize **400 independent Docker questions**.

Build this mental chain:

```text
                 APPLICATION
                     |
                     ↓
                 DOCKERFILE
                     |
                     ↓
                   IMAGE
                     |
          +----------+----------+
          |                     |
       REGISTRY               BUILD
          |                     |
          ↓                     ↓
       PULL/PUSH            BUILDKIT
          |
          ↓
       CONTAINER
          |
    +-----+------+-------+--------+
    |            |       |        |
 NETWORK       PORT    VOLUME   PROCESS
    |            |       |        |
   DNS          NAT     DATA     PID1
    |            |       |        |
    +------------+-------+--------+
                     |
                     ↓
                 RESOURCES
                     |
             CPU / MEMORY / DISK
                     |
                     ↓
                  LOGGING
                     |
                     ↓
               OBSERVABILITY
                     |
                     ↓
                  SECURITY
                     |
                     ↓
                   CI/CD
                     |
                     ↓
                KUBERNETES
                     |
                     ↓
             CLOUD / AWS / IaC
```

That is why the same troubleshooting problem keeps appearing in different technologies. **Docker → Kubernetes → Linux → AWS → CI/CD are often the same underlying problem at different layers.**

For example:

```text
Docker:
Container OOMKilled
       ↓
Linux:
OOM Killer / cgroups
       ↓
Kubernetes:
Pod OOMKilled
       ↓
K8s:
memory requests/limits
       ↓
Monitoring:
memory alert
       ↓
Application:
memory leak
       ↓
Java:
JVM heap
```

That is the **8-year-level way to answer**, rather than treating each as a separate topic.

Also, don't underestimate BuildKit/Buildx, multi-platform builds, build cache, secrets, resource controls and security: these are areas where current Docker capabilities go substantially beyond the basic PATHNEX material. ([Docker Docs][6])

If you master the **400-question bank above + the 30 priority scenarios + the connection map**, you will have a much more interview-ready Docker troubleshooting framework than simply memorizing Docker commands.

[1]: https://docs.docker.com/engine/daemon/troubleshoot/?utm_source=chatgpt.com "Troubleshooting the Docker daemon | Docker Docs"
[2]: https://docs.docker.com/engine/containers/resource_constraints/?utm_source=chatgpt.com "Resource constraints | Docker Docs"
[3]: https://docs.docker.com/engine/network/?utm_source=chatgpt.com "Networking overview | Docker Docs"
[4]: https://docs.docker.com/get-started/docker-concepts/building-images/using-the-build-cache/?utm_source=chatgpt.com "Using the build cache | Docker Docs"
[5]: https://docs.docker.com/dhi/how-to/troubleshoot/?utm_source=chatgpt.com "Troubleshoot | Docker Docs"
[6]: https://docs.docker.com/reference/cli/docker/buildx/build/?utm_source=chatgpt.com "docker buildx build | Docker Docs"
[7]: https://docs.docker.com/guides/lab-compose-quickstart/?utm_source=chatgpt.com "Lab: Docker Compose Quickstart | Docker Docs"
[8]: https://docs.docker.com/engine/logging/drivers/json-file/?utm_source=chatgpt.com "JSON File logging driver | Docker Docs"
[9]: https://docs.docker.com/engine/?utm_source=chatgpt.com "Docker Engine | Docker Docs"
[10]: https://docs.docker.com/engine/security/?utm_source=chatgpt.com "Docker Engine security | Docker Docs"
[11]: https://docs.docker.com/engine/security/rootless/?utm_source=chatgpt.com "Rootless mode | Docker Docs"
[12]: https://docs.docker.com/build/buildkit/?utm_source=chatgpt.com "BuildKit | Docker Docs"
[13]: https://docs.docker.com/build/building/multi-platform/?utm_source=chatgpt.com "Multi-platform builds | Docker Docs"
