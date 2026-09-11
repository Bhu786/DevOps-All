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
 A Dockerfile is a text file containing instructions to build a Docker image.
### 44. What is `FROM`?
FROM Dockerfile ki starting point hai.
=> Jab Docker image banata hai, Docker ko pehle ek base environment chahiye hota hai. FROM batata hai ki kis existing image se start karna hai.

Bilkul simple way mein:

### `FROM` kya hai?

`FROM` Dockerfile ki **starting point** hai.

Jab Docker image banata hai, Docker ko pehle ek **base environment** chahiye hota hai. `FROM` batata hai ki **kis existing image se start karna hai**.

```dockerfile
FROM ubuntu:22.04
```

Matlab:

> "Meri image Ubuntu 22.04 se start karo."

---

### Kyu likhte hain?

Maan lo tumhari application Python mein hai.

Tum khud se ye sab setup nahi karna chahte:

```text
Linux
↓
Python install
↓
pip install
↓
Python dependencies
↓
Application
```

Instead:

```dockerfile
FROM python:3.12
```

Docker ko Python wala ready-made environment mil gaya.

Phir:

```dockerfile
FROM python:3.12

COPY app.py .
RUN pip install flask
CMD ["python", "app.py"]
```

So:

```text
Python Image
     ↓
   FROM
     ↓
Add your dependencies
     ↓
Add your application
     ↓
Docker Image
```

### `FROM` mein kya-kya likh sakte hain?

Usually **Docker image ka naam + optional tag**:

```dockerfile
FROM ubuntu
FROM ubuntu:22.04
FROM python:3.12
FROM node:22
FROM nginx:latest
FROM alpine:3.20
```

You can also use a **private/custom image**:

```dockerfile
FROM mycompany/base-image:1.0
```

---

### Important: `FROM` OS hi hona zaroori nahi

Ye common interview confusion hai.

```dockerfile
FROM ubuntu:22.04
```

→ Ubuntu-based image

```dockerfile
FROM python:3.12
```

→ Python environment wali image

```dockerfile
FROM nginx:latest
```

→ Nginx wali image

So **`FROM` ka matlab simply "base image choose karo."**

### Ek line mein yaad karo 🧠

**`FROM = Meri Docker image kis existing image se start hogi?`**

**Interview answer:**

> "`FROM` specifies the base image used to build a Docker image."


### 45. What is `WORKDIR`?
Container ke andar bata dena ki application ka kaam kis folder ke andar hoga.

Haan, **working directory set karna** simple language mein matlab hai:

> **Container ke andar bata dena ki application ka kaam kis folder ke andar hoga.**

### Example

```dockerfile
WORKDIR /app
```

Matlab Docker ko bol rahe ho:

> **"Container ke andar `/app` folder ko current/default folder maan lo."**

Ab agar:

```dockerfile
COPY app.py .
```

to `app.py` **`/app` ke andar** jayegi.

```text
Container
│
├── bin
├── etc
└── app          ← WORKDIR
    └── app.py
```

Aur agar:

```dockerfile
RUN python app.py
```

to Docker `/app` ke andar se `app.py` run karega.

### Iska main kaam kya hai?

`WORKDIR` basically **`cd` jaisa hai**, lekin Dockerfile ke liye permanent/default working location set karta hai.

```dockerfile
WORKDIR /app
```

ke baad:

```dockerfile
COPY . .
RUN ...
CMD ...
```

normally `/app` ko working directory maan kar operate karte hain.

### Yaad rakhna 🧠

**WORKDIR = "Container ke andar mera kaam kis folder mein hoga?"**

👉 **Interview:** "`WORKDIR` sets the default working directory for subsequent Dockerfile instructions and the container."
==============
`WORKDIR /app` mein **`/app` container ke andar hota hai**, tumhari local machine ke normal folder mein nahi.

### Example

Dockerfile:

```dockerfile
FROM ubuntu
WORKDIR /app
COPY . .
```

Jab image build hoti hai, Docker container/image ke filesystem mein `/app` directory create/use karta hai:

```text
Container
│
├── bin/
├── etc/
├── usr/
└── app/          ← Docker ne create/use kiya
    ├── app.py
    └── config/
```

### `/app` kaise banta hai?

Tumhe pehle manually folder banane ki zarurat nahi hai.

```dockerfile
WORKDIR /app
```

Docker **agar `/app` exist nahi karta, to automatically create kar deta hai**.

---

### Local machine par kya hai?

Maan lo tumhari local machine par:

```text
my-project/
├── Dockerfile
├── app.py
└── requirements.txt
```

Aur Dockerfile mein:

```dockerfile
WORKDIR /app
COPY . .
```

`COPY . .` ka matlab:

```text
Local machine                  Container

my-project/                    /app/
├── app.py       ──────────→   ├── app.py
├── Dockerfile   ──────────→   ├── Dockerfile
└── requirements  ─────────→   └── requirements.txt
```

So **local `my-project` aur container ka `/app` alag locations hain**.

### Sabse important 🧠

```text
WORKDIR /app
        ↓
Container ke andar /app folder
        ↓
Aage ki commands yahin se chalengi
```

**`/app` koi special Docker folder nahi hai.** Tum naam kuch bhi rakh sakte ho:

```dockerfile
WORKDIR /myapp
```

ya

```dockerfile
WORKDIR /usr/src/app
```

Bas convention ke taur par `/app` bahut commonly use hota hai.
=============
Haan, **`WORKDIR` ki zarurat mainly isliye hoti hai taaki container ke andar application ka ek fixed working folder ho.**

### Without `WORKDIR`

Tumhe baar-baar path dena padega:

```dockerfile
COPY app.py /app/app.py
RUN python /app/app.py
```

### With `WORKDIR`

```dockerfile
WORKDIR /app
COPY app.py .
RUN python app.py
```

Docker samajhta hai ki **ab `/app` hi current folder hai**.

### Real benefit

Agar application mein 20–30 files hain, toh har command mein `/app/...` likhne ki zarurat nahi.

```text
WORKDIR /app
     ↓
Application ka fixed folder
     ↓
COPY, RUN, CMD etc. easily kaam karte hain
```

🧠 **Yaad rakho:**
**`WORKDIR` = Container ke andar application ka "current/default folder" set karna.**

**Interview:** "`WORKDIR` provides a consistent working location for the application and subsequent Dockerfile instructions."

### 46. What is `COPY`?
### `COPY` kya hai?

`COPY` Dockerfile ka instruction hai jo **local machine ke files/folders ko Docker image ke andar copy karta hai**.

### Example

Local machine:

```text
my-project/
├── Dockerfile
├── app.py
└── config.txt
```

Dockerfile:

```dockerfile
FROM python:3.12
WORKDIR /app
COPY . .
```

`COPY . .` ka matlab:

> **Local project ki files ko container/image ke `/app` folder mein copy karo.**

```text
Local Machine              Docker Image/Container
     ↓                              ↓
my-project/                    /app/
├── app.py        ───────→     ├── app.py
├── config.txt    ───────→     └── config.txt
```

### Specific file bhi copy kar sakte ho

```dockerfile
COPY app.py /app/
```

Ya:

```dockerfile
COPY requirements.txt .
```

Yahan `.` ka matlab **current `WORKDIR`** hai.

### Important

`COPY` mainly **build time** par kaam karta hai.

```text
Dockerfile
   ↓
docker build
   ↓
COPY files
   ↓
Docker Image
   ↓
docker run
   ↓
Container
```

🧠 **Yaad rakho:**
**`COPY = Local machine se files/folders → Docker image ke andar`**
==============
copy image ki time chalta hai 

Haan, **exactly**. ✅

`COPY` **Docker image build karte time** chalta hai, `docker run` ke time nahi.

```text
Dockerfile
   ↓
docker build
   ↓
COPY runs here
   ↓
Docker Image
   ↓
docker run
   ↓
Container
```

Example:

```dockerfile
FROM python:3.12
WORKDIR /app
COPY . .
```

Jab tum:

```bash
docker build -t myapp .
```

karte ho, tab `COPY . .` local files ko image ke `/app` mein copy karta hai.

Phir:

```bash
docker run myapp
```

par woh already image mein copied files **container mein available** hoti hain.

🧠 **Shortcut:**
**COPY → `docker build` time**
**CMD/ENTRYPOINT → `docker run` time**
=============

### 47. What is `ADD`?
### `ADD` kya hai?

`ADD` bhi `COPY` ki tarah **files/folders ko Docker image ke andar copy** karta hai.

```dockerfile
ADD app.py /app/
```

Matlab:

```text
Local machine → Docker image → /app/app.py
```

### `ADD` aur `COPY` mein difference

**`COPY`** → Simple file/folder copy.

**`ADD`** → Copy ke saath kuch extra features bhi deta hai, jaise **local `.tar` archive ko automatically extract** karna.

Example:

```dockerfile
ADD app.tar /app/
```

Docker `.tar` ko `/app` mein extract kar sakta hai.

👉 **Best practice:** Normal files copy karne ke liye generally **`COPY` prefer** karo. `ADD` tab use karo jab uske special features actually chahiye.

🧠 **Yaad rakho:**
**COPY = simple copy**
**ADD = copy + extra features**

### 48. COPY vs ADD?
### `COPY` vs `ADD`

| `COPY`                                  | `ADD`                                            |
| --------------------------------------- | ------------------------------------------------ |
| Files/folders copy karta hai            | Files/folders copy karta hai                     |
| Simple & predictable                    | Extra features hain                              |
| `.tar` automatically extract nahi karta | Local `.tar` automatically extract kar sakta hai |
| Generally preferred                     | Special cases mein use                           |
| Easy to understand                      | More behavior                                    |

### Example

```dockerfile
COPY app.py /app/
```

Simple file copy.

```dockerfile
ADD app.tar /app/
```

`.tar` archive ko extract kar sakta hai.

🧠 **Interview shortcut:**

> **COPY = simple copy → preferred**
> **ADD = copy + extra features → only when needed**


### 49. What is `RUN`?
### `RUN` kya hai?

`RUN` Dockerfile mein **image build karte waqt command execute** karta hai.

Example:

```dockerfile
FROM ubuntu
RUN apt update
RUN apt install -y nginx
```

Matlab:

```text
docker build
    ↓
RUN apt update
    ↓
RUN nginx install
    ↓
Docker Image ready
```

### Iska kaam kya hai?

Image ke andar **software install, configuration, files create/update** karne ke liye.

Examples:

```dockerfile
RUN apt update
RUN pip install flask
RUN npm install
RUN mkdir /app/logs
```

### Important difference

`RUN` **container start hone par nahi**, **image build hone par** chalta hai.

```text
RUN        → docker build time
CMD        → docker run/start time
```

🧠 **Yaad rakho:**
**`RUN = Image banate waqt command chalao.`**

### 50. What is `CMD`?
### `CMD` kya hai?

`CMD` Dockerfile mein **default command** batata hai jo **container start hone par run hota hai**.

Example:

```dockerfile
FROM python:3.12
WORKDIR /app
COPY . .
CMD ["python", "app.py"]
```

Jab:

```bash
docker run myapp
```

hoga, Docker:

```text
Container start
     ↓
CMD execute
     ↓
python app.py
     ↓
Application running
```

### `RUN` vs `CMD`

🧠 **Sabse important:**

```text
RUN → Image BUILD karte time
CMD → Container START karte time
```

Example:

```dockerfile
RUN pip install flask      # Build time
CMD ["python", "app.py"]   # Container start time
```

### CMD ko override kar sakte hain?

**Haan.**

Dockerfile:

```dockerfile
CMD ["python", "app.py"]
```

Lekin:

```bash
docker run myapp python test.py
```

to `CMD` ki jagah `python test.py` chalega.

👉 **Interview line:**
**“CMD defines the default command that runs when a container starts, and it can be overridden at runtime.”**

### 51. What is `ENTRYPOINT`?
### `ENTRYPOINT` kya hai?

`ENTRYPOINT` container ka **main/default executable** set karta hai — yani container start hote hi **kaunsa program run hona chahiye**.

Example:

```dockerfile
FROM ubuntu
ENTRYPOINT ["echo"]
```

Run:

```bash
docker run myimage Hello
```

Output:

```text
Hello
```

Yahan `echo` **ENTRYPOINT** hai aur `Hello` usko argument mila.

### CMD vs ENTRYPOINT 🧠

```dockerfile
ENTRYPOINT ["python"]
CMD ["app.py"]
```

Run:

```bash
docker run myimage
```

→ `python app.py`

Agar:

```bash
docker run myimage test.py
```

→ `python test.py`

**Simple yaad rakho:**

* **ENTRYPOINT = main program/executable**
* **CMD = default argument/default command**

👉 **Interview line:** **“ENTRYPOINT defines the main executable of a container, while CMD provides default arguments or a default command that can be overridden.”**

### 52. CMD vs ENTRYPOINT?
### CMD vs ENTRYPOINT

| CMD                                              | ENTRYPOINT                                             |
| ------------------------------------------------ | ------------------------------------------------------ |
| Default command/arguments deta hai               | Main executable set karta hai                          |
| Runtime par easily override hota hai             | Normally main program fixed rakhta hai                 |
| Optional/default behavior ke liye                | Container ka primary purpose define karne ke liye      |
| `docker run image <new>` se replace ho sakta hai | `docker run image <new>` usually argument ban jata hai |

### Example

```dockerfile
ENTRYPOINT ["python"]
CMD ["app.py"]
```

Normal:

```bash
docker run myimage
```

➡️ `python app.py`

Override:

```bash
docker run myimage test.py
```

➡️ `python test.py`

### 🧠 Easy trick

**ENTRYPOINT = "Kya run karna hai?"**
**CMD = "Default mein kya dena hai?"**

👉 **Interview:**
**“ENTRYPOINT defines the main executable, while CMD provides default arguments or a default command that can be overridden.”**

### 53. What is `EXPOSE`?
### `EXPOSE` kya hai?

`EXPOSE` Dockerfile mein **batata hai ki container ke andar application kis port par listen karegi**.

Example:

```dockerfile
EXPOSE 8080
```

Matlab:

> **“Meri application container ke andar port 8080 par listen kar rahi hai.”**

### Important ⚠️

`EXPOSE` **port ko actually internet/host par open nahi karta**.

Port ko host se connect karne ke liye:

```bash
docker run -p 8080:8080 myapp
```

```text
Host:8080
    ↓
Container:8080
    ↓
Application
```

🧠 **Yaad rakho:**

**`EXPOSE` = documentation/metadata: container ka kaunsa port intended hai.**

**`-p` = actual port mapping.**

👉 **Interview line:**
**“EXPOSE documents the port on which a containerized application listens; it does not publish the port by itself.”**

### 54. Does `EXPOSE` actually publish a port?
**No. ❌ `EXPOSE` port ko publish nahi karta.**

```dockerfile
EXPOSE 8080
```

Sirf Docker ko batata hai:

> “Application container ke andar port `8080` par listen kar sakti hai.”

Actual port publish karne ke liye:

```bash
docker run -p 8080:8080 myapp
```

### 🧠 Yaad rakho

**EXPOSE → Inform/document**
**`-p` → Publish/map**

👉 **Interview:** “`EXPOSE` does not publish a port; `-p` is used to publish/map the container port to the host.”

### 55. `EXPOSE` vs `-p`?
### `EXPOSE` vs `-p`

| `EXPOSE`                               | `-p`                                          |
| -------------------------------------- | --------------------------------------------- |
| Dockerfile instruction                 | `docker run` option                           |
| Port ko **declare/document** karta hai | Port ko **publish/map** karta hai             |
| Actual traffic allow nahi karta        | Host se container tak traffic route karta hai |
| Build time metadata                    | Container run time par use                    |
| Example: `EXPOSE 8080`                 | Example: `-p 8080:8080`                       |

### Example

```dockerfile
EXPOSE 8080
```

➡️ **“Container app 8080 par listen karegi.”**

```bash
docker run -p 8080:8080 myapp
```

➡️ **“Host ke 8080 ko container ke 8080 se connect karo.”**

```text
Without -p:

Host ❌ → Container:8080

With -p:

Host:8080 → Container:8080 → App
```

🧠 **Shortcut:**

**`EXPOSE` = batana**
**`-p` = connect/publish karna**

### cmd vs entrypoint vs run vs copy 
| Instruction      | Kab chalta hai? | Kya karta hai?                          |
| ---------------- | --------------- | --------------------------------------- |
| **`COPY`**       | `docker build`  | Local files → image mein copy           |
| **`RUN`**        | `docker build`  | Image banate waqt command execute       |
| **`ENTRYPOINT`** | `docker run`    | Container ka main program set karta hai |
| **`CMD`**        | `docker run`    | Default command/arguments deta hai      |

### 56. What is `ENV`?
### `ENV` kya hai?

`ENV` Dockerfile mein **environment variable set** karta hai. Ye value container ke andar application use kar sakti hai.

Example:

```dockerfile
ENV APP_ENV=production
ENV PORT=8080
```

Ab container ke andar:

```text
APP_ENV = production
PORT    = 8080
```

Application in values ko read kar sakti hai.

### Kyu use karte hain?

Configuration ko code se alag rakhne ke liye.

Example:

```text
Development → APP_ENV=dev
Testing     → APP_ENV=test
Production  → APP_ENV=production
```

### Important

`ENV` se set ki gayi value **image ka part** ban sakti hai aur container mein available hoti hai.

⚠️ **Password/API key jaise secrets `ENV` mein hard-code nahi karne chahiye.**

🧠 **Yaad rakho:**
**`ENV = Container/application ke liye environment variable set karo.`**

**Interview:** "`ENV` sets environment variables that are available to subsequent build instructions and running containers."
### expose me bhi port de rahe env me bhi kon lega kya diff hai 
Haan, confusion natural hai — **`EXPOSE` mein bhi port number hai aur `ENV` mein bhi port number de sakte hain**, lekin dono ka **purpose alag** hai.

### Example

```dockerfile
EXPOSE 8080
ENV PORT=8080
```

Dono `8080` hain, but:

**`EXPOSE 8080`**
→ Docker ko batata hai:

> “Application **8080 port par listen karne ka intention** rakhti hai.”

**`ENV PORT=8080`**
→ **Application ko value deta hai:**

> “Tumhara port number `8080` hai.”

### Kaun use karega?

```text
EXPOSE 8080
     ↓
Docker / developer / networking metadata

ENV PORT=8080
     ↓
Application
```

Example application:

```python
app.run(port=os.getenv("PORT"))
```

Application `ENV` se `8080` read karegi.

### Aur actual traffic?

Uske liye:

```bash
docker run -p 8080:8080 myapp
```

```text
ENV PORT=8080
      ↓
Application listens on 8080

EXPOSE 8080
      ↓
Documents container port

-p 8080:8080
      ↓
Host:8080 → Container:8080
```

🧠 **3 cheezein yaad rakho:**

**ENV = Application ko configuration/value**
**EXPOSE = Container ka intended port/documentation**
**`-p` = Actual host-to-container port mapping**
=================
Haan — **almost koi bhi Linux command `RUN` mein technically chala sakte ho**, aur bahut si commands ko runtime par `CMD/ENTRYPOINT` se bhi chala sakte ho. **Lekin “kuch bhi, bas jagah alag” 100% sahi nahi hai.** Kuch kaam build-time ke hain, kuch runtime ke.

### Sabse important distinction

| Kaam                           |               Image build time (`RUN`) | Container runtime (`CMD/ENTRYPOINT`) | Typical choice |
| ------------------------------ | -------------------------------------: | -----------------------------------: | -------------- |
| `npm install`                  |                                      ✅ |                                    ✅ | Build          |
| `pip install`                  |                                      ✅ |                                    ✅ | Build          |
| `apt install curl`             |                                      ✅ |                          ⚠️ Possible | Build          |
| Files create karna             |                                      ✅ |                                    ✅ | Depends        |
| App compile/build karna        |                                      ✅ |                          ⚠️ Possible | Build          |
| `npm start`                    | ⚠️ Technically possible, usually wrong |                                    ✅ | Runtime        |
| Web server start karna         |                        ❌ Usually wrong |                                    ✅ | Runtime        |
| Database se connect karna      |                       ⚠️ Usually avoid |                                    ✅ | Runtime        |
| Runtime API call               |                       ⚠️ Usually avoid |                                    ✅ | Runtime        |
| Runtime config read karna      |             ❌ Can't know future values |                                    ✅ | Runtime        |
| Environment variable use karna |              Build-time value possible |                                    ✅ | Runtime        |
| Port listen karna              |                                      ❌ |                                    ✅ | Runtime        |
| User request serve karna       |                                      ❌ |                                    ✅ | Runtime        |
| Health endpoint serve karna    |                                      ❌ |                                    ✅ | Runtime        |

---

# 🧠 Best mental model

### Build time = **"Image ko ready karo"**

```dockerfile
RUN apt-get update
RUN npm ci
RUN npm run build
RUN mkdir /app/logs
```

Matlab:

> "Container banne se pehle jo preparation karni hai, kar do."

Result:

```text
Dockerfile
   ↓
docker build
   ↓
RUN commands
   ↓
Docker IMAGE
   ↓
Ready
```

---

### Runtime = **"Ready image se application chalao"**

```dockerfile
CMD ["npm", "start"]
```

Matlab:

> "Ab container start hua hai, application chalao."

```text
Docker IMAGE
    ↓
docker run
    ↓
CMD / ENTRYPOINT
    ↓
CONTAINER
    ↓
Application running
```

---

# 🔥 Example: `npm install`

Technically dono jagah possible:

### Build time — recommended

```dockerfile
FROM node:22-alpine

WORKDIR /app

COPY package*.json ./

RUN npm ci

COPY . .

CMD ["npm", "start"]
```

```text
BUILD:
npm ci
  ↓
dependencies image mein
  ↓
RUN complete

RUNTIME:
npm start
```

---

### Runtime — possible but usually bad

```dockerfile
FROM node:22-alpine

WORKDIR /app

COPY package*.json ./
COPY . .

CMD ["sh", "-c", "npm install && npm start"]
```

```text
BUILD:
Nothing installed

RUNTIME:
npm install
   ↓
npm start
```

Problem:

* Container start slow
* Registry/network required
* Runtime failure possible
* Every new container potentially installs dependencies again
* Reproducibility/cache benefit reduced

---

# ⚠️ Ek important case: Runtime information

Suppose:

```dockerfile
ENV DB_HOST=localhost
```

Ye image mein default configuration rakh sakta hai.

But actual production DB:

```bash
docker run -e DB_HOST=prod-db myimage
```

Ye value **runtime par** milti hai.

Isliye:

```text
Build time:
"Image kaise banegi?"

Runtime:
"Ye particular environment mein kaise chalegi?"
```

---

# ⭐ Kuch cheezein runtime par hi meaningful hain

Example:

```dockerfile
CMD ["npm", "start"]
```

Application ko database chahiye:

```text
Container starts
      ↓
Application starts
      ↓
DB se connect
      ↓
Requests serve
```

Build ke waqt production DB se connect karna generally **wrong design** hai.

---

# ⭐ Kuch cheezein build time par hi honi chahiye

Example:

```dockerfile
RUN npm run build
```

Suppose React application:

```text
Source code
    ↓
npm run build
    ↓
dist/
    ↓
Image
```

Runtime par tum generally source compile nahi karna chahte.

---

# 🔥 Aur ek bahut important distinction

`RUN` **sirf "build-time command" hone ki wajah se special nahi hai**.

Actually:

```dockerfile
RUN <command>
```

Docker build ke time ek temporary container/layer mein command execute karta hai aur resulting filesystem changes image layer mein capture karta hai.

Whereas:

```dockerfile
CMD [...]
```

**command execute nahi karta during build**.

It tells Docker:

> "Container start hoga to default mein ye command chalana."

---

# Final rule — interview mein ye bolo

> **Technically many commands can be executed at either build time or runtime, but they serve different purposes. Build-time operations prepare an immutable, reusable image; runtime operations start and configure the application for its actual environment.**

### Yaad karne ke liye:

```text
BUILD TIME
──────────
Install
Compile
Build
Create files/directories
Copy application
Set image filesystem
       ↓
     IMAGE
       ↓
RUNTIME
────────
Start application
Listen on port
Connect to DB
Read runtime config
Process requests
Handle traffic
       ↓
   CONTAINER
```

**Isliye “kuch bhi kar sakte hain, bas jagah alag hai” ko interview mein mat bolna.** Better line hai: **“Many commands are technically possible in both, but we choose build vs runtime based on whether the operation prepares the image or depends on the running environment.”**
=================
### 57. What is `ARG`?
### What is `ARG` in Docker?

`ARG` stands for **Argument**. It is used to define a **variable that is available during Docker image build time**.

```dockerfile
ARG APP_VERSION=1.0
RUN echo "Building version $APP_VERSION"
```

Build it with:

```bash
docker build --build-arg APP_VERSION=2.0 -t myapp .
```

Now during the build, `APP_VERSION` will be `2.0`.

### `ARG` vs `ENV`

| `ARG`                                  | `ENV`                              |
| -------------------------------------- | ---------------------------------- |
| Build-time variable                    | Runtime environment variable       |
| Mainly available during `docker build` | Available inside running container |
| Can be passed using `--build-arg`      | Can be set using `-e`              |
| Not normally available after build     | Available when container runs      |

Example:

```dockerfile
ARG VERSION=1.0
ENV APP_ENV=production

RUN echo $VERSION
```

🧠 **Yaad rakho:**

**`ARG` → Build ke time value**
**`ENV` → Container/Application run time value**

👉 **Interview line:**

> "`ARG` defines build-time variables that can be passed to Docker during image creation using `--build-arg`."

### 58. ARG vs ENV?
## `ARG` vs `ENV` in Docker

Simple difference:

**`ARG` = Build time**
**`ENV` = Runtime**

|                                     | `ARG`                        | `ENV`                   |
| ----------------------------------- | ---------------------------- | ----------------------- |
| Full form                           | Argument                     | Environment Variable    |
| Used when?                          | `docker build`               | Container runtime       |
| Set using                           | `--build-arg`                | `-e` / Dockerfile `ENV` |
| Available during build?             | ✅ Yes                        | ✅ Yes                   |
| Available inside running container? | ❌ Not by default             | ✅ Yes                   |
| Typical use                         | Version, build configuration | App configuration       |
| Secret?                             | ❌ Don't use for secrets      | ❌ Don't use for secrets |

### Example

```dockerfile
FROM python:3.12

ARG APP_VERSION=1.0

ENV APP_ENV=production

RUN echo "Building version $APP_VERSION"

CMD ["python", "app.py"]
```

Build:

```bash
docker build --build-arg APP_VERSION=2.0 -t myapp .
```

Here:

* `APP_VERSION=2.0` → used **while building the image**
* `APP_ENV=production` → available **when the container runs**

### Easy real-life example

Suppose you're building an application:

```text
ARG VERSION=2.0
```

means:

> "Build this image using version 2.0."

```text
ENV APP_ENV=production
```

means:

> "When the application runs, run it in production environment."

### 🧠 Best shortcut

> **ARG → Build configuration**
> **ENV → Application/Runtime configuration**

👉 **Interview line:**
**"`ARG` is for build-time variables, whereas `ENV` is for environment variables available to the running container."**
### arguments and env variable me kya diff hai 
Simple language mein:

### 1. Argument kya hota hai?

**Argument = kisi command/program ko input dena.**

Example:

```bash
docker build --build-arg VERSION=2.0 .
```

Yahan `VERSION=2.0` ek **argument** hai.

Matlab:

> "Docker ko build karte time ye value de do."

Ye mainly **build ke time** use hota hai.

---

### 2. Environment variable kya hota hai?

**Environment variable = application ke environment mein ek value store karna**, jise application runtime par read kar sakti hai.

Example:

```bash
docker run -e APP_ENV=production myapp
```

Application ke andar:

```text
APP_ENV = production
```

Matlab:

> "Jab application chale, usko batao ki environment production hai."

---

### Real-life example

Socho tum restaurant mein ho:

**Argument:**

> Customer order dete waqt bolta hai: "Pizza large banana."

→ Ek specific command/input ke saath value di.

**Environment variable:**

> Restaurant ke system mein `LOCATION=Delhi` already configured hai.

→ System/application jab bhi chale, wo value use kar sakta hai.

### Docker mein 🧠

```text
ARG → Docker build ko input
ENV → Running application ko configuration
```

Example:

```dockerfile
ARG VERSION=2.0
ENV APP_ENV=production
```

**Interview line:**

> **Argument is an input passed to a command/build, while an environment variable is a named value available to a process/application in its environment.**

### 59. What is `USER`?
## What is `USER` in Docker?

`USER` Dockerfile instruction **decides which Linux user will run commands/processes inside the container**.

### Example

```dockerfile
FROM ubuntu:22.04

RUN useradd -m appuser

USER appuser

CMD ["./app.sh"]
```

Here:

```text
USER appuser
     ↓
Container ka main application
     ↓
appuser ke permissions se chalega
```

### Why use `USER`?

Main reason = **security**.

By default, many containers run as **root** user, which has high privileges.

Instead:

```dockerfile
USER appuser
```

runs the application as a **non-root user**, reducing the impact if the application is compromised.

### 🧠 Yaad rakho

> **`USER` = Container ke andar application kis user ke naam/permission se chalegi.**

👉 **Interview line:**

> "`USER` specifies the user or UID that will be used to run subsequent Dockerfile instructions and the container's main process."

### 60. What is `VOLUME`?
## What is `VOLUME` in Docker?

`VOLUME` is used to create a **persistent storage location** for a container.

Normally, container ke andar jo data create/change hota hai, **container delete hone par lost ho sakta hai**.

`VOLUME` ka purpose hai:

> **Container ke important data ko container lifecycle se separate rakhna.**

### Example

```dockerfile
FROM mysql:8

VOLUME /var/lib/mysql
```

MySQL ka data `/var/lib/mysql` mein store hoga, aur Docker us location ko persistent volume ke saath manage kar sakta hai.

### Without Volume

```text
Container
   |
   └── Application data
            ↓
      Container deleted
            ↓
         Data lost ❌
```

### With Volume

```text
Container
   |
   └── /data
        |
        ↓
     Docker Volume
        |
        ↓
    Data remains ✅
```

### Important difference

```dockerfile
VOLUME /data
```

**`VOLUME` → Dockerfile mein storage location declare karta hai.**

While:

```bash
docker run -v mydata:/data myapp
```

**`-v` → actual volume ko container ke `/data` se mount karta hai.**

### 🧠 Yaad rakho

> **Volume = Container ke bahar persistent data storage.**

👉 **Interview line:**

> "`VOLUME` declares a mount point for persistent data so that the data can survive beyond the container's lifecycle."

### 61. What is `HEALTHCHECK`?
## What is `HEALTHCHECK` in Docker?

`HEALTHCHECK` Docker ko batata hai ki **container ke andar application actually healthy hai ya nahi**.

Container running hona ≠ application healthy hona.

### Example

```dockerfile
FROM nginx

HEALTHCHECK --interval=30s --timeout=5s \
  CMD curl -f http://localhost:80/ || exit 1
```

Docker har **30 seconds** check karega:

```text
Container running?
       ↓
   Healthcheck
       ↓
Application responding?
   ↓           ↓
  YES          NO
healthy      unhealthy
```

### Status kaise dekhein?

```bash
docker ps
```

Example:

```text
Up 2 minutes (healthy)
```

or

```text
Up 2 minutes (unhealthy)
```

Detailed information:

```bash
docker inspect <container>
```

### Important point

`HEALTHCHECK` **container ko restart nahi karta by itself**.

It mainly reports:

```text
healthy / unhealthy
```

Orchestration systems such as Kubernetes have their own **liveness/readiness probes** for deciding what action to take.

### 🧠 Yaad rakho

> **HEALTHCHECK = "Container ke andar application sach mein healthy hai?"**

👉 **Interview line:**

> "`HEALTHCHECK` defines a command that Docker periodically runs to determine whether a container's application is healthy."

### 62. What is `SHELL`?
## What is `SHELL` in Docker?

`SHELL` Dockerfile instruction **defines which shell Docker should use to execute shell-form commands** such as `RUN`.

### Example — Linux

```dockerfile
FROM ubuntu:22.04

SHELL ["/bin/bash", "-c"]

RUN echo $SHELL
RUN source /etc/profile && echo "Hello"
```

Here Docker will use **Bash** instead of the default `/bin/sh`.

### Windows example

```dockerfile
SHELL ["cmd", "/S", "/C"]
```

or:

```dockerfile
SHELL ["powershell", "-Command"]
```

So basically:

```text
SHELL
  ↓
Which shell should execute commands?
  ↓
RUN command
```

### Why use it?

When you specifically need features of a particular shell.

For example:

```dockerfile
SHELL ["/bin/bash", "-c"]
RUN source setup.sh && ./install.sh
```

`source` is a Bash feature, so you may need Bash instead of `/bin/sh`.

### 🧠 Yaad rakho

> **`SHELL` = Dockerfile ke shell-form commands kis shell ke through run honge.**

👉 **Interview line:**

> "`SHELL` specifies the default shell used to execute shell-form commands in a Dockerfile."

### 63. What is `LABEL`?
## What is `LABEL` in Docker?

`LABEL` Docker image mein **metadata/information add karne** ke liye use hota hai.

Example:

```dockerfile
LABEL maintainer="devops-team"
LABEL version="1.0"
LABEL environment="production"
```

Ye information image ke saath store hoti hai.

### Why use `LABEL`?

Image ko **identify, organize aur manage** karne ke liye.

For example:

```text
Image
 ├── version = 1.0
 ├── environment = production
 ├── team = devops
 └── project = payment
```

Check kar sakte ho:

```bash
docker inspect myapp
```

### `LABEL` vs `ENV`

**LABEL:**

> Image ke baare mein information/metadata.

**ENV:**

> Application ko runtime configuration/value.

Example:

```dockerfile
LABEL version="1.0"
ENV APP_PORT="8080"
```

* `LABEL version` → image ki information
* `ENV APP_PORT` → application ki configuration

### 🧠 Yaad rakho

> **`LABEL` = Image ke baare mein metadata/information.**

👉 **Interview line:**

> "`LABEL` adds metadata to a Docker image, such as version, maintainer, project, or environment information."

### 64. What is `ONBUILD`?
## What is `ONBUILD` in Docker?

`ONBUILD` ka matlab hai:

> **"Abhi command mat chalao; jab koi doosri image is image ko `FROM` kare, tab command chalao."**

### Simple example

Suppose tum ek **base image** bana rahe ho:

```dockerfile
FROM node:22

ONBUILD COPY . /app
ONBUILD RUN npm install
```

Ab koi developer is image ko use karta hai:

```dockerfile
FROM my-node-base
CMD ["npm", "start"]
```

Jab `my-node-base` se **new image build** hogi:

```text
FROM my-node-base
       ↓
ONBUILD COPY . /app
       ↓
ONBUILD RUN npm install
       ↓
New image ready
```

### Normal `RUN` vs `ONBUILD`

```dockerfile
RUN npm install
```

➡️ **Isi image ko build karte waqt** execute hoga.

```dockerfile
ONBUILD RUN npm install
```

➡️ **Child image ko build karte waqt** execute hoga.

### 🧠 Yaad rakho

> **`RUN` = abhi execute karo**
> **`ONBUILD` = child image build hone par execute karo**

👉 **Interview line:**

> "`ONBUILD` adds a trigger to an image that executes a Dockerfile instruction when another image uses it as a base image."

### 65. What is `STOPSIGNAL`?
## What is `STOPSIGNAL` in Docker?

`STOPSIGNAL` Docker ko batata hai ki **container stop karte waqt main process ko kaunsa OS signal bhejna hai**.

Example:

```dockerfile
FROM nginx

STOPSIGNAL SIGTERM
```

When you run:

```bash
docker stop mycontainer
```

Docker main process ko configured signal bhejega.

### Why use it?

Application ko **gracefully stop** karne ke liye.

Example:

```text
docker stop
     ↓
STOPSIGNAL SIGTERM
     ↓
Application ko signal
     ↓
Cleanup / connections close
     ↓
Application exits gracefully
```

Agar application ko kisi specific signal ki requirement hai, `STOPSIGNAL` useful hota hai.

### Common signals

```text
SIGTERM → Gracefully stop
SIGKILL → Forcefully kill
SIGINT  → Interrupt
```

Example:

```dockerfile
STOPSIGNAL SIGTERM
```

### 🧠 Yaad rakho

> **`STOPSIGNAL` = Container stop karte waqt main process ko kaunsa signal dena hai.**

👉 **Interview line:**

> "`STOPSIGNAL` specifies the system signal that Docker should send to the container's main process when stopping the container."

### 66. What is `MAINTAINER` and why isn't it generally used?
## What is `MAINTAINER` in Docker?

`MAINTAINER` was an old Dockerfile instruction used to specify **who maintains the image**.

Example:

```dockerfile
MAINTAINER bhupendra@example.com
```

Meaning:

> "This image is maintained by this person/team."

### Why isn't it generally used now?

Because `MAINTAINER` is **deprecated**.

Docker recommends using `LABEL` instead:

```dockerfile
LABEL maintainer="bhupendra@example.com"
```

`LABEL` is more flexible because you can store multiple pieces of metadata:

```dockerfile
LABEL maintainer="devops-team"
LABEL version="1.0"
LABEL description="Production application"
```

### 🧠 Easy difference

```text
MAINTAINER → Old way ❌
LABEL       → Modern/recommended way ✅
```

👉 **Interview line:**

> "`MAINTAINER` was used to specify the image maintainer, but it is deprecated and `LABEL` is preferred for storing maintainer and other image metadata."

### 67. Which Dockerfile instructions create layers?
## Which Dockerfile instructions create layers?

The important interview answer is:

### ✅ Instructions that create filesystem layers

* `RUN`
* `COPY`
* `ADD`

Example:

```dockerfile
FROM ubuntu:22.04

RUN apt-get update          # Layer
COPY app.py /app/           # Layer
RUN pip install flask       # Layer
ADD config.tar /app/        # Layer
```

Each of these can create a **new image layer**.

### ❌ Instructions that generally don't create filesystem layers

These mainly add metadata/configuration:

```text
CMD
ENTRYPOINT
ENV
ARG
EXPOSE
WORKDIR
USER
LABEL
VOLUME
STOPSIGNAL
SHELL
ONBUILD
```

### Important interview nuance

`ENV`, `CMD`, `ENTRYPOINT`, etc. can affect the image's **configuration/metadata**, but they don't create a normal filesystem layer like `RUN`, `COPY`, and `ADD`.

### 🧠 Super-short trick

> **`RUN + COPY + ADD` → filesystem layers**

And:

> **Docker image = multiple read-only layers + container writable layer**

**Interview line:**

> "The main Dockerfile instructions that create filesystem layers are `RUN`, `COPY`, and `ADD`."

### 68. What is Docker build context?
## What is Docker Build Context?

**Docker build context = woh files/folders ka set jo Docker ko `docker build` ke time available karaya jata hai.**

Example:

```bash
docker build -t myapp .
```

Yahan:

```text
.  ← Build context
```

Matlab current directory ke andar ki files Docker build ke liye available hain.

Suppose folder:

```text
myapp/
├── Dockerfile
├── app.py
├── requirements.txt
└── config/
    └── app.conf
```

Command:

```bash
docker build -t myapp .
```

Then Docker ko ye files build context mein milti hain:

```text
Docker build context
        ↓
 ┌─────────────────┐
 │ Dockerfile      │
 │ app.py          │
 │ requirements.txt│
 │ config/         │
 └─────────────────┘
```

Therefore Dockerfile mein:

```dockerfile
COPY app.py /app/
COPY requirements.txt /app/
```

possible hai, because these files are inside the build context.

### Important: Build context ≠ Image

```text
Local files
    ↓
Build Context
    ↓ docker build
Dockerfile instructions
    ↓
Docker Image
    ↓
Container
```

### Why is it important?

Docker build ke time `COPY` and `ADD` **build context ke bahar ki files access nahi kar sakte**.

For example:

```bash
docker build -t myapp /home/user/project
```

Context = `/home/user/project`

Agar Dockerfile mein:

```dockerfile
COPY /home/user/secret.txt /app/
```

likha, aur `secret.txt` context ke bahar hai → ❌ not allowed.

### `.dockerignore`

Unnecessary files ko context mein bhejne se rokne ke liye:

```text
node_modules
.git
*.log
.env
```

`.dockerignore` use karte hain.

Isse **build faster hota hai aur unnecessary/sensitive files context mein nahi jaati.**

### 🧠 Yaad rakho

> **Build Context = `docker build` ko diye gaye files/folder ka area, jise Docker build ke time access kar sakta hai.**

👉 **Interview line:**

> "Docker build context is the set of files and directories sent to the Docker daemon and made available to Dockerfile instructions such as `COPY` and `ADD`."

### 69. What does `.` mean in `docker build -t app .`?
In:

```bash
docker build -t app .
```

the **`.` means the current directory**.

It tells Docker:

> **“Use this current directory as the Docker build context.”**

### Example

Suppose you are inside:

```text
myapp/
├── Dockerfile
├── app.py
└── requirements.txt
```

You run:

```bash
cd myapp
docker build -t app .
```

Here:

```text
. 
↓
myapp/          ← Build Context
├── Dockerfile
├── app.py
└── requirements.txt
```

So Docker can use these files in `COPY` / `ADD`.

### Command breakdown

```bash
docker build -t app .
            │   │  │
            │   │  └── . = current directory / build context
            │   └───── image name = app
            └───────── build an image
```

🧠 **Yaad rakho:**

> **`.` = “current directory ko Docker build context bana do.”**

And importantly, **`.` does not mean the Dockerfile itself**. It means the **build context**.

### 70. What is `.dockerignore`?
## What is `.dockerignore`?

`.dockerignore` is a file that tells Docker:

> **"Build context mein se in files/folders ko Docker ko mat bhejo."**

It works similar to `.gitignore`.

### Example

Project:

```text
myapp/
├── Dockerfile
├── app.py
├── node_modules/
├── .git/
├── .env
└── debug.log
```

`.dockerignore`:

```text
node_modules
.git
.env
*.log
```

When you run:

```bash
docker build -t app .
```

Docker build context mein unnecessary files exclude kar dega.

### Why use `.dockerignore`?

**1. Faster builds** ⚡
Large unnecessary files Docker ko send nahi hote.

**2. Smaller build context**
Less data Docker build process ko process karna padta hai.

**3. Avoid sensitive files** 🔐
For example:

```text
.env
*.pem
credentials/
```

**4. Cleaner builds**

### `.dockerignore` vs `.gitignore`

```text
.gitignore     → Git ko files ignore karne ke liye
.dockerignore  → Docker build context se files exclude karne ke liye
```

### 🧠 Yaad rakho

> **`.dockerignore` = Docker build context se unwanted files ko exclude karo.**

👉 **Interview line:**

> "`.dockerignore` specifies files and directories that should be excluded from the Docker build context."

### 71. Why should we use `.dockerignore`?
## Why should we use `.dockerignore`?

Mainly **4 reasons**:

### 1. ⚡ Faster Docker builds

Agar project mein `node_modules`, `.git`, logs, etc. hain, Docker ko unnecessarily build context mein ye files process/send karni pad sakti hain.

```text
Without .dockerignore
Project → 500 MB context → Docker

With .dockerignore
Project → 50 MB context → Docker
```

Less context = faster build.

### 2. 🔐 Avoid sensitive files

Aisi files ko exclude kar sakte hain:

```text
.env
credentials
*.pem
secrets/
```

So they don't become part of the build context and accidentally get copied into the image.

**Important:** `.dockerignore` alone is **not a complete secret-management solution**; secrets should be handled with proper secret mechanisms.

### 3. 📦 Reduce unnecessary data

Example:

```text
node_modules/
.git/
*.log
tmp/
```

Inki application image banane ke liye usually zarurat nahi hoti.

### 4. 🧹 Cleaner and predictable builds

Only required files are available to Docker's build process.

### 🧠 Interview shortcut

> **`.dockerignore` = Unwanted + unnecessary + sensitive files ko Docker build context se exclude karna.**

👉 **Interview line:**

> "We use `.dockerignore` to reduce build context size, improve build performance, prevent unnecessary files from being included, and reduce the risk of accidentally exposing sensitive files."

### 72. What happens if `.dockerignore` is missing?
If `.dockerignore` is **missing**, Docker **normally sends the entire build context** to the Docker build process, except for files Docker excludes by its own built-in behavior.

Example:

```text
myapp/
├── Dockerfile
├── app.py
├── node_modules/   ← unnecessary
├── .git/           ← unnecessary
├── .env             ← sensitive
└── logs/            ← unnecessary
```

Run:

```bash
docker build -t app .
```

`.` means **this whole directory is the build context**.

### What problems can happen?

* 🐌 **Slower build** → large context has to be transferred/processed.
* 💾 **More data** → unnecessary files are available to build instructions.
* 🔐 **Security risk** → you could accidentally `COPY` sensitive files into the image.
* 🧹 **Less clean builds** → unnecessary files are available to the build.

### Important distinction

Without `.dockerignore`:

```text
Build Context
     ↓
Docker can access files in context
     ↓
COPY . .
     ↓
Unwanted files may enter image ❌
```

With `.dockerignore`:

```text
Project
  ↓
.dockerignore filters files
  ↓
Smaller/cleaner context
  ↓
Docker build
```

🧠 **Interview line:**

> "If `.dockerignore` is missing, unwanted files in the build context are not filtered by `.dockerignore`, which can increase build time and may lead to accidentally copying unnecessary or sensitive files into the image."

### 73. How do you reduce Docker image size?
## How do you reduce Docker image size?

Interview mein **main points** ye bolna:

### 1. Use a smaller base image

Instead of:

```dockerfile
FROM ubuntu:22.04
```

use a smaller suitable image:

```dockerfile
FROM python:3.12-slim
```

or sometimes:

```dockerfile
FROM alpine
```

⚠️ Alpine is not always better; compatibility matters.

---

### 2. Use Multi-stage builds ⭐

Build tools ko final image mein mat rakho.

```dockerfile
FROM node:22 AS builder
WORKDIR /app
COPY . .
RUN npm install && npm run build

FROM nginx:alpine
COPY --from=builder /app/dist /usr/share/nginx/html
```

Final image mein sirf required output aata hai.

---

### 3. Use `.dockerignore`

Unnecessary files ko build context se exclude karo:

```text
node_modules
.git
*.log
.env
```

---

### 4. Don't install unnecessary packages

Avoid:

```dockerfile
RUN apt-get install -y vim curl git ...
```

Agar application ko zarurat nahi hai, install mat karo.

---

### 5. Remove package-manager cache

For example:

```dockerfile
RUN apt-get update && \
    apt-get install -y nginx && \
    rm -rf /var/lib/apt/lists/*
```

---

### 6. Combine related `RUN` commands

Instead of:

```dockerfile
RUN apt-get update
RUN apt-get install -y nginx
RUN rm -rf /var/lib/apt/lists/*
```

use:

```dockerfile
RUN apt-get update && \
    apt-get install -y nginx && \
    rm -rf /var/lib/apt/lists/*
```

This can reduce unnecessary intermediate filesystem data.

---

### 7. Don't copy unnecessary files

Instead of blindly:

```dockerfile
COPY . .
```

use:

```dockerfile
COPY package*.json ./
RUN npm install

COPY src ./src
```

Only required files are copied.

---

### 8. Use production dependencies only

For Node.js:

```bash
npm ci --omit=dev
```

Don't include development dependencies in the production image when they're unnecessary.

---

### 🧠 Interview shortcut

Remember:

> **Small base image + Multi-stage build + `.dockerignore` + only required dependencies/files + clean caches**

### ⭐ Best interview answer

> "I reduce Docker image size by choosing a minimal suitable base image, using multi-stage builds, excluding unnecessary files with `.dockerignore`, installing only required production dependencies, avoiding unnecessary packages, and cleaning package-manager caches."

### 74. How do you optimize a Dockerfile?
## How do you optimize a Dockerfile?

Dockerfile optimize karne ka main goal hai:

> **Smaller image + faster build + better caching + better security.**

### 1. Use a minimal base image

```dockerfile
FROM python:3.12-slim
```

Instead of unnecessarily large:

```dockerfile
FROM ubuntu:22.04
```

---

### 2. Use Multi-stage builds ⭐

Build dependencies ko final image mein mat rakho.

```dockerfile
FROM node:22 AS builder
WORKDIR /app

COPY package*.json ./
RUN npm ci

COPY . .
RUN npm run build

FROM nginx:alpine
COPY --from=builder /app/dist /usr/share/nginx/html
```

---

### 3. Optimize Docker cache ⭐

Frequently changing files ko baad mein copy karo.

❌ Bad:

```dockerfile
COPY . .
RUN npm install
```

Har code change par `npm install` cache invalidate ho sakta hai.

✅ Better:

```dockerfile
COPY package*.json ./
RUN npm ci

COPY . .
```

Dependency files change nahi hui → `npm ci` layer cache ho sakti hai.

---

### 4. Use `.dockerignore`

```text
.git
node_modules
.env
*.log
```

Unnecessary files build context mein mat bhejo.

---

### 5. Don't install unnecessary packages

Sirf application ko required packages install karo.

```dockerfile
RUN apt-get update && \
    apt-get install -y --no-install-recommends curl && \
    rm -rf /var/lib/apt/lists/*
```

---

### 6. Combine related commands

Instead of:

```dockerfile
RUN apt-get update
RUN apt-get install -y curl
RUN rm -rf /var/lib/apt/lists/*
```

Use:

```dockerfile
RUN apt-get update && \
    apt-get install -y --no-install-recommends curl && \
    rm -rf /var/lib/apt/lists/*
```

---

### 7. Run as non-root user 🔐

```dockerfile
RUN useradd -r appuser
USER appuser
```

Security improve hoti hai.

---

### 8. Use `.dockerignore` + selective `COPY`

Instead of blindly:

```dockerfile
COPY . .
```

Only required files copy karo where practical.

---

### 9. Use proper `CMD` / `ENTRYPOINT`

Prefer exec form:

```dockerfile
CMD ["python", "app.py"]
```

instead of:

```dockerfile
CMD python app.py
```

Exec form generally gives better signal handling and avoids an unnecessary shell.

---

### 10. Pin important versions

Instead of:

```dockerfile
FROM python:latest
```

prefer a controlled version:

```dockerfile
FROM python:3.12-slim
```

This makes builds more predictable.

---

### 🧠 Interview shortcut

Remember:

**`B-C-S-S-D`**

* **B** → Base image small
* **C** → Cache layers properly
* **S** → Stage builds (multi-stage)
* **S** → Security: non-root
* **D** → Don't copy/install unnecessary things

👉 **Interview line:**

> "I optimize a Dockerfile by using a minimal base image, maximizing layer caching, using multi-stage builds, minimizing dependencies and build context, running as a non-root user, and keeping builds reproducible."

### 75. Why should dependencies be copied before application source?
Because of **Docker layer caching**. ⭐

Suppose Node.js application hai.

### ❌ Bad Dockerfile

```dockerfile
FROM node:22

WORKDIR /app

COPY . .
RUN npm install
```

Ab tum sirf `app.js` mein ek small change karte ho:

```text
app.js changed
      ↓
COPY . . changed
      ↓
RUN npm install
      ↓
Cache invalidated ❌
      ↓
npm install again
```

Build slow ho jayega.

---

### ✅ Better Dockerfile

```dockerfile
FROM node:22

WORKDIR /app

COPY package*.json ./
RUN npm install

COPY . .
```

Ab:

```text
package.json unchanged
      ↓
npm install layer cached ✅

app.js changed
      ↓
COPY . . runs again
      ↓
npm install doesn't run again ✅
```

### Why?

Docker **layer by layer cache** karta hai.

Dependencies:

```text
package.json
package-lock.json
```

usually application source code se **less frequently change** hote hain.

So hum:

```text
Dependencies
     ↓
Install dependencies
     ↓
Application source
```

rakhte hain.

### 🧠 Yaad rakho

> **Dependencies first, source code later = better Docker cache = faster builds.**

👉 **Interview line:**

> "We copy dependency files before application source so that the dependency installation layer can be cached and doesn't need to be rebuilt when only application code changes."

### 76. How does Docker build cache work?
## How does Docker build cache work?

Docker build ke time Docker **har instruction ka result cache** karta hai. Agar next build mein same instruction aur required inputs same hain, Docker **cached layer reuse** kar leta hai instead of running it again.

### Simple example

```dockerfile
FROM node:22

WORKDIR /app

COPY package*.json ./
RUN npm install

COPY . .

CMD ["npm", "start"]
```

First build:

```text
FROM          → Build
WORKDIR       → Build
COPY package  → Build
npm install   → Build
COPY source   → Build
```

Next build, agar sirf `app.js` change hua:

```text
FROM          → CACHE ✅
WORKDIR       → CACHE ✅
COPY package  → CACHE ✅
npm install   → CACHE ✅
COPY source   → Build again
```

So Docker ko `npm install` dobara nahi karna pada.

---

## 🔥 Important rule: Cache break hone ke baad?

Docker instructions ko **top-to-bottom** process karta hai.

Agar kisi instruction ka cache match nahi hua, **us instruction se onward subsequent instructions generally cache reuse nahi karte**.

Example:

```dockerfile
COPY package*.json ./
RUN npm install
COPY . .
RUN npm run build
```

Agar `package.json` change hua:

```text
COPY package*.json → CACHE MISS ❌
RUN npm install    → RUN again
COPY . .           → RUN again
npm run build      → RUN again
```

### Why dependency files first?

Isi wajah se hum:

```dockerfile
COPY package*.json ./
RUN npm install

COPY . .
```

karte hain.

Agar source code change ho:

```text
Source changed
    ↓
COPY . . → rebuild
    ↓
npm install → CACHE ✅
```

Build fast ho jata hai.

---

### 🧠 Easy formula

> **Same instruction + same relevant inputs → Cache HIT ✅**

> **Changed input → Cache MISS ❌ → instruction runs again**

### Interview line

> **"Docker build cache reuses previously built layers when the Dockerfile instruction and its relevant inputs haven't changed, which makes subsequent builds faster."**

### 77. What invalidates Docker cache?
## What invalidates Docker build cache?

**Cache invalidation = Docker ko existing cached layer reuse nahi karni padti, so it builds that layer again.**

### Common things that invalidate cache:

### 1. Dockerfile instruction changes ⭐

```dockerfile
RUN npm install
```

Change to:

```dockerfile
RUN npm install --production
```

→ Cache miss ❌

---

### 2. `COPY` / `ADD` source files change ⭐

```dockerfile
COPY . .
```

Agar copied files ka content change hua:

```text
app.py changed
    ↓
COPY . . → Cache miss
```

---

### 3. Files added/removed from the `COPY` source

Example:

```text
COPY . .
```

A new file build context mein aa gaya ya relevant copied files change/remove hue → cache can be invalidated.

---

### 4. Previous layer changes

This is **very important**.

```dockerfile
COPY package.json .
RUN npm install
COPY . .
RUN npm build
```

If `package.json` changes:

```text
COPY package.json → MISS
        ↓
RUN npm install   → RUN again
        ↓
COPY . .           → RUN again
        ↓
RUN npm build      → RUN again
```

Because cache is evaluated sequentially.

---

### 5. Base image changes

```dockerfile
FROM node:22
```

If the resolved base image changes, downstream layers may need rebuilding.

For reproducibility, pinning versions/digests can help.

---

### 6. Build arguments can affect cache

Example:

```dockerfile
ARG VERSION
RUN echo $VERSION
```

Build:

```bash
docker build --build-arg VERSION=1.0 .
```

Then:

```bash
docker build --build-arg VERSION=2.0 .
```

The affected instruction can get a cache miss.

---

### 7. Cache explicitly disabled

If you run:

```bash
docker build --no-cache -t app .
```

Docker won't reuse the normal build cache.

---

## 🧠 Super shortcut

Remember:

> **Dockerfile changed → Cache may break**
> **COPY/ADD input changed → Cache breaks**
> **Previous layer changed → Following layers rebuild**
> **Base image changed → Following layers may rebuild**
> **`--no-cache` → Don't use cache**

👉 **Interview line:**

> "Docker cache is invalidated when an instruction or its relevant inputs change, such as Dockerfile instructions, `COPY`/`ADD` source content, build arguments, or the base image. Once a layer misses, subsequent dependent layers generally need to be rebuilt."

### 78. How do you debug a failed Docker build?
## How do you debug a failed Docker build?

Interview mein ek **fixed troubleshooting pattern** follow karo:

> **Read error → identify failed instruction → check context → reproduce → fix → rebuild**

### 1. Build output dekho ⭐

```bash
docker build -t myapp .
```

Sabse pehle dekho **kaunsi Dockerfile instruction fail hui**.

Example:

```text
Step 5/8 : RUN npm install
 ---> Running...
npm ERR! ...
ERROR
```

👉 Problem likely `RUN npm install` mein hai.

---

### 2. Detailed output use karo

```bash
docker build --progress=plain -t myapp .
```

Ye detailed logs deta hai, especially BuildKit builds mein.

---

### 3. Dockerfile instruction check karo

Common issues:

```text
RUN     → command/package installation problem
COPY    → file/context problem
FROM    → image/tag/registry problem
RUN npm → dependency/network problem
```

---

### 4. Build context check karo ⭐

Agar:

```dockerfile
COPY app.py /app/
```

error aa raha hai:

```text
COPY failed: file not found
```

Check:

```bash
ls
```

and confirm `app.py` **build context ke andar** hai.

Also check `.dockerignore`—kahin file accidentally ignore toh nahi ho rahi.

---

### 5. Base image check karo

```dockerfile
FROM python:3.12-slim
```

Check whether image can be pulled:

```bash
docker pull python:3.12-slim
```

Possible issues:

* wrong image/tag
* registry authentication
* network issue
* private registry unavailable

---

### 6. Failed command ko independently test karo

Suppose:

```dockerfile
RUN apt-get install -y nginx
```

Fail ho raha hai.

Base image run karke manually test:

```bash
docker run -it ubuntu:22.04 bash
```

Then:

```bash
apt-get update
apt-get install -y nginx
```

This helps determine whether the problem is with the **command/environment**.

---

### 7. Cache issue ho toh clean rebuild

```bash
docker build --no-cache -t myapp .
```

If it works with `--no-cache`, investigate whether stale cache was involved.

---

### 8. `.dockerignore` check karo

Agar required file context mein nahi ja rahi:

```text
.dockerignore
     ↓
file accidentally excluded ❌
     ↓
COPY fails
```

---

### 9. Disk/resource issues check karo

```bash
docker system df
```

If Docker environment is running out of space, cleanup may be required:

```bash
docker system prune
```

⚠️ `prune` carefully use karo because it removes unused Docker resources.

---

## 🔥 Scenario example

**Problem:**

```text
COPY package.json ./
ERROR: file not found
```

**Troubleshooting:**

```text
1. Check current directory
       ↓
2. Check build context
       ↓
3. Check package.json exists
       ↓
4. Check .dockerignore
       ↓
5. Fix path/context
       ↓
6. Rebuild
```

### 🧠 Master pattern

```text
BUILD FAILED
    ↓
Read exact error
    ↓
Find failed Dockerfile instruction
    ↓
COPY? → Context / .dockerignore / path
RUN?  → Command / package / network
FROM? → Image / tag / registry
    ↓
Reproduce & fix
    ↓
docker build again
```

👉 **Interview line:**

> "I debug a failed Docker build by identifying the exact failed instruction from the build logs, checking the Dockerfile, build context and `.dockerignore`, validating the base image and dependencies, reproducing the failing command when necessary, and rebuilding with `--no-cache` if cache-related issues are suspected."

### 79. How do you make Docker builds reproducible?
## How do you make Docker builds reproducible?

**Reproducible build** ka matlab:

> **Same Dockerfile + same source + same dependencies → consistently same image/result.**

### Main practices:

### 1. Pin the base image ⭐

❌ Avoid:

```dockerfile
FROM python:latest
```

Better:

```dockerfile
FROM python:3.12.8-slim
```

Even stronger: pin by **image digest** when strict reproducibility is required:

```dockerfile
FROM python:3.12.8-slim@sha256:<digest>
```

---

### 2. Pin dependency versions ⭐

❌

```text
flask
requests
```

Better:

```text
flask==3.0.3
requests==2.32.3
```

Or use lock files:

```text
package-lock.json
poetry.lock
requirements.lock
```

---

### 3. Use deterministic package installation

For example, Node.js:

```dockerfile
RUN npm ci
```

instead of:

```dockerfile
RUN npm install
```

`npm ci` uses the lock file to install the specified dependency versions.

---

### 4. Don't use `latest`

Avoid:

```dockerfile
FROM nginx:latest
```

because `latest` can point to a different image later.

---

### 5. Control build arguments

If you use:

```dockerfile
ARG VERSION
```

make sure CI/CD provides a known value rather than something changing randomly.

---

### 6. Don't depend on current external state

Avoid builds that depend on:

```dockerfile
RUN apt-get install nginx
```

without controlling the package repository/version.

The package available today may differ from the package available later.

---

### 7. Use a lock file

Dependency lock files ensure:

```text
Application
   ↓
Exact dependency versions
   ↓
Same dependency tree
   ↓
More predictable image
```

---

### 8. Use a consistent build environment

Build using the same:

* Docker/BuildKit setup
* build arguments
* dependency sources
* platform/architecture where relevant

CI/CD builds are useful because they provide a controlled environment.

---

## 🧠 Interview shortcut

Remember:

> **Pin everything that can change.**

```text
Base image       → Pin version/digest
Dependencies     → Pin versions/lock files
Build arguments  → Fixed values
Package sources  → Controlled
Build environment→ Consistent
```

👉 **Interview line:**

> **"I make Docker builds reproducible by pinning base images and dependencies, using lock files and deterministic package installation, avoiding mutable tags like `latest`, controlling build arguments and external dependencies, and using a consistent CI build environment."**

### 80. How do you build a production-grade Dockerfile?
## How do you build a production-grade Dockerfile?

Production-grade Dockerfile ka goal sirf **small image** banana nahi hai. Main goals hain:

> **Security + Small size + Reproducibility + Fast builds + Reliability**

### 1. Use a minimal, pinned base image

```dockerfile
FROM python:3.12.8-slim
```

Strict environments mein digest bhi pin kar sakte ho.

---

### 2. Use multi-stage builds ⭐

Build dependencies final image mein nahi honi chahiye.

```dockerfile
FROM node:22 AS builder

WORKDIR /app
COPY package*.json ./
RUN npm ci
COPY . .
RUN npm run build

FROM nginx:alpine
COPY --from=builder /app/dist /usr/share/nginx/html
```

Final image mein sirf required runtime files.

---

### 3. Optimize layer caching

Dependencies pehle copy karo:

```dockerfile
COPY package*.json ./
RUN npm ci

COPY . .
```

Code change hone par dependency installation layer cached reh sakti hai.

---

### 4. Use `.dockerignore`

```text
.git
node_modules
.env
*.log
tests/
```

Unnecessary/sensitive files context mein mat bhejo.

---

### 5. Run as non-root user 🔐

❌ Avoid running application as root.

```dockerfile
RUN useradd -r appuser
USER appuser
```

Container compromise hone par privileges reduce hote hain.

---

### 6. Don't put secrets in Dockerfile

❌ Don't do:

```dockerfile
ENV DB_PASSWORD=secret123
```

Secrets ko runtime secret management / CI/CD secret mechanism se inject karo.

---

### 7. Use `CMD`/`ENTRYPOINT` exec form

Prefer:

```dockerfile
CMD ["python", "app.py"]
```

instead of:

```dockerfile
CMD python app.py
```

Better signal handling milta hai.

---

### 8. Add a health check when appropriate

```dockerfile
HEALTHCHECK CMD curl -f http://localhost:8080/health || exit 1
```

Application actually healthy hai ya nahi, detect karne mein help karta hai.

---

### 9. Minimize packages and clean caches

```dockerfile
RUN apt-get update && \
    apt-get install -y --no-install-recommends curl && \
    rm -rf /var/lib/apt/lists/*
```

Only required packages install karo.

---

### 10. Make configuration external

Environment-specific values ko hard-code mat karo:

```dockerfile
ENV APP_ENV=production
```

But secrets ko image mein bake mat karo.

---

### 11. Pin dependencies

For example:

```text
flask==3.0.3
requests==2.32.3
```

or use a lock file.

---

### 12. Don't run unnecessary processes

Ideally container mein **one main application process** run karo.

---

## ⭐ Production Dockerfile checklist

```text
✅ Minimal/pinned base image
✅ Multi-stage build
✅ Good layer caching
✅ .dockerignore
✅ Non-root USER
✅ No secrets
✅ Pinned dependencies
✅ Minimal packages
✅ Clean package caches
✅ Exec-form CMD/ENTRYPOINT
✅ HEALTHCHECK where appropriate
✅ External configuration
```

### 🧠 Interview answer

> **"For a production-grade Dockerfile, I use a minimal pinned base image, multi-stage builds, optimized layer caching, `.dockerignore`, pinned dependencies, non-root execution, no secrets in the image, minimal packages, proper health checks, and exec-form `CMD` or `ENTRYPOINT`. I also keep configuration external and make the build reproducible."**

---
===============
## build n runtime time cmd 
Haan, Dockerfile instructions ko **build-time vs container runtime** ke hisaab se aise yaad karo:

### 🔨 Build time — `docker build` ke time

Ye image banate waqt execute/configure hote hain:

| Instruction | Main purpose                           |
| ----------- | -------------------------------------- |
| `FROM`      | Base image choose                      |
| `RUN`       | Command execute during build           |
| `COPY`      | Files build context se image mein copy |
| `ADD`       | Files add/copy                         |
| `ARG`       | Build-time variable                    |

Example:

```dockerfile
FROM python:3.12
ARG VERSION=1.0
WORKDIR /app
COPY requirements.txt .
RUN pip install -r requirements.txt
COPY . .
```

Flow:

```text
docker build
    ↓
FROM
    ↓
ARG
    ↓
WORKDIR
    ↓
COPY
    ↓
RUN
    ↓
IMAGE READY
```

---

### 🚀 Container runtime — `docker run` ke time

Ye mainly container start hone par application ke behavior/configuration ko define karte hain:

| Instruction   | Main purpose                      |
| ------------- | --------------------------------- |
| `CMD`         | Default command                   |
| `ENTRYPOINT`  | Main executable                   |
| `ENV`         | Runtime environment variable      |
| `USER`        | Kis user se process chalega       |
| `WORKDIR`     | Runtime default working directory |
| `EXPOSE`      | Intended listening port metadata  |
| `HEALTHCHECK` | Container health check            |
| `STOPSIGNAL`  | Stop karte waqt signal            |

⚠️ **Important:** `ENV`, `USER`, `WORKDIR`, `EXPOSE`, etc. Docker image mein configuration/metadata ke roop mein **build ke time set** hote hain, but unka effect **container runtime** par hota hai. So strictly speaking, inhe simply “runtime-only instructions” kehna technically incomplete hai.

---

## 🧠 Sabse important distinction

### `RUN` vs `CMD`

```dockerfile
RUN apt-get install -y nginx
```

➡️ **Image build karte waqt**

```dockerfile
CMD ["nginx", "-g", "daemon off;"]
```

➡️ **Container start karte waqt**

### `ARG` vs `ENV`

```dockerfile
ARG VERSION=1.0
```

➡️ **Build-time value**

```dockerfile
ENV APP_ENV=production
```

➡️ **Container/application runtime mein available**

### `COPY` vs `CMD`

```dockerfile
COPY app.py /app/
```

➡️ Build time

```dockerfile
CMD ["python", "/app/app.py"]
```

➡️ Container start time

---

### 🔥 Interview ke liye one-line trick

> **`FROM, RUN, COPY, ADD, ARG` → mainly build process**

> **`CMD, ENTRYPOINT` → container start/run**

> **`ENV, USER, WORKDIR, EXPOSE, HEALTHCHECK, STOPSIGNAL` → image configuration that affects runtime behavior**

Aur **`VOLUME`, `LABEL`, `ONBUILD`, `SHELL`** ko alag category mein rakhna better hai—they primarily declare metadata/configuration or build behavior rather than being simply “build-time commands” or “runtime commands.”

=============
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
Yes. ✅ **`CMD` can be overridden.**

Suppose Dockerfile:

```dockerfile
CMD ["python", "app.py"]
```

Normally:

```bash
docker run myapp
```

runs:

```text
python app.py
```

But you can override it:

```bash
docker run myapp python test.py
```

Now it runs:

```text
python test.py
```

### 🧠 Remember

> **CMD = default command → easily override kar sakte ho.**

### `CMD` vs `ENTRYPOINT`

```dockerfile
ENTRYPOINT ["python"]
CMD ["app.py"]
```

Then:

```bash
docker run myapp
```

→ `python app.py`

```bash
docker run myapp test.py
```

→ `python test.py`

Here `ENTRYPOINT` stays fixed, while `CMD`'s value is replaced by the runtime argument.

👉 **Interview line:**

> **"Yes, CMD can be overridden by providing a command when running the container."**

### 83. Can ENTRYPOINT be overridden?
Yes, but **not in the same way as `CMD`**. ✅

### `ENTRYPOINT`

Suppose:

```dockerfile
ENTRYPOINT ["python"]
CMD ["app.py"]
```

Normally:

```bash
docker run myapp
```

➡️ `python app.py`

If you do:

```bash
docker run myapp test.py
```

➡️ `python test.py`

Here **ENTRYPOINT is NOT overridden**. `test.py` becomes an argument to `python`.

---

### How to actually override ENTRYPOINT?

Use:

```bash
docker run --entrypoint /bin/bash myapp
```

Now:

```text
ENTRYPOINT ["python"]
        ↓
--entrypoint /bin/bash
        ↓
ENTRYPOINT replaced
```

So `/bin/bash` becomes the container's executable.

### 🧠 Remember

```text
CMD        → normal docker run command can override it
ENTRYPOINT → use --entrypoint to override it
```

👉 **Interview line:**

> "`ENTRYPOINT` can be overridden using Docker's `--entrypoint` option, while normal arguments passed to `docker run` are typically appended to the ENTRYPOINT rather than replacing it."

### 84. What does `docker run --entrypoint` do?
## What does `docker run --entrypoint` do?

`--entrypoint` ka use **Dockerfile mein defined `ENTRYPOINT` ko replace/override** karne ke liye hota hai.

### Example

Dockerfile:

```dockerfile
FROM ubuntu:22.04

ENTRYPOINT ["python"]
CMD ["app.py"]
```

Normally:

```bash
docker run myapp
```

➡️ Runs:

```text
python app.py
```

Now:

```bash
docker run --entrypoint /bin/bash myapp
```

➡️ Dockerfile ka:

```text
ENTRYPOINT ["python"]
```

replace ho gaya:

```text
ENTRYPOINT → /bin/bash
```

So container `/bin/bash` se start hoga.

### Why is it useful?

Mostly **debugging/troubleshooting** ke liye.

Suppose application start nahi ho rahi:

```bash
docker run --entrypoint /bin/bash myapp
```

Ab container ke andar jaakar check kar sakte ho:

```bash
ls
env
cat config.yaml
```

### 🧠 Remember

```text
docker run image command
        ↓
CMD override

docker run --entrypoint xxx image
        ↓
ENTRYPOINT override
```

👉 **Interview line:**

> "`docker run --entrypoint` overrides the image's default ENTRYPOINT and allows us to start the container with a different executable."

### 85. Shell form vs exec form?
## Shell form vs Exec form in Docker

Ye mainly **`RUN`, `CMD`, aur `ENTRYPOINT`** mein dekhne ko milta hai.

### 1. Shell form

Command ko shell ke through run karta hai.

```dockerfile
CMD python app.py
```

Equivalent conceptually:

```text
/bin/sh -c "python app.py"
```

### 2. Exec form ⭐

JSON array format hota hai:

```dockerfile
CMD ["python", "app.py"]
```

Yahan Docker **directly `python` process** start karta hai, shell ke through nahi.

---

### Main difference

| Shell form                  | Exec form                                   |
| --------------------------- | ------------------------------------------- |
| `CMD python app.py`         | `CMD ["python", "app.py"]`                  |
| Shell involved              | Shell normally involved nahi                |
| `/bin/sh -c`                | Direct process                              |
| Signal handling less direct | Better signal handling                      |
| Shell features available    | Shell features automatically available nahi |

### Example: `CMD`

**Shell form:**

```dockerfile
CMD python app.py
```

Flow:

```text
Docker
 ↓
/bin/sh
 ↓
python app.py
```

**Exec form:**

```dockerfile
CMD ["python", "app.py"]
```

Flow:

```text
Docker
 ↓
python app.py
```

### Why exec form is preferred for applications?

Especially production containers mein:

```dockerfile
CMD ["python", "app.py"]
```

Better hai because application directly main process (`PID 1`) ban sakti hai, so **OS signals like SIGTERM** more directly reach the application.

This helps graceful shutdown.

---

### Shell features chahiye toh?

For example:

```dockerfile
CMD echo "Hello" && echo "World"
```

Shell form mein `&&` shell handle karta hai.

Exec form mein:

```dockerfile
CMD ["sh", "-c", "echo Hello && echo World"]
```

Agar shell behavior explicitly chahiye, exec form ke andar shell explicitly specify kar sakte ho.

### 🧠 Yaad rakho

> **Shell form = command through shell**
> **Exec form = command directly**

👉 **Interview line:**

> **"Shell form executes the command through a shell, while exec form starts the executable directly. Exec form is generally preferred for container applications because it provides better process and signal handling."**

### 86. Why is exec form preferred?
## Why is Exec form preferred in Docker?

Main reason: **better process and signal handling**. ⭐

Example:

```dockerfile
CMD ["python", "app.py"]
```

### 1. Application directly main process hoti hai

Exec form:

```text
Docker
  ↓
python app.py
  ↓
Application = PID 1
```

Shell form:

```dockerfile
CMD python app.py
```

usually:

```text
Docker
  ↓
/bin/sh -c
  ↓
python app.py
```

Yahan shell beech mein aa sakta hai.

---

### 2. Signals properly reach application ⭐

When you do:

```bash
docker stop myapp
```

Docker sends a stop signal to the container's main process.

With exec form, application directly main process hai, so signal handling is more predictable.

```text
docker stop
    ↓
SIGTERM
    ↓
Application
    ↓
Graceful shutdown
```

This is especially important for **production applications**.

---

### 3. No unnecessary shell

Exec form:

```dockerfile
CMD ["nginx", "-g", "daemon off;"]
```

Docker directly starts `nginx`.

Shell form:

```dockerfile
CMD nginx -g "daemon off;"
```

normally involves a shell.

---

### 4. Arguments are handled predictably

Exec form:

```dockerfile
CMD ["python", "app.py"]
```

Each item is a separate argument.

This avoids some shell parsing/quoting behavior.

---

## 🧠 Easy shortcut

> **Exec form = Direct process → better PID 1 + signal handling + predictable arguments**

### Interview line

> **"Exec form is preferred because it starts the application directly without an intermediate shell, providing better signal handling, process management, and predictable argument handling."**

### 87. How does signal handling differ between shell and exec form?
## Shell vs Exec form — Signal handling

This is an important **Docker interview question**.

### 1. Exec form ✅

```dockerfile
CMD ["python", "app.py"]
```

Flow:

```text
docker stop
     ↓
 SIGTERM
     ↓
python process (PID 1)
     ↓
Application receives signal
     ↓
Graceful shutdown
```

Because the application itself is normally the container's **PID 1**, it can directly receive and handle the signal.

---

### 2. Shell form ⚠️

```dockerfile
CMD python app.py
```

Docker normally runs it through a shell:

```text
docker stop
     ↓
 SIGTERM
     ↓
/bin/sh (PID 1)
     ↓
python app.py
```

The problem is that the shell may **not forward the signal to the child application process** in the way you expect.

So the application may not receive `SIGTERM` properly and may not get a chance to gracefully shut down.

---

### Example

Suppose application needs 10 seconds to:

```text
save data
close DB connection
finish request
```

With proper exec-form signal handling:

```text
SIGTERM
  ↓
App receives it
  ↓
Cleanup
  ↓
Exit
```

With problematic shell-form behavior:

```text
SIGTERM
  ↓
Shell
  ↓
App may not receive/handle it properly
  ↓
Graceful cleanup may not happen
```

Docker eventually uses a **forceful kill (`SIGKILL`) after the stop timeout** if the container hasn't exited.

---

### ⭐ Important nuance

Shell form is **not always broken**. A shell script can explicitly forward signals, for example with `exec`:

```sh
#!/bin/sh
exec python app.py
```

Here `exec` replaces the shell with Python, so Python becomes PID 1.

That's why the safest simple recommendation for application commands is:

```dockerfile
CMD ["python", "app.py"]
```

### 🧠 Interview shortcut

> **Exec form → App becomes PID 1 → signals reach app directly.**

> **Shell form → Shell can become PID 1 → signal forwarding may be problematic.**

👉 **Interview line:**

> "`Exec` form provides more reliable signal handling because the application runs directly as the container's main process, whereas shell form introduces a shell that may not properly forward signals to the child process."

### 88. Why does PID 1 matter inside a container?
## Why does PID 1 matter inside a container?

Container ke andar **PID 1 = main process** hota hai. ⭐

Example:

```dockerfile
CMD ["python", "app.py"]
```

Container ke andar:

```text
PID 1
  ↓
python app.py
```

### 1. Signal handling ⭐

Docker jab:

```bash
docker stop myapp
```

karta hai, container ke main process ko termination signal bhejta hai.

Agar application PID 1 hai:

```text
docker stop
    ↓
SIGTERM
    ↓
PID 1 (Application)
    ↓
Graceful shutdown
```

Isliye exec form useful hai:

```dockerfile
CMD ["python", "app.py"]
```

---

### 2. PID 1 has special Linux behavior

Container ke PID namespace mein PID 1 **special role** rakhta hai.

Normal Linux processes ke unlike, PID 1 ko certain signals ke liye special handling/default behavior hota hai. Agar application PID 1 ke roop mein signals handle nahi karti, shutdown behavior unexpected ho sakta hai.

---

### 3. Zombie/orphan process handling

PID 1 ko container ke orphaned child processes ko **reap** karne ki responsibility bhi ho sakti hai.

Complex applications ke liye lightweight init such as:

```bash
docker run --init myapp
```

useful ho sakta hai.

---

### Simple example

❌ Shell form:

```dockerfile
CMD python app.py
```

```text
PID 1 → /bin/sh
           ↓
       python app.py
```

✅ Exec form:

```dockerfile
CMD ["python", "app.py"]
```

```text
PID 1 → python app.py
```

### 🧠 Yaad rakho

> **PID 1 = container ka main process.**

Aur:

> **PID 1 matters because it is the primary target for container lifecycle signals and has special process-management responsibilities.**

👉 **Interview line:**

> "PID 1 matters in containers because it is the container's main process and has special responsibilities for signal handling and reaping child processes, which directly affects graceful shutdown and process management."

### 89. What happens when PID 1 doesn't handle SIGTERM correctly?
If **PID 1 doesn't handle SIGTERM correctly**, the container may **not shut down gracefully**.

### Simple flow

```text
docker stop mycontainer
        ↓
Docker sends SIGTERM
        ↓
PID 1
        ↓
Doesn't handle/forward SIGTERM properly
        ↓
Application keeps running
        ↓
Docker waits for stop timeout
        ↓
Docker sends SIGKILL
        ↓
Application is forcefully killed
```

### What problems can happen?

1. **Graceful shutdown doesn't happen**

   * App doesn't get time to finish current requests.

2. **Requests can be interrupted**

   * Users may get failed/incomplete requests.

3. **Data can be lost/corrupted**

   * If the application was writing data and gets force-killed.

4. **Connections aren't cleaned up**

   * DB connections, files, sockets, etc. may not close properly.

5. **Child processes may remain unmanaged**

   * PID 1 is also responsible for reaping orphaned child processes.

### Example

Bad:

```dockerfile
CMD python app.py
```

Here a shell may become PID 1:

```text
PID 1 → /bin/sh
          ↓
       python app.py
```

Better:

```dockerfile
CMD ["python", "app.py"]
```

Now:

```text
PID 1 → python app.py
```

So `SIGTERM` reaches the application more directly.

### 🧠 Interview shortcut

> **If PID 1 doesn't handle SIGTERM properly, the container may fail to shut down gracefully and eventually be force-killed with SIGKILL after Docker's stop timeout.**

### 90. Why can an application fail to shut down gracefully inside Docker?
An application can fail to shut down gracefully inside Docker mainly because **SIGTERM doesn't reach the application properly, or the application doesn't handle it**.

### Common reasons

**1. PID 1 doesn't handle SIGTERM**

```text
Docker
  ↓ SIGTERM
PID 1 (shell)
  ↓
Application
```

The shell may not forward the signal correctly to the application.

**2. Using shell form**

```dockerfile
CMD python app.py
```

A shell can become PID 1 instead of Python.

Better:

```dockerfile
CMD ["python", "app.py"]
```

Now Python can be PID 1.

---

**3. Application doesn't handle SIGTERM**

The application itself may not have shutdown logic.

For example, it doesn't:

```text
receive SIGTERM
      ↓
stop accepting new requests
      ↓
finish existing requests
      ↓
close DB connections
      ↓
exit
```

---

**4. Application takes too long to shut down**

Docker waits for the stop timeout. If the application still hasn't exited:

```text
SIGTERM
  ↓
wait
  ↓
timeout
  ↓
SIGKILL
```

`SIGKILL` cannot be caught or handled, so the process is immediately terminated.

---

**5. Multiple processes inside the container**

If one container runs several processes:

```text
PID 1
 ├── app
 ├── worker
 └── child process
```

PID 1 may not properly forward signals or manage child processes.

---

**6. PID 1 doesn't reap child processes**

Poor process management can leave zombie processes and cause lifecycle problems, especially for applications spawning many children.

### 🧠 Interview shortcut

> **Graceful shutdown fails when SIGTERM doesn't reach the application, the application doesn't handle SIGTERM, or it takes longer than the Docker stop timeout.**

**Best practice:** use **exec-form `CMD/ENTRYPOINT`**, make the application handle **SIGTERM**, and use an init process such as `docker run --init` when appropriate.
  
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
