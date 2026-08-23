Very simple:

### CI vs CD

**CI = Continuous Integration**
👉 **Code ko frequently build + test karna.**

**CD = Continuous Delivery / Deployment**
👉 **Tested code ko automatically release/deploy karna.**

Think of it like:

**Developer pushes code → CI → CD → Production**

|           | CI                        | CD                             |
| --------- | ------------------------- | ------------------------------ |
| Full form | Continuous Integration    | Continuous Delivery/Deployment |
| Main job  | Build + Test              | Release + Deploy               |
| Goal      | Code is working           | Code reaches environment       |
| Example   | Maven build + JUnit tests | Docker → Kubernetes/EKS        |
| Trigger   | Code push/PR              | After CI succeeds              |

### Real example

You push Java/Spring Boot code to GitHub:

**CI:**

```text
Git Push
   ↓
Jenkins
   ↓
mvn build
   ↓
Unit Tests
   ↓
Success
```

**CD:**

```text
CI Success
   ↓
Build Docker Image
   ↓
Push to Registry
   ↓
Deploy to Kubernetes
   ↓
Production
```

### Interview trick 🧠

> **CI asks: "Is my new code safe and working?"**
> **CD asks: "How do I get this working code to users?"**

And remember:

====================================================================================
The easiest difference is **manual vs automatic production deployment**.

### Continuous Delivery vs Continuous Deployment

|                   | Continuous Delivery                                 | Continuous Deployment                        |
| ----------------- | --------------------------------------------------- | -------------------------------------------- |
| Code reaches      | Ready for release                                   | Automatically released                       |
| Production deploy | **Manual approval**                                 | **Automatic**                                |
| Automation        | Build + test + package + prepare release            | Build + test + package + deploy              |
| Human involvement | Yes, before production                              | No, normally                                 |
| Example           | Jenkins builds image → waits for approval → deploys | Jenkins builds image → automatically deploys |

### Simple flow

**Continuous Delivery:**

```text
Developer
   ↓
Git Push
   ↓
Build + Test
   ↓
Docker Image
   ↓
READY FOR PRODUCTION
   ↓
👨‍💻 Manual Approval
   ↓
Production
```

**Continuous Deployment:**

```text
Developer
   ↓
Git Push
   ↓
Build + Test
   ↓
Docker Image
   ↓
🚀 Automatic Deployment
   ↓
Production
```

### 🧠 Interview trick

> **Continuous Delivery = Always ready to deploy, but deployment may require manual approval.**

> **Continuous Deployment = Automatically deploy every change that successfully passes the pipeline.**

So:

**Delivery → "Ready to go"**
**Deployment → "Already gone" 🚀**
====================================================================================================================


**CI = Build & Test**
**CD = Release & Deploy**
