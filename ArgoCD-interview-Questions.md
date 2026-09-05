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
Argo CD ka **Repository Server (repo-server)** ka simple role hai:

> **Git se application configuration lena aur usko final Kubernetes manifests mein render/prepare karna.**

### Flow

```text
              Git
               │
               │
               ▼
       ┌────────────────┐
       │ Repository     │
       │ Server         │
       └───────┬────────┘
               │
               │ Final Kubernetes YAML
               ▼
       Application Controller
               │
               ▼
          Kubernetes
```

### Example 1 — Plain YAML

Git mein:

```text
deployment.yaml
service.yaml
```

Repo Server un manifests ko retrieve karta hai aur Controller ko provide karta hai.

### Example 2 — Helm

Git mein:

```text
my-chart/
  ├── Chart.yaml
  ├── values.yaml
  └── templates/
```

Repo Server:

```text
Helm Chart + values.yaml
          ↓
      Helm render
          ↓
Final Kubernetes YAML
```

### Example 3 — Kustomize

```text
base + overlay
      ↓
Repo Server
      ↓
Final Kubernetes manifests
```

### Sabse important distinction

**Repo Server deploy nahi karta.**

```text
Repo Server
   ↓
"Ye manifests deploy hone chahiye"
   ↓
Controller
   ↓
"Main check/reconcile karta hoon"
   ↓
Kubernetes
```

### Interview mein bolo:

> **"Repository Server is responsible for fetching application configuration from Git and generating or rendering the final Kubernetes manifests. It supports sources such as plain YAML, Helm and Kustomize. It does not deploy the application; the Application Controller handles reconciliation and deployment."**

**Yaad rakho:**

**Repo Server = Fetch + Render**
**Controller = Compare + Reconcile**

29. What does the Application Controller do?
Argo CD ka **Application Controller** sabse important component hai. Isko Argo CD ka **brain** samjho. 🧠

> **Application Controller ka main kaam hai Git ki desired state aur Kubernetes ki actual state ko continuously compare karna aur difference hone par reconciliation karna.**

### Simple flow

```text
              Git
               │
               │ Desired State
               ▼
         Repository Server
               │
               │ Rendered YAML
               ▼
      ┌─────────────────────┐
      │ Application         │
      │ Controller 🧠       │
      └──────────┬──────────┘
                 │
          Compare / Reconcile
                 │
                 ▼
            Kubernetes
            Actual State
```

### Example

Git mein:

```yaml
replicas: 3
image: myapp:v2
```

Lekin Kubernetes mein:

```text
replicas: 2
image: myapp:v1
```

Controller compare karega:

```text
Desired State = replicas 3, image v2
Actual State  = replicas 2, image v1

             ↓

          OutOfSync
```

Agar **auto-sync enabled** hai, Controller Kubernetes ko Git wali state mein le aayega:

```text
Kubernetes
replicas → 3
image    → v2
```

Agar auto-sync enabled nahi hai, to application **OutOfSync** rahegi jab tak manual sync nahi kiya jata.

---

### Controller ki main responsibilities

1. **Desired state obtain karna** — Repo Server se rendered manifests leta hai.
2. **Live state check karna** — Kubernetes resources ki current state dekhta hai.
3. **Diff detect karna** — desired vs actual compare karta hai.
4. **Health/status assess karna** — application healthy, degraded, progressing etc. hai ya nahi.
5. **Reconciliation** — difference hone par resources ko desired state mein laata hai.
6. **Sync operations execute karna** — automatic ya manually triggered sync ko perform karta hai.

### ⭐ Interview answer

> **"The Application Controller is the core reconciliation component of Argo CD. It continuously compares the desired state obtained from Git with the live state in Kubernetes, detects drift, evaluates application health, and reconciles the cluster back to the desired state. If automated sync is enabled, it can automatically apply the required changes."**

**Easy trick:**

**Repo Server → Fetch + Render**
**Application Controller → Compare + Detect + Reconcile**
**Kubernetes → Run**

31. What is Dex?
Haan, **bilkul** — Argo CD API Server bhi authentication aur authorization handle karta hai. Confusion isliye hoti hai kyunki **Dex aur API Server ke roles overlap jaise lagte hain**, but actually dono ka kaam different hai.

### Simple distinction

```text
User
  |
  | Login
  ↓
Argo CD API Server
  |
  | "User ko authenticate karna hai"
  ↓
Dex
  |
  | External Identity Provider
  ↓
AD / LDAP / GitHub / OIDC
  |
  | Authentication successful
  ↓
Dex → API Server
  |
  | "Ab user kya kar sakta hai?"
  ↓
Argo CD RBAC
  |
  ↓
Allow / Deny
```

### 1. API Server kya karta hai?

**API Server = Argo CD ka main gateway**

Ye:

* User/API requests receive karta hai
* Authentication mechanism ko handle karta hai
* Token/session validate karta hai
* RBAC/authorization enforce karta hai
* Repository/Application operations ke requests route karta hai

Example:

> "Bhupendra ne Argo CD mein login kiya. Kya iska token valid hai? Aur kya is user ko `prod` application sync karne ki permission hai?"

Ye **API Server + RBAC** side ka responsibility hai.

---

### 2. Dex kya karta hai?

**Dex = external identity system se authentication karwane ka broker**

Suppose company mein:

```text
Company AD
   ↓
   Dex
   ↓
Argo CD API Server
```

Dex ka role hai:

> "Ye user actually company ke AD/LDAP/GitHub/OIDC mein valid user hai ya nahi?"

Dex **identity verification** ko external identity provider ke saath integrate karta hai.

---

### Authentication vs Authorization

Yaad rakhne ka easiest way:

| Question                            | Responsibility                  |
| ----------------------------------- | ------------------------------- |
| **Who are you?**                    | Dex / external IdP + API Server |
| **Is your login/token valid?**      | API Server                      |
| **What can you do?**                | Argo CD RBAC / API Server       |
| **Can you sync production?**        | Argo CD RBAC                    |
| **Can you login using company AD?** | Dex + AD                        |

### Interview mein kaise bolna hai?

> **"Argo CD API Server handles incoming requests, authentication/token validation, and authorization through RBAC. Dex is used as an authentication broker when Argo CD needs to integrate with external identity providers such as LDAP, GitHub, OIDC, or SAML. So Dex handles the external identity integration, while the API Server enforces access to Argo CD resources."**

**One-line memory trick:**

> **Dex = Identity verify karwane wala bridge**
> **API Server = Request ko authenticate/authorize karke Argo CD access control karne wala gateway**

33. Why would you use Dex?
   You use **Dex when you want Argo CD to authenticate users through an external Identity Provider (IdP)** instead of managing users independently inside Argo CD.

### Simple example

Suppose your company already has **Active Directory (AD)**:

```text
Developer
    |
    | Login
    ↓
 Argo CD
    |
    ↓
   Dex
    |
    ↓
Active Directory
    |
    ↓
"Yes, this user is valid"
    |
    ↓
Argo CD API Server
    |
    ↓
Argo CD RBAC
    |
    ↓
"What is this user allowed to do?"
```

### Why Dex?

**1. SSO (Single Sign-On)**
Users can use the same company identity to access Argo CD.

**2. External authentication**
You can connect Argo CD with:

* LDAP / Active Directory
* GitHub
* GitLab
* Google
* OIDC providers
* SAML-based identity systems

**3. Centralized user management**

Instead of creating/managing users separately in Argo CD:

```text
Argo CD users
   ❌ user1
   ❌ user2
   ❌ user3
```

You manage them in your company's identity system:

```text
Active Directory
   ├── Developers
   ├── DevOps
   └── Admins
```

**4. Group-based access**

For example:

```text
AD Group: devops
       ↓
     Dex
       ↓
   Argo CD
       ↓
RBAC: allow sync
```

So you can say:

> Developers can view applications, but only DevOps can sync production.

### Most important distinction

Don't say:

> "Dex does authorization."

Instead:

> **Dex primarily provides the bridge between Argo CD and external identity providers for authentication. Argo CD API Server and RBAC handle access control/authorization.**

### Interview answer 🎯

> **"We use Dex when we want Argo CD to integrate with an external identity provider and provide SSO. Dex acts as an authentication broker between Argo CD and systems like LDAP, Active Directory, GitHub, or OIDC providers. After the user is authenticated, Argo CD API Server validates the identity/token and its RBAC policies determine what the user is authorized to do."**

35. How does Argo CD communicate with Kubernetes?
   Argo CD **Kubernetes API Server ke through communicate karta hai**. Argo CD directly Pods/Deployments se baat nahi karta.

### Flow samjho

```text
          Git Repository
               |
               | manifests
               ↓
        ┌───────────────┐
        │    Argo CD    │
        │   Controller  │
        └───────┬───────┘
                |
                | Kubernetes API calls
                ↓
       ┌──────────────────┐
       │ Kubernetes API   │
       │     Server       │
       └────────┬─────────┘
                |
        ┌───────┴────────┐
        ↓                ↓
   Deployment           Service
        ↓
       Pods
```

### Step-by-step

**1. Argo CD Git se desired state read karta hai**

Example Git mein:

```yaml
replicas: 3
image: nginx:1.27
```

**2. Argo CD current state Kubernetes se check karta hai**

Argo CD Kubernetes API Server ko query karta hai:

> "Currently kya deployed hai?"

```text
Desired state: 3 replicas
Current state: 2 replicas
```

**3. Argo CD difference detect karta hai**

```text
Desired ≠ Current
       ↓
OutOfSync
```

**4. Argo CD API Server ko request bhejta hai**

For example, Deployment ko update karne ke liye Kubernetes API call:

```text
Argo CD
   |
   | PATCH / UPDATE Deployment
   ↓
Kubernetes API Server
```

**5. Kubernetes baaki ka kaam karta hai**

Kubernetes API Server change accept karta hai, phir controllers/scheduler etc. desired state ko actual state mein le jaate hain.

```text
Argo CD
   ↓
Kubernetes API Server
   ↓
Deployment Controller
   ↓
ReplicaSet
   ↓
Pods
```

### Authentication kaise hota hai?

Argo CD cluster credentials use karta hai, commonly:

* ServiceAccount/token
* Kubernetes credentials
* TLS certificates, depending on configuration

Aur Kubernetes **RBAC** decide karta hai ki Argo CD ko kya permissions hain.

### Interview answer 🎯

> **"Argo CD communicates with Kubernetes through the Kubernetes API Server. The Argo CD Application Controller compares the desired state from Git with the live state retrieved from the Kubernetes API Server. If there is a difference, Argo CD uses Kubernetes API calls to create, update, or delete resources. Kubernetes RBAC controls what Argo CD is allowed to modify."**

**Golden line:**
**Argo CD → Kubernetes API Server → Kubernetes resources**.

37. How does Argo CD communicate with Git?
Argo CD **Git repository se manifests/configuration read karne ke liye communicate karta hai**. Is communication ka main component **Repository Server** hai.

### Simple flow

```text
             Git Repository
          (GitHub / GitLab etc.)
                  ↑
                  │
            Git protocol
         HTTPS / SSH / etc.
                  │
                  ↓
        ┌──────────────────┐
        │ Argo CD          │
        │ Repository       │
        │ Server           │
        └────────┬─────────┘
                 │
                 ↓
        Kubernetes manifests
                 │
                 ↓
        Application Controller
                 │
                 ↓
        Kubernetes API Server
```

### Step-by-step

**1. Argo CD ko Git repository configured hoti hai**

Example:

```text
repo: github.com/company/my-app
path: k8s/
```

**2. Repository Server Git se connect karta hai**

Argo CD Git repository ko access karne ke liye commonly:

```text
HTTPS
   or
SSH
```

use karta hai.

Agar private repository hai, Argo CD credentials use karta hai, jaise:

```text
SSH private key
Personal Access Token
Git credentials
```

**3. Repository Server repository ko fetch/clone karta hai**

For example:

```text
Git
 |
 | git fetch / clone
 ↓
Repository Server
```

**4. Manifests generate/render hote hain**

Agar plain YAML hai:

```text
deployment.yaml
service.yaml
```

to directly use ho sakta hai.

Agar Helm/Kustomize hai, Repository Server unhe render karke Kubernetes manifests generate karta hai.

```text
Git
 ↓
Helm/Kustomize
 ↓
Final Kubernetes manifests
```

**5. Application Controller ko desired state milti hai**

```text
Repository Server
       ↓
Desired state
       ↓
Application Controller
       ↓
Compare with Kubernetes
```

Then:

```text
Desired State ≠ Live State
          ↓
       OutOfSync
          ↓
Sync
          ↓
Kubernetes API Server
```

### Git change hone par Argo CD ko kaise pata chalta hai?

Do common mechanisms:

```text
Git change
   ↓
Webhook ───────→ Argo CD
```

**OR**

```text
Argo CD
   ↓
Periodic polling
   ↓
Git repository
```

Webhook generally change detection ko faster banata hai, while Argo CD also periodically refreshes repositories.

### Important interview distinction

| Component                  | Git ke saath kya karta hai?                       |
| -------------------------- | ------------------------------------------------- |
| **Repository Server**      | Git repo access, fetch/clone, manifest generation |
| **Application Controller** | Desired state vs live Kubernetes state compare    |
| **API Server**             | Argo CD API/UI requests handle karta hai          |
| **Git**                    | Desired state ka source of truth                  |

### 🎯 Interview answer

> **"Argo CD communicates with Git primarily through the Repository Server. The Repository Server connects to the configured Git repository using protocols such as HTTPS or SSH, authenticates using configured credentials, fetches the application source, and generates the desired Kubernetes manifests. The Application Controller then compares those manifests with the live state in Kubernetes and syncs the application when required."**

39. What happens when Repository Server cannot access Git?
Agar **Argo CD Repository Server Git repository ko access nahi kar paata**, to Argo CD **Git se latest desired state fetch nahi kar paayega**.

### Flow

```text
             Git Repository
                   ❌
              Connection
               failed
                   ↑
                   |
        ┌──────────────────┐
        │ Repository Server │
        └────────┬─────────┘
                 |
                 ❌
       Cannot fetch manifests
                 |
                 ↓
        Application Controller
                 |
                 ↓
       Latest desired state
          unavailable
```

### Kya hota hai?

**1. Repository Server Git access try karta hai**

For example:

```text
GitHub
   ↑
   | HTTPS/SSH
   |
Repository Server
```

But connection fail ho sakta hai because:

* Git server down
* Network issue
* DNS problem
* Wrong repository URL
* Invalid/expired credentials
* SSH key problem
* Proxy/firewall issue

---

**2. Repository Server manifests fetch/render nahi kar paata**

Suppose Git mein latest version hai:

```text
Git:
image: app:v2
```

But Repository Server Git access nahi kar pa raha.

Argo CD ko `v2` ka latest desired state nahi milega.

---

**3. Argo CD sync nahi kar paayega**

Because Argo CD ko pata hi nahi chalega ki Git mein desired state kya hai.

```text
Git unavailable
      ↓
No latest manifests
      ↓
Cannot calculate latest desired state
      ↓
Sync fails / cannot proceed
```

---

### Important: Existing application ka kya hoga?

**Existing Kubernetes workloads automatically stop nahi hote.**

For example:

```text
Kubernetes
   ↓
Pod v1
   ↓
Running
```

Agar suddenly Git unavailable ho gaya:

```text
Git ❌

Kubernetes
   ↓
Pod v1
   ↓
Still running
```

Argo CD Git access failure ki wajah se normally running resources ko delete nahi karta.

So **Git outage ≠ application outage**.

But Argo CD **new Git changes sync nahi kar paayega** until repository access is restored.

### Interview answer 🎯

> **"If the Repository Server cannot access Git, Argo CD cannot fetch or generate the latest desired manifests. As a result, reconciliation or synchronization of new Git changes cannot proceed. However, already running Kubernetes workloads generally continue running because they are managed by Kubernetes itself. Once Git connectivity is restored, Argo CD can fetch the desired state and resume reconciliation."**

41. What happens when Application Controller goes down?
   Agar **Argo CD Application Controller down ho jata hai**, to sabse important impact ye hai ki **Argo CD reconciliation/sync temporarily stop ho jata hai**.

### Simple flow

```text
Git
 ↓
Repository Server
 ↓
Desired State
 ↓
❌ Application Controller DOWN
 ↓
No reconciliation
 ↓
Kubernetes
```

### Kya-kya hoga?

**1. Existing Pods normally chalte rahenge**

Application Controller down hone ka matlab ye **nahi** hai ki Kubernetes workloads stop ho jayenge.

```text
Application Controller ❌
        |
        X
        |
Kubernetes
   ↓
Pods → Running ✅
```

Kubernetes apne controllers ke through Pods, Deployments, Services etc. ko manage karta rahega.

---

**2. Git → Kubernetes reconciliation stop ho jayega**

Normally:

```text
Git desired state
       ↓
Application Controller
       ↓
Compare
       ↓
Kubernetes live state
       ↓
Sync if needed
```

Controller down:

```text
Git desired state
       ↓
Application Controller ❌
       ↓
       STOP
```

Isliye **new changes automatically sync nahi honge**.

---

**3. Drift detect nahi hoga**

Suppose Git says:

```text
replicas: 3
```

Someone manually Kubernetes mein change kar deta hai:

```text
replicas: 1
```

Normally Application Controller detect karta:

```text
Git = 3
K8s = 1
   ↓
OutOfSync
   ↓
Reconcile
```

Controller down hone par ye reconciliation nahi hogi.

---

**4. Controller wapas aane par**

Jaise hi Application Controller recover hota hai:

```text
Application Controller
        ↓
Read desired state from Git
        ↓
Read live state from Kubernetes
        ↓
Compare
        ↓
Detect difference
        ↓
Reconcile / Sync
```

So system **eventually catch up** kar sakta hai.

### 🎯 Interview answer

> **"If the Argo CD Application Controller goes down, Argo CD temporarily stops its reconciliation loop. Existing Kubernetes workloads continue running because Kubernetes manages them independently. However, Argo CD will not detect drift or automatically synchronize new Git changes while the controller is down. Once the controller recovers, it compares the desired state from Git with the live Kubernetes state and resumes reconciliation."**

**Easy memory:**

> **Controller DOWN → Kubernetes application keeps running, but Argo CD stops watching and reconciling.**

   
43. What happens when Argo CD API Server goes down?
   Agar **Argo CD API Server down** ho jaye, to mainly **Argo CD ka UI, CLI aur API access** impact hota hai. But **Application Controller independently reconciliation karta reh sakta hai**.

### Flow

```text
                    Git
                     ↓
              Repository Server
                     ↓
          Application Controller
                     ↓
             Kubernetes API
                     ↓
                   Pods
                  ✅ Running


User ──X──> ❌ Argo CD API Server
             (DOWN)
              ↑
          UI / CLI
```

### 1. UI access nahi hoga ❌

```text
Browser
   ↓
Argo CD API Server ❌
```

Argo CD Web UI accessible nahi hogi.

### 2. Argo CD CLI/API commands fail honge ❌

For example:

```bash
argocd app list
argocd app sync my-app
```

API Server down hone par ye requests fail hongi because CLI normally API Server ke through communicate karta hai.

### 3. Existing applications continue running ✅

Ye **important interview point** hai.

```text
API Server ❌

Kubernetes
   ↓
Pods
   ↓
Running ✅
```

API Server Argo CD ka API component hai; **Kubernetes API Server alag hai**.

So:

> **Argo CD API Server down ≠ Kubernetes API Server down**

Existing Pods/Services normally continue running.

### 4. Application Controller reconciliation kar sakta hai ✅

Application Controller ka direct relationship Kubernetes API Server aur Repository Server ke saath hota hai.

So API Server down hone ke bawajood:

```text
Git
 ↓
Repository Server
 ↓
Application Controller
 ↓
Kubernetes API Server
 ↓
Sync/Reconciliation
```

**continue kar sakta hai**, assuming those components are healthy.

### 5. Manual operations affected ❌

User manually:

```text
argocd app sync
argocd app delete
argocd app get
```

nahi kar paayega through the unavailable API Server.

---

### Quick comparison

| Component down             | Main impact                                 |
| -------------------------- | ------------------------------------------- |
| **Repository Server**      | Git se manifests fetch/render nahi honge    |
| **Application Controller** | Reconciliation/sync stop                    |
| **API Server**             | UI/CLI/API access unavailable               |
| **Kubernetes API Server**  | Argo CD + Kubernetes communication affected |

### 🎯 Interview answer

> **"If the Argo CD API Server goes down, the Argo CD UI, CLI, and API access become unavailable. However, existing applications continue running in Kubernetes, and the Application Controller can continue reconciliation independently, provided it can access the Repository Server and Kubernetes API Server. Once the API Server recovers, users can access Argo CD again."**

**Memory trick:**

> **API Server DOWN → User access DOWN; Kubernetes workloads and Controller can continue.**

   
45. Is Argo CD itself deployed inside Kubernetes?
Yes. In most real-world setups, Argo CD itself runs as an application inside a Kubernetes cluster.

### Architecture

![](data\:image/svg+xml;charset=utf-8,%3Csvg%20font-family%3D%22-apple-system-body%2C%20ui-sans-serif%2C%20-apple-system%2C%20system-ui%2C%20%26quot%3BSegoe%20UI%26quot%3B%2C%20Helvetica%2C%20%26quot%3BApple%20Color%20Emoji%26quot%3B%2C%20Arial%2C%20sans-serif%2C%20%26quot%3BSegoe%20UI%20Emoji%26quot%3B%2C%20%26quot%3BSegoe%20UI%20Symbol%26quot%3B%22%20font-weight%3D%22400%22%20data-d-component%3D%22svg%22%20fill%3D%22currentColor%22%20style%3D%22color%3Argb\(255%2C%20255%2C%20255\)%22%20viewBox%3D%220%200%20640%20360%22%20xmlns%3D%22http%3A%2F%2Fwww.w3.org%2F2000%2Fsvg%22%3E%3Crect%20width%3D%22640%22%20height%3D%22360%22%20rx%3D%2212%22%20fill%3D%22none%22%20stroke%3D%22currentColor%22%20stroke-width%3D%222%22%2F%3E%3Ctext%20x%3D%2224%22%20y%3D%2238%22%20font-size%3D%2222%22%20font-weight%3D%22bold%22%20fill%3D%22currentColor%22%3EKubernetes%20Cluster%3C%2Ftext%3E%3Crect%20x%3D%2236%22%20y%3D%2270%22%20width%3D%22130%22%20height%3D%2256%22%20rx%3D%2210%22%20fill%3D%22none%22%20stroke%3D%22currentColor%22%2F%3E%3Ctext%20x%3D%22101%22%20y%3D%22103%22%20font-size%3D%2214%22%20text-anchor%3D%22middle%22%20fill%3D%22currentColor%22%3EAPI%20Server%3C%2Ftext%3E%3Crect%20x%3D%22190%22%20y%3D%2270%22%20width%3D%22130%22%20height%3D%2256%22%20rx%3D%2210%22%20fill%3D%22none%22%20stroke%3D%22currentColor%22%2F%3E%3Ctext%20x%3D%22255%22%20y%3D%2296%22%20font-size%3D%2214%22%20text-anchor%3D%22middle%22%20fill%3D%22currentColor%22%3ERepository%3C%2Ftext%3E%3Ctext%20x%3D%22255%22%20y%3D%22112%22%20font-size%3D%2214%22%20text-anchor%3D%22middle%22%20fill%3D%22currentColor%22%3EServer%3C%2Ftext%3E%3Crect%20x%3D%22344%22%20y%3D%2270%22%20width%3D%22130%22%20height%3D%2256%22%20rx%3D%2210%22%20fill%3D%22none%22%20stroke%3D%22currentColor%22%2F%3E%3Ctext%20x%3D%22409%22%20y%3D%2296%22%20font-size%3D%2214%22%20text-anchor%3D%22middle%22%20fill%3D%22currentColor%22%3EApplication%3C%2Ftext%3E%3Ctext%20x%3D%22409%22%20y%3D%22112%22%20font-size%3D%2214%22%20text-anchor%3D%22middle%22%20fill%3D%22currentColor%22%3EController%3C%2Ftext%3E%3Crect%20x%3D%22498%22%20y%3D%2270%22%20width%3D%22106%22%20height%3D%2256%22%20rx%3D%2210%22%20fill%3D%22none%22%20stroke%3D%22currentColor%22%2F%3E%3Ctext%20x%3D%22551%22%20y%3D%22103%22%20font-size%3D%2214%22%20text-anchor%3D%22middle%22%20fill%3D%22currentColor%22%3EDex%3C%2Ftext%3E%3Crect%20x%3D%22172%22%20y%3D%22222%22%20width%3D%22296%22%20height%3D%2278%22%20rx%3D%2212%22%20fill%3D%22none%22%20stroke%3D%22currentColor%22%20stroke-width%3D%222%22%2F%3E%3Ctext%20x%3D%22320%22%20y%3D%22248%22%20font-size%3D%2216%22%20font-weight%3D%22bold%22%20text-anchor%3D%22middle%22%20fill%3D%22currentColor%22%3EKubernetes%20API%20Server%3C%2Ftext%3E%3Ctext%20x%3D%22320%22%20y%3D%22268%22%20font-size%3D%2212%22%20text-anchor%3D%22middle%22%20fill%3D%22currentColor%22%3EDeployments%20%E2%80%A2%20Services%20%E2%80%A2%20Pods%3C%2Ftext%3E%3Cpath%20d%3D%22M409%20126%20V222%22%20stroke%3D%22currentColor%22%20stroke-width%3D%222%22%20fill%3D%22none%22%2F%3E%3Cpolygon%20points%3D%22403%2C212%20409%2C222%20415%2C212%22%20fill%3D%22currentColor%22%2F%3E%3Cpath%20d%3D%22M255%20126%20V166%20H96%20V182%22%20stroke%3D%22currentColor%22%20stroke-width%3D%222%22%20fill%3D%22none%22%2F%3E%3Cpolygon%20points%3D%2290%2C172%2096%2C182%20102%2C172%22%20fill%3D%22currentColor%22%2F%3E%3Ctext%20x%3D%2224%22%20y%3D%22188%22%20font-size%3D%2213%22%20fill%3D%22currentColor%22%3EGit%3C%2Ftext%3E%3C%2Fsvg%3E)

### Argo CD namespace

When you install Argo CD:

Bash

```
kubectl create namespace argocd
kubectl apply -n argocd -f install.yaml
```

It creates Pods like:

```
argocd-server
argocd-repo-server
argocd-application-controller
argocd-dex-server
argocd-redis
```

These are just Kubernetes Pods running in the `argocd` namespace.

### Real example

![](data\:image/svg+xml;charset=utf-8,%3Csvg%20font-family%3D%22-apple-system-body%2C%20ui-sans-serif%2C%20-apple-system%2C%20system-ui%2C%20%26quot%3BSegoe%20UI%26quot%3B%2C%20Helvetica%2C%20%26quot%3BApple%20Color%20Emoji%26quot%3B%2C%20Arial%2C%20sans-serif%2C%20%26quot%3BSegoe%20UI%20Emoji%26quot%3B%2C%20%26quot%3BSegoe%20UI%20Symbol%26quot%3B%22%20font-weight%3D%22400%22%20data-d-component%3D%22svg%22%20fill%3D%22currentColor%22%20style%3D%22color%3Argb\(255%2C%20255%2C%20255\)%22%20viewBox%3D%220%200%20640%20260%22%20xmlns%3D%22http%3A%2F%2Fwww.w3.org%2F2000%2Fsvg%22%3E%3Crect%20width%3D%22640%22%20height%3D%22260%22%20rx%3D%2212%22%20fill%3D%22none%22%20stroke%3D%22currentColor%22%20stroke-width%3D%222%22%2F%3E%3Ctext%20x%3D%2222%22%20y%3D%2234%22%20font-size%3D%2220%22%20font-weight%3D%22bold%22%20fill%3D%22currentColor%22%3EKubernetes%20Cluster%3C%2Ftext%3E%3Crect%20x%3D%2226%22%20y%3D%2256%22%20width%3D%22260%22%20height%3D%22178%22%20rx%3D%2210%22%20fill%3D%22none%22%20stroke%3D%22currentColor%22%2F%3E%3Ctext%20x%3D%2242%22%20y%3D%2278%22%20font-size%3D%2216%22%20font-weight%3D%22bold%22%20fill%3D%22currentColor%22%3Eargocd%20namespace%3C%2Ftext%3E%3Crect%20x%3D%2244%22%20y%3D%2292%22%20width%3D%2296%22%20height%3D%2234%22%20rx%3D%228%22%20fill%3D%22none%22%20stroke%3D%22currentColor%22%2F%3E%3Ctext%20x%3D%2292%22%20y%3D%22113%22%20font-size%3D%2212%22%20text-anchor%3D%22middle%22%20fill%3D%22currentColor%22%3EAPI%20Server%3C%2Ftext%3E%3Crect%20x%3D%22154%22%20y%3D%2292%22%20width%3D%22114%22%20height%3D%2234%22%20rx%3D%228%22%20fill%3D%22none%22%20stroke%3D%22currentColor%22%2F%3E%3Ctext%20x%3D%22211%22%20y%3D%22113%22%20font-size%3D%2212%22%20text-anchor%3D%22middle%22%20fill%3D%22currentColor%22%3ERepo%20Server%3C%2Ftext%3E%3Crect%20x%3D%2244%22%20y%3D%22146%22%20width%3D%22224%22%20height%3D%2240%22%20rx%3D%228%22%20fill%3D%22none%22%20stroke%3D%22currentColor%22%2F%3E%3Ctext%20x%3D%22156%22%20y%3D%22170%22%20font-size%3D%2212%22%20text-anchor%3D%22middle%22%20fill%3D%22currentColor%22%3EApplication%20Controller%3C%2Ftext%3E%3Crect%20x%3D%22354%22%20y%3D%2256%22%20width%3D%22260%22%20height%3D%22178%22%20rx%3D%2210%22%20fill%3D%22none%22%20stroke%3D%22currentColor%22%2F%3E%3Ctext%20x%3D%22370%22%20y%3D%2278%22%20font-size%3D%2216%22%20font-weight%3D%22bold%22%20fill%3D%22currentColor%22%3Eecommerce%20namespace%3C%2Ftext%3E%3Crect%20x%3D%22384%22%20y%3D%22108%22%20width%3D%22200%22%20height%3D%2256%22%20rx%3D%2210%22%20fill%3D%22none%22%20stroke%3D%22currentColor%22%2F%3E%3Ctext%20x%3D%22484%22%20y%3D%22132%22%20font-size%3D%2213%22%20text-anchor%3D%22middle%22%20fill%3D%22currentColor%22%3EDeployment%3C%2Ftext%3E%3Ctext%20x%3D%22484%22%20y%3D%22148%22%20font-size%3D%2213%22%20text-anchor%3D%22middle%22%20fill%3D%22currentColor%22%3EPods%3C%2Ftext%3E%3Cpath%20d%3D%22M268%20166%20H384%22%20stroke%3D%22currentColor%22%20stroke-width%3D%222%22%20fill%3D%22none%22%2F%3E%3Cpolygon%20points%3D%22374%2C160%20384%2C166%20374%2C172%22%20fill%3D%22currentColor%22%2F%3E%3Ctext%20x%3D%22326%22%20y%3D%22156%22%20font-size%3D%2211%22%20text-anchor%3D%22middle%22%20fill%3D%22currentColor%22%3Emanages%3C%2Ftext%3E%3C%2Fsvg%3E)

### Interview answer

> Yes. Argo CD is typically deployed inside a Kubernetes cluster as a set of Pods (API Server, Repository Server, Application Controller, Dex, etc.) in the `argocd` namespace. It manages applications in the same cluster or in external Kubernetes clusters by communicating with their Kubernetes API Servers.

### Follow-up interview question: “If Argo CD is inside Kubernetes, who deploys Argo CD?”

Answer: Usually one of these:

* `kubectl apply` (initial bootstrap)

* Helm chart

* Another GitOps bootstrap tool (self-managed Argo CD)

This is called the GitOps bootstrap process.

47. Which Kubernetes namespace is normally used for Argo CD?
   Normally, Argo CD **`argocd` namespace** mein install hota hai.

```text
Kubernetes Cluster
│
├── kube-system
├── default
├── argocd          ← Argo CD
│   ├── argocd-server
│   ├── argocd-repo-server
│   ├── argocd-application-controller
│   ├── argocd-dex-server
│   └── argocd-redis
│
└── my-app
    └── application Pods
```

Install commonly:

```bash
kubectl create namespace argocd
```

Then:

```bash
kubectl apply -n argocd -f install.yaml
```

### 🎯 Interview answer

> **"The default and commonly used Kubernetes namespace for Argo CD is `argocd`. Argo CD components such as the API Server, Repository Server, Application Controller, Dex, and Redis are typically deployed in this namespace."**

**Remember:** `argocd` is the **namespace where Argo CD itself runs**, not necessarily where your application runs.

49. What Kubernetes resources does Argo CD create internally?
   Yes. Jab aap Argo CD ko Kubernetes mein install karte ho, to Argo CD **khud ko run karne ke liye multiple Kubernetes resources** create karta hai.

### Main resources

```text
argocd namespace
│
├── Pods
├── Deployments
├── Services
├── ConfigMaps
├── Secrets
├── ServiceAccounts
├── Roles
├── RoleBindings
├── ClusterRoles
├── ClusterRoleBindings
└── Custom Resource Definitions (CRDs)
```

### 1. Deployments

Argo CD ke components ko run karne ke liye:

```text
argocd-server
argocd-repo-server
argocd-dex-server
```

Usually **Deployments** ke through run hote hain.

---

### 2. Application Controller

Application Controller bhi Kubernetes workload ke roop mein deployed hota hai, commonly:

```text
argocd-application-controller
```

Iska main job:

```text
Git desired state
       ↓
Application Controller
       ↓
Compare
       ↓
Kubernetes live state
       ↓
Reconcile
```

---

### 3. Services

Internal/external communication ke liye Services create hote hain.

Example:

```text
argocd-server
argocd-repo-server
argocd-dex-server
```

---

### 4. ConfigMaps

Configuration store karne ke liye.

Examples:

```text
argocd-cm
argocd-rbac-cm
argocd-cmd-params-cm
```

For example, RBAC policies:

```text
argocd-rbac-cm
      ↓
Who can do what?
```

---

### 5. Secrets

Sensitive information ke liye:

```text
Git credentials
Repository credentials
TLS certificates
Admin password-related data
```

---

### 6. ServiceAccounts + RBAC

Argo CD ko Kubernetes resources access/manage karne ke liye permissions chahiye.

```text
ServiceAccount
      ↓
Role / ClusterRole
      ↓
RoleBinding / ClusterRoleBinding
      ↓
Permissions
```

For example:

> Application Controller ko Deployments, Services, ConfigMaps etc. read/update karne ki permission.

---

### 7. CRDs ⭐ Important

Argo CD apne **Custom Resource Definitions** bhi install karta hai.

Most important:

```text
Application
AppProject
ApplicationSet
```

Then Kubernetes mein aap aise resources create kar sakte ho:

```yaml
apiVersion: argoproj.io/v1alpha1
kind: Application
```

Yani:

> **Application normal built-in Kubernetes resource nahi hai; Argo CD CRD hai.**

---

### Interview answer 🎯

> **"When Argo CD is installed, it creates Kubernetes resources required to run and configure itself, including Deployments or workloads for its components, Services, ConfigMaps, Secrets, ServiceAccounts, Roles, ClusterRoles, RoleBindings, ClusterRoleBindings, and Argo CD-specific CRDs such as Application, AppProject, and ApplicationSet."**

**Easy memory:**

> **Argo CD itself = Kubernetes resources + Argo CD CRDs.**

51. How would you make Argo CD highly available?
    Haan. **Argo CD ko highly available (HA) banane ka main idea hai: single Pod/component par depend nahi karna.** Critical Argo CD components ke multiple replicas run karte hain.

### HA architecture

```text
                         Users
                           |
                    Load Balancer
                           |
                ┌──────────┴──────────┐
                ↓                     ↓
         argocd-server-1       argocd-server-2
                │                     │
                └──────────┬──────────┘
                           │
                    Argo CD Services
                           │
              ┌────────────┴────────────┐
              ↓                         ↓
      repo-server-1              repo-server-2
              │                         │
              └────────────┬────────────┘
                           ↓
                  Application Controller
                     ┌────────┴────────┐
                     ↓                 ↓
                 replica-1         replica-2
                     │                 │
                     └───────┬─────────┘
                             ↓
                    Kubernetes API Server
```

### 1. Multiple replicas

Critical components ke replicas increase karo:

```text
argocd-server
      ↓
  2+ replicas

repo-server
      ↓
  2+ replicas

application-controller
      ↓
  HA configuration / multiple replicas
```

Agar ek Pod fail ho:

```text
Pod-1 ❌
Pod-2 ✅
```

Service traffic ko healthy Pod par route kar sakti hai.

---

### 2. Multiple nodes par spread karo ⭐

Sirf replicas banana enough nahi hai.

Bad:

```text
Node-1
 ├── server-1
 ├── server-2
 └── repo-1
```

Node-1 down → multiple components down.

Better:

```text
Node-1             Node-2             Node-3
  │                   │                  │
server-1           server-2          repo-server
controller-1       repo-server-2     controller-2
```

Iske liye **Pod anti-affinity / topology spread constraints** use kar sakte ho.

---

### 3. Load Balancer / Ingress

Multiple `argocd-server` replicas ke saamne:

```text
User
 ↓
Load Balancer / Ingress
 ↓
┌──────────────┐
│ argocd-server│
├──────────────┤
│ Pod 1        │
│ Pod 2        │
└──────────────┘
```

Agar Pod 1 fail ho jaye, traffic Pod 2 ko ja sakta hai.

---

### 4. Application Controller ko HA mode mein run karo

Application Controller **reconciliation ka brain** hai.

Agar ye single instance hai:

```text
Controller ❌
     ↓
Reconciliation stops
```

HA configuration mein controller replicas/sharding use ki ja sakti hai so workload can continue despite individual instance failure.

---

### 5. Repository Server ko HA karo

Repository Server Git repositories se manifests fetch/render karta hai.

```text
Git
 ↓
┌───────────────────┐
│ Repo Server 1     │
│ Repo Server 2     │
└───────────────────┘
```

One Repo Server fail → another can serve requests.

---

### 6. Redis HA

Argo CD uses Redis for some cached/application state.

Production HA setup mein **Redis HA** important hai so Redis itself doesn't become a single point of failure.

---

### 7. Kubernetes cluster itself HA hona chahiye

Ye bhi important hai:

> **Argo CD HA hai but underlying Kubernetes cluster itself single-node hai → overall system HA nahi hai.**

Production:

```text
Multiple control-plane nodes
+
Multiple worker nodes
+
Argo CD multiple replicas
```

---

### Interview answer 🎯

> **"To make Argo CD highly available, I would run multiple replicas of the critical Argo CD components, distribute them across different Kubernetes nodes using anti-affinity or topology spread constraints, expose the Argo CD server through a load balancer or ingress, configure the Application Controller for HA, run multiple Repository Server replicas, and avoid single points of failure such as Redis. I would also ensure the underlying Kubernetes cluster is itself highly available."**

### ⭐ 8-year DevOps interview mein ek important point

Don't simply say:

> **"Increase replicas."**

Better answer:

> **"HA means removing single points of failure at both the Argo CD component level and the Kubernetes infrastructure level."**

53. How would you deploy Argo CD in production?
    Production mein main Argo CD ko **HA + secure + GitOps-based** setup mein deploy karunga.

### Production architecture

```text
                         Developers
                              |
                              ↓
                         Git Repo
                              |
                              ↓
                    ┌──────────────────┐
                    │     Argo CD      │
                    │                  │
                    │ API Server (HA)  │
                    │ Repo Server (HA) │
                    │ Controller (HA)  │
                    │ Dex / SSO        │
                    │ Redis HA          │
                    └────────┬─────────┘
                             |
                             ↓
                    Kubernetes API
                             |
              ┌──────────────┴──────────────┐
              ↓                             ↓
          App Cluster 1                 App Cluster 2
          Production                    DR / Other env
```

### Main steps

**1. Dedicated namespace**

```bash
kubectl create namespace argocd
```

Normally Argo CD ko `argocd` namespace mein deploy karunga.

**2. Use official Helm chart or official manifests**

Production mein version **pin** karunga rather than blindly using latest.

```text
Argo CD version
     ↓
Pinned / tested version
     ↓
Production
```

**3. HA configuration**

Critical components ke multiple replicas:

```text
argocd-server       → multiple replicas
argocd-repo-server  → multiple replicas
application-controller → HA
Redis               → HA
```

Aur Pods ko different nodes par spread karunga.

**4. SSO + RBAC**

Production mein local admin credentials par depend nahi karunga.

```text
User
 ↓
SSO / OIDC
 ↓
Argo CD
 ↓
RBAC
```

For example, company IdP/AD ke groups ko Argo CD RBAC se map kar sakte hain.

**5. Secure external access**

```text
Internet / Corporate Network
          ↓
       HTTPS
          ↓
Ingress / Load Balancer
          ↓
    Argo CD Server
```

TLS, network policies and restricted access configure karunga.

**6. Git repository security**

Private repositories ke liye credentials securely store karunga, preferably appropriate secret-management integration ke saath.

```text
Argo CD
   ↓
Secure Git credentials
   ↓
Private Git repo
```

**7. Multi-cluster setup**

Agar multiple environments/clusters hain:

```text
             Argo CD
                |
       ┌────────┼────────┐
       ↓        ↓        ↓
      Dev      Stage     Prod
    Cluster   Cluster   Cluster
```

Central Argo CD multiple Kubernetes clusters manage kar sakta hai.

**8. Monitoring & alerting**

Argo CD aur Kubernetes ke metrics/logs monitor karunga:

* Application health
* Sync status
* OutOfSync applications
* Controller/repo-server health
* API errors
* Resource usage

**9. Backup & disaster recovery**

Important Argo CD configuration and Kubernetes resources ka backup/restore strategy maintain karunga.

Git itself remains the primary source of truth for application configuration.

**10. Upgrade strategy**

Production upgrade:

```text
Test / Dev
    ↓
Staging
    ↓
Validate
    ↓
Production
```

Version upgrade ko controlled rollout ke through karunga.

---

### 🎯 Strong 8-year DevOps interview answer

> **"For production, I would deploy Argo CD in a dedicated `argocd` namespace using a pinned, tested version of the official Helm chart or manifests. I would configure HA for the API Server, Repository Server and Application Controller, distribute replicas across nodes, and ensure Redis is not a single point of failure. I would integrate Argo CD with the enterprise IdP for SSO and enforce RBAC, expose it securely through HTTPS and an ingress or load balancer, securely manage Git credentials, configure monitoring and alerting, and establish backup, DR and upgrade procedures. For multiple environments, I would use Argo CD to manage multiple Kubernetes clusters while keeping Git as the source of truth."**

### Interview mein ek line aur add karna ⭐

> **"I would not consider Argo CD production-ready just because the Pods are running; I would validate HA, security, access control, observability, backup/DR, upgrade strategy, and failure recovery."**

55. How would you monitor Argo CD components?
    Argo CD monitoring ko main **3 layers** mein divide karunga: **metrics, logs, aur health/status**.

### 1. Metrics ⭐

Argo CD components Prometheus-compatible metrics expose karte hain.

```text id="2lqj8d"
Argo CD
 ├── API Server
 ├── Repo Server
 └── Application Controller
          |
          ↓
      Prometheus
          |
          ↓
       Grafana
```

Main monitor karunga:

**API Server**

* Request rate
* Error rate
* Request latency
* Authentication/API failures

**Repository Server**

* Git/repository errors
* Manifest generation errors
* Request latency
* Repository fetch failures

**Application Controller ⭐**

* Reconciliation rate
* Reconciliation errors
* Queue/backlog
* Application sync/health status
* Controller resource usage

---

### 2. Logs

Argo CD components ke logs Kubernetes se collect karunga:

```bash
kubectl logs -n argocd <pod>
```

Production mein:

```text id="9n0v4p"
Argo CD Pods
    ↓
Fluent Bit / Vector
    ↓
Loki / Elasticsearch
    ↓
Grafana / Kibana
```

Search for:

```text
ERROR
WARN
repository connection failed
authentication failed
sync failed
manifest generation failed
```

---

### 3. Application health & sync status

Ye Argo CD-specific monitoring hai.

For example:

```text id="3x7n4a"
Application
   ↓
Healthy + Synced       ✅
Healthy + OutOfSync    ⚠️
Degraded               ❌
Unknown                 ❌
```

Important alerts:

* Application **OutOfSync** for too long
* Application **Degraded**
* Sync failures
* Repository connection failure
* Controller unavailable

---

### 4. Kubernetes-level monitoring

Argo CD khud Kubernetes mein run karta hai, so Kubernetes metrics bhi monitor karunga:

```text
CPU
Memory
Pod restarts
OOMKilled
Pod availability
Node health
```

Example:

```bash
kubectl get pods -n argocd
```

Agar:

```text
argocd-server-xxx       0/1 CrashLoopBackOff
argocd-repo-server-xxx  1/1 Running
```

to alert generate hona chahiye.

---

### 5. Alerts ⭐

Production mein useful alerts:

```text
ArgoCD API Server unavailable
Repository Server unavailable
Application Controller unavailable
High controller reconciliation errors
Git repository connection failure
Application OutOfSync
Application Degraded
High sync failure rate
High Pod restart count
High CPU/memory
```

### Complete monitoring architecture

```text id="9g1f3p"
                  Argo CD
        ┌──────────┼──────────┐
        ↓          ↓          ↓
    API Server  Repo Server  Controller
        │          │          │
        └──────────┼──────────┘
                   ↓
               Metrics
                   ↓
               Prometheus
                   ↓
                Grafana
                   │
                   ↓
                Alerts


Logs ──→ Loki/ELK ──→ Grafana/Kibana

Kubernetes ──→ Prometheus ──→ Grafana
```

### 🎯 Interview answer

> **"I would monitor Argo CD at three levels: component metrics, centralized logs, and application-level health. I would scrape Argo CD metrics using Prometheus and visualize them in Grafana, collect component logs centrally using a logging stack, and create alerts for API/repository/controller failures, reconciliation errors, sync failures, OutOfSync or Degraded applications, pod restarts, and resource saturation. I would also monitor the underlying Kubernetes resources because Argo CD itself runs inside Kubernetes."**

**Senior-level point:**
Don't monitor only **Argo CD Pods**. Monitor **whether Argo CD is successfully reconciling applications** — that's the actual business outcome.

57. How would you troubleshoot a Repository Server issue?
    Bilkul. Production interview mein **Repository Server issue troubleshoot** karte waqt main ek fixed flow follow karunga:

> **Pod → Logs → Git connectivity → Credentials → Manifest generation → Dependencies → Resources**

### Architecture first

```text id="j7q8x1"
Git Repository
     ↑
     │ HTTPS / SSH
     │
Repository Server
     │
     ↓
Manifest Generation
     │
     ↓
Application Controller
```

Agar Repo Server problem hai, pehle identify karna hai ki **Git access problem hai ya manifest generation problem**.

---

## 1. Check Repository Server Pod

```bash
kubectl get pods -n argocd
```

Look for:

```text
Running
CrashLoopBackOff
Pending
OOMKilled
Restarting
```

Then:

```bash
kubectl describe pod -n argocd <repo-server-pod>
```

Check:

* Events
* Resource limits
* Mount failures
* Probes
* Scheduling issues

---

## 2. Check Repository Server logs ⭐

```bash
kubectl logs -n argocd deploy/argocd-repo-server
```

If multiple containers:

```bash
kubectl logs -n argocd <pod-name> -c <container-name>
```

Look for errors like:

```text
authentication failed
repository not found
permission denied
connection timeout
host key verification failed
manifest generation failed
```

---

## 3. Check Git connectivity

First identify repository configuration.

Then test whether the Repo Server can reach Git.

For HTTPS:

```text id="e0w6am"
Repo Server
     |
     | HTTPS
     ↓
GitHub/GitLab
```

Check:

* DNS resolution
* Network connectivity
* Firewall
* Proxy
* Egress NetworkPolicy
* Git server availability

For example:

```bash
kubectl exec -n argocd <repo-server-pod> -- nslookup github.com
```

Depending on the image/tools available, you may use an appropriate connectivity test.

---

## 4. Check Git credentials ⭐

Very common issue.

```text id="8n9x0a"
Repo URL ✅
       +
Credentials ❌
       ↓
Git access fails
```

Check:

* SSH private key
* HTTPS token
* Username/password if configured
* Token expiry
* Repository permissions
* SSH known-host configuration
* Credential configuration in Argo CD

For SSH-specific problems, check whether the Git host key is trusted.

---

## 5. Check repository URL

Sometimes simple mistake:

```text id="7z3v2c"
Expected:
github.com/company/app.git

Configured:
github.com/company/apps.git
                         ↑
                       wrong
```

Check the configured repository URL and project/path.

---

## 6. Check manifest generation

Git access may be working but **Helm/Kustomize/plugin rendering** may fail.

```text id="r1q4m7"
Git access ✅
     ↓
Manifest generation ❌
```

Possible causes:

* Invalid Helm chart
* Invalid values
* Kustomize error
* Missing file
* Wrong path
* Plugin failure
* Dependency unavailable

Repository Server logs are especially useful here.

---

## 7. Check Application status

```bash
argocd app get <app-name>
```

Look for:

```text
ComparisonError
Manifest generation error
Failed to load target state
```

This helps connect the Repo Server problem to the affected application.

---

## 8. Check Repository Server resources

A Repo Server can fail because of resource pressure:

```bash
kubectl top pod -n argocd
```

Check:

```text
CPU
Memory
OOMKilled
Restarts
```

Large repositories or expensive Helm/Kustomize rendering can consume significant resources.

---

## 9. Check dependencies

If using:

```text id="8g9h2k"
Helm
Kustomize
Config Management Plugin
Private Git
Private Helm repository
```

check their connectivity/configuration too.

---

# Real production troubleshooting example

Suppose Argo CD shows:

```text id="5v7d1x"
Application: my-app
Status: Unknown
Error: Failed to load target state
```

I would investigate:

```text id="c2m8s4"
1. Repo Server Pod healthy?
          ↓
2. Repo Server logs?
          ↓
3. Git reachable?
          ↓
4. Credentials valid?
          ↓
5. Correct repo URL?
          ↓
6. Correct path/branch?
          ↓
7. Helm/Kustomize rendering working?
          ↓
8. CPU/Memory sufficient?
```

### 🎯 8-year DevOps interview answer

> **"I would troubleshoot a Repository Server issue systematically. First, I would check the Repo Server Pod status, restarts, events and resource utilization. Then I would inspect its logs for Git authentication, connectivity or manifest-generation errors. I would verify repository URL, branch/path and Git credentials, and test DNS and network connectivity from the Repo Server. If Git access is healthy, I would investigate Helm, Kustomize or config-management-plugin rendering issues. Finally, I would check the affected Argo CD application's status and confirm that the Repository Server can successfully generate the desired manifests."**

### ⭐ Senior-level distinction

**Don't immediately restart the Repo Server.**

First determine:

```text
Git connectivity issue?
        OR
Authentication issue?
        OR
Manifest generation issue?
        OR
Resource issue?
        OR
Repo Server itself unhealthy?
```

Then fix the **root cause**, rather than simply restarting the Pod.

59. How would you troubleshoot an Application Controller issue?
Application Controller issue ko troubleshoot karte waqt main ye samjhunga ki **reconciliation kyun nahi ho rahi**.

### Architecture

```text id="e3w9q1"
             Git
              ↓
       Repository Server
              ↓
     Desired Manifests
              ↓
   ┌──────────────────────┐
   │ Application Controller│
   └──────────┬───────────┘
              ↓
     Kubernetes API Server
              ↓
       Deployments / Pods
```

Agar Controller issue hai, mainly 3 cheezein check karni hain:

**Git → Controller**
**Controller → Kubernetes API**
**Controller itself**

---

## 1. Check Controller Pod ⭐

```bash
kubectl get pods -n argocd
```

Look for:

```text
Running
CrashLoopBackOff
OOMKilled
Pending
Restarting
```

Then:

```bash
kubectl describe pod -n argocd <controller-pod>
```

Check:

* Pod events
* CPU/memory
* OOMKilled
* Liveness/readiness probes
* Scheduling issues

---

## 2. Check Controller logs ⭐⭐⭐

Most important step:

```bash
kubectl logs -n argocd <controller-pod>
```

Look for:

```text
reconciliation error
failed to sync
permission denied
connection refused
timeout
resource not found
rate limit
comparison error
```

If controller has multiple replicas/containers, make sure you're checking the relevant instance/container.

---

## 3. Check whether Kubernetes API Server is reachable

Controller Kubernetes API Server ke saath continuously communicate karta hai.

```text id="m9d2x7"
Application Controller
        |
        | Kubernetes API
        ↓
Kubernetes API Server
```

Check:

* API Server availability
* Network connectivity
* DNS
* NetworkPolicy
* TLS/certificate issues
* API throttling

If API Server inaccessible:

```text
Controller
    ↓
❌ Kubernetes API
    ↓
No reconciliation
```

---

## 4. Check RBAC permissions ⭐

Very common production issue.

Suppose Controller ko Deployment update karna hai:

```text id="q1a7v3"
Application Controller
       ↓
Update Deployment
       ↓
Kubernetes API Server
       ↓
RBAC ❌
```

Logs might show:

```text
forbidden
User cannot update resource
```

Check ServiceAccount:

```bash
kubectl get sa -n argocd
```

Then inspect permissions/RBAC.

---

## 5. Check Application status

```bash
argocd app get <app-name>
```

Look at:

```text
Sync Status
Health Status
Conditions
Events
```

For example:

```text
Sync: OutOfSync
Health: Degraded
```

Then determine **why**.

---

## 6. Check whether Repository Server is healthy

Controller ko desired manifests Repository Server se milte hain.

```text id="q7r4m1"
Git
 ↓
Repository Server ❌
 ↓
Controller doesn't get desired manifests
```

So if Controller logs show:

```text
comparison error
failed to generate manifests
```

Repo Server ko bhi investigate karo.

**Important:** Har reconciliation problem Controller ki problem nahi hoti.

---

## 7. Check Controller resource usage

Large number of applications/resources hone par Controller resource pressure mein aa sakta hai.

```bash
kubectl top pod -n argocd
```

Check:

```text
CPU
Memory
Restarts
OOMKilled
```

Also investigate reconciliation backlog/latency through metrics.

---

## 8. Check Kubernetes events

```bash
kubectl get events -n argocd
```

And application namespace mein:

```bash
kubectl get events -n <application-namespace>
```

This can reveal:

```text
FailedScheduling
Forbidden
ImagePullBackOff
ResourceQuota
Admission webhook failure
```

---

## 9. Check if controller is actually reconciling

This is a **senior-level check**.

Don't only ask:

> "Is the Pod Running?"

Ask:

> **"Is the controller successfully reconciling applications?"**

```text id="9s7k2p"
Controller Pod = Running ✅
       ↓
But reconciliation failing ❌
       ↓
Applications remain OutOfSync
```

So metrics/logs + application status are more important than just Pod status.

---

# Production troubleshooting flow

```text id="h6k4w2"
Application not syncing
        ↓
Controller Pod healthy?
        |
       YES
        ↓
Check Controller logs
        ↓
 ┌───────────────┬─────────────────┐
 ↓               ↓                 ↓
Git/Repo issue   K8s API issue    RBAC issue
 ↓               ↓                 ↓
Repo Server      API Server       Permissions
        \          |              /
         \         |             /
          └──── Root Cause ─────┘
                    ↓
                  Fix
                    ↓
              Reconciliation
                    ↓
                  Synced
```

### 🎯 8-year DevOps interview answer

> **"If the Application Controller has an issue, I first check its Pod status, restarts, events and resource utilization. Then I inspect controller logs and application conditions to identify reconciliation errors. I verify connectivity and authentication to the Kubernetes API Server and check the Controller's RBAC permissions. I also verify that the Repository Server is healthy because the Controller depends on the desired manifests generated by it. Finally, I check reconciliation metrics, backlog/latency and Kubernetes events to confirm that the controller is actually processing applications successfully."**

### ⭐ Remember this distinction

**Repository Server problem:**

> **"Mujhe Git se desired state nahi mil rahi."**

**Application Controller problem:**

> **"Desired state mil gayi, but usko Kubernetes ke live state ke saath reconcile/sync nahi kar paa raha."**


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
