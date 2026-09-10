Absolutely. For an **8-year developer**, you should prepare Docker practical questions in the form:

> **"Here is a problem / requirement — write the Docker command, Dockerfile, Compose YAML, or troubleshoot it."**

Your uploaded PDF already contains practical exercises around installation, `pull`, `run`, `ps`, `stop/start/rm`, build, tag, login, push, inspect, logs, volume mapping, port mapping, `exec`, and cleanup. 

But for your experience level, I would prepare a much larger **hands-on question bank**.

# 🔥 Docker Practical / Coding Interview Master Bank

I'll organize it from **basic → intermediate → senior → production troubleshooting**.

---

# 1. Basic Docker Command Practical Questions

### Q1. Check Docker version.

```bash
docker --version
```

### Q2. Check detailed Docker information.

```bash
docker info
```

### Q3. Pull nginx image.

```bash
docker pull nginx
```

### Q4. List all local images.

```bash
docker images
```

### Q5. Run nginx container.

```bash
docker run nginx
```

### Q6. Run nginx in background.

```bash
docker run -d nginx
```

### Q7. Give the container a custom name.

```bash
docker run -d --name nginx-container nginx
```

### Q8. List running containers.

```bash
docker ps
```

### Q9. List all containers including stopped ones.

```bash
docker ps -a
```

### Q10. Stop container.

```bash
docker stop nginx-container
```

### Q11. Start stopped container.

```bash
docker start nginx-container
```

### Q12. Restart container.

```bash
docker restart nginx-container
```

### Q13. Remove container.

```bash
docker rm nginx-container
```

### Q14. Force remove running container.

```bash
docker rm -f nginx-container
```

### Q15. Remove image.

```bash
docker rmi nginx
```

These basic lifecycle commands are directly represented in your uploaded material. 

---

# 2. Port Mapping Practical Questions

## Q16. Run nginx and expose container port 80 as host port 8080.

```bash
docker run -d -p 8080:80 nginx
```

Meaning:

```text
Host              Container
8080      --->      80
```

Your source uses this exact example. 

---

## Q17. Run application on host port 9000 and container port 8080.

```bash
docker run -d -p 9000:8080 myapp
```

---

## Q18. Publish multiple ports.

```bash
docker run -d \
  -p 8080:8080 \
  -p 9090:9090 \
  myapp
```

---

## Q19. Bind port only to localhost.

```bash
docker run -d -p 127.0.0.1:8080:80 nginx
```

---

## Q20. Application works inside container but not from browser. Troubleshoot.

Expected commands:

```bash
docker ps
docker logs <container>
docker inspect <container>
docker exec -it <container> sh
```

Then:

```bash
curl localhost:<container-port>
```

inside the container.

Check:

```text
Application listening address
Application port
-p mapping
Firewall
Container status
```

---

# 3. Interactive / Exec Questions

## Q21. Enter running container.

```bash
docker exec -it nginx-container /bin/bash
```

Your uploaded notes explicitly give this as the standard troubleshooting command. 

---

## Q22. Alpine container doesn't have bash. What do you do?

```bash
docker exec -it <container> /bin/sh
```

---

## Q23. Execute `ls` inside a running container.

```bash
docker exec <container> ls
```

---

## Q24. Execute a command as root.

```bash
docker exec -u 0 -it <container> sh
```

---

## Q25. Check environment variables inside container.

```bash
docker exec <container> env
```

---

## Q26. Check processes inside container.

```bash
docker top <container>
```

---

# 4. Environment Variable Practical Questions

## Q27. Pass an environment variable.

```bash
docker run -d \
  -e ENVIRONMENT=production \
  myapp
```

---

## Q28. Pass database host and port.

```bash
docker run -d \
  -e DB_HOST=db \
  -e DB_PORT=5432 \
  myapp
```

---

## Q29. Use an env file.

```bash
docker run --env-file .env myapp
```

---

## Q30. Override Dockerfile ENV.

```bash
docker run -e APP_ENV=prod myapp
```

---

## Q31. How would you verify the environment variable?

```bash
docker exec <container> env
```

---

# 5. Dockerfile Coding Questions

This is **very important**.

---

## Q32. Write Dockerfile for a Node.js application.

Basic:

```dockerfile
FROM node:20

WORKDIR /app

COPY package*.json ./

RUN npm ci

COPY . .

EXPOSE 3000

CMD ["npm", "start"]
```

---

## Q33. Build this image.

```bash
docker build -t mynodeapp:v1 .
```

---

## Q34. Run it.

```bash
docker run -d \
  --name nodeapp \
  -p 3000:3000 \
  mynodeapp:v1
```

---

# 6. Dockerfile Ordering Questions

## Q35. Why would you write:

```dockerfile
COPY package*.json ./
RUN npm ci
COPY . .
```

instead of:

```dockerfile
COPY . .
RUN npm ci
```

Expected reasoning:

```text
Dependency files change less frequently
             ↓
npm install layer stays cached
             ↓
Build becomes faster
```

---

# 7. Dockerfile Optimization Practical Questions

## Q36. Image is 1.5 GB. Reduce it.

Possible approach:

```text
1. Multi-stage build
2. Smaller runtime base image
3. .dockerignore
4. Remove build dependencies
5. Combine/optimize package installation
6. Don't copy unnecessary files
7. Use production dependencies only
```

Investigate first:

```bash
docker history myimage
```

---

## Q37. Find which Dockerfile layers are large.

```bash
docker history myimage
```

---

## Q38. Inspect image configuration.

```bash
docker inspect myimage
```

---

# 8. `.dockerignore` Practical

## Q39. Write `.dockerignore` for Node.js.

```text
node_modules
npm-debug.log
.git
.gitignore
Dockerfile
.dockerignore
.env
coverage
dist
```

---

## Q40. Why should `.env` potentially be excluded?

Because you don't want secrets/configuration accidentally copied into the build context/image.

---

# 9. CMD / ENTRYPOINT Practical Coding

## Q41. Write a Dockerfile where Python is the entrypoint and script is default argument.

```dockerfile
FROM python:3.12-slim

WORKDIR /app

COPY . .

ENTRYPOINT ["python"]
CMD ["app.py"]
```

---

## Q42. What happens here?

```bash
docker run myimage
```

Equivalent:

```bash
python app.py
```

---

## Q43. Override CMD.

```bash
docker run myimage test.py
```

Result:

```text
python test.py
```

---

## Q44. Override ENTRYPOINT.

```bash
docker run --entrypoint /bin/sh myimage
```

---

# 10. COPY / ADD Practical

## Q45. Copy application files.

```dockerfile
COPY . /app
```

---

## Q46. Copy only package files.

```dockerfile
COPY package*.json /app/
```

---

## Q47. Copy files from another build stage.

```dockerfile
COPY --from=builder /app/build /usr/share/nginx/html
```

---

# 11. Multi-stage Build Questions

## Q48. Write a production Dockerfile for React.

```dockerfile
FROM node:20 AS builder

WORKDIR /app

COPY package*.json ./
RUN npm ci

COPY . .
RUN npm run build


FROM nginx:alpine

COPY --from=builder /app/build /usr/share/nginx/html

EXPOSE 80
```

---

## Q49. Write multi-stage Dockerfile for Go.

```dockerfile
FROM golang:1.24 AS builder

WORKDIR /app

COPY go.mod go.sum ./
RUN go mod download

COPY . .
RUN go build -o app .


FROM alpine:latest

WORKDIR /app

COPY --from=builder /app/app .

CMD ["./app"]
```

---

## Q50. Why is the final image smaller?

Because:

```text
Builder
   ↓
compiler
dependencies
source
build tools
   ↓
Final image
   ↓
Only runtime + application
```

---

# 12. Volume Practical Questions

Your source explicitly demonstrates host-directory → container-directory mapping using `-v`. 

---

## Q51. Create named volume.

```bash
docker volume create appdata
```

---

## Q52. List volumes.

```bash
docker volume ls
```

---

## Q53. Inspect volume.

```bash
docker volume inspect appdata
```

---

## Q54. Mount named volume.

```bash
docker run -d \
  --name db \
  -v appdata:/var/lib/postgresql/data \
  postgres
```

---

## Q55. Mount host directory.

```bash
docker run -d \
  -v /host/data:/container/data \
  myapp
```

---

## Q56. Make mount read-only.

```bash
docker run -d \
  -v /host/config:/app/config:ro \
  myapp
```

---

# 13. Volume Troubleshooting

## Q57. Container lost data after recreation. Why?

Likely application data was stored in the container writable layer rather than persistent storage.

---

## Q58. Container cannot write to volume.

Check:

```bash
docker inspect <container>
```

Then:

```text
Mount path
Ownership
Permissions
Container user
Host filesystem permissions
SELinux/AppArmor where applicable
```

---

## Q59. Backup a Docker volume.

Practical pattern:

```bash
docker run --rm \
  -v appdata:/data \
  -v "$PWD":/backup \
  alpine \
  tar czf /backup/appdata.tar.gz -C /data .
```

---

# 14. Docker Network Coding Questions

## Q60. List networks.

```bash
docker network ls
```

---

## Q61. Create bridge network.

```bash
docker network create app-network
```

---

## Q62. Run two containers on same network.

```bash
docker run -d \
  --name backend \
  --network app-network \
  backend:v1
```

```bash
docker run -d \
  --name frontend \
  --network app-network \
  frontend:v1
```

---

## Q63. How does frontend connect to backend?

Instead of:

```text
172.x.x.x
```

use:

```text
backend:<port>
```

because Docker's user-defined network provides service/container-name based DNS.

---

## Q64. Connect existing container to network.

```bash
docker network connect app-network mycontainer
```

---

## Q65. Disconnect.

```bash
docker network disconnect app-network mycontainer
```

---

## Q66. Inspect network.

```bash
docker network inspect app-network
```

---

# 15. Network Troubleshooting Practical

## Q67. Container A cannot communicate with B. What commands?

```bash
docker ps
docker network ls
docker network inspect <network>
docker inspect <containerA>
docker inspect <containerB>
```

Then:

```bash
docker exec -it containerA sh
```

and test:

```bash
curl http://containerB:<port>
```

---

## Q68. Container can connect by IP but not hostname.

Investigate:

```text
DNS
Network membership
User-defined bridge network
Container name
Network aliases
```

---

## Q69. Container can't access internet.

Check:

```bash
docker inspect <container>
docker network inspect bridge
```

Then investigate:

```text
DNS
NAT
Host networking
Firewall
Docker daemon configuration
```

---

# 16. Host Network Practical

## Q70. Run using host network.

```bash
docker run --network host myapp
```

---

## Q71. What happens to `-p` with host networking?

This is a classic interview trap: host networking doesn't use the normal Docker port-publishing mechanism in the same way because the container shares the host network namespace.

---

# 17. None Network

## Q72. Run container with no network.

```bash
docker run --network none myimage
```

Your source defines `none` as having no network interface. 

---

# 18. Docker Compose Coding Questions

## Q73. Write Compose for frontend + backend.

```yaml
services:

  frontend:
    image: frontend:v1
    ports:
      - "3000:3000"
    depends_on:
      - backend

  backend:
    image: backend:v1
    ports:
      - "8080:8080"
```

---

# 19. Compose with Database

## Q74. Write Compose for application + PostgreSQL.

```yaml
services:

  app:
    build: .
    ports:
      - "8080:8080"
    environment:
      DB_HOST: db
      DB_PORT: 5432
      DB_NAME: appdb
      DB_USER: appuser
      DB_PASSWORD: secret
    depends_on:
      - db

  db:
    image: postgres:17
    environment:
      POSTGRES_DB: appdb
      POSTGRES_USER: appuser
      POSTGRES_PASSWORD: secret
    volumes:
      - postgres-data:/var/lib/postgresql/data

volumes:
  postgres-data:
```

---

# 20. Compose Commands

### Q75. Start services.

```bash
docker compose up
```

### Q76. Start in background.

```bash
docker compose up -d
```

### Q77. Stop services.

```bash
docker compose down
```

### Q78. Rebuild.

```bash
docker compose build
```

### Q79. Rebuild and start.

```bash
docker compose up -d --build
```

### Q80. View logs.

```bash
docker compose logs
```

### Q81. Follow logs.

```bash
docker compose logs -f
```

### Q82. View only backend logs.

```bash
docker compose logs -f backend
```

### Q83. Execute command in Compose container.

```bash
docker compose exec backend sh
```

---

# 21. Compose Troubleshooting

### Q84. `depends_on` exists, but app fails because DB isn't ready. Fix it.

Expected concepts:

```text
depends_on
      ≠
application readiness
```

Use health checks/readiness logic rather than assuming that "container started" means "database ready."

---

# 22. Docker Registry Practical

Your source explicitly covers tagging, login and push. 

## Q85. Tag image.

```bash
docker tag myapp:v1 registry.example.com/myapp:v1
```

---

## Q86. Login.

```bash
docker login registry.example.com
```

---

## Q87. Push.

```bash
docker push registry.example.com/myapp:v1
```

---

## Q88. Pull.

```bash
docker pull registry.example.com/myapp:v1
```

---

# 23. Image Versioning Practical

## Q89. Build version 1.

```bash
docker build -t myapp:v1 .
```

## Q90. Build version 2.

```bash
docker build -t myapp:v2 .
```

## Q91. Roll back.

```bash
docker run myapp:v1
```

---

# 24. Digest Questions

## Q92. Run exact image using digest.

Conceptually:

```bash
docker pull registry.example.com/myapp@sha256:<digest>
```

### Interview question:

> Why is digest safer than `latest`?

Because digest identifies an immutable image content rather than relying on a mutable tag.

---

# 25. Logging Practical

## Q93. View logs.

```bash
docker logs app
```

## Q94. Follow logs.

```bash
docker logs -f app
```

## Q95. Show last 100 lines.

```bash
docker logs --tail 100 app
```

## Q96. Show logs since time.

```bash
docker logs --since 10m app
```

---

# 26. Container Health Practical

## Q97. Add health check.

```dockerfile
HEALTHCHECK \
  --interval=30s \
  --timeout=5s \
  --retries=3 \
  CMD curl -f http://localhost:8080/health || exit 1
```

---

## Q98. Check health status.

```bash
docker ps
```

or:

```bash
docker inspect <container>
```

---

# 27. Resource Limiting Practical

## Q99. Limit memory to 512 MB.

```bash
docker run -d \
  --memory=512m \
  myapp
```

---

## Q100. Limit CPU.

```bash
docker run -d \
  --cpus="1.0" \
  myapp
```

---

## Q101. Limit both.

```bash
docker run -d \
  --memory=512m \
  --cpus="1.0" \
  myapp
```

---

# 28. Resource Troubleshooting

## Q102. Find container consuming high CPU.

```bash
docker stats
```

Then:

```bash
docker top <container>
```

Then inspect application processes/logs.

---

## Q103. Container gets killed due to memory.

Check:

```bash
docker stats
docker inspect <container>
docker logs <container>
```

Investigate:

```text
Memory limit
Application memory usage
Memory leak
Heap configuration
Host memory
```

---

# 29. Docker Security Practical

## Q104. Run container as non-root.

```bash
docker run --user 1000:1000 myapp
```

or Dockerfile:

```dockerfile
USER 1000
```

---

## Q105. Drop Linux capabilities.

Example:

```bash
docker run \
  --cap-drop=ALL \
  myapp
```

Then add only required capabilities.

---

## Q106. Run read-only root filesystem.

```bash
docker run \
  --read-only \
  myapp
```

---

## Q107. Why is this dangerous?

```bash
docker run --privileged myapp
```

Because it grants substantially elevated access to host resources and should not be used casually.

---

# 30. Secret Management Practical

## Q108. Where should DB password NOT be stored?

Don't bake it into:

```dockerfile
ENV DB_PASSWORD=secret
```

and don't put secrets directly into the image.

---

## Q109. Pass secret at runtime.

For simple local cases:

```bash
docker run \
  -e DB_PASSWORD="$DB_PASSWORD" \
  myapp
```

For production, use the organization's secret-management mechanism rather than baking secrets into images.

---

# 31. Docker Build Cache Questions

## Q110. Build is slow. How do you improve it?

Check:

```text
Dockerfile instruction ordering
.dockerignore
Dependency layers
Build cache
Multi-stage build
Build context size
```

---

## Q111. Why does this cause poor caching?

```dockerfile
COPY . .
RUN npm install
```

Every source change can invalidate the layer before dependency installation.

Better:

```dockerfile
COPY package*.json ./
RUN npm ci
COPY . .
```

---

# 32. Build Context Practical

## Q112. Explain:

```bash
docker build -t app .
```

The `.` specifies the **build context**.

---

## Q113. Build using another Dockerfile.

```bash
docker build \
  -f Dockerfile.prod \
  -t app:prod .
```

---

## Q114. Build with argument.

```bash
docker build \
  --build-arg APP_VERSION=1.2.0 \
  -t app:v1 .
```

Dockerfile:

```dockerfile
ARG APP_VERSION
```

---

# 33. Dockerfile ARG / ENV Practical

## Q115. Use build-time argument.

```dockerfile
ARG NODE_VERSION=20
FROM node:${NODE_VERSION}
```

Build:

```bash
docker build \
  --build-arg NODE_VERSION=22 \
  -t app .
```

---

## Q116. Difference practical scenario:

> Build needs a value, but runtime doesn't.

Use:

```text
ARG
```

> Application needs the value when running.

Use:

```text
ENV
```

---

# 34. Docker Cleanup Practical

Your source specifically covers all of these prune operations. 

### Q117. Remove stopped containers.

```bash
docker container prune
```

### Q118. Remove dangling images.

```bash
docker image prune
```

### Q119. Remove unused images.

```bash
docker image prune -a
```

### Q120. Remove unused volumes.

```bash
docker volume prune
```

### Q121. Remove unused networks.

```bash
docker network prune
```

### Q122. Remove build cache.

```bash
docker builder prune
```

### Q123. General cleanup.

```bash
docker system prune
```

### Q124. Aggressive cleanup.

```bash
docker system prune -a
```

---

# 35. Disk Full Scenario

## Q125.

> Production Docker host is 95–100% full. What commands do you run?

First:

```bash
docker system df
```

Then inspect:

```bash
docker images
docker ps -a
docker volume ls
```

Potential cleanup:

```bash
docker container prune
docker image prune
docker builder prune
```

Don't blindly execute:

```bash
docker system prune -a
```

on production.

---

# 36. Container Immediately Exits

## Q126.

> You run the container and it immediately exits. Troubleshoot.

```bash
docker ps -a
docker logs <container>
docker inspect <container>
```

Check:

```text
Exit code
CMD
ENTRYPOINT
Application exception
Configuration
Environment variables
```

---

# 37. Container Restart Loop

## Q127.

> Container keeps restarting.

Run:

```bash
docker ps
docker inspect <container>
docker logs --tail 200 <container>
```

Look for:

```text
Application crash
Health check
OOM
Bad configuration
Dependency unavailable
Restart policy
```

---

# 38. Port Already Allocated

## Q128.

You get:

```text
Bind for 0.0.0.0:8080 failed: port is already allocated
```

What do you do?

```bash
docker ps
```

Find the container using the port.

Then:

```bash
docker stop <container>
```

or choose another host port:

```bash
docker run -p 8081:8080 myapp
```

---

# 39. Permission Denied

## Q129.

Container can't write to mounted directory.

Investigate:

```bash
docker inspect <container>
```

Then:

```text
Host ownership
UID/GID
Container USER
Filesystem permissions
SELinux/AppArmor if applicable
```

---

# 40. Docker Daemon Troubleshooting

## Q130.

You get:

```text
Cannot connect to the Docker daemon
```

Check:

```bash
docker info
```

On Linux:

```bash
systemctl status docker
```

Then, where appropriate:

```bash
sudo systemctl restart docker
```

---

# 41. Image Pull Failure

## Q131.

```text
pull access denied
```

What do you check?

```text
Image name
Repository
Tag
Registry URL
Authentication
Permissions
Network
```

Try:

```bash
docker login
docker pull <image>
```

---

# 42. Image Push Failure

## Q132.

```bash
docker push registry.example.com/app:v1
```

fails.

Check:

```text
docker login
repository name
registry
permissions
tag
network
```

---

# 43. Image Doesn't Contain Expected Changes

## Q133.

You changed source code but container still shows old code.

Investigate:

```text
Build cache
Image tag
Running container image ID
Volume mounts
Build context
Dockerfile COPY
```

Commands:

```bash
docker images
docker inspect <container>
docker history <image>
```

Then rebuild:

```bash
docker build --no-cache -t app:v2 .
```

---

# 44. "Works on My Machine" Scenario

## Q134.

Developer says:

> "It works on my laptop."

Docker version fails.

What do you investigate?

```text
Environment variables
OS dependencies
Runtime version
File paths
Permissions
CPU architecture
Network
Port
Configuration
Dependency versions
```

---

# 45. Architecture Mismatch

## Q135.

Image works on x86 but fails on ARM.

What do you investigate?

```text
docker image inspect <image>
```

Then build/publish appropriate platform variants where needed.

Concept:

```text
linux/amd64
linux/arm64
```

---

# 46. Multi-platform Build

## Q136.

Build image for AMD64 and ARM64.

Typical modern approach:

```bash
docker buildx build \
  --platform linux/amd64,linux/arm64 \
  -t registry.example.com/app:v1 \
  --push .
```

---

# 47. Production Image Security Scenario

## Q137.

> Security scanner reports critical CVEs in your Docker image. What do you do?

Expected process:

```text
Identify vulnerable package
        ↓
Check whether vulnerability is actually reachable/exploitable
        ↓
Update base image/package
        ↓
Rebuild
        ↓
Rescan
        ↓
Test
        ↓
Promote
```

Don't simply suppress every vulnerability.

---

# 48. Production Dockerfile Question

## Q138.

> Write a production-grade Dockerfile.

Interviewer is looking for:

```text
Small base image
Pinned versions
Multi-stage build
Non-root USER
.dockerignore
Minimal packages
No secrets
Healthcheck where appropriate
Proper signal handling
Reproducible dependencies
```

---

# 49. Zero Downtime Deployment

## Q139.

> How would you deploy a new Docker image without downtime?

Expected architecture:

```text
Load Balancer
      |
      +---- Container v1
      +---- Container v1
      |
     deploy
      |
      +---- Container v2
      +---- Container v2
      |
    health check
      |
  remove old v1
```

In larger production systems, this is usually handled by an orchestrator such as Kubernetes rather than manually managing individual Docker containers.

---

# 50. Rollback Scenario

## Q140.

Production is running:

```text
app:v2
```

and v2 is broken.

What do you do?

```bash
docker stop app
docker run -d --name app app:v1
```

In a real production orchestration system, you'd normally roll back the deployment rather than manually replacing containers.

---

# 51. Docker + CI/CD Practical

## Q141.

> Write a typical CI/CD Docker flow.

```text
Developer
   ↓
Git
   ↓
CI
   ↓
Unit Tests
   ↓
Docker Build
   ↓
Security Scan
   ↓
Tag Image
   ↓
Push Registry
   ↓
Deploy
   ↓
Health Check
   ↓
Production
```

---

# 52. CI Docker Commands

### Q142. Build image.

```bash
docker build -t myapp:$GIT_COMMIT .
```

### Q143. Scan.

Use your organization's image scanner.

### Q144. Push.

```bash
docker push registry.example.com/myapp:$GIT_COMMIT
```

### Q145. Deploy exact version.

```text
registry.example.com/myapp:<immutable-version>
```

---

# 53. Important Senior Practical Questions

These are the ones I would expect from someone with **8 years**.

### Q146. Build a production Dockerfile for Java Spring Boot.

### Q147. Build a production Dockerfile for Node.js.

### Q148. Build a production Dockerfile for Python.

### Q149. Build a production Dockerfile for Go.

### Q150. Build a production Dockerfile for React + Nginx.

### Q151. Convert a VM-based application into containers.

### Q152. Containerize a monolithic application.

### Q153. Containerize a microservice.

### Q154. Design frontend + backend + database using Docker Compose.

### Q155. Add Redis to Compose.

### Q156. Add health checks.

### Q157. Add persistent database storage.

### Q158. Add custom Docker network.

### Q159. Add environment-specific configuration.

### Q160. Add non-root user.

### Q161. Reduce a 2 GB image to <300 MB.

### Q162. Make Docker build 5× faster.

### Q163. Secure the Docker image.

### Q164. Troubleshoot high CPU.

### Q165. Troubleshoot high memory.

### Q166. Troubleshoot disk-full.

### Q167. Troubleshoot networking.

### Q168. Troubleshoot DNS.

### Q169. Troubleshoot volume permissions.

### Q170. Troubleshoot image pull.

### Q171. Troubleshoot container restart loop.

### Q172. Troubleshoot health check failure.

### Q173. Troubleshoot slow application startup.

### Q174. Implement graceful shutdown.

### Q175. Implement image versioning.

### Q176. Implement immutable deployments.

### Q177. Implement Docker image promotion.

### Q178. Implement Docker image rollback.

### Q179. Implement multi-platform image builds.

### Q180. Design Docker security controls.

---

# 🔥 20 REAL INTERVIEW-STYLE PRACTICAL SCENARIOS

These are **more valuable than memorizing commands**.

## Scenario 1

> "I give you a Dockerfile. Build it, run it and expose port 8080."

---

## Scenario 2

> "The container is running, but browser cannot access it. Fix it."

---

## Scenario 3

> "Container exits immediately. Find the reason."

---

## Scenario 4

> "Container keeps restarting every few seconds."

---

## Scenario 5

> "Two containers need to communicate. Configure networking."

---

## Scenario 6

> "Application needs PostgreSQL. Write Docker Compose."

---

## Scenario 7

> "Database data must survive container deletion."

Configure:

```yaml
volumes:
```

---

## Scenario 8

> "Application image is 2 GB. Optimize it."

---

## Scenario 9

> "Docker build takes 10 minutes. Optimize it."

---

## Scenario 10

> "Application password must not appear inside the Docker image."

Design secret handling.

---

## Scenario 11

> "Container is consuming 100% CPU."

Troubleshoot using:

```bash
docker stats
docker top
docker logs
docker inspect
```

---

## Scenario 12

> "Container is being killed due to memory."

Find:

```text
Memory limit
Actual usage
Application leak
Host resources
```

---

## Scenario 13

> "Docker host disk is full."

Start:

```bash
docker system df
```

Then identify:

```text
Images
Containers
Volumes
Build cache
```

---

## Scenario 14

> "Image works on AMD64 but not ARM64."

Investigate multi-platform image support.

---

## Scenario 15

> "Production deployment must be zero downtime."

Explain immutable image + rolling deployment.

---

## Scenario 16

> "New version is broken. Roll back immediately."

Explain image versioning and immutable deployment.

---

## Scenario 17

> "Security scanner finds a critical vulnerability."

Explain:

```text
scan → assess → patch → rebuild → rescan → test → deploy
```

---

## Scenario 18

> "Container needs to run as non-root."

Modify:

```dockerfile
USER appuser
```

and ensure filesystem permissions work.

---

## Scenario 19

> "Container can't resolve another service by name."

Troubleshoot:

```bash
docker network ls
docker network inspect <network>
```

---

## Scenario 20

> "Design Docker architecture for 50 microservices."

Expected discussion:

```text
Docker images
     ↓
Registry
     ↓
CI/CD
     ↓
Kubernetes
     ↓
Services
     ↓
Pods
     ↓
Networking
     ↓
Volumes
     ↓
Monitoring
     ↓
Logging
     ↓
Security
```

---

# 🧠 MOST IMPORTANT PRACTICAL PATTERN

For your **8-year interview**, don't memorize 180 commands independently.

Memorize this troubleshooting sequence:

```text
PROBLEM
   ↓
docker ps
   ↓
docker ps -a
   ↓
docker logs
   ↓
docker inspect
   ↓
docker stats
   ↓
docker exec
   ↓
docker network inspect
   ↓
docker volume inspect
   ↓
docker history
   ↓
docker system df
```

Think:

```text
STATUS
  ↓
LOGS
  ↓
CONFIG
  ↓
RESOURCE
  ↓
INSIDE CONTAINER
  ↓
NETWORK
  ↓
STORAGE
  ↓
IMAGE
  ↓
HOST
```

That's a **much stronger interview answer** than randomly giving commands.

And your uploaded notes already reinforce the core operational trio:

> `docker inspect` = detailed information, `docker logs` = what happened, and `docker exec` = enter/execute inside a running container. 

### Your Docker practical preparation should ultimately cover:

```text
                     DOCKER
                        |
     +------------------+------------------+
     |                  |                  |
   BUILD              RUN               OPERATE
     |                  |                  |
Dockerfile           Container          logs
Layers               Ports              inspect
Cache                Env                exec
Multi-stage          Network            stats
Security             Volume             top
     |                  |                  |
     +------------------+------------------+
                        |
                  TROUBLESHOOT
                        |
       +----------------+----------------+
       |                |                |
    Build            Network          Storage
       |                |                |
    Cache             DNS             Volume
    Image             Port            Permission
    CVE               NAT             Disk
                        |
                        |
                     DEPLOY
                        |
              Registry → CI/CD
                        |
                 Compose/K8s
```

**This is the practical Docker syllabus I'd use for an 8-year candidate.** The original PDF is your foundation; the additional sections above are what you should add to make it interview-ready at senior level.
