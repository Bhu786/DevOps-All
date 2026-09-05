Yes. Since the uploaded PDF is specifically about **Argo CD**, for an **8-year DevOps Engineer** interview, I would not limit preparation to “What is Argo CD?”. An interviewer will usually go from fundamentals → architecture → implementation → production scenarios → troubleshooting → security → GitOps design.

The PDF covers Argo CD concepts such as GitOps, Application, Sync, health/sync status, architecture, automated sync, self-healing, pruning, RBAC, Helm/Kustomize, multi-cluster, App of Apps, hooks, and CLI commands. 

# Argo CD — 8 Years DevOps Interview Question Bank

## 1. Basic / Fundamentals

1. What is Argo CD?
=> Argo cd is open source and automation tools for k8s basicaaly we used it for continous deplyment and its sync with running state and github or desired state 
3. Why do we use Argo CD?
=> like we can go kenkin but smooth and controlled deploymeny we choose argocd and jenkins is push basd but argocd is pull based so it automatically makes changes .
5. What problem does Argo CD solve?
=>Argo CD solves the problem of keeping the Kubernetes cluster in sync with the desired state defined in Git.
Without Argo CD, we may have to manually run kubectl commands or use a CI tool like Jenkins to push deployments to Kubernetes. This can lead to configuration drift and inconsistent deployments.
Argo CD follows a GitOps approach where Git is the source of truth. It continuously compares the desired state in Git with the actual state running in the cluster and automatically syncs the cluster when there is a difference.
7. What is GitOps?

=>
Haan, **naam se hi samjho: GitOps = Git + Operations**.

### 1. GitOps kyun bolte hain?

Normally **Operations** ka matlab hai:

> Application/infrastructure ko deploy karna, update karna, maintain karna.

Aur **GitOps** mein hum ye Operations ka kaam **Git ke through/manage according to Git** karte hain.

Isliye:

**Git + Operations = GitOps**

---

### 2. Actual mein hota kya hai?

Normal approach:

```text
Developer
   ↓
Jenkins / kubectl
   ↓
Kubernetes
```

Yahan deployment ka control Jenkins commands ya manually `kubectl` se ho sakta hai.

GitOps approach:

```text
              Git
        (Desired State)
              ↓
           Argo CD
              ↓
        Kubernetes
```

Git mein hum likhte hain:

```yaml
replicas: 5
image: myapp:v2
```

Matlab:

> **"Production mein mujhe 5 replicas aur v2 image chahiye."**

Ye **desired state** hai.

Argo CD dekhta hai:

```text
Git says:          5 replicas, v2
Kubernetes has:    3 replicas, v1

             ↓

       Difference मिला
             ↓
          Sync
             ↓

Kubernetes:        5 replicas, v2
```

---

### 3. Toh GitOps ka main concept kya hai?

**Git ko deployment/operations ka source of truth bana dena.**

Isliye agar koi pooche:

> **Why is it called GitOps?**

Tum bolo:

> **Because we manage Kubernetes operations and deployments through the desired configuration stored in Git. Git becomes the source of truth, hence Git + Operations = GitOps.**

### Ekdum yaad rakhne wali line 🧠

> **GitOps ka matlab Git mein desired state rakho, aur automation/tool ensure kare ki actual environment Git jaisa hi rahe.**

Aur **Argo CD = GitOps ko Kubernetes mein implement karne wala tool.**

9. Why is Git considered the source of truth in GitOps?
Git is considered the source of truth because it stores the approved desired state of our application and infrastructure. Any change to the environment should be reflected in Git, and GitOps tools like Argo CD use that state to keep the actual Kubernetes environment in sync."

11. How is Argo CD different from Jenkins?
=>### How is Argo CD different from Jenkins?

Sabse pehle **ek important point**:

> **Jenkins aur Argo CD exact same kaam nahi karte.**

Dono deployment pipeline mein use ho sakte hain, but **Jenkins = CI/automation**, while **Argo CD = Kubernetes GitOps/CD**.

### Simple example

Suppose developer ne code change kiya:

```text
Developer
   ↓
Git
   ↓
Jenkins
   ↓
Build + Test + Docker Image
   ↓
Image Registry
```

Ab Kubernetes mein deploy karna hai:

```text
Git (K8s YAML)
   ↓
Argo CD
   ↓
Kubernetes
```

So commonly:

```text
             CI                         CD
             
Code → Jenkins → Docker Image

K8s YAML → Argo CD → Kubernetes
```

### Main difference

| Jenkins                                          | Argo CD                                                                      |
| ------------------------------------------------ | ---------------------------------------------------------------------------- |
| Mainly CI/CD automation tool                     | Mainly Kubernetes CD/GitOps tool                                             |
| Usually **push-based** deployment                | **Pull/reconciliation-based**                                                |
| Pipeline execute karta hai                       | Cluster ko continuously desired state ke saath compare karta hai             |
| Jenkins pipeline deploy command chala sakti hai  | Argo CD Git se desired state read karta hai                                  |
| General-purpose                                  | Kubernetes-focused                                                           |
| `Jenkinsfile` commonly pipeline define karta hai | Kubernetes manifests/Helm/Kustomize Git mein desired state define karte hain |

### "Push vs Pull" ko simple samjho

**Jenkins:**

```text
Jenkins
   │
   │ "Deploy this"
   ↓
Kubernetes
```

Jenkins khud deployment **push** karta hai.

**Argo CD:**

```text
Git
 ↓
Argo CD
 ↓
Kubernetes
```

Argo CD continuously dekhta hai:

> "Git mein kya hona chahiye?"
> "Cluster mein actually kya hai?"

Difference mila → **sync**.

### Real-world setup

Aksar dono saath bhi use hote hain:

```text
Developer
   ↓
Git (Application Code)
   ↓
Jenkins
   ↓
Build / Test / Docker Image
   ↓
Registry
   ↓
Update K8s YAML in Git
   ↓
Argo CD
   ↓
Kubernetes
```

### Interview mein strong answer

> **"Jenkins is primarily a CI/CD automation server used to build, test and automate pipelines, whereas Argo CD is a Kubernetes-focused GitOps continuous delivery tool. Jenkins generally pushes deployment changes to the cluster through a pipeline, while Argo CD continuously pulls the desired state from Git and reconciles the Kubernetes cluster with it. They can also work together, where Jenkins handles CI and Argo CD handles Kubernetes CD."**

🧠 **Yaad rakho:**

**Jenkins:** *"Pipeline chalao aur deploy karo."*
**Argo CD:** *"Git mein jo desired state hai, cluster ko uske according rakho."*
    
13. Is Argo CD a CI tool or CD tool?
**Argo CD is a CD tool**, specifically a **Continuous Delivery tool for Kubernetes**.

### Simple distinction

```text
CI = Code ko ready karna
CD = Ready code ko environment mein deploy karna
```

Typical flow:

```text
Developer
   ↓
Git
   ↓
Jenkins          ← CI
   ↓
Build + Test
   ↓
Docker Image
   ↓
Git (K8s manifest)
   ↓
Argo CD           ← CD
   ↓
Kubernetes
```

### Argo CD kya karta hai?

Argo CD:

* Git se desired Kubernetes configuration read karta hai
* Cluster ki actual state check karta hai
* Difference detect karta hai
* Sync karke desired state apply karta hai
* Application deployment status monitor karta hai

So interview mein simply bolo:

> **"Argo CD is a Kubernetes-native Continuous Delivery (CD) tool that follows the GitOps approach. It continuously reconciles the Kubernetes cluster with the desired state stored in Git."**

🧠 **Shortcut:**

**Jenkins → CI**
**Argo CD → CD**

15. What is declarative deployment?
Declarative = WHAT you want
Imperative = HOW to do it
we define what we want
"Declarative deployment means defining the desired final state of the application or infrastructure, rather than specifying the steps to achieve it. Kubernetes and Argo CD then automatically work to make the actual state match that desired state."

17. What is the difference between imperative and declarative deployment?
### Imperative vs Declarative Deployment

Sabse simple way:

> **Imperative = "Kya steps karne hain"**
> **Declarative = "Final mein kya chahiye"**

### Example: 5 Pods chahiye

**Imperative:**

Tum commands dete ho:

```bash
kubectl scale deployment myapp --replicas=5
```

Tum Kubernetes ko **action** bata rahe ho:

> "Ye command execute karo aur replicas 5 karo."

---

**Declarative:**

Tum YAML mein likhte ho:

```yaml
spec:
  replicas: 5
```

Tum sirf bol rahe ho:

> **"Final state mein 5 replicas hone chahiye."**

Kubernetes khud decide karta hai ki us state tak kaise pahunchna hai.

---

### Direct comparison

| Imperative                                   | Declarative                                 |
| -------------------------------------------- | ------------------------------------------- |
| Steps/actions define karte ho                | Desired/final state define karte ho         |
| **HOW** batate ho                            | **WHAT** batate ho                          |
| Commands commonly use hoti hain              | YAML/configuration commonly use hoti hai    |
| Manual commands/pipeline driven ho sakta hai | System desired state ko reconcile karta hai |
| Example: `kubectl scale ...`                 | Example: `replicas: 5`                      |

### Argo CD connection

Argo CD **declarative approach** use karta hai:

```text
Git
 ↓
replicas: 5
 ↓
Argo CD
 ↓
Kubernetes
 ↓
Ensure actual state = 5 replicas
```

Agar kisi ne manually replicas ko 3 kar diya:

```text
Git        → 5  (Desired)
K8s        → 3  (Actual)
              ↓
         Argo CD detects drift
              ↓
            Sync
              ↓
K8s        → 5
```

### 🎯 Interview answer

> **"Imperative deployment specifies the steps or commands needed to make a change, whereas declarative deployment specifies the desired final state and lets the system determine how to achieve it. Kubernetes and Argo CD primarily follow the declarative model."**

**Shortcut:**
👉 **Imperative = Do this**
👉 **Declarative = Make it like this**

19. How does Argo CD continuously monitor Git?
### How does Argo CD continuously monitor Git?

Isko **"Argo CD Git ko continuously dekhta rehta hai"** aise mat imagine karo ki har second GitHub page open karke check kar raha hai 😄

Simple flow:

```text
                 Git Repository
              (Desired State)
                     │
          ┌──────────┴──────────┐
          │                     │
       Polling              Webhook
          │                     │
          └──────────┬──────────┘
                     ↓
                  Argo CD
                     ↓
             Compare / Reconcile
                     ↓
             Kubernetes Cluster
                (Actual State)
```

### Step-by-step

**1. Git mein YAML hai**

```yaml
replicas: 5
image: myapp:v2
```

Ye **desired state** hai.

**2. Argo CD Git repository ko check karta hai**

Argo CD repository changes ko detect kar sakta hai through **polling** and/or a **Git webhook**.

For example:

```text
Git:
v1 → v2
```

Argo CD ko pata chal gaya ki repository mein change hua.

**3. Argo CD desired vs actual state compare karta hai**

```text
Git              Kubernetes

v2       vs       v1
5 Pods   vs       3 Pods
```

Difference = **OutOfSync**

**4. Sync**

Agar auto-sync enabled hai:

```text
Git
 ↓
Argo CD
 ↓
Detect change
 ↓
Compare
 ↓
Sync
 ↓
Kubernetes
```

Kubernetes eventually:

```text
v2
5 Pods
```

### Important interview point

**"Continuously monitor" ka matlab continuously reconciliation process chalna hai.**

Argo CD:

> **Git ki desired state aur Kubernetes ki actual state ko repeatedly compare karta hai.**

Aur ek important distinction:

* **Git change detect karna** → polling/webhook
* **Cluster ko desired state mein lana** → reconciliation/sync
* **Automatic deployment** → auto-sync enabled hone par

### 🎯 Interview answer

> **"Argo CD monitors the Git repository through periodic polling and/or webhooks. When it detects a change, it compares the desired state from Git with the actual state in the Kubernetes cluster. If there is a difference, Argo CD marks the application OutOfSync and, when automated sync is enabled, reconciles the cluster to the desired state."**

21. How does Argo CD know that something has changed in Git?
these 2 ways :
Webhook ka matlab Git → Argo CD notification hai.
Polling ka matlab Argo CD → Git repeatedly check hai.
Haan, isko **sirf 2 mechanisms** se yaad rakho:

> **Argo CD ko Git change ka pata 2 tarike se chal sakta hai: Polling ya Webhook.**

### 1. Polling — Argo CD khud check karta hai

```text
Argo CD
   ↓
Git: "Kuch change hua?"
   ↓
Git
   ↓
"No"
```

Phir kuch time baad dobara check:

```text
Argo CD → Git → Check
Argo CD → Git → Check
Argo CD → Git → Check
```

Agar Git mein new commit milta hai:

```text
Git
 ↓
New Commit
 ↓
Argo CD detects it
```

---

### 2. Webhook — Git khud Argo CD ko batata hai

Ye aur simple hai:

```text
Developer
   ↓
git push
   ↓
GitHub
   ↓
"Hey Argo CD, new change aaya hai!"
   ↓
Argo CD
```

GitHub/ GitLab se **webhook notification** Argo CD ko milti hai.

---

### Phir Argo CD kya karta hai?

Change detect hone ke baad:

```text
Git
 ↓
New commit
 ↓
Argo CD
 ↓
Desired state read
 ↓
Compare with Kubernetes
 ↓
Difference?
 ↓
OutOfSync
 ↓
Auto-sync enabled?
 ↓
YES → Deploy/Sync
```

### 🧠 Interview mein short answer

> **"Argo CD detects Git changes either through periodic polling of the repository or through webhooks from Git providers like GitHub or GitLab. Once a change is detected, it compares the new desired state with the actual Kubernetes state and reconciles them if required."**

**Important:**
Webhook ka matlab **Git → Argo CD notification** hai.
Polling ka matlab **Argo CD → Git repeatedly check** hai.

23. What happens after a developer pushes a change to Git
Bilkul. Isko **complete flow** ki tarah samjho. Ye Argo CD ka bahut important interview question hai.

### Developer `git push` karta hai

Maan lo developer ne YAML change kiya:

```yaml
replicas: 5
```

Aur Git mein push kiya.

### Uske baad kya hota hai?

```text
Developer
    ↓
git push
    ↓
GitHub
    ↓
Argo CD detects change
    ↓
Argo CD reads new YAML
    ↓
Compare
    ↓
Git = Desired State
K8s = Actual State
    ↓
Difference?
    ↓
OutOfSync
    ↓
Auto-sync enabled?
    ↓
YES
    ↓
Argo CD applies changes
    ↓
Kubernetes
    ↓
5 Pods
```

### Ek example

Pehle:

```text
Git:          replicas = 3
Kubernetes:   replicas = 3
Status:       Synced
```

Developer change karta hai:

```text
Git:          replicas = 5
```

Ab:

```text
Git:          5
K8s:          3
```

Argo CD detect karta hai:

> **"Git aur Kubernetes mein difference hai."**

Status:

```text
OutOfSync
```

Agar **auto-sync enabled** hai:

```text
Argo CD
   ↓
Sync
   ↓
Kubernetes
   ↓
replicas = 5
```

Ab:

```text
Git:          5
K8s:          5
Status:       Synced
```

### 🎯 Interview answer

> **"When a developer pushes a change to Git, Argo CD detects the change through polling or a webhook. It reads the updated desired state and compares it with the actual state of the Kubernetes cluster. If there is a difference, the application becomes OutOfSync. If automated sync is enabled, Argo CD applies the required changes to Kubernetes and brings the cluster back to the desired state."**

🧠 **Flow yaad rakho:**

**Push → Detect → Compare → OutOfSync → Sync → Synced**

25. Can Argo CD deploy applications without Jenkins
**Yes. Argo CD Jenkins ke bina application deploy kar sakta hai.** ✅

Lekin ek important distinction samjho:

### Argo CD ko Jenkins ki zaroorat nahi hoti

Agar Git mein Kubernetes deployment manifest already hai:

```text id="s8dj7q"
Git
 │
 │  deployment.yaml
 │  replicas: 5
 │  image: myapp:v2
 ↓
Argo CD
 ↓
Kubernetes
```

Argo CD Git se desired state lekar **directly Kubernetes mein deploy/sync** kar sakta hai.

---

### Lekin application ka Docker image kaun banayega?

Ye alag concern hai.

```text id="b0s0m7"
Developer
   ↓
Code
   ↓
CI tool
   ↓
Docker Image
   ↓
Container Registry
   ↓
Git (image tag update)
   ↓
Argo CD
   ↓
Kubernetes
```

CI tool **Jenkins hona compulsory nahi hai**. GitHub Actions, GitLab CI, Tekton, etc. bhi ho sakte hain.

---

### Jenkins + Argo CD vs Argo CD alone

**Jenkins + Argo CD:**

```text id="2m2l3a"
Jenkins → Build/Test/Image
                  ↓
              Git update
                  ↓
              Argo CD
                  ↓
             Kubernetes
```

**Only Argo CD:**

```text id="n9v7t1"
Git (already has deployable image/config)
              ↓
           Argo CD
              ↓
         Kubernetes
```

### 🎯 Interview answer

> **"Yes, Argo CD can deploy applications without Jenkins. Argo CD is responsible for Kubernetes continuous delivery, so if the desired Kubernetes manifests and container image are already available, Argo CD can deploy and synchronize the application directly. Jenkins is only needed if we also want it to perform CI activities such as build, test, and image creation."**

🧠 **Golden point:**

**Jenkins ≠ mandatory for Argo CD.**
**Argo CD can do CD independently; CI and CD can be separate.**

27. Can Argo CD work with plain Kubernetes YAML?
Haan 👍 **"plain YAML" ka matlab YAML ke andar koi extra templating/tool nahi — directly normal Kubernetes manifest.**

### Plain YAML

Example:

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: myapp
spec:
  replicas: 3
```

Ye **plain Kubernetes YAML** hai.

Isme koi:

* Helm template nahi
* Kustomize overlay nahi
* Jinja variable nahi
* Extra templating nahi

Bas **direct Kubernetes manifest**.

### Compare karo

**Plain YAML:**

```yaml
replicas: 3
image: nginx:1.25
```

**Helm YAML/template:**

```yaml
replicas: {{ .Values.replicas }}
image: {{ .Values.image }}
```

Yahan `{{ ... }}` Helm templating hai.

### Argo CD dono kar sakta hai

```text
                 Argo CD
                    ↓
        ┌───────────┴───────────┐
        ↓                       ↓
   Plain YAML                  Helm
        ↓                       ↓
        └───────────┬───────────┘
                    ↓
               Kubernetes
```

So jab interview mein poocha:

> **Can Argo CD work with plain Kubernetes YAML?**

Answer:

> **Yes. Argo CD can directly deploy standard Kubernetes YAML manifests stored in Git, without requiring Helm or Kustomize.**

**Ek line:**
👉 **Plain YAML = direct Kubernetes YAML, bina Helm/Kustomize templating ke.**

29. What deployment formats does Argo CD support?
Haan, is question ka answer **plain YAML se thoda broader** hai.

### What deployment formats does Argo CD support?

Argo CD Kubernetes applications ke liye mainly ye formats/sources support karta hai:

```text
1. Plain Kubernetes YAML
2. Helm
3. Kustomize
4. Jsonnet
5. Custom plugins
```

### 1. Plain Kubernetes YAML

Direct manifests:

```yaml
apiVersion: apps/v1
kind: Deployment
spec:
  replicas: 3
```

```text
Git
 ↓
YAML
 ↓
Argo CD
 ↓
Kubernetes
```

### 2. Helm

Helm chart use kar sakte ho:

```text
Git
 ↓
Helm Chart
 ↓
Argo CD
 ↓
Kubernetes
```

Example:

```text
values.yaml
templates/deployment.yaml
templates/service.yaml
```

### 3. Kustomize

Base + overlays:

```text
base/
  deployment.yaml

overlays/
  production/
    kustomization.yaml
```

Argo CD Kustomize ko process karke Kubernetes resources deploy karta hai.

### 4. Jsonnet

Jsonnet configuration language se Kubernetes resources generate kar sakte ho.

### 5. Custom Config Management Plugins

Agar tumhara configuration format Argo CD ke built-in supported formats mein nahi hai, toh **Config Management Plugin** ke through custom tool use kar sakte ho.

---

### 🧠 Interview mein best answer

> **"Argo CD supports multiple Kubernetes configuration formats, including plain Kubernetes YAML/JSON manifests, Helm charts, Kustomize, Jsonnet, and custom Config Management Plugins."**

**Important:**
Ye mat bolo ki **Argo CD khud Helm/Kustomize hai**.

Argo CD ka kaam hai:

> **Source se desired Kubernetes resources obtain/render karke cluster ke saath synchronize karna.**

So:

**YAML / Helm / Kustomize / Jsonnet → Argo CD → Kubernetes**.

31. Does Argo CD support Helm?
yes
33. Does Argo CD support Kustomize?
yes
35. What is the benefit of using Git as the source of truth?
### What is the benefit of using Git as the source of truth?

Simple language mein:

> **Git mein hum define karte hain ki environment mein exactly kya hona chahiye.**

Iske major benefits hain:

### 1. History milti hai

Agar kisi ne replicas `3 → 5` kiye:

```text
Git History

10:00  replicas: 3
11:00  replicas: 5
```

Pata chal sakta hai **kab aur kya change hua**.

---

### 2. Review & Approval

Direct production mein change karne ke bajay:

```text
Developer
   ↓
Git change
   ↓
Pull Request
   ↓
Review / Approval
   ↓
Merge
   ↓
Argo CD
   ↓
Kubernetes
```

Isse unauthorized changes kam hote hain.

---

### 3. Rollback easy hai

Agar new configuration se problem ho:

```text
Current
v2 ❌

   ↓ rollback

Previous Git version
v1 ✅
```

Previous Git commit/configuration restore kar sakte ho.

---

### 4. Audit trail

Git mein record hota hai:

```text
WHO    → kisne change kiya
WHAT   → kya change kiya
WHEN   → kab change kiya
```

---

### 5. Drift detect karna easy

Maan lo Git mein:

```text
replicas: 5
```

Kisi ne Kubernetes mein manually:

```text
replicas: 2
```

kar diya.

Argo CD detect karega:

```text
Git = 5        ← Desired
K8s = 2        ← Actual

       ↓

    OutOfSync
```

So Git ke saath compare karke **configuration drift** identify ho jata hai.

---

### 🎯 Interview answer

> **"Using Git as the source of truth provides version control, change history, review and approval, auditability, easy rollback, and a consistent desired state. In GitOps, Argo CD uses this desired state from Git to detect drift and keep the Kubernetes cluster synchronized."**

🧠 **Yaad rakho:**

**Git = Record + Review + Rollback + Desired State**.

37. What are the advantages of GitOps?
GitOps ke main advantages ko **8 years DevOps interview perspective** se samjho:

### 1. Git becomes the Source of Truth

Application ka desired state Git mein stored hota hai.

```text
Developer
   ↓
   Git
   ↓
Argo CD
   ↓
Kubernetes
```

Matlab production mein kya deploy hona chahiye → **Git decide karta hai**.

---

### 2. Declarative Deployment

Aap ye nahi bolte:

> "Pod create karo, image update karo, replicas 3 karo."

Instead Git mein simply desired configuration likhte ho:

```yaml
replicas: 3
image: myapp:v2
```

Argo CD automatically cluster ko is state mein le aata hai.

---

### 3. Easy Rollback

Agar new deployment fail ho gaya:

```text
v2 ❌
 ↓
Git revert
 ↓
v1 ✅
```

Git history ki wajah se previous working configuration easily restore kar sakte ho.

---

### 4. Full Audit Trail

Git mein clearly pata hota hai:

* kisne change kiya
* kya change kiya
* kab change kiya
* kis commit se change hua

Example:

```text
Commit: abc123
Developer: Rahul
Change: image v1 → v2
Time: 10:30 AM
```

Interview mein ye **auditability** bolna important hai.

---

### 5. Better Security

Normally developers ko production Kubernetes cluster mein direct access dene ki zarurat nahi hoti.

```text
Developer
   ↓
  Git
   ↓
Argo CD
   ↓
Production Cluster
```

Developer Git mein change karta hai, aur Argo CD deployment karta hai.

So **direct kubectl access reduce** kiya ja sakta hai.

---

### 6. Automatic Drift Detection & Correction

Suppose Git says:

```text
replicas = 3
```

Lekin kisi ne manually cluster mein:

```bash
kubectl scale deployment app --replicas=5
```

kar diya.

Ab:

```text
Git → 3 replicas
Cluster → 5 replicas
```

Ye **configuration drift** hai.

Argo CD detect kar sakta hai aur, depending on configuration, cluster ko wapas Git ke desired state mein synchronize kar sakta hai.

---

### 7. Consistency Across Environments

Same GitOps approach use karke:

```text
dev
 ↓
staging
 ↓
production
```

environments ko consistently manage kar sakte ho.

Isse "works in staging but not production" type configuration issues kam hote hain.

---

### 8. CI/CD Separation

GitOps mein CI aur CD ko separate kar sakte ho:

```text
CI
Developer
   ↓
Build
   ↓
Test
   ↓
Docker Image
   ↓
Registry

CD
Git
   ↓
Argo CD
   ↓
Kubernetes
```

**CI builds the artifact.
GitOps/CD deploys the artifact.**

---

### 9. Disaster Recovery

Agar Kubernetes cluster completely destroy ho jaye, to Git repository mein infrastructure/application configuration available hoti hai.

New cluster create karke GitOps controller install karo → applications ko Git se reconstruct kiya ja sakta hai.

---

## ⭐ Interview Answer

Agar interviewer pooche **"What are the advantages of GitOps?"**, short answer:

> **"The main advantages of GitOps are Git as a single source of truth, declarative deployments, automated synchronization, drift detection and correction, easy rollback, complete auditability, improved security by reducing direct cluster access, consistency across environments, and easier disaster recovery."**

### Ek line mein yaad rakho:

**GitOps = Git + Declarative State + Automation + Auditability + Easy Rollback + Drift Correction.**

39. What are the disadvantages of GitOps?
Haan. **GitOps ke disadvantages** ko bhi interview perspective se samjho:

### 1. Git par dependency

GitOps mein Git **source of truth** hota hai.

```text
Developer → Git → Argo CD → Kubernetes
```

Agar Git repository unavailable hai, **new deployments/configuration changes** difficult ho sakte hain.

> Existing workloads usually continue running; Git outage ka matlab ye nahi ki running application immediately down ho jayegi.

---

### 2. Learning Curve

Team ko multiple concepts samajhne padte hain:

* Git
* Kubernetes
* YAML
* Argo CD / Flux
* Helm/Kustomize
* Declarative configuration

Initially traditional deployment se complex lag sakta hai.

---

### 3. Secrets Management Complex Ho Sakta Hai

Passwords, API keys, certificates etc. ko directly Git mein store nahi karna chahiye.

Isliye additional tools/process chahiye:

```text
GitOps
  +
Secrets Manager / Vault / External Secrets
```

---

### 4. Emergency Changes Complicated Ho Sakte Hain

Suppose production mein immediately replicas increase karne hain.

Traditional approach:

```bash
kubectl scale deployment app --replicas=10
```

GitOps mein ideally:

```text
Git change
   ↓
Review
   ↓
Merge
   ↓
Argo CD sync
```

Emergency situation mein ye additional steps ho sakte hain.

---

### 5. Large Repositories Complex Ho Sakte Hain

Agar hundreds of applications/environments hain:

```text
Git
 ├── dev
 ├── staging
 ├── production
 ├── app1
 ├── app2
 ├── app3
 └── ...
```

Repository structure, Helm values, Kustomize overlays etc. manage karna difficult ho sakta hai.

---

### 6. Misconfiguration Automatically Deploy Ho Sakti Hai

GitOps automation powerful hai—but dangerous bhi.

Agar incorrect configuration Git mein merge ho gayi:

```text
Bad Config
    ↓
Git
    ↓
Argo CD
    ↓
Production ❌
```

Isliye **PR reviews, validation, policy checks, testing** important hain.

---

### 7. Troubleshooting Initially Difficult

Agar deployment fail hai, problem multiple layers mein ho sakti hai:

```text
Git
 ↓
Argo CD
 ↓
Manifest rendering
 ↓
Kubernetes API
 ↓
Deployment
 ↓
Pod
```

Engineer ko understand karna padta hai ki failure kis layer par hai.

---

### 8. Not Everything Fits Naturally into GitOps

Kubernetes/application configuration GitOps ke liye excellent hai, but kuch operational tasks inherently imperative hote hain.

Examples:

* emergency debugging
* one-time data migration
* manual incident recovery
* ad-hoc operational commands

In cases mein pure GitOps workflow inconvenient ho sakta hai.

---

## ⭐ Interview Answer

Agar interviewer pooche **"What are the disadvantages of GitOps?"**, bolo:

> **"The main disadvantages are dependency on Git and GitOps tooling, initial learning curve, complexity of secret management, slower or more controlled emergency changes, repository and configuration management complexity at scale, risk of automatically deploying bad configurations, and additional troubleshooting complexity. GitOps is excellent for declarative application and infrastructure management, but some imperative operational tasks still require controlled manual intervention."**

### Simple memory trick:

**GitOps disadvantages =**

**Git dependency + Learning curve + Secrets + Emergency changes + Complexity + Bad config risk + Troubleshooting**.

---

# 2. Argo CD Architecture

The PDF identifies the major components as **API Server, Repository Server, Application Controller and optional Dex**. 

21. Explain Argo CD architecture.
Git = kya chahiye
Controller = compare + reconcile
CLI = manage/control karne ka interface


Bilkul. Argo CD architecture ko **sirf 3 components — Git, CLI, Controller** se samjho. Sabse important hai ki **CLI aur Controller ka role confuse na ho.**

![Image](https://images.openai.com/static-rsc-4/IOXp7AyfQj96NBaM4HP6U2Ngnlok5xTb8x6Yvqzqu5Q49bLcCIS0L18jLN2x_M-bH6JIwwlYm79cWPmEsJCjrjc31KCnChrrqV74VxljJIZ6eOZLnOiFzUQq2SNTEui4Yc80D5YTSRvR_r1A8oYhUKxLneTPn7lzFvLNwNoEJ4vhrO_bBARD5U4HL9BX33NF?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/mflc_kQEkUQABsf_PAQFnRLBgZ_b8GcXlzzASWHwKSvpL2RqxZq9DAlAV2lldw4RHqdyEAUomtFXHBJgehRtmIHxHlKN6YdJzUyf4Kr3uL3_Eoa6nDvYLz8cxxAVNWlspeGUceKIdSHrvORRQ8RoUSKxGRDdptjXnURCIQLK2tOPh736usDWzrUg04_gZ22Q?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/hs1ZVQf826oJw5Oj5TUQgTi4q5vycFSnATNH7Tp2ya1IDSZCSywnP4Fyo3mztJ-p5a5bAeahbJlTEbkmdq65nW4cMK9JtB-MnpCJjMZGbZmJHKG-IeuyHseosUdCH7Ul92mtyaof4xwMb0_ascXNdGardFzogEwRroVAtvbkJZniqFKQIVssuNE8L8BnTp3x?purpose=fullsize)

## Overall Flow

```text
                    Git Repository
                         │
                         │
                         ▼
                  ┌──────────────┐
                  │   Argo CD    │
                  │  Controller  │
                  └──────┬───────┘
                         │
                         │ Sync / Deploy
                         ▼
                  ┌──────────────┐
                  │  Kubernetes  │
                  │   Cluster    │
                  └──────────────┘

Developer
    │
    │ commands
    ▼
 Argo CD CLI
    │
    └──────────────► Argo CD
```

---

# 1. Git — Source of Truth

Git mein application ka **desired state** rakha hota hai.

For example:

```yaml
replicas: 3
image: myapp:v2
```

Git basically bol raha hai:

> "Mujhe Kubernetes mein application ki state aisi chahiye."

Git mein ho sakta hai:

```text
Git
 └── my-app/
      ├── deployment.yaml
      ├── service.yaml
      └── ingress.yaml
```

### Important

Git **deployment nahi karta**.

Git sirf desired configuration store karta hai.

---

# 2. Argo CD CLI

CLI ek **management interface** hai.

Example:

```bash
argocd login <argocd-server>
```

Ya:

```bash
argocd app list
argocd app get myapp
argocd app sync myapp
```

CLI se aap Argo CD ko commands de sakte ho.

For example:

```text
You
 ↓
argocd app sync myapp
 ↓
Argo CD
```

### Important distinction

CLI **continuously Git ko monitor nahi karta**.

Ye bahut important interview point hai.

Continuous monitoring/synchronization ka actual kaam **Argo CD controller** karta hai.

---

# 3. Argo CD Controller — Brain 🧠

Controller sabse important component hai.

Iska basic kaam:

> **Git mein desired state kya hai aur Kubernetes cluster mein actual state kya hai — dono compare karna.**

Example:

Git:

```text
replicas = 3
```

Kubernetes:

```text
replicas = 2
```

Controller detect karega:

```text
Desired State ≠ Actual State
```

So application:

```text
OutOfSync
```

Agar automated sync enabled hai:

```text
Git
 ↓
Controller
 ↓
Kubernetes
 ↓
replicas = 3
```

Agar auto-sync enabled nahi hai, controller difference detect karega aur application **OutOfSync** show karega; sync manually karna padega.

---

# 🔥 Complete Example

Suppose developer ne Git mein change kiya:

```text
image: myapp:v1
```

se:

```text
image: myapp:v2
```

### Step 1 — Developer Git mein change karta hai

```text
Git
image: myapp:v2
```

### Step 2 — Controller Git ki desired state dekhta hai

```text
Git → v2
```

### Step 3 — Controller Kubernetes ki actual state check karta hai

```text
Kubernetes → v1
```

### Step 4 — Difference detect

```text
Desired = v2
Actual  = v1

      ↓

OutOfSync
```

### Step 5 — Auto-sync enabled hai

Controller Kubernetes ko update karta hai:

```text
Kubernetes → v2
```

---

# CLI ka role kaha aata hai?

CLI **optional management path** hai.

For example:

```text
                 Git
                  │
                  ▼
              Controller
                  │
                  ▼
             Kubernetes


Developer
    │
    ▼
   CLI
    │
    ▼
 Argo CD API
```

CLI se developer:

```bash
argocd app sync myapp
```

kar sakta hai.

Lekin **CLI deployment engine nahi hai**.

---

## 🎯 Interview mein exactly aise bolo

> **"Argo CD follows a GitOps architecture where Git acts as the source of truth, the Argo CD CLI provides a command-line interface for managing applications, and the Argo CD controller continuously compares the desired state in Git with the actual state in Kubernetes. If there is a difference, the application becomes OutOfSync, and if automated sync is enabled, the controller reconciles the cluster back to the desired state."**

### Ek line mein:

**Git = kya chahiye**
**Controller = compare + reconcile**
**CLI = manage/control karne ka interface**

23. What are the major components of Argo CD?
Argo CD ke **major components** ko interview mein generally **4 main components** ke roop mein explain kiya jata hai:

```text
                         Git Repository
                              │
                              ▼
                    ┌──────────────────┐
                    │  Repo Server     │
                    │ Manifest Generate│
                    └────────┬─────────┘
                             │
                             ▼
                    ┌──────────────────┐
                    │ Application      │
                    │ Controller       │
                    │ Compare/Reconcile│
                    └────────┬─────────┘
                             │
                             ▼
                       Kubernetes API
                             │
                             ▼
                         Workloads


        User / CI
           │
           ▼
   ┌──────────────────┐
   │ API Server        │
   │ UI / CLI / API    │
   └──────────────────┘
```

### 1. **API Server**

Ye Argo CD ka **entry point** hai.

Iske through:

* Web UI
* CLI
* API
* Authentication/authorization

handle hote hain.

Example:

```bash
argocd app list
argocd app sync myapp
```

CLI → **Argo CD API Server** se communicate karta hai.

---

### 2. **Application Controller** 🧠

Ye Argo CD ka **brain** hai.

Iska main job:

```text
Git Desired State
       ↓
   Compare
       ↑
Kubernetes Actual State
```

Agar difference hai:

```text
Desired = v2
Actual  = v1

→ OutOfSync
```

Auto-sync enabled ho to controller cluster ko desired state mein reconcile karta hai.

---

### 3. **Repository Server**

Iska main responsibility hai **Git repository se application manifests retrieve aur generate karna**.

Ye support karta hai:

* Plain Kubernetes YAML
* Helm
* Kustomize
* Jsonnet
* Plugins

Example:

```text
Git
 ↓
Repo Server
 ↓
Rendered Kubernetes manifests
 ↓
Application Controller
```

**Important:** Repo Server khud Kubernetes mein deployment nahi karta. Ye manifests prepare/provide karta hai.

---

### 4. **Redis**

Argo CD Redis ka use **caching** ke liye karta hai.

For example:

* repository information
* application/state-related cached data
* performance improve karna

Redis **source of truth nahi hai**.

**Git = source of truth.**

---

## Bonus: Other Supporting Components

Production architecture mein aapko kuch additional components bhi mil sakte hain:

| Component                     | Main role                                           |
| ----------------------------- | --------------------------------------------------- |
| **API Server**                | UI/CLI/API requests                                 |
| **Application Controller**    | Compare + reconcile                                 |
| **Repo Server**               | Fetch/render manifests                              |
| **Redis**                     | Cache                                               |
| **ApplicationSet Controller** | Multiple applications automatically generate/manage |
| **Dex**                       | SSO/identity integration, when configured           |
| **Argo CD CLI/UI**            | User interaction                                    |

### ⭐ Interview mein short answer

> **"The major Argo CD components are the API Server, Application Controller, Repository Server, and Redis. The API Server handles UI, CLI and API requests; the Repository Server fetches and renders manifests from Git; the Application Controller compares the desired state with the Kubernetes actual state and reconciles differences; and Redis provides caching."**

**Yaad rakho:**

**API Server = communication**
**Repo Server = manifests**
**Controller = reconciliation**
**Redis = cache**


25. What is the responsibility of Argo CD API Server?
"Argo CD API Server is the central interface between users and Argo CD. It exposes APIs used by the UI and CLI, handles authentication and authorization, manages application operations, and triggers actions such as sync. The actual continuous reconciliation of Git desired state with Kubernetes state is handled by the Application Controller."
API Server = Request receive + Auth + Permission + Operations

27. What does the Repository Server do?
28. What does the Application Controller do?
29. What is Dex?
30. Why would you use Dex?
31. How does Argo CD communicate with Kubernetes?
32. How does Argo CD communicate with Git?
33. What happens when Repository Server cannot access Git?
34. What happens when Application Controller goes down?
35. What happens when Argo CD API Server goes down?
36. Is Argo CD itself deployed inside Kubernetes?
37. Which Kubernetes namespace is normally used for Argo CD?
38. What Kubernetes resources does Argo CD create internally?
39. How would you make Argo CD highly available?
40. How would you deploy Argo CD in production?
41. How would you monitor Argo CD components?
42. How would you troubleshoot a Repository Server issue?
43. How would you troubleshoot an Application Controller issue?

---

# 3. Argo CD Application

The PDF describes an **Application** as the main Argo CD object defining what to deploy, where, and how. 

41. What is an Argo CD Application?
42. What is the purpose of the Application CRD?
43. What is `apiVersion: argoproj.io/v1alpha1`?
44. What is the difference between an Argo Application and a Kubernetes Deployment?
45. What is `source` in an Argo CD Application?
46. What is `destination`?
47. What is `repoURL`?
48. What is `targetRevision`?
49. What does `path` represent?
50. What is the difference between `targetRevision: HEAD` and a specific Git tag?
51. How do you deploy from a Git branch?
52. How do you deploy from a Git tag?
53. How do you deploy from a Git commit?
54. Can one Git repository contain multiple applications?
55. Can one Argo Application deploy to multiple namespaces?
56. Can one Argo Application deploy to multiple clusters?
57. What is an Argo CD Project?
58. Why do we use Projects?
59. How do you restrict an application to specific repositories?
60. How do you restrict an application to specific clusters?

---

# 4. Desired State vs Actual State

61. What is desired state?
62. What is actual/live state?
63. Where is desired state stored in Argo CD?
64. Where does Argo CD get actual state from?
65. How does Argo CD compare desired and actual state?
66. What does reconciliation mean?
67. What is drift?
68. How does Argo CD detect configuration drift?
69. What happens if someone manually changes a Kubernetes Deployment?
70. What happens if someone manually deletes a Pod?
71. What happens if someone manually changes replicas?
72. What happens if someone changes an environment variable directly using `kubectl`?
73. How does self-healing work?
74. When should self-healing be enabled?
75. What are the risks of enabling self-healing?

---

# 5. Sync Status

The PDF lists the sync states as **Synced, OutOfSync and Unknown**. 

76. What is Sync Status?
77. What does `Synced` mean?
78. What does `OutOfSync` mean?
79. What does `Unknown` mean?
80. Why can an application become OutOfSync?
81. How do you troubleshoot OutOfSync?
82. Can an application be Healthy but OutOfSync?
83. Can an application be Synced but unhealthy?
84. What is the difference between Sync Status and Health Status?
85. What causes `Unknown` sync status?
86. How do you manually synchronize an OutOfSync application?

---

# 6. Health Status

87. What is Argo CD Health Status?
88. What does Healthy mean?
89. What does Progressing mean?
90. What does Degraded mean?
91. What does Missing mean?
92. Can an application be Synced but Degraded?
93. Why would a Deployment show Degraded?
94. How would you troubleshoot a Degraded application?
95. What happens if a resource is Missing?
96. How do you identify which Kubernetes resource is unhealthy?
97. How do you troubleshoot an application stuck in Progressing?

---

# 7. Manual vs Automatic Sync

The PDF distinguishes manual and automatic synchronization and shows `selfHeal` and `prune` under automated sync. 

98. What is manual sync?
99. What is automatic sync?
100. How do you enable automated sync?
101. What is `selfHeal`?
102. What is `prune`?
103. What happens when `prune: true` is enabled?
104. What happens if you delete a Kubernetes resource manually with self-healing enabled?
105. What happens if you remove a resource from Git with prune enabled?
106. What is the difference between self-heal and prune?
107. Would you enable prune in production?
108. What are the risks of enabling prune?
109. How would you safely introduce automated sync into production?
110. How would you prevent accidental deletion of production resources?

---

# 8. GitOps Scenario Questions

111. Developer changes replica count from 3 to 5 in Git. What happens?
112. Developer changes an image tag in Git. Explain the complete flow.
113. Someone changes replicas using `kubectl`. What happens?
114. Someone deletes a Pod manually. What happens?
115. Someone deletes a Deployment manually. What happens?
116. Someone modifies a ConfigMap manually. What happens?
117. Git says replicas = 3 but cluster says replicas = 5. What will Argo CD show?
118. Git repository is unavailable. What happens to existing applications?
119. Kubernetes API server is unavailable. What happens?
120. Git commit was made but Argo CD doesn't detect it. How do you troubleshoot?
121. Argo CD detects the commit but doesn't sync. Why?
122. Application is OutOfSync even though YAML looks identical. What could cause it?
123. Argo CD continuously changes a resource back and forth. Why?
124. Someone wants to make an emergency production change directly using kubectl. What should you do?
125. How do you handle emergency changes while following GitOps?

---

# 9. Helm + Argo CD

The PDF explicitly lists Helm as a supported source format. 

126. How does Argo CD work with Helm?
127. Is Argo CD a Helm replacement?
128. What is the difference between Helm and Argo CD?
129. Can Argo CD deploy a Helm chart from Git?
130. Can Argo CD deploy a chart from a Helm repository?
131. How do you provide Helm values?
132. What is `values.yaml`?
133. How do you override Helm values using Argo CD?
134. How would you manage different values for dev, QA and production?
135. How do you troubleshoot a Helm rendering failure?
136. What happens if Helm template rendering fails?
137. How do you debug an Argo CD Helm application?
138. Helm vs Kustomize — which would you choose and why?

---

# 10. Kustomize

139. What is Kustomize?
140. How does Argo CD support Kustomize?
141. What is a Kustomization?
142. What are overlays?
143. How would you maintain dev/QA/prod using Kustomize?
144. Helm vs Kustomize?
145. How do you troubleshoot Kustomize errors in Argo CD?
146. Can you combine Kustomize and Helm?
147. How would you structure a Git repository for Kustomize + Argo CD?

---

# 11. Multi-Cluster

The PDF specifically mentions Argo CD's **multi-cluster support**. 

148. Can Argo CD manage multiple Kubernetes clusters?
149. How do you register a cluster with Argo CD?
150. How do you deploy the same application to multiple clusters?
151. How would you manage dev, staging and production clusters?
152. How do you restrict an application to a particular cluster?
153. How do you handle cluster credentials securely?
154. What happens if one managed cluster becomes unavailable?
155. Can one Argo CD instance manage multiple production clusters?
156. What are the benefits of centralized Argo CD?
157. What are the risks of centralized Argo CD?
158. How would you design Argo CD for 50+ Kubernetes clusters?

---

# 12. App of Apps

The PDF identifies **App of Apps** as a pattern for managing multiple Argo CD applications from a single Git repository. 

159. What is App of Apps pattern?
160. Why do we use App of Apps?
161. How does App of Apps work?
162. What is the parent application?
163. What are child applications?
164. How would you manage 100 microservices using App of Apps?
165. App of Apps vs ApplicationSet?
166. What are the risks of App of Apps?
167. How would you structure a Git repository for App of Apps?
168. How would you handle dev/stage/prod using App of Apps?

---

# 13. Hooks

169. What are Argo CD hooks?
170. What is a PreSync hook?
171. What is a PostSync hook?
172. When would you use PreSync?
173. When would you use PostSync?
174. How would you run a database migration before deployment?
175. How would you run smoke tests after deployment?
176. What happens if a PreSync hook fails?
177. What happens if a PostSync hook fails?
178. How do you clean up hook resources?
179. What are the risks of using hooks?

---

# 14. Authentication & RBAC

The PDF mentions SSO through Dex and RBAC configuration through `argocd-rbac-cm`. 

180. How does authentication work in Argo CD?
181. What is Dex?
182. What is SSO?
183. How would you integrate Argo CD with LDAP?
184. How would you integrate Argo CD with GitHub SSO?
185. How would you integrate Argo CD with SAML?
186. What is Argo CD RBAC?
187. Where is Argo CD RBAC configured?
188. What is `argocd-rbac-cm`?
189. How would you give developers read-only access?
190. How would you give DevOps sync permission?
191. How would you restrict production access?
192. How would you implement least privilege in Argo CD?
193. How do you audit who deployed an application?
194. How would you prevent developers from deploying directly to production?

---

# 15. Security — 8-Year Level

195. How do you secure Argo CD in production?
196. How do you secure Git credentials?
197. How do you store private repository credentials?
198. How do you prevent secrets from being exposed in Git?
199. Should Kubernetes Secrets be stored directly in Git?
200. How would you integrate Argo CD with Vault?
201. How would you implement secret management with GitOps?
202. How do you secure Argo CD API Server?
203. How do you secure Argo CD UI?
204. How do you restrict network access to Argo CD?
205. How would you implement TLS?
206. How do you implement RBAC for multiple teams?
207. How do you separate production and non-production access?
208. How would you audit Argo CD activities?

---

# 16. Argo CD CLI

The PDF includes commands such as `argocd login`, `argocd app list`, `argocd app sync`, and `argocd app delete`. 

209. How do you login to Argo CD CLI?
210. How do you list applications?
211. How do you manually sync an application?
212. How do you delete an application?
213. How do you get application details?
214. How do you see application history?
215. How do you rollback an application?
216. How do you see application resources?
217. How do you refresh an application?
218. How do you troubleshoot an application using CLI?
219. What is the difference between refresh and sync?

---

# 17. Installation & Operations

The PDF shows installation into the `argocd` namespace and accessing the server through port-forwarding. 

220. How do you install Argo CD?
221. What are the prerequisites?
222. How do you expose Argo CD UI?
223. How do you access Argo CD without port-forward?
224. How would you expose Argo CD through an Ingress?
225. How would you expose Argo CD through LoadBalancer?
226. How do you retrieve the initial admin password?
227. What would you do after the initial installation?
228. How would you install Argo CD in EKS?
229. How would you install Argo CD using Helm?
230. How would you upgrade Argo CD?
231. How would you perform an Argo CD backup?
232. How would you restore Argo CD?
233. How would you migrate Argo CD to another cluster?

---

# 18. Production Troubleshooting — VERY IMPORTANT

For an 8-year candidate, these are often more important than definitions.

234. **Application is OutOfSync. How do you troubleshoot it?**
235. **Application is Synced but Degraded. What do you check?**
236. **Application is stuck in Progressing. What do you check?**
237. **Argo CD is not detecting the latest Git commit. What will you check?**
238. **Argo CD detects Git changes but doesn't sync automatically. Why?**
239. **Auto-sync is enabled but deployment doesn't happen. Troubleshoot.**
240. **Self-healing is enabled but Argo CD isn't correcting drift. Why?**
241. **Prune isn't deleting an old resource. Why?**
242. **Argo CD says resource is Missing. What do you check?**
243. **Repository authentication fails. How do you troubleshoot?**
244. **Private Git repository cannot be accessed. What do you check?**
245. **Argo CD cannot connect to Kubernetes API. What do you check?**
246. **Helm chart fails to render. How do you debug?**
247. **Kustomize build fails. How do you debug?**
248. **Deployment succeeds but Pods aren't becoming Ready. What do you check?**
249. **Argo CD continuously shows OutOfSync. What could cause it?**
250. **A resource keeps getting recreated. Why?**
251. **Argo CD UI is unavailable. How do you troubleshoot?**
252. **Argo CD Application Controller is consuming high CPU. What do you investigate?**
253. **Repository Server is consuming high memory. What could be happening?**
254. **Argo CD sync is taking too long. How do you troubleshoot?**
255. **One application is slow while others work normally. What do you investigate?**

---

# 19. Real Production Scenarios

256. You have **100 microservices**. How would you design Argo CD?
257. You have **dev, QA, staging and production**. How would you structure Git?
258. You have **10 Kubernetes clusters**. How would you manage them?
259. Developers need deployment access but should not have production admin access. Design RBAC.
260. A developer manually changes production resources. How would you handle it?
261. Production deployment failed halfway. How would you recover?
262. Git contains a bad configuration and Argo CD automatically synced it. What would you do?
263. How would you implement rollback?
264. How would you implement blue-green deployment with Argo CD?
265. How would you implement canary deployment with Argo CD?
266. How would you implement zero-downtime deployments?
267. How would you integrate Argo CD with CI?
268. Should CI deploy directly to Kubernetes when using Argo CD?
269. How would Jenkins/GitLab/GitHub Actions and Argo CD work together?
270. What would happen if CI succeeds but Argo CD fails?
271. What would happen if Git is unavailable during deployment?
272. How would you design disaster recovery for Argo CD?
273. How would you handle Argo CD failure during a production deployment?
274. How would you implement auditability?
275. How would you implement approval before production deployment?

---

# 20. CI/CD + GitOps Architecture

A very common **8-year DevOps interview question**:

### "Design a complete CI/CD pipeline using GitOps."

Be prepared to explain:

```text
Developer
   ↓
Git Application Source Code
   ↓
CI Pipeline
   ↓
Build
   ↓
Unit Test
   ↓
Security Scan
   ↓
Docker Build
   ↓
Push Image → Container Registry
   ↓
Update Image Tag
   ↓
GitOps Repository
   ↓
Argo CD
   ↓
Kubernetes
   ↓
Application
```

Questions:

276. Where does Jenkins fit in this architecture?
277. Where does Argo CD fit?
278. Why shouldn't Jenkins directly deploy to Kubernetes?
279. How does image promotion happen?
280. How does Argo CD know about a new image?
281. How would you implement automatic image updates?
282. How would you promote an image from dev → QA → prod?
283. How would you prevent an untested image from reaching production?
284. Where would security scanning happen?
285. Where would approval happen?
286. How would you implement rollback?
287. How would you maintain deployment history?

---

# 21. Advanced Architecture Questions

288. How does Argo CD scale?
289. What are the scalability bottlenecks?
290. How would you manage thousands of applications?
291. How would you reduce reconciliation load?
292. How would you design Argo CD for a large enterprise?
293. One Argo CD per cluster vs centralized Argo CD?
294. How would you isolate teams?
295. How would you isolate environments?
296. How would you handle multiple Git repositories?
297. How would you handle multiple Git organizations?
298. How would you handle multiple Kubernetes clusters?
299. How would you design Git repository structure?
300. How would you design branch strategy for GitOps?
301. How would you handle configuration management?
302. How would you manage secrets?
303. How would you implement compliance?
304. How would you implement disaster recovery?
305. How would you monitor Argo CD?

---

# 22. Tricky Interview Questions

306. Is Argo CD continuously polling Git?
307. Does Argo CD require Jenkins?
308. Can Argo CD deploy applications without CI?
309. Is Argo CD push-based or pull-based?
310. Why is GitOps generally considered pull-based?
311. What happens if someone changes the cluster manually?
312. What is the difference between Sync and Refresh?
313. What is the difference between Healthy and Synced?
314. What is the difference between selfHeal and prune?
315. What happens if you delete an application from Argo CD?
316. What happens if you delete an application YAML from Git?
317. What happens when `prune=true`?
318. Can Argo CD manage resources that were not originally created by Argo CD?
319. What happens if two Argo Applications manage the same resource?
320. Can two Argo Applications point to the same Git repository?
321. Can one Argo CD instance manage multiple clusters?
322. Can Argo CD manage non-Kubernetes infrastructure?
323. Is Helm itself a deployment tool like Argo CD?
324. What happens if Git and the Kubernetes cluster are both unavailable?
325. Does Argo CD store the complete desired state internally?

---

# 23. "Explain Your Project" Questions

At **8 years**, expect the interviewer to move from theory to your experience:

326. Explain your Argo CD architecture from your current/previous project.
327. How many clusters did you manage?
328. How many applications did you manage?
329. How many developers used Argo CD?
330. How did you structure your Git repositories?
331. How did you manage environments?
332. How did you manage secrets?
333. How did you implement RBAC?
334. How did you implement SSO?
335. How did you implement automated sync?
336. Did you use self-healing?
337. Did you use pruning?
338. Did you use Helm or Kustomize?
339. Did you use App of Apps?
340. Did you use ApplicationSet?
341. How did you handle production approvals?
342. How did you handle rollback?
343. How did you troubleshoot failed deployments?
344. What was the biggest Argo CD issue you faced?
345. What performance issue did you face?
346. What security issue did you face?
347. What improvements did you make to your Argo CD platform?

---

# 24. Top 20 Questions You MUST Be Able to Answer

If your interview is soon, prioritize these:

1. **What is Argo CD and why do we use it?**
2. **Explain Argo CD architecture.**
3. **Explain GitOps.**
4. **Explain desired state vs actual state.**
5. **What is reconciliation?**
6. **Explain Sync vs Health status.**
7. **What is OutOfSync and how do you troubleshoot it?**
8. **Manual sync vs automated sync.**
9. **Explain selfHeal and prune.**
10. **What happens when someone manually changes Kubernetes resources?**
11. **How does Argo CD work with Helm?**
12. **How does Argo CD work with Kustomize?**
13. **How do you manage multiple clusters?**
14. **Explain App of Apps.**
15. **Explain Argo CD RBAC and SSO.**
16. **How do you secure Argo CD?**
17. **How do you troubleshoot a failed sync?**
18. **How do Jenkins/GitLab CI and Argo CD work together?**
19. **Design Argo CD for multiple environments and clusters.**
20. **Explain your real production Argo CD implementation.**

### Important for your 8-year level

Don't prepare these as **one-line definitions only**. The interviewer can easily turn:

> "What is self-healing?"

into:

> "Okay, someone manually changes replicas in production. Show me what happens."

and then:

> "What if self-heal is enabled but it doesn't revert?"

and then:

> "How would you troubleshoot that?"

That **definition → implementation → scenario → troubleshooting → architecture** progression is what you should practice for an 8-year DevOps interview.

The uploaded PDF itself demonstrates this progression from Argo CD fundamentals through architecture, application creation, sync strategies, RBAC, advanced features and a deployment demo.  
