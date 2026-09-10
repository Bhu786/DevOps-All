# DOCKER — INTERVIEW NOTES

**Start-to-End • Simple to Learn • Easy to Remember • Interview Ready**

> **IMPORTANT:** This version keeps the complete topic coverage and commands from the uploaded PATHNEX Docker PDF, while reorganizing the material into simpler interview-friendly language, memory tricks, examples, and revision sections. The source document covers Docker from containers through cleanup commands. fileciteturn1file0L5-L18

---

# 1. What is Docker?

Docker is an **open-source platform** that allows developers to automate:

- Deployment
- Scaling
- Management of applications

Docker runs applications inside **lightweight, portable containers**.

## What is a Container?

A container is an:

- Isolated
- Self-contained
- Lightweight
- Portable

environment that contains everything an application needs to run, such as:

- Code
- Libraries
- Dependencies
- System tools

### Interview Answer

> **Docker is an open-source platform used to automate the deployment, scaling, and management of applications using lightweight and portable containers. A container packages the application along with its dependencies so it can run consistently across environments.**

### Memory Trick

**Docker = PACKAGE + PORTABLE + RUN**

---

# 2. Containers

## What are Containers?

Containers package an application and its dependencies into a consistent environment.

The purpose is to make the application behave consistently across:

```text
Development
     ↓
Staging
     ↓
Production
```

Because the environment is containerized, the application can work consistently regardless of the host environment.

---

## Isolation and Portability

Containers are isolated from the host system.

However, they share the **same OS kernel** with the host.

This makes containers lightweight compared with traditional Virtual Machines (VMs).

### Isolation

Isolation means one container/application does not interfere with other applications running on the same system.

### Portability

A container can run on any system where Docker is installed.

### Interview Answer

> **Containers package an application and its dependencies into an isolated and portable environment. They share the host OS kernel, which makes them lighter than traditional virtual machines.**

### Memory Trick

**Container = ISOLATED + LIGHTWEIGHT + PORTABLE**

---

# 3. Dockerfile

A **Dockerfile** is a script containing instructions used to build a Docker image.

It tells Docker:

- Which base image to use
- How to copy application code
- How to install dependencies
- Which commands should run when the container starts

---

## Example Dockerfile

```dockerfile
FROM node:14

WORKDIR /user/pathnex

COPY . .

RUN npm install

EXPOSE 3000

CMD ["npm", "start"]
```

## Understand Each Instruction

### FROM

```dockerfile
FROM node:14
```

Specifies the base image.

### WORKDIR

```dockerfile
WORKDIR /user/pathnex
```

Sets the working directory inside the image/container.

### COPY

```dockerfile
COPY . .
```

Copies application files into the image.

### RUN

```dockerfile
RUN npm install
```

Runs a command while building the image.

### EXPOSE

```dockerfile
EXPOSE 3000
```

Documents the port the application is expected to use.

### CMD

```dockerfile
CMD ["npm", "start"]
```

Specifies the default command to run when the container starts.

### Interview Answer

> **A Dockerfile is a text file containing instructions used to build a Docker image. It defines the base image, application files, dependencies, and the default command for running the application.**

### Memory Trick

**Dockerfile = BUILD INSTRUCTIONS**

---

# 4. Images

## What is a Docker Image?

A Docker image is a **read-only template** used to create containers.

It contains things required to run an application, such as:

- Application code
- Runtime
- Libraries
- Environment variables
- Configuration files

Images can be built from a Dockerfile.

### Simple Relationship

```text
Dockerfile
     ↓
   Build
     ↓
Docker Image
     ↓
   Run
     ↓
Container
```

### Interview Answer

> **A Docker image is a read-only template containing the application code, runtime, libraries, environment variables, and configuration required to run an application. Containers are created from images.**

---

# 5. Base Images and Custom Images

You can start with an existing **base image**.

Examples mentioned in the source:

- Ubuntu
- Alpine Linux
- Node.js

Then you can add your application on top of the base image.

```text
Base Image
    ↓
Application
    ↓
Dependencies
    ↓
Custom Image
```

## Docker Hub

Docker Hub is a central repository where you can find pre-built images for:

- Programming languages
- Services
- Applications

### Interview Answer

> **I can use a base image such as Ubuntu, Alpine, or Node.js and layer my application and dependencies on top of it to create a custom image.**

### Memory Trick

**Base Image = STARTING POINT**

**Custom Image = BASE + APPLICATION**

---

# 6. Docker Engine

Docker Engine is the core component that runs containers.

The source describes Docker Engine as a **client-server application**.

The three major components described are:

1. Docker Daemon
2. Docker CLI
3. REST API

---

## 6.1 Docker Daemon — dockerd

The Docker daemon is the background service responsible for managing:

- Containers
- Images
- Networks
- Storage volumes

### Important Source Note

The uploaded source notes:

> `dockerd` is not being used nowadays and says Containerd is now used.

For interview preparation, preserve the source's wording but be careful not to overstate this as a complete replacement of the Docker Engine architecture.

---

## 6.2 Docker CLI

The Docker CLI is the command-line interface used by users to interact with Docker.

Example:

```bash
docker run nginx
```

---

## 6.3 REST API

The REST API allows external programs to interact with Docker and manage containers.

### Interview Answer

> **Docker Engine is the core component responsible for running containers. The Docker client provides the CLI, and Docker exposes an API for programmatic interaction.**

### Memory Trick

**Engine = RUN**

**CLI = COMMAND**

**API = PROGRAMMATIC ACCESS**

---

# 7. Docker Compose

Docker Compose is a tool used for defining and running **multi-container Docker applications**.

A YAML file, commonly:

```text
docker-compose.yml
```

can define:

- Services
- Relationships between services
- Networks
- Volumes

For example:

- Web server
- Database

---

## Example docker-compose.yml

```yaml
version: '3'

services:
  web:
    image: nginx
    ports:
      - "8080:80"

  db:
    image: sql
    environment:
      MYSQL_ROOT_PASSWORD: pathnex
```

### Understand the Example

```text
web
 ↓
nginx
 ↓
8080:80

db
 ↓
sql
 ↓
MYSQL_ROOT_PASSWORD
```

### Interview Answer

> **Docker Compose is used to define and run multi-container applications using a YAML file. It lets us configure services, networking, relationships, and volumes together.**

### Memory Trick

**Compose = MULTIPLE CONTAINERS TOGETHER**

---

# 8. Docker Registry

A Docker registry is a place where Docker images are stored.

The source mentions:

- Docker Hub → popular public registry
- Private registries → can be used by organizations

Registries allow us to:

- Push images
- Pull images

from remote repositories.

### Basic Flow

```text
Local Machine
     ↓
 docker push
     ↓
Registry
     ↓
 docker pull
     ↓
Another Machine
```

### Interview Answer

> **A Docker registry stores Docker images. Docker Hub is a popular public registry, while organizations can also use private registries.**

### Memory Trick

**Registry = IMAGE STORAGE**

---

# 9. Docker Networking

Docker containers are isolated by default.

Docker networks control how containers communicate:

- With each other
- With the outside world

---

# 10. Default Docker Network Types

The source mentions four network types:

1. Bridge
2. Host
3. Overlay
4. None

---

## 10.1 Bridge

Bridge is the default network for standalone containers.

### Remember

**Bridge = DEFAULT**

---

## 10.2 Host

In host networking, the container shares the host's networking stack.

### Remember

**Host = SHARE HOST NETWORK**

---

## 10.3 Overlay

Overlay is used for **multi-host networking in Swarm mode**.

### Remember

**Overlay = MULTI-HOST / SWARM**

---

## 10.4 None

None means the container has no network interface.

### Remember

**None = NO NETWORK**

---

## Network Memory Trick

```text
Bridge  → Default
Host    → Host network
Overlay → Multi-host / Swarm
None    → No network
```

### Interview Answer

> **Docker provides different network types depending on the communication requirement. Bridge is the default for standalone containers, Host shares the host network stack, Overlay supports multi-host networking in Swarm, and None provides no network interface.**

---

# 11. Volumes

Volumes provide **persistent storage** for Docker containers.

By default, data inside a container is **ephemeral**.

That means data can be lost when the container is removed.

Volumes allow data to persist across:

- Container restarts
- Container removal

Volumes can also be shared between containers.

### Simple Diagram

```text
Without Volume:

Container
   ↓
Data
   ↓
Container Removed
   ↓
Data Lost


With Volume:

Container
   ↓
Volume
   ↓
Persistent Data
```

### Interview Answer

> **Docker volumes are used for persistent storage. Since container data is normally ephemeral, volumes allow data to survive container restarts or container removal and can also be shared between containers.**

### Memory Trick

**Volume = DATA SURVIVAL**

---

# 12. Docker Swarm and Kubernetes

## 12.1 Docker Swarm

Docker Swarm is Docker's native orchestration tool for managing clusters of Docker hosts/nodes.

It allows you to:

- Deploy applications
- Manage applications
- Scale applications

across a cluster of machines.

### Remember

**Swarm = Docker's Native Orchestration**

---

## 12.2 Kubernetes

Kubernetes is a container orchestration platform used to automate:

- Deployment
- Scaling
- Operations

of application containers.

The source notes that Kubernetes can be used with Docker, while Docker is being replaced as the default container runtime in some environments.

### Interview Answer

> **Docker Swarm is Docker's native orchestration solution, while Kubernetes is a broader container orchestration platform used to automate deployment, scaling, and operations of containerized applications.**

### Memory Trick

**Docker = Container Platform**

**Swarm/Kubernetes = Orchestration**

---

# 13. Benefits of Docker

The source gives five major benefits.

---

## 13.1 Portability

Containers can run consistently regardless of the host system.

### Remember

**Portability = RUN ANYWHERE DOCKER IS AVAILABLE**

---

## 13.2 Efficiency

Containers are lightweight and start quickly.

### Remember

**Efficiency = LIGHT + FAST**

---

## 13.3 Isolation

Applications and services run in isolated environments.

This helps reduce dependency conflicts.

### Remember

**Isolation = FEWER CONFLICTS**

---

## 13.4 Version Control

Docker images can be versioned.

This makes it possible to roll back to previous versions.

### Remember

**Versioning = EASY ROLLBACK**

---

## 13.5 CI/CD Integration

Docker integrates well with continuous:

- Integration
- Deployment

pipelines.

### Interview Answer

> **Docker provides portability, efficiency, isolation, image versioning, rollback capability, and strong integration with CI/CD pipelines.**

### Memory Trick

**PEIVC**

- **P**ortability
- **E**fficiency
- **I**solation
- **V**ersion Control
- **C**I/CD

---

# 14. Common Docker Commands

The source lists these common commands.

| Command | Purpose |
|---|---|
| `docker build` | Builds an image from a Dockerfile |
| `docker run` | Runs a container from an image |
| `docker ps` | Lists running containers |
| `docker stop` | Stops a running container |
| `docker rm` | Removes a stopped container |
| `docker pull` | Pulls an image from a registry |
| `docker push` | Pushes an image to a registry |

### Memory Trick

```text
build → Image
run   → Container
ps    → Check
stop  → Stop
rm    → Remove Container
pull  → Registry → Local
push  → Local → Registry
```

---

# 15. Use Cases for Docker

## 15.1 Microservices

Docker is commonly used in microservice architectures.

Each service can run in its own container.

```text
Application
    |
    +--- User Service → Container
    |
    +--- Order Service → Container
    |
    +--- Payment Service → Container
```

### Interview Answer

> **Docker is useful for microservices because each service can run in an isolated container with its own dependencies.**

---

## 15.2 DevOps & CI/CD

Docker containers can be integrated into CI/CD pipelines.

This helps provide consistent environments for:

- Testing
- Production

### Interview Answer

> **Docker integrates well with CI/CD because the same containerized environment can be used consistently across testing and production stages.**

---

## 15.3 Cloud Deployment

Docker is widely used in cloud environments for:

- Application deployment
- Scaling

### Interview Answer

> **Docker is commonly used in cloud environments to package, deploy, and scale applications.**

---

## 15.4 Environment Consistency

Docker helps keep environments consistent across:

- Development
- Testing
- Production

### Memory Trick

**Use Cases = MICC**

- **M**icroservices
- **I**ntegrated CI/CD
- **C**loud deployment
- **C**onsistent environments

---

# 16. Docker Conclusion

Docker simplifies the process of:

- Developing applications
- Shipping applications
- Running applications

by using containers.

It makes it easier to:

- Manage dependencies
- Scale applications
- Maintain consistent environments

across different stages of the software lifecycle.

### Interview Answer

> **Docker simplifies developing, shipping, and running applications by packaging them into containers. This helps manage dependencies, improve consistency, and support application scaling across different environments.**

---

# 17. Docker Command Sequence

The source includes a practical command sequence.

> **Note:** `bash` shown before a command means the command is intended to be run in a Bash terminal. `yaml` indicates a YAML script.

---

## 17.1 Install Docker on Ubuntu

```bash
sudo apt update
sudo apt install docker.io
sudo systemctl enable --now docker
```

### What this does

1. Updates package information
2. Installs Docker
3. Enables and starts Docker

---

# 18. Verify Docker Installation

Check Docker version:

```bash
docker --version
```

### Interview/Practical Point

Use this to verify that Docker is installed and available from the command line.

---

# 19. Check Docker Service Status

```bash
sudo systemctl status docker
```

This checks whether the Docker service is running.

---

# 20. Pull Nginx Image

Pull the Nginx image from Docker Hub:

```bash
docker pull nginx
```

### Flow

```text
Docker Hub
    ↓
docker pull nginx
    ↓
Local Machine
```

---

# 21. List Docker Images

```bash
docker images
```

This lists Docker images available on your local system.

---

# 22. Run Nginx Container Interactively

```bash
docker run -it nginx /bin/bash
```

### Understand

- `docker run` → create/start container
- `-i` → interactive
- `-t` → terminal
- `nginx` → image
- `/bin/bash` → command to execute

### Memory Trick

**`-it` = INTERACTIVE TERMINAL**

---

# 23. Run Nginx in Detached Mode

```bash
docker run -d --name nginx-container nginx
```

### Understand

- `-d` → detached/background mode
- `--name nginx-container` → assigns container name
- `nginx` → image

### Memory Trick

**`-d` = DETACHED**

---

# 24. List Running Containers

```bash
docker ps
```

Shows running containers.

---

# 25. List All Containers

```bash
docker ps -a
```

Shows:

- Running containers
- Stopped containers

### Memory Trick

```text
docker ps    → Running
docker ps -a → All
```

---

# 26. Stop a Running Container

```bash
docker stop nginx-container
```

Stops the running Nginx container.

---

# 27. Start a Stopped Container

```bash
docker start nginx-container
```

Starts the stopped container again.

### Memory Trick

```text
stop  → Running → Stopped
start → Stopped → Running
```

---

# 28. Remove a Container

Make sure the container is stopped first.

```bash
docker rm nginx-container
```

### Important

`docker rm` removes a **container**.

It does not remove an image.

---

# 29. Remove an Image

```bash
docker rmi nginx
```

### Remember

```text
rm  → Container
rmi → Image
```

---

# 30. Build a Custom Image

If you have a Dockerfile:

```bash
docker build -t nginx-image .
```

### Understand

- `docker build` → build image
- `-t` → tag/name the image
- `nginx-image` → image name/tag
- `.` → current directory as build context

### Tags

Tags are useful for:

- Naming images
- Versioning images

Example:

```text
nginx-image:v1
nginx-image:v2
```

### Interview Answer

> **I use `docker build -t image-name .` to build an image from the Dockerfile in the current directory and assign it a name/tag.**

---

# 31. Tag a Custom Image

```bash
docker tag nginx-image repo/nginx-image:v1
```

This gives the image a repository/tag name.

### Understand

```text
repo/nginx-image:v1
     │          │
     │          └── Tag / Version
     └───────────── Repository/Image name
```

### Memory Trick

**Tag = NAME + VERSION**

---

# 32. Login to Docker Registry

```bash
docker login
```

This logs in to the Docker registry.

---

# 33. Push Custom Image

After logging in:

```bash
docker push repo/nginx-image:v1
```

### Flow

```text
Local Image
     ↓
docker push
     ↓
Registry
```

### Interview Answer

> **I tag the image with the repository name and version, log in to the registry, and then push the image using `docker push`.**

---

# 34. Inspect a Container

```bash
docker inspect nginx-container
```

This is used to inspect the Nginx container.

### Remember

**inspect = DETAILED INFORMATION**

---

# 35. View Container Logs

```bash
docker logs nginx-container
```

This displays logs from the Nginx container.

### Remember

**logs = WHAT HAPPENED INSIDE**

---

# 36. Volume Mapping

The source gives this example:

```bash
docker run -d -v /path/to/host/directory:/usr/share/nginx/html -p 8080:80 nginx
```

This maps a host directory to the Nginx directory inside the container.

### Understand

```text
Host Directory
      ↓
     -v
      ↓
Container Directory
/usr/share/nginx/html
```

### Memory Trick

**`-v` = VOLUME / DIRECTORY MAPPING**

---

# 37. Port Mapping

The source gives:

```bash
docker run -d -p 8080:80 nginx
```

This maps:

```text
Host Port 8080
       ↓
Container Port 80
```

### Memory Trick

**`-p` = PORT MAPPING**

---

# 38. Interact with a Running Container

```bash
docker exec -it nginx-container /bin/bash
```

This opens an interactive Bash shell inside the running Nginx container.

### Understand

- `docker exec` → execute a command in a running container
- `-it` → interactive terminal
- `nginx-container` → container
- `/bin/bash` → shell

### Interview Answer

> **I use `docker exec -it <container> /bin/bash` when I need to enter a running container and inspect or troubleshoot it interactively.**

### Memory Trick

**exec = ENTER / EXECUTE INSIDE RUNNING CONTAINER**

---

# 39. Complete Practical Docker Flow

Remember this practical sequence:

```text
1. Install Docker
       ↓
2. Verify Docker
       ↓
3. Pull Image
       ↓
4. Check Images
       ↓
5. Run Container
       ↓
6. Check Container
       ↓
7. Stop / Start
       ↓
8. Remove Container
       ↓
9. Build Custom Image
       ↓
10. Tag Image
       ↓
11. Login Registry
       ↓
12. Push Image
       ↓
13. Inspect
       ↓
14. Check Logs
       ↓
15. Volume Mapping
       ↓
16. Port Mapping
       ↓
17. Exec into Container
```

---

# 40. Docker Command Cheat Sheet

| Command | Easy Meaning |
|---|---|
| `docker --version` | Docker version |
| `docker pull nginx` | Download image |
| `docker images` | List images |
| `docker run nginx` | Run container |
| `docker run -it nginx /bin/bash` | Run interactively |
| `docker run -d --name nginx-container nginx` | Run in background |
| `docker ps` | Running containers |
| `docker ps -a` | All containers |
| `docker stop nginx-container` | Stop container |
| `docker start nginx-container` | Start container |
| `docker rm nginx-container` | Remove container |
| `docker rmi nginx` | Remove image |
| `docker build -t nginx-image .` | Build image |
| `docker tag nginx-image repo/nginx-image:v1` | Tag image |
| `docker login` | Login to registry |
| `docker push repo/nginx-image:v1` | Push image |
| `docker inspect nginx-container` | Inspect container |
| `docker logs nginx-container` | View logs |
| `docker exec -it nginx-container /bin/bash` | Enter running container |
| `docker run -d -p 8080:80 nginx` | Port mapping |
| `docker run -d -v host:container nginx` | Volume mapping |

---

# 41. Docker Cleanup Commands — Page 7

The final page of the source contains cleanup/prune commands.

## `docker system prune`

```bash
docker system prune
```

Removes:

- Stopped containers
- Unused networks
- Dangling images
- Unused volumes

---

## `docker system prune -a`

```bash
docker system prune -a
```

More aggressive cleanup.

It removes unused images, not only dangling images.

---

## `docker container prune`

```bash
docker container prune
```

Removes stopped containers.

---

## `docker image prune`

```bash
docker image prune
```

Removes dangling images.

---

## `docker image prune -a`

```bash
docker image prune -a
```

Removes unused images, including non-dangling unused images.

---

## `docker volume prune`

```bash
docker volume prune
```

Removes unused volumes.

---

## `docker network prune`

```bash
docker network prune
```

Removes unused networks.

---

## `docker builder prune`

```bash
docker builder prune
```

Removes build cache used during image builds.

### Cleanup Memory Trick

```text
system   → Overall cleanup
container → Containers
image     → Images
volume    → Volumes
network   → Networks
builder   → Build cache
```

### Important Interview Point

Be careful with:

```bash
docker system prune -a
```

It is more aggressive and can remove unused resources you may still want.

---

# 42. Important Docker Relationships

## Image vs Container

```text
Image
  ↓ docker run
Container
```

### Image

- Read-only template
- Contains application/runtime/dependencies
- Used to create containers

### Container

- Running/created instance of an image
- Isolated environment
- Runs the application

### Interview Answer

> **An image is a read-only template, while a container is an instance created from that image.**

### Memory Trick

**IMAGE = BLUEPRINT**

**CONTAINER = RUNNING INSTANCE**

---

# 43. Dockerfile vs Image vs Container

```text
Dockerfile
    ↓ docker build
Image
    ↓ docker run
Container
```

Remember:

- Dockerfile → Instructions
- Image → Template
- Container → Running instance

### Interview Answer

> **Dockerfile contains build instructions, the image is the resulting read-only template, and the container is created from that image to run the application.**

---

# 44. Registry vs Local Docker

```text
                 Registry
                /        \
             pull        push
              ↓            ↑
        Local Docker Engine
              ↓
           Image
              ↓
          Container
```

Remember:

- `pull` → Registry to local
- `push` → Local to registry

---

# 45. Volume vs Container Storage

```text
Container
    |
    | without volume
    ↓
Ephemeral Data
    ↓
Container Removed
    ↓
Data Lost
```

With volume:

```text
Container
    |
    ↓
Volume
    |
    ↓
Persistent Data
```

### Interview Answer

> **I use volumes when application data needs to survive the lifecycle of the container.**

---

# 46. Port Mapping — Easy Understanding

Suppose Nginx listens inside the container on:

```text
80
```

We expose it on the host as:

```text
8080
```

Command:

```bash
docker run -d -p 8080:80 nginx
```

Think:

```text
HOST                  CONTAINER

8080  ─────────────→   80
```

### Memory Trick

**LEFT = HOST**

**RIGHT = CONTAINER**

---

# 47. Volume Mapping — Easy Understanding

Command:

```bash
docker run -d \
-v /path/to/host/directory:/usr/share/nginx/html \
nginx
```

Think:

```text
HOST DIRECTORY
      ↓
     -v
      ↓
CONTAINER DIRECTORY
```

### Memory Trick

**LEFT = HOST**

**RIGHT = CONTAINER**

---

# 48. `docker run` — Important Options

## Interactive

```bash
docker run -it nginx /bin/bash
```

**`-it` = Interactive Terminal**

---

## Detached

```bash
docker run -d nginx
```

**`-d` = Detached/background**

---

## Name

```bash
docker run -d --name nginx-container nginx
```

**`--name` = Container Name**

---

## Port

```bash
docker run -d -p 8080:80 nginx
```

**`-p` = Port Mapping**

---

## Volume

```bash
docker run -d -v host-path:container-path nginx
```

**`-v` = Volume/Directory Mapping**

---

# 49. One-Minute Interview Revision

If the interviewer asks:

> **“Tell me about Docker.”**

Use this:

> **Docker is an open-source platform used to package, deploy, and run applications in lightweight and portable containers. A container packages the application and its dependencies in an isolated environment and shares the host OS kernel, which makes it lighter than a traditional VM. A Dockerfile contains instructions to build an image, and an image is a read-only template used to create containers. Docker Engine runs containers, while Docker Compose helps manage multi-container applications. Docker registries such as Docker Hub store images. Docker also provides networking and volumes for communication and persistent storage. Docker is widely used in microservices, CI/CD, cloud deployment, and environment consistency.**

---

# 50. Fast Docker Memory Map

| Concept | Remember As | Key Point |
|---|---|---|
| Docker | **PLATFORM** | Containers |
| Container | **RUNNING ENVIRONMENT** | Isolated + portable |
| Dockerfile | **INSTRUCTIONS** | Builds image |
| Image | **BLUEPRINT** | Creates containers |
| Engine | **RUNNER** | Runs containers |
| CLI | **COMMAND** | User interaction |
| API | **PROGRAMMATIC ACCESS** | External programs |
| Compose | **MULTI-CONTAINER** | YAML |
| Registry | **IMAGE STORAGE** | Push/Pull |
| Network | **COMMUNICATION** | Container connectivity |
| Volume | **PERSISTENCE** | Data survives |
| Swarm | **DOCKER ORCHESTRATION** | Cluster |
| Kubernetes | **CONTAINER ORCHESTRATION** | Deployment/scaling |
| `docker build` | **BUILD** | Image |
| `docker run` | **RUN** | Container |
| `docker ps` | **CHECK** | Containers |
| `docker pull` | **DOWNLOAD** | Registry → Local |
| `docker push` | **UPLOAD** | Local → Registry |
| `docker exec` | **ENTER** | Running container |

---

# 51. Interview Traps to Avoid

## Trap 1 — Image vs Container

Wrong:

> Image is the running application.

Correct:

> Image is a read-only template; container is created from the image.

---

## Trap 2 — Dockerfile vs Image

Wrong:

> Dockerfile is the image.

Correct:

> Dockerfile contains instructions used to build an image.

---

## Trap 3 — Container vs VM

The source emphasizes:

- Containers share the host OS kernel
- Containers are lightweight
- Containers are isolated
- VMs are traditional virtual machines

### Interview Line

> **Containers share the host OS kernel and are therefore generally more lightweight than traditional virtual machines.**

---

## Trap 4 — Volume

Do not say:

> Container data is always permanent.

The source explicitly says container data is ephemeral by default.

Use a volume when persistence is required.

---

## Trap 5 — `docker ps` vs `docker ps -a`

```text
docker ps    → Running containers
docker ps -a → All containers
```

---

## Trap 6 — `docker rm` vs `docker rmi`

```text
docker rm  → Container
docker rmi → Image
```

---

## Trap 7 — Pull vs Push

```text
pull → Registry → Local
push → Local → Registry
```

---

## Trap 8 — Port Mapping

For:

```bash
-p 8080:80
```

Remember:

```text
8080 = Host
80   = Container
```

---

## Trap 9 — Volume Mapping

For:

```bash
-v host-path:container-path
```

Remember:

```text
LEFT  = Host
RIGHT = Container
```

---

## Trap 10 — `exec`

```bash
docker exec -it nginx-container /bin/bash
```

This is used to execute a command inside a **running container**.

---

# 52. Complete Docker Mental Model

```text
                         DOCKER
                            |
                            ↓
                  Container Platform
                            |
              +-------------+-------------+
              |                           |
              ↓                           ↓
          Dockerfile                   Registry
              |                       Docker Hub
              ↓                           |
            BUILD                         pull/push
              ↓                           |
            IMAGE <------------------------+
              |
            docker run
              ↓
          CONTAINER
              |
       +------+------+------+
       |      |      |      |
       ↓      ↓      ↓      ↓
    Network Volume Ports  Logs
       |
       ↓
 Communication
```

---

# 53. Complete Docker Lifecycle

```text
Write Dockerfile
       ↓
docker build
       ↓
Create Image
       ↓
docker tag
       ↓
docker login
       ↓
docker push
       ↓
Registry
       ↓
docker pull
       ↓
docker run
       ↓
Container
       ↓
docker ps
       ↓
docker logs / inspect / exec
       ↓
docker stop
       ↓
docker start
       ↓
docker rm
       ↓
Cleanup / prune
```

---

# 54. Final Interview Formula

For almost any basic Docker question, remember:

```text
WHAT?
  ↓
Docker is a container platform.

WHY?
  ↓
Portability + Efficiency + Isolation + Versioning + CI/CD.

CONTAINER?
  ↓
Isolated application environment.

DOCKERFILE?
  ↓
Instructions to build an image.

IMAGE?
  ↓
Read-only template.

CONTAINER?
  ↓
Instance created from image.

ENGINE?
  ↓
Runs containers.

COMPOSE?
  ↓
Multiple containers.

REGISTRY?
  ↓
Stores images.

NETWORK?
  ↓
Container communication.

VOLUME?
  ↓
Persistent data.

ORCHESTRATION?
  ↓
Swarm / Kubernetes.

PRACTICAL?
  ↓
Pull → Run → Check → Stop → Remove
```

---

# 55. Final 30-Second Revision

```text
Docker
= Container Platform

Container
= Isolated + Lightweight + Portable Environment

Dockerfile
= Build Instructions

Image
= Read-only Blueprint

Container
= Image Instance

Engine
= Runs Containers

Compose
= Multi-container Applications

Registry
= Stores Images

Network
= Communication

Volume
= Persistent Data

Swarm/Kubernetes
= Orchestration

Important Commands:
pull
images
build
run
ps
stop
start
rm
rmi
tag
login
push
inspect
logs
exec
```

> **If you remember only one sentence:**
>
> **“Docker packages an application and its dependencies into an image, runs that image as a container, uses networks for communication, volumes for persistent data, registries for image storage, and Compose/orchestration tools for managing larger applications.”**

---

# 56. Source Coverage Check — Start to End

This document intentionally covers the topics present throughout the uploaded 7-page PATHNEX Docker document:

- Docker definition
- Containers
- Container packaging
- Isolation
- Portability
- Shared OS kernel
- Dockerfile
- Dockerfile instructions
- Dockerfile example
- Images
- Read-only image template
- Base images
- Custom images
- Docker Hub
- Docker Engine
- Docker daemon
- Containerd note from source
- Docker CLI
- REST API
- Docker Compose
- `docker-compose.yml`
- Multi-container applications
- Registry
- Docker Hub
- Private registries
- Push and pull
- Networking
- Network isolation
- Bridge
- Host
- Overlay
- None
- Volumes
- Persistent storage
- Docker Swarm
- Kubernetes
- Docker benefits
- Portability
- Efficiency
- Isolation
- Version control
- CI/CD integration
- Common Docker commands
- Microservices
- DevOps/CI/CD
- Cloud deployment
- Environment consistency
- Conclusion
- Ubuntu installation commands
- Docker version
- Docker service status
- Pull Nginx
- List images
- Interactive Nginx container
- Detached Nginx container
- List running containers
- List all containers
- Stop container
- Start container
- Remove container
- Remove image
- Build custom image
- Image tags
- Tag custom image
- Docker login
- Push image
- Inspect container
- View logs
- Volume mapping
- Port mapping
- `docker exec`
- System cleanup
- Container cleanup
- Image cleanup
- Volume cleanup
- Network cleanup
- Builder cache cleanup

The final page of the source also contains the cleanup/prune command table, and those commands are included above.

---

# FINAL MASTER MEMORY

```text
DOCKER

Docker
  ↓
Container Platform
  ↓
Dockerfile
  ↓
Build
  ↓
Image
  ↓
Run
  ↓
Container
  ↓
Network + Volume + Ports
  ↓
Logs + Inspect + Exec
  ↓
Registry
  ↓
Push / Pull
  ↓
Compose / Swarm / Kubernetes
  ↓
CI/CD + Microservices + Cloud
```

> **Master line:**
>
> **Dockerfile BUILDS the image, image CREATES the container, container RUNS the application, network CONNECTS it, volume PRESERVES data, registry STORES the image, and Compose/orchestration MANAGES multiple containers.**

