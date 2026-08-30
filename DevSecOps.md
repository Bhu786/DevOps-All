Bilkul. Maine **Security Tools PDF ke poore 9 pages ka content cover kiya hai**—SAST, SCA, Container Security, IaC, DAST, Secrets, Runtime Security, SIEM/Logging, Vulnerability Management, CI/CD integration, learning path, aur **saare 8 practical labs** bhi. Main content ko remove nahi kar raha; sirf language ko simple aur interview-friendly bana raha hoon. 

# 🔐 DEVSECOPS SECURITY TOOLS — SIMPLE MASTER NOTES

## 1. DevSecOps kya hai?

Simple:

> **DevSecOps = Development + Security + Operations**

Security ko application ke **end mein nahi**, development aur CI/CD process ke **starting se hi include** karna.

```text
Developer Code
      ↓
Security Check
      ↓
Build
      ↓
Test
      ↓
Container Scan
      ↓
IaC Scan
      ↓
Deploy
      ↓
Runtime Security
      ↓
Monitoring
```

Main goal:

> **Security problems ko jaldi find karo, fix karo aur production tak vulnerable code na pahunchne do.**

---

# 2. Security Tools ko kaise yaad karein?

Sabse important master flow:

```text
CODE
 ↓
SAST
 ↓
DEPENDENCIES
 ↓
SCA
 ↓
CONTAINER
 ↓
Container Security
 ↓
INFRASTRUCTURE
 ↓
IaC Security
 ↓
RUNNING APPLICATION
 ↓
DAST
 ↓
SECRETS
 ↓
Secrets Detection/Management
 ↓
RUNTIME
 ↓
Runtime Security
 ↓
LOGS
 ↓
SIEM / Monitoring
 ↓
VULNERABILITY MANAGEMENT
 ↓
CI/CD
```

---

# 3. SAST — Static Application Security Testing ⭐

### Simple meaning

**SAST = Source code ko run kiye bina security problems check karna.**

Matlab developer ne code likha:

```java
String password = "admin123";
```

SAST tool code ko scan karke problem identify kar sakta hai.

### Kab?

👉 **Before deployment / while developing**

PDF ke according SAST source code ko scan karke vulnerabilities aur coding flaws detect karta hai. 

### Tools

| Tool                          | Simple meaning                            |
| ----------------------------- | ----------------------------------------- |
| **SonarQube**                 | Bugs + vulnerabilities + code smells      |
| **Semgrep**                   | Fast code/security scanner + custom rules |
| **Bandit**                    | Python security linter                    |
| **ESLint + Security Plugins** | JavaScript/Node.js linting + security     |

### Yaad rakho:

```text
SAST
 ↓
SOURCE CODE
 ↓
Security problems
```

---

# 4. SonarQube

SonarQube code ko analyze karta hai.

Find kar sakta hai:

* Bugs
* Vulnerabilities
* Code smells

### Simple interview answer

> **SonarQube is a code quality and security analysis tool used to identify bugs, vulnerabilities and code smells.**

---

# 5. Semgrep

Semgrep:

* fast scanner hai
* source code ko analyze karta hai
* syntax-aware hai
* custom security rules bana sakte hain

PDF practical lab mein Semgrep se hardcoded secrets aur weak cryptography identify karne ka example diya hai. 

---

# 6. Bandit

**Bandit = Python-specific security linter.**

```text
Python Code
    ↓
Bandit
    ↓
Security Issues
```

---

# 7. ESLint + Security Plugins

JavaScript/Node.js code ko lint karta hai aur security-related plugins ke through additional security checks karta hai. 

---

# 8. SCA — Software Composition Analysis ⭐

### Simple meaning

Modern application mein hum khud ka code hi nahi likhte.

Dependencies use karte hain:

```text
Spring Boot
Log4j
Maven libraries
npm packages
etc.
```

In third-party/open-source libraries mein vulnerability ho sakti hai.

**SCA dependencies ko scan karta hai.**

PDF ke according SCA third-party aur open-source dependencies ko known vulnerabilities ke liye analyze karta hai. 

### Master trick

```text
SAST → MY CODE
SCA  → MY DEPENDENCIES
```

---

# 9. SCA Tools

### Snyk

Vulnerabilities identify/fix karne mein help karta hai in:

* Dependencies
* Docker images
* IaC

### OWASP Dependency-Check

Known vulnerable libraries ko **CVE data** ke basis par scan karta hai.

### Trivy

Scan kar sakta hai:

* Code
* Container images
* IaC

### Retire.js

JavaScript libraries mein known vulnerabilities find karta hai. 

---

# 10. Container Security ⭐

Docker/container image mein vulnerabilities ho sakti hain.

Container Security tools:

> **Container images aur registries ko scan/secure karte hain.**



### Tools

| Tool                          | Simple meaning                                       |
| ----------------------------- | ---------------------------------------------------- |
| **Clair**                     | Docker container image vulnerability scanning        |
| **Anchore Engine**            | Deep container image inspection + policy enforcement |
| **Trivy**                     | Fast container image scanning                        |
| **Docker Bench for Security** | Docker host security best-practice audit             |

---

# 11. Trivy

Trivy bahut useful DevSecOps tool hai because ye multiple areas scan kar sakta hai:

```text
Trivy
 ├── Code
 ├── Container Images
 └── IaC
```

PDF practical example:

```bash
trivy image <image-name>
```

Image scan karne ke liye. 

Agar vulnerability mile:

```text
Find vulnerability
       ↓
Check severity
       ↓
Update base image/library
       ↓
Scan again
```

---

# 12. Docker Bench for Security

Docker host ki configuration ko security best practices ke against check karta hai.

Example findings:

* Container root user se run ho raha hai
* Unnecessary/exposed ports
* Security misconfiguration



---

# 13. IaC Security ⭐

### IaC = Infrastructure as Code

Example:

```text
Terraform
CloudFormation
Kubernetes YAML
```

Infrastructure configuration mein security mistake ho sakti hai.

Example:

```text
Security Group
     ↓
0.0.0.0/0
     ↓
Too open ❌
```

IaC security tools aisi misconfiguration detect karte hain.

PDF ke according IaC security Terraform, CloudFormation, Kubernetes YAML etc. mein misconfigurations detect karti hai. 

---

# 14. IaC Security Tools

### Checkov

Scan:

* Terraform
* CloudFormation
* Kubernetes

for security misconfigurations.

### Terrascan

IaC mein:

* security violations
* compliance violations

detect karta hai.

### KICS

Infrastructure as Code ko scan karta hai.

### TFLint

Terraform ke liye linter hai, mainly code quality aur security focus ke saath. 

---

# 15. DAST — Dynamic Application Security Testing ⭐

Ye SAST ka opposite way samajho.

### SAST

```text
Code
 ↓
Scan
```

### DAST

```text
Running Application
 ↓
Attack/Testing
 ↓
Vulnerability
```

DAST **running application** ko test karta hai.

PDF ke according DAST running applications par attacks simulate karke vulnerabilities find karta hai. 

### Common vulnerabilities

* SQL Injection
* XSS
* CSRF
* Insecure headers
* Broken authentication

PDF ke ZAP lab mein SQL Injection, XSS aur CSRF jaise examples diye gaye hain. 

---

# 16. DAST Tools

| Tool                     | Simple meaning                               |
| ------------------------ | -------------------------------------------- |
| **OWASP ZAP**            | Web application security scanner             |
| **Burp Suite Community** | Manual + semi-automated web security testing |
| **Nikto**                | Web server scanner                           |
| **Arachni**              | High-performance Ruby-based web scanner      |



---

# 17. SAST vs DAST ⭐⭐⭐

Interview favourite:

| SAST                                   | DAST                             |
| -------------------------------------- | -------------------------------- |
| Source code scan                       | Running application scan         |
| Application ko run karna required nahi | Application running honi chahiye |
| White-box approach                     | Black-box style testing          |
| Development phase mein useful          | Running/staging app testing      |
| Example: SonarQube, Semgrep            | Example: ZAP, Burp               |

### One-line trick

> **SAST looks inside the code; DAST attacks/tests the running application from outside.**

---

# 18. Secrets Management & Detection ⭐

Secrets kya hain?

```text
API Keys
Passwords
Tokens
Credentials
```

Inko code/Git repository mein hardcode nahi karna chahiye.

PDF ke according secrets tools API keys, passwords aur tokens jaise sensitive data ko protect/detect karte hain. 

---

# 19. Secrets Tools

### HashiCorp Vault

Centralized secrets management.

Features:

* Secrets store
* Encryption
* Dynamic credentials

### CyberArk Conjur

Applications/containers ke liye:

* secrets management
* machine identity

### Gitleaks

Git repository mein **hardcoded/exposed secrets** find karta hai.

### TruffleHog

Git history mein sensitive data detect karta hai.



---

# 20. Vault vs Gitleaks

Very important:

```text
Vault
 ↓
SECRET KO SECURELY STORE/MANAGE

Gitleaks
 ↓
SECRET CODE/GIT MEIN LEAK HUA HAI?
```

Example:

```java
String apiKey = "ABC123";
```

Gitleaks → detect karega.

Instead:

```text
Application
     ↓
Vault
     ↓
Get secret at runtime
```

PDF lab specifically application ko runtime par Vault se secret retrieve karne ke example se explain karta hai instead of hardcoding. 

---

# 21. Runtime Security ⭐

Ab application deploy ho chuki hai.

Runtime security ka job:

> **Running application/container/infrastructure mein suspicious activity detect karna.**



### Tools

| Tool              | Simple meaning                                      |
| ----------------- | --------------------------------------------------- |
| **Falco**         | Container/Kubernetes suspicious behavior monitoring |
| **AppArmor**      | Linux mandatory access control                      |
| **SELinux**       | Linux mandatory access control                      |
| **Sysdig Secure** | Container activity + anomaly detection              |
| **Auditd**        | Linux system calls/events auditing                  |

---

# 22. Falco ⭐

Falco runtime par:

```text
Container
    ↓
Activity
    ↓
Suspicious behavior?
    ↓
Falco
    ↓
Alert
```

Example:

* privilege escalation attempt
* sensitive file access

PDF lab mein Falco se container activity aur system calls monitor karna aur abnormal behavior par alert generate karna demonstrate kiya gaya hai. 

---

# 23. Security Logging & SIEM

### Simple meaning

Infrastructure ke different systems se security logs/data collect karo aur analyze karo.

```text
Servers
Containers
Applications
Network
    ↓
Logs
    ↓
Central System
    ↓
Analysis
    ↓
Alert / Investigation
```

PDF mein Security Logging & SIEM ka purpose infrastructure-wide security data collect aur analyze karna diya hai. 

---

# 24. SIEM Tools

### ELK Stack

```text
E → Elasticsearch
L → Logstash
K → Kibana
```

Purpose:

> Centralized logging + visualization

### Fluentd + Elasticsearch

Container environments mein logs forward/aggregate karne ke liye.

### Security Onion

Network security monitoring platform.

### Wazuh

Security analytics +:

* threat detection
* file integrity monitoring



---

# 25. Vulnerability Management

Problem:

Different security tools different findings generate karte hain.

```text
SonarQube → Findings
Snyk      → Findings
Trivy     → Findings
ZAP       → Findings
Checkov   → Findings
```

Ab in findings ko:

* collect
* track
* prioritize
* assign
* remediate

karna hai.

**Vulnerability Management** ye process handle karta hai.

PDF ke according it scanning, triage aur remediation workflows ko centralize/manage karta hai. 

---

# 26. Vulnerability Management Tools

### DefectDojo

Different security tools ke findings aggregate karta hai aur remediation track karta hai.

### TheHive

Security incidents ko:

* create
* manage
* track
* respond

karne ke liye platform.

### Faraday

Collaborative vulnerability analysis and management. 

---

# 27. TheHive — Simple Flow

```text
ZAP / Snyk
    ↓
Security Finding
    ↓
TheHive
    ↓
Create Case
    ↓
Assign Team Member
    ↓
Fix
    ↓
Add Remediation Notes
    ↓
Close/Track
```

PDF lab mein ZAP/Snyk jaise scanners ke findings TheHive mein import karke incidents/cases manage karne ka flow diya hai. 

---

# 28. CI/CD Integration ⭐⭐⭐

Security ko pipeline mein integrate karna = **DevSecOps** ka major part.

Example:

```text
Developer Push
      ↓
CI/CD Pipeline
      ↓
Build
      ↓
SAST
      ↓
SCA
      ↓
IaC Scan
      ↓
Container Scan
      ↓
Test
      ↓
Deploy
```

PDF ke according CI/CD integration ka purpose security ko pipeline mein integrate karke **shift-left security** enable karna hai. 

---

# 29. Jenkins + Security Tools

Example:

```text
Jenkins
  ↓
Build
  ↓
SonarQube
  ↓
Snyk
  ↓
Trivy
  ↓
Deploy
```

PDF mein Jenkins + Snyk/SonarQube plugins ko inline build scanning ke example ke roop mein diya hai. 

---

# 30. GitLab CI

GitLab pipeline mein:

* Secret scanning
* SAST
* DAST

stages integrate kiye ja sakte hain. 

---

# 31. GitHub Actions

Example:

```text
Pull Request
      ↓
GitHub Actions
      ↓
Semgrep
      ↓
Trivy
      ↓
Security Check
```

PDF mein GitHub Actions + Trivy/Semgrep ka PR scanning example diya hai. 

---

# 32. SHIFT LEFT SECURITY ⭐

### Meaning

Security testing ko deployment ke end tak wait na karke **development ke early stage mein karna**.

```text
OLD WAY

Code → Build → Test → Deploy → Security ❌


SHIFT LEFT

Code
 ↓
Security
 ↓
Build
 ↓
Test
 ↓
Deploy
```

### Benefit

Problem early milti hai → early fix hoti hai → production risk kam.

---

# 🧪 PRACTICAL LABS — SIMPLE VERSION

PDF mein **8 practical labs** hain. Inhe bhi yaad karna important hai. 

---

# LAB 1 — SAST with SonarQube + Semgrep

### Objective

Code ko vulnerabilities ke liye scan karna.

### Tools

```text
SonarQube
Semgrep
```

### Flow

```text
Vulnerable Java/Python Repo
          ↓
      SonarQube
          ↓
 Bugs / Vulnerabilities / Code Issues
          ↓
       Semgrep
          ↓
 Security Issues
```

PDF ke steps mein SonarQube ko Docker/local run karna, IDE plugin install karna, vulnerable repo clone karna, scan karna, phir same repo ko Semgrep se scan karna included hai. 

Semgrep se examples:

* hardcoded secrets
* weak cryptography

detect kiye ja sakte hain.

Finally:

> **SonarQube vs Semgrep findings compare karo.**

---

# LAB 2 — Container Security with Trivy + Docker Bench

### Objective

Docker containers/images ko security vulnerabilities aur best practices ke liye check karna.

### Tools

```text
Docker
Trivy
Docker Bench
```

### Flow

```text
Docker Image
     ↓
Trivy
     ↓
Image Vulnerabilities
     ↓
Fix
     ↓
Scan Again
```

Command:

```bash
trivy image <image-name>
```

Docker Bench:

```text
Docker Host
    ↓
Docker Bench
    ↓
Security Misconfiguration
```

Examples:

* root user
* exposed ports



---

# LAB 3 — IaC Security with Checkov + Terrascan

### Objective

Terraform/CloudFormation infrastructure configuration ko scan karna.

### Tools

```text
Terraform
Checkov
Terrascan
```

Flow:

```text
Terraform Code
      ↓
Checkov
      ↓
Security Misconfiguration
      ↓
Fix
      ↓
Re-scan

Terraform Code
      ↓
Terrascan
      ↓
Compare Results
```

PDF example mein open security groups aur insecure IAM roles jaise issues identify karne ka example diya gaya hai. 

Commands given in PDF:

```bash
terraform init
terraform apply
```

Checkov:

```bash
checkov -d ..
```

Terrascan:

```bash
terrascan scan -i terraform -d ..
```

---

# LAB 4 — DAST with OWASP ZAP

### Objective

**Live/running web application** ko security test karna.

### Tools

```text
OWASP ZAP
DVWA / OWASP Juice Shop
```

Flow:

```text
Running Web App
      ↓
    ZAP
      ↓
Automated Scan
      ↓
Vulnerabilities
```

Possible findings:

```text
SQL Injection
XSS
CSRF
Insecure Headers
Broken Authentication
```

PDF mein ZAP proxy setup, browser traffic route karna, automated scan, manual scan, Spider/Active Scan/Passive Scan aur report generation sab included hai. 

---

# LAB 5 — Secrets with Vault + GitLeaks

### Objective

Secrets ko securely manage karna aur leaked secrets detect karna.

### Tools

```text
HashiCorp Vault
GitLeaks
```

### Vault flow

```text
Application
     ↓
Vault
     ↓
Secret
     ↓
Runtime par retrieve
```

### GitLeaks flow

```text
Git Repository
      ↓
GitLeaks
      ↓
Secret found?
      ↓
Remove securely
```

PDF mein leaked secret ko Git history se remove karne ke liye `git filter-branch` ya BFG Repo-Cleaner ka example diya gaya hai. 

CI/CD mein:

```text
Code
 ↓
GitLeaks
 ↓
Secret found?
 ↓
Pipeline fail/alert
```

---

# LAB 6 — Runtime Security with Falco

### Objective

Running containers mein abnormal behavior detect karna.

### Tools

```text
Kubernetes / Docker
Falco
```

Flow:

```text
Container Running
       ↓
    Activity
       ↓
      Falco
       ↓
Suspicious Behavior?
       ↓
     ALERT
```

Example:

```text
Privilege escalation
Sensitive file access
```

Falco alerts ko:

* Email
* Slack
* SIEM

tak bhejne ka example PDF mein diya gaya hai. 

---

# LAB 7 — Vulnerability Management with TheHive

### Objective

Security vulnerabilities/incidents ko track aur manage karna.

### Tools

```text
TheHive
Cortex (optional)
```

Flow:

```text
ZAP / Snyk
    ↓
Findings
    ↓
TheHive
    ↓
Case
    ↓
Assign
    ↓
Fix
    ↓
Remediation Notes
```



---

# LAB 8 — CI/CD Security Integration

### Objective

Security tools ko CI/CD pipeline mein automatically run karna.

### Tools

```text
Jenkins / GitLab

SonarQube
Checkov
Snyk
Trivy
```

Pipeline:

```text
Developer Push
      ↓
   Pipeline
      ↓
     Build
      ↓
     Test
      ↓
 Security Scans
      ↓
     Deploy
```

Security stages:

```text
SonarQube → Code analysis
Trivy     → Docker image scan
Checkov   → IaC scan
Snyk      → Dependency/IaC etc.
```

PDF ke final lab mein push-triggered pipeline, build/test/deploy stages aur security scans ko integrate karna diya hai. 

---

# 🚨 Security Issue Milne Par Kya Karoge?

Interview mein ye scenario aa sakta hai.

Suppose Trivy ne critical vulnerability find ki.

### Approach:

```text
1. Identify vulnerability
        ↓
2. Check severity
        ↓
3. Find affected package/base image
        ↓
4. Update package/image
        ↓
5. Rebuild
        ↓
6. Scan again
        ↓
7. If clean → continue pipeline
        ↓
8. If critical → block deployment
```

---

# 🔥 ALL TOOLS — CATEGORY WISE

| Category                     | Tools                                               |
| ---------------------------- | --------------------------------------------------- |
| **SAST**                     | SonarQube, Semgrep, Bandit, ESLint                  |
| **SCA**                      | Snyk, OWASP Dependency-Check, Trivy, Retire.js      |
| **Container**                | Clair, Anchore, Trivy, Docker Bench                 |
| **IaC**                      | Checkov, Terrascan, KICS, TFLint                    |
| **DAST**                     | OWASP ZAP, Burp Suite, Nikto, Arachni               |
| **Secrets**                  | Vault, CyberArk Conjur, Gitleaks, TruffleHog        |
| **Runtime**                  | Falco, AppArmor, SELinux, Sysdig Secure, Auditd     |
| **Logging/SIEM**             | ELK, Fluentd + Elasticsearch, Security Onion, Wazuh |
| **Vulnerability Management** | DefectDojo, TheHive, Faraday                        |
| **CI/CD**                    | Jenkins, GitLab CI, GitHub Actions                  |

Ye categorization PDF ke 10 security-tool areas ke according hai. 

---

# 🧠 MASTER DIFFERENCE — SAB KUCH EK SAATH

```text
SONARQUBE / SEMGREP
        ↓
   MY SOURCE CODE
        ↓
      SAST


SNYK / DEPENDENCY-CHECK
        ↓
 THIRD-PARTY LIBRARIES
        ↓
       SCA


TRIVY / CLAIR
        ↓
 CONTAINER IMAGE
        ↓
 CONTAINER SECURITY


CHECKOV / TERRASCAN
        ↓
 TERRAFORM / K8S / IaC
        ↓
    IaC SECURITY


ZAP / BURP
        ↓
 RUNNING APPLICATION
        ↓
       DAST


GITLEAKS
        ↓
 GIT / SOURCE CODE
        ↓
 SECRET DETECTION


VAULT
        ↓
 SECURE SECRET STORAGE
        ↓
 SECRET MANAGEMENT


FALCO
        ↓
 RUNNING CONTAINER
        ↓
 RUNTIME SECURITY


ELK / WAZUH
        ↓
 LOGS + SECURITY DATA
        ↓
 MONITORING / SIEM


DEFECTDOJO / THEHIVE
        ↓
 SECURITY FINDINGS
        ↓
 TRACK + MANAGE + REMEDIATE


JENKINS / GITLAB
        ↓
 AUTOMATE ALL CHECKS
        ↓
       CI/CD
```

---

# 🎯 PDF KA SUGGESTED LEARNING PATH

PDF specifically learning ko is order mein rakhta hai: 

```text
1. SAST
   ↓
   SonarQube, Semgrep

2. SCA
   ↓
   Snyk, Trivy

3. Container Security
   ↓
   Clair, Anchore, Docker Bench

4. IaC Security
   ↓
   Checkov, Terrascan

5. DAST
   ↓
   OWASP ZAP, Burp Suite

6. Secrets
   ↓
   Vault, Gitleaks, TruffleHog

7. Runtime Protection
   ↓
   Falco, AppArmor

8. Logging & Monitoring
   ↓
   ELK, Wazuh

9. Vulnerability Management
   ↓
   DefectDojo

10. CI/CD Integration
    ↓
    Jenkins / GitLab
```

---

# 🏆 MASTER SHORT NOTES — 2 MINUTE REVISION

```text
DEVSECOPS SECURITY
│
├── SAST
│   └── Source Code Scan
│       → SonarQube
│       → Semgrep
│       → Bandit
│       → ESLint
│
├── SCA
│   └── Dependency Scan
│       → Snyk
│       → Dependency-Check
│       → Trivy
│       → Retire.js
│
├── CONTAINER SECURITY
│   └── Docker/Image Scan
│       → Trivy
│       → Clair
│       → Anchore
│       → Docker Bench
│
├── IaC SECURITY
│   └── Terraform/K8s/CloudFormation
│       → Checkov
│       → Terrascan
│       → KICS
│       → TFLint
│
├── DAST
│   └── Running Application Scan
│       → OWASP ZAP
│       → Burp Suite
│       → Nikto
│       → Arachni
│
├── SECRETS
│   ├── Store/Manage
│   │   → Vault
│   │   → CyberArk Conjur
│   │
│   └── Detect Leaks
│       → Gitleaks
│       → TruffleHog
│
├── RUNTIME SECURITY
│   └── Running System Monitoring
│       → Falco
│       → AppArmor
│       → SELinux
│       → Sysdig Secure
│       → Auditd
│
├── LOGGING / SIEM
│   → ELK
│   → Fluentd + Elasticsearch
│   → Security Onion
│   → Wazuh
│
├── VULNERABILITY MANAGEMENT
│   → DefectDojo
│   → TheHive
│   → Faraday
│
└── CI/CD
    → Jenkins
    → GitLab CI
    → GitHub Actions
```

---

# ⭐ MOST IMPORTANT INTERVIEW MEMORY TRICK

Bas ye **10 lines** yaad rakh lo:

```text
SAST       → My Code
SCA        → My Dependencies
Container  → My Docker Image
IaC        → My Infrastructure Code
DAST       → My Running Application
Gitleaks   → Secret Leak Detection
Vault      → Secret Storage/Management
Falco      → Runtime Behavior
ELK/Wazuh  → Logs + Security Monitoring
TheHive    → Findings/Incidents Management
```

### Aur complete DevSecOps flow:

```text
CODE
 ↓
SAST
 ↓
DEPENDENCIES
 ↓
SCA
 ↓
IaC
 ↓
Checkov
 ↓
CONTAINER
 ↓
Trivy
 ↓
DAST
 ↓
ZAP
 ↓
SECRETS
 ↓
Gitleaks / Vault
 ↓
DEPLOY
 ↓
RUNTIME
 ↓
Falco
 ↓
LOGGING
 ↓
ELK / Wazuh
 ↓
VULNERABILITY MANAGEMENT
 ↓
TheHive / DefectDojo
 ↓
CI/CD AUTOMATION
```

**Ek sentence mein:**

> **DevSecOps mein hum code, dependencies, infrastructure, containers aur running application ko different stages par security tools se check karte hain; findings ko manage karte hain aur ye checks CI/CD pipeline mein automate karte hain.** 
