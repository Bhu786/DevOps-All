# Networking

. Main **sirf AWS Networking** par focus karunga—compute, database, DevOps etc. ko side mein rakhenge.

Goal:Bilkul **AWS ke networking components ko simple language mein samajhna + kya hai + kyun chahiye + kahan use hota hai + interview mein kaise explain karna hai.**

# AWS Networking — Complete Map

Sabse pehle poora picture:

```text
                         INTERNET
                            |
                     Route 53 / DNS
                            |
                     CloudFront / CDN
                            |
                    Internet Gateway
                            |
        +------------------- VPC -------------------+
        |                                            |
        |             Route Tables                  |
        |                  |                         |
        |       +----------+----------+              |
        |       |                     |              |
        |   Public Subnet        Private Subnet     |
        |       |                     |              |
        |   Load Balancer          Application      |
        |       |                     |              |
        |       +----------+----------+              |
        |                  |                         |
        |                NAT Gateway                |
        |                  |                         |
        |              Internet                     |
        |                                            |
        | Security Groups                            |
        | Network ACLs                               |
        | VPC Endpoints                              |
        +--------------------------------------------+

Other important networking:
VPC Peering
Transit Gateway
VPN
Direct Connect
PrivateLink
Elastic IP
ENI
IPv4 / IPv6
DHCP
DNS
Network Firewall
AWS WAF
Global Accelerator
AWS Network Load Balancer
Application Load Balancer
Gateway Load Balancer
```

Ab ek-ek component.

---

# 1. VPC — Virtual Private Cloud

### Kya hai?

**VPC AWS ke andar tumhara private network hai.**

Jaise company ka apna network hota hai:

```text
Company Network
     |
  Servers
  Database
  Applications
```

AWS mein:

```text
AWS
 |
 VPC
 |
 +-- Subnet
 +-- Route Table
 +-- Security Group
 +-- NACL
 +-- Gateway
```

### Example

Hotel Management System ke liye:

```text
Hotel VPC
10.0.0.0/16

   |
   +--- Public Subnet
   |
   +--- Private App Subnet
   |
   +--- Private DB Subnet
```

### Why?

Resources ko isolated network mein rakhne ke liye.

### Interview:

> "VPC is a logically isolated virtual network in AWS where we define IP ranges, subnets, routing and network security for our application."

---

# 2. CIDR

VPC banate waqt IP range define karte ho.

Example:

```text
10.0.0.0/16
```

Isko **CIDR block** bolte hain.

Example:

```text
VPC
10.0.0.0/16

       |
       +-- Public subnet
       |   10.0.1.0/24
       |
       +-- Private App
       |   10.0.2.0/24
       |
       +-- Private DB
           10.0.3.0/24
```

### Simple meaning

CIDR basically batata hai:

> "Is network mein kaunse IP addresses available hain."

---

# 3. Subnet

VPC ke andar network ko smaller networks mein divide karte hain.

```text
VPC
10.0.0.0/16
       |
       +--- Public Subnet
       |
       +--- Private Subnet
```

### Public subnet

Jahan resource ko internet se communication ki possibility hoti hai.

Example:

```text
Internet
   |
Internet Gateway
   |
Public Subnet
   |
Load Balancer
```

### Private subnet

Direct inbound internet access nahi hota.

Example:

```text
Internet
   X
Private Subnet
   |
Application
```

---

# 4. Availability Zone

AWS Region ke andar multiple isolated locations hoti hain.

Example:

```text
Mumbai Region

    Region
      |
      +--- AZ-1
      |
      +--- AZ-2
      |
      +--- AZ-3
```

Networking mein AZ important hai because highly available architecture ke liye resources multiple AZs mein rakhte hain.

Example:

```text
          Load Balancer
          /            \
       AZ-1            AZ-2
        |                |
      App              App
```

---

# 5. Route Table

Ye bahut important hai.

### Simple definition:

**Route Table decides traffic ko kahan bhejna hai.**

Example:

```text
Destination       Target

10.0.0.0/16       local
0.0.0.0/0         Internet Gateway
```

Meaning:

```text
10.0.0.0/16
   |
same VPC → local

0.0.0.0/0
   |
other networks → Internet Gateway
```

### Example

Public subnet ke route table:

```text
Destination       Target

10.0.0.0/16       local
0.0.0.0/0         IGW
```

Private subnet:

```text
Destination       Target

10.0.0.0/16       local
0.0.0.0/0         NAT Gateway
```

---

# 6. Internet Gateway — IGW

Internet Gateway VPC ko **Internet se connect** karta hai.

```text
Internet
   |
  IGW
   |
 VPC
```

Public subnet ke resources internet se communicate kar sakte hain, provided routing and security allow it.

### Important

Sirf IGW attach kar dene se subnet automatically public nahi hota.

Public subnet generally requires:

```text
Subnet
 +
Route table → IGW
 +
Resource public IPv4 / suitable internet addressing
 +
Security rules
```

---

# 7. NAT Gateway

NAT = **Network Address Translation**

Private subnet ke resource ko **outbound internet access** dene ke liye commonly use hota hai.

Example:

```text
                INTERNET
                    |
                   IGW
                    |
              NAT Gateway
                    |
             Private Subnet
                    |
               Application
```

Application:

```text
Private EC2
     |
     | download package/API call
     ↓
NAT Gateway
     ↓
Internet
```

But internet generally **directly private resource ko initiate karke access nahi kar sakta** through NAT Gateway.

### Real example

Private application needs:

```text
GitHub API
External payment API
OS package repository
```

NAT Gateway use ho sakta hai.

---

# 8. Elastic IP — EIP

**Static public IPv4 address**.

Normal public IP change ho sakta hai in certain lifecycle situations.

Elastic IP:

```text
Static Public IP
       |
Resource
```

Useful when you need a stable public IPv4 address.

---

# 9. ENI — Elastic Network Interface

ENI basically **virtual network card** hai.

Jaise physical server mein:

```text
Network Card
     |
IP Address
     |
MAC Address
```

AWS mein:

```text
EC2
 |
 ENI
 |
 +-- Private IP
 +-- MAC address
 +-- Security Groups
```

Ek EC2 ke multiple ENIs bhi ho sakte hain, depending on instance/network limits.

---

# 10. Private IP

VPC ke andar resource ka internal IP.

Example:

```text
EC2
10.0.2.15
```

Application-to-application communication ke liye commonly private IP/DNS use hota hai.

```text
App Server
10.0.2.15
     |
     ↓
DB
10.0.3.20
```

---

# 11. Public IP

Internet-facing IPv4 address.

Example:

```text
EC2
Private IP: 10.0.1.10
Public IP: 3.x.x.x
```

Public IP allows internet communication when routing/security configuration permits.

---

# 12. IPv4 / IPv6

AWS networking supports both.

### IPv4

Example:

```text
10.0.1.10
```

### IPv6

Example:

```text
2001:db8::1234
```

IPv6 has a huge address space.

---

# 13. Security Group

Security Group is a **stateful virtual firewall** attached to resources such as ENIs.

Example:

```text
EC2 Security Group

Inbound:
22 → SSH
80 → HTTP
443 → HTTPS
8080 → Application
```

Suppose:

```text
Internet
   |
   X
EC2
```

because SG doesn't allow that traffic.

### Important interview point

Security Group is:

**Stateful**

If inbound traffic is allowed, response traffic is automatically allowed.

---

# 14. Network ACL — NACL

NACL = **Network Access Control List**

Subnet level security.

```text
VPC
 |
Subnet
 |
NACL
 |
Resources
```

Security Group:

```text
Resource level
```

NACL:

```text
Subnet level
```

### NACL is stateless

Return traffic needs its own rule.

---

# SG vs NACL

| Security Group                       | NACL                                      |
| ------------------------------------ | ----------------------------------------- |
| Resource/ENI level                   | Subnet level                              |
| Stateful                             | Stateless                                 |
| Allow rules                          | Allow + deny rules                        |
| Return traffic automatically allowed | Return traffic must be explicitly allowed |
| Commonly primary resource firewall   | Additional subnet-level control           |

---

# 15. DNS

DNS converts names into IP addresses.

Instead of:

```text
10.0.2.50
```

application can use:

```text
api.hotel.com
```

DNS resolves:

```text
api.hotel.com
       ↓
IP address
```

AWS mein **Route 53** major DNS service hai.

---

# 16. Route 53

Route 53 is AWS's highly available **DNS service**.

Uses:

* Domain name resolution
* DNS records
* Health checks
* Routing policies
* Domain registration

Example:

```text
hotel.com
   |
api.hotel.com
   |
Load Balancer
```

---

# 17. Route 53 Routing Policies

Important ones:

### Simple

Basic DNS routing.

### Weighted

Traffic percentage ke basis par.

```text
90% → Server A
10% → Server B
```

Useful for testing/canary type DNS traffic distribution.

### Latency-based

User ko lower-latency region ke endpoint ki taraf route karna.

```text
India user → Mumbai
US user    → Virginia
```

### Failover

Primary unhealthy → secondary.

```text
Primary
   ↓
Unhealthy
   ↓
Secondary
```

### Geolocation

User location ke basis par routing.

### Geoproximity

Resources aur users ke geographic relationship ke basis par routing, with traffic-flow configuration.

### IP-based

Client IP information ke basis par routing.

---

# 18. VPC DNS

VPC ke andar AWS-provided DNS capability available hoti hai.

Iska use internal resource name resolution ke liye hota hai.

Example:

```text
EC2
 |
internal DNS
 |
private resource IP
```

---

# 19. DHCP Options Set

DHCP = Dynamic Host Configuration Protocol.

AWS VPC mein DHCP options set se network configuration provide ki ja sakti hai, such as:

* DNS servers
* Domain name
* NTP-related configuration

Usually normal AWS architecture mein tumhe isko frequently modify nahi karna padta.

---

# 20. VPC Endpoint

Very important.

Private resources ko AWS services access karne ke liye **public internet route ki zarurat avoid** kar sakte ho.

Example:

```text
Private EC2
    |
VPC Endpoint
    |
    S3
```

instead of:

```text
Private EC2
   |
 NAT
   |
Internet
   |
 S3
```

Main types:

### Gateway Endpoint

Primarily:

```text
S3
DynamoDB
```

### Interface Endpoint

Powered by AWS PrivateLink.

Used for many AWS services and endpoint services.

---

# 21. AWS PrivateLink

Private connectivity provide karta hai between VPC and supported services/endpoints **without traversing the public internet**.

Conceptually:

```text
Consumer VPC
     |
Interface Endpoint
     |
PrivateLink
     |
Service Provider
```

Very useful when one organization/application wants to expose a service privately to another VPC/account.

---

# 22. VPC Peering

Two VPCs ko directly connect karna.

```text
VPC A
10.0.0.0/16
     |
 VPC Peering
     |
VPC B
10.1.0.0/16
```

Then routes are added in route tables so traffic can flow.

### Important

VPC Peering:

**one-to-one connectivity**

---

# 23. Transit Gateway

Agar bahut saare VPCs hain, individual peering difficult ho sakti hai.

Instead:

```text
VPC A ----\
VPC B -----\
VPC C ------ Transit Gateway
VPC D -----/
VPC E ----/
```

Transit Gateway acts as a **central network hub**.

Useful for:

* Many VPCs
* Multi-account architecture
* Hybrid networking
* Centralized routing

---

# 24. Site-to-Site VPN

On-premises network ko AWS VPC se securely connect karna.

```text
Company Data Center
        |
     VPN
        |
   AWS VPC
```

Usually IPsec-based encrypted tunnels are used.

Example:

```text
Company Hotel System
        |
VPN
        |
AWS
```

---

# 25. Virtual Private Gateway — VGW

VPC side ka VPN gateway.

Concept:

```text
On-Prem
   |
Customer Gateway
   |
VPN
   |
Virtual Private Gateway
   |
VPC
```

---

# 26. Customer Gateway — CGW

On-premises side ko represent karta hai for AWS Site-to-Site VPN configuration.

```text
On-Prem Device
      |
Customer Gateway
      |
VPN
      |
AWS VGW / TGW
```

---

# 27. Direct Connect

Dedicated network connection between on-premises and AWS.

```text
Company
   |
Dedicated Connection
   |
AWS
```

VPN ke comparison mein:

```text
VPN
→ Internet-based encrypted connection

Direct Connect
→ Dedicated connectivity
```

Use cases:

* High bandwidth
* Consistent network performance
* Hybrid cloud
* Large data transfer

---

# 28. Direct Connect Gateway

Multiple VPCs/regions or network architecture ko Direct Connect connectivity ke through connect karne mein help karta hai.

Conceptually:

```text
On-Prem
   |
Direct Connect
   |
DX Gateway
   |
Transit Gateway / VPC connectivity
```

---

# 29. Load Balancer

Load Balancer incoming traffic ko multiple targets ke across distribute karta hai.

```text
              Users
                |
          Load Balancer
          /      |      \
       App1    App2    App3
```

AWS ke important load balancers:

```text
ALB
NLB
GWLB
```

---

# 30. Application Load Balancer — ALB

Layer 7 load balancer.

Works with HTTP/HTTPS.

Can route based on:

* Host
* Path
* HTTP headers
* Query strings

Example:

```text
api.hotel.com/booking
          |
         ALB
          |
      Booking Service

api.hotel.com/payment
          |
         ALB
          |
      Payment Service
```

---

# 31. Network Load Balancer — NLB

Layer 4.

Primarily TCP/UDP/TLS traffic.

Useful when you need:

* Very high performance
* Low latency
* Static IP support
* TCP/UDP workloads

Example:

```text
Client
  |
 NLB
  |
TCP application
```

---

# 32. Gateway Load Balancer — GWLB

Used for deploying and scaling **network virtual appliances**.

Examples:

```text
Firewall
IDS/IPS
Deep packet inspection
Security appliance
```

Concept:

```text
Traffic
   |
GWLB
   |
Security Appliance
   |
Application
```

---

# 33. AWS WAF

WAF = **Web Application Firewall**

Layer 7 web traffic protection.

Can help protect applications from things such as:

* SQL injection
* Cross-site scripting
* Bad bots
* IP-based rules
* HTTP request patterns

Typical:

```text
Internet
   |
  WAF
   |
 ALB
   |
Application
```

---

# 34. AWS Network Firewall

Different from WAF.

AWS Network Firewall is a **managed network firewall** for VPC traffic inspection and filtering.

Think:

```text
WAF
→ Web/HTTP application traffic

Network Firewall
→ Network-level traffic inspection/control
```

---

# 35. CloudFront

CloudFront = AWS CDN.

Content ko users ke geographically closer **edge locations** se serve karta hai.

```text
India User
    |
CloudFront Edge
    |
Origin

US User
    |
CloudFront Edge
    |
Origin
```

Benefits:

* Lower latency
* Caching
* Global content delivery
* HTTPS
* Integration with AWS origins

---

# 36. Global Accelerator

Global Accelerator improves global application traffic routing using AWS global network infrastructure.

```text
User
 |
AWS Global Accelerator
 |
AWS Edge
 |
Regional Application
```

It can provide static anycast IP addresses and route users toward healthy endpoints.

### CloudFront vs Global Accelerator

```text
CloudFront
→ Content delivery / caching

Global Accelerator
→ Application network traffic acceleration
```

---

# 37. Elastic Load Balancer

ELB is the overall AWS load-balancing service family.

Under it:

```text
ELB
 |
 +-- ALB
 +-- NLB
 +-- GWLB
```

---

# 38. Target Group

Load balancer ko actual backend targets se connect karta hai.

Example:

```text
ALB
 |
Target Group
 |
 +-- EC2-1
 +-- EC2-2
 +-- EC2-3
```

Health checks bhi target groups ke through configure hote hain.

---

# 39. VPC Flow Logs

Very important for troubleshooting.

VPC Flow Logs capture information about IP traffic going to/from network interfaces.

Useful for:

```text
Why connection failing?
Why timeout?
Is traffic reaching server?
Which IP is communicating?
Is traffic rejected?
```

Example:

```text
Client
  |
  X
Server

Flow Logs
   ↓
Traffic rejected/accepted information
```

---

# 40. Traffic Mirroring

Network traffic ko inspect karne ke liye ENI traffic ko security/monitoring appliance tak mirror kar sakte ho.

```text
ENI
 |
Traffic Mirror
 |
Security Tool
```

Useful for:

* Network monitoring
* Troubleshooting
* Security analysis

---

# 41. VPC Reachability Analyzer

Networking troubleshooting tool.

Question:

> "Kya source se destination tak network path possible hai?"

Example:

```text
EC2 → DB
```

Reachability Analyzer configuration analyze karke bata sakta hai ki connectivity possible hai ya kis network component/rule ki wajah se path blocked hai.

---

# 42. VPC Lattice

Application networking service for connecting services across VPCs/accounts with centralized service-to-service connectivity, security and traffic management.

Simple:

```text
Service A
   |
VPC Lattice
   |
Service B
```

Useful especially for distributed/microservice architectures.

---

# 43. Service Discovery

Applications ko services locate karne mein help karta hai.

Instead of hardcoding:

```text
10.0.2.15
```

application can discover a service through a DNS/service name.

AWS ecosystem mein **Cloud Map** service discovery ke liye important service hai.

---

# 44. Amazon API Gateway

Strictly speaking API Gateway is an **API management/service entry point**, not simply a subnet networking component, but networking architecture mein frequently involved hota hai.

```text
Client
  |
API Gateway
  |
Backend
```

It can provide:

* API endpoint
* Routing
* Authentication/authorization integrations
* Throttling
* API management

---

# 45. AWS Private API Gateway connectivity

Private APIs can be accessed through VPC connectivity mechanisms such as interface VPC endpoints.

Concept:

```text
Private Network
      |
VPC Endpoint
      |
Private API
```

Useful when API should not be publicly reachable.

---

# 46. Egress-only Internet Gateway

IPv6 networks ke liye.

Private IPv6 resources ko outbound internet communication allow karne ke liye use hota hai while preventing internet-initiated inbound connections.

```text
IPv6 Private Resource
        |
Egress-only IGW
        |
Internet
```

IPv4 NAT Gateway ke concept se compare kar sakte ho, but this is specifically for IPv6.

---

# 47. NAT Instance

Historically NAT instance bhi use kiya ja sakta tha.

```text
Private Subnet
      |
 NAT Instance
      |
Internet
```

But managed **NAT Gateway** is generally preferred for most production architectures.

Interview mein difference pata hona useful hai.

---

# 48. Network Address Translation — NAT

NAT ka basic purpose:

```text
Private IP
   ↓
Public connectivity
   ↓
Internet
```

Example:

```text
10.0.2.15
    ↓
NAT
    ↓
Public IP
    ↓
Internet
```

---

# 49. AWS Network Connectivity Center Concepts

Large enterprise networking mein commonly:

```text
VPC
 |
Transit Gateway
 |
VPN
 |
Direct Connect
 |
On-Prem
```

combine kiye ja sakte hain.

---

# 50. Transit Gateway Peering

Multiple Transit Gateways ko connect kar sakte ho.

Example:

```text
Region A
 TGW
  |
TGW Peering
  |
 TGW
Region B
```

Useful for multi-region network architecture.

---

# 51. VPC Peering vs Transit Gateway

### VPC Peering

```text
A -------- B
```

One-to-one.

### Transit Gateway

```text
 A \
 B  \
 C -- TGW
 D  /
 E /
```

Centralized hub.

---

# 52. VPN vs Direct Connect

| VPN                               | Direct Connect                                                       |
| --------------------------------- | -------------------------------------------------------------------- |
| Internet-based                    | Dedicated connectivity                                               |
| Usually quicker to establish      | More setup                                                           |
| Encrypted tunnels                 | Dedicated connection itself isn't the same as application encryption |
| Good for many normal hybrid cases | Good for predictable/high-volume connectivity                        |
| Generally lower initial cost      | Higher infrastructure/setup cost                                     |

---

# 53. Public vs Private Subnet

This is one of the **most important interview topics**.

### Public subnet

Route:

```text
0.0.0.0/0 → IGW
```

### Private subnet

Typically:

```text
0.0.0.0/0 → NAT Gateway
```

for IPv4 outbound internet access.

### Remember:

**Public/private subnet is determined mainly by routing, not simply by its name.**

---

# 54. Complete Real Enterprise Architecture

Ab sabko ek saath connect karo:

```text
                         INTERNET
                            |
                       Route 53
                            |
                       CloudFront
                            |
                           WAF
                            |
                           ALB
                            |
              +-------------+-------------+
              |                           |
          Public Subnet               Public Subnet
              |                           |
            ALB node                   ALB node
              |                           |
              +-------------+-------------+
                            |
                     Private App Subnets
                       /            \
                     AZ-1          AZ-2
                      |              |
                    App            App
                      |              |
                      +------+-------+
                             |
                       Private DB
                       Subnets
                       /       \
                     AZ-1      AZ-2

Private App
     |
     | outbound internet
     ↓
NAT Gateway
     |
    IGW
     |
 Internet
```

Security:

```text
Internet
   ↓
WAF
   ↓
ALB SG
   ↓
App SG
   ↓
DB SG
```

Networking:

```text
VPC
 |
 +-- CIDR
 |
 +-- Subnets
 |     |
 |     +-- Public
 |     +-- Private
 |
 +-- Route Tables
 |
 +-- IGW
 |
 +-- NAT Gateway
 |
 +-- Security Groups
 |
 +-- NACL
 |
 +-- VPC Endpoints
 |
 +-- Flow Logs
```

---

# 55. The MOST Important Networking Troubleshooting Flow

Interview mein agar poocha:

> **"Application server cannot connect to database. How will you troubleshoot?"**

Networking perspective se:

```text
1. DNS
   ↓
2. Source IP
   ↓
3. Destination IP
   ↓
4. Route Table
   ↓
5. Security Group
   ↓
6. NACL
   ↓
7. Network connectivity
   ↓
8. Port
   ↓
9. Application/service listening
   ↓
10. VPC Flow Logs
   ↓
11. Reachability Analyzer
```

Example:

```text
App
10.0.2.15
   |
   | TCP 5432
   ↓
DB
10.0.3.20
```

Check:

```text
App SG
   ↓
Does it allow outbound?

DB SG
   ↓
Does it allow inbound TCP 5432
from App SG?

Route table
   ↓
Is route available?

NACL
   ↓
Is traffic/return traffic allowed?

DB
   ↓
Is service listening on 5432?
```

---

# 56. AWS Networking — Interview Memory Map

Isko **5 groups** mein yaad karo.

### 🟢 Group 1 — Network Foundation

```text
VPC
CIDR
Subnet
AZ
IPv4
IPv6
ENI
Private IP
Public IP
Elastic IP
DHCP
```

### 🔵 Group 2 — Traffic/Routing

```text
Route Table
Internet Gateway
NAT Gateway
Egress-only IGW
VPC Peering
Transit Gateway
Transit Gateway Peering
```

### 🟡 Group 3 — Security

```text
Security Group
NACL
AWS WAF
AWS Network Firewall
VPC Flow Logs
Traffic Mirroring
```

### 🟠 Group 4 — Connectivity

```text
VPC Endpoint
PrivateLink
Site-to-Site VPN
Customer Gateway
Virtual Private Gateway
Direct Connect
Direct Connect Gateway
```

### 🔴 Group 5 — Traffic Distribution / Global Networking

```text
Route 53
ALB
NLB
GWLB
CloudFront
Global Accelerator
Target Groups
VPC Lattice
Service Discovery
```

---

## One-line revision

| Component                 | Simple meaning                          |
| ------------------------- | --------------------------------------- |
| **VPC**                   | AWS ka private network                  |
| **CIDR**                  | IP address range                        |
| **Subnet**                | VPC ka smaller network                  |
| **AZ**                    | Region ke andar isolated location       |
| **Route Table**           | Traffic ka route decide karta hai       |
| **IGW**                   | VPC ↔ Internet                          |
| **NAT Gateway**           | Private subnet → Internet outbound      |
| **EIP**                   | Static public IPv4                      |
| **ENI**                   | Virtual network card                    |
| **SG**                    | Resource-level stateful firewall        |
| **NACL**                  | Subnet-level stateless firewall         |
| **Route 53**              | DNS                                     |
| **VPC Endpoint**          | Private access to AWS/services          |
| **PrivateLink**           | Private service connectivity            |
| **VPC Peering**           | VPC-to-VPC connection                   |
| **Transit Gateway**       | Central network hub                     |
| **VPN**                   | Encrypted network tunnel                |
| **Direct Connect**        | Dedicated AWS connectivity              |
| **ALB**                   | HTTP/HTTPS Layer-7 load balancer        |
| **NLB**                   | TCP/UDP/TLS Layer-4 load balancer       |
| **GWLB**                  | Network security appliances             |
| **WAF**                   | Web/application firewall                |
| **Network Firewall**      | VPC network firewall                    |
| **CloudFront**            | CDN                                     |
| **Global Accelerator**    | Global application traffic acceleration |
| **Flow Logs**             | Network traffic visibility              |
| **Reachability Analyzer** | Network path troubleshooting            |
| **Traffic Mirroring**     | Copy network traffic for inspection     |
| **VPC Lattice**           | Service-to-service networking           |
| **Egress-only IGW**       | IPv6 outbound internet                  |
| **Target Group**          | LB backend targets                      |

### Sabse important conceptual chain

Agar tum AWS networking ko genuinely samajhna chahte ho, ye chain dimaag mein rakho:

```text
VPC
 ↓
CIDR
 ↓
Subnet
 ↓
Route Table
 ↓
Gateway
 ↓
Security Group
 ↓
NACL
 ↓
DNS
 ↓
Load Balancer
 ↓
VPC Endpoint / NAT
 ↓
Peering / TGW
 ↓
VPN / Direct Connect
 ↓
Flow Logs / Reachability Analyzer
```

**Ye networking ka backbone hai.** Is backbone ko samajh lene ke baad scenario-based troubleshooting questions kaafi easy ho jaate hain.
====================
Networking End
=====================

# IAM
Bilkul. Ab **AWS IAM + Security** ko exactly interview-oriented way mein karte hain—**simple English + simple Hindi meaning + use + real enterprise example + troubleshooting + 6-year experience questions**. Sirf relevant security concepts rakhenge, unnecessary AWS services mein nahi jayenge.

# AWS IAM + SECURITY — COMPLETE INTERVIEW NOTES

## 1. IAM kya hai?

**IAM = Identity and Access Management**

Simple:

> **IAM decides WHO can access WHAT and WHAT they are allowed to do.**

Example:

```text
Developer
   |
   ↓
IAM
   |
   ├── EC2 → allowed
   ├── S3 → read only
   └── RDS → denied
```

IAM ke 3 basic questions:

```text
WHO?       → Identity
WHAT?      → Resource
DO WHAT?   → Permission
```

---

# 2. Authentication vs Authorization

Ye interview mein bahut important hai.

### Authentication

> **Who are you?**

Example:

```text
Username + Password
MFA
```

### Authorization

> **What are you allowed to do?**

Example:

```text
User can:
✓ Read S3

User cannot:
✗ Delete S3
```

Remember:

```text
Authentication → Identity check
Authorization  → Permission check
```

---

# 3. IAM User

IAM User represents a person/application identity that needs long-term AWS access.

Example:

```text
IAM
 |
 +-- Developer
 +-- Tester
 +-- Admin
```

User can have:

* Console password
* Access keys
* Policies

### But production applications ke liye?

Usually **IAM User access keys hardcode nahi karni chahiye**.

Instead:

> **Use IAM Role + temporary credentials.**

---

# 4. IAM Group

Group multiple IAM users ko organize karta hai.

Example:

```text
Developers Group
 |
 +-- Rahul
 +-- Amit
 +-- Priya
```

Group ko policy:

```text
S3ReadPolicy
```

attach kar do.

Then users inherit permissions.

### Why?

Instead of:

```text
Rahul → policy
Amit → policy
Priya → policy
```

Use:

```text
Developers Group
       |
   S3 Read Policy
       |
   All developers
```

---

# 5. IAM Role

**Role is one of the most important IAM concepts.**

Role provides permissions that can be **assumed** by trusted entities.

Example:

```text
EC2
 |
Assume IAM Role
 |
Temporary Credentials
 |
S3
```

Application ke andar:

```text
EC2
 ↓
IAM Role
 ↓
S3
```

No access key hardcoding required.

---

# 6. Real Java application example

Suppose hotel management application EC2 par running hai.

Application ko S3 mein invoices upload karne hain.

Bad approach:

```text
application.properties

AWS_ACCESS_KEY=xxxx
AWS_SECRET_KEY=xxxx
```

❌ Security risk.

Better:

```text
EC2
 |
IAM Role
 |
S3 permissions
```

Application AWS SDK se role credentials use kar leti hai.

### Interview answer

> "For production workloads, we avoid hardcoding access keys. We attach an IAM role to the compute resource and use temporary credentials provided through the AWS credential provider chain."

---

# 7. IAM Policy

Policy defines permissions.

Simple:

> **Policy tells IAM what actions are allowed or denied on which resources.**

Example:

```text
Allow
Action:
s3:GetObject

Resource:
specific bucket
```

Conceptually:

```text
WHO
 ↓
CAN DO WHAT
 ↓
ON WHICH RESOURCE
```

---

# 8. Policy ke important elements

Typical IAM policy:

```json
{
  "Effect": "Allow",
  "Action": "s3:GetObject",
  "Resource": "arn:aws:s3:::hotel-bucket/*"
}
```

Understand:

### Effect

```text
Allow
Deny
```

### Action

What operation?

```text
s3:GetObject
s3:PutObject
s3:DeleteObject
```

### Resource

Kis AWS resource par?

```text
S3 bucket/object
```

### Principal

Who is allowed?

Mostly resource-based policies mein important.

---

# 9. ARN

ARN = **Amazon Resource Name**

AWS resources ko uniquely identify karta hai.

Example:

```text
arn:aws:s3:::hotel-bucket
```

Concept:

```text
arn
 ↓
partition
 ↓
service
 ↓
region
 ↓
account
 ↓
resource
```

Har service ka ARN format slightly different ho sakta hai.

---

# 10. Managed Policy

AWS ya customer-created reusable policy.

Two major types:

### AWS Managed Policy

AWS provides it.

Example:

```text
AmazonS3ReadOnlyAccess
```

### Customer Managed Policy

Company khud create karti hai.

Example:

```text
HotelApplicationS3ReadPolicy
```

Reusable across identities.

---

# 11. Inline Policy

Policy directly ek particular identity/resource relationship par embedded hoti hai.

Example:

```text
IAM Role
   |
Inline Policy
```

Usually reusable permission model ke liye customer-managed policies easier to manage hote hain.

---

# 12. Identity-based Policy

Policy identity par attach hoti hai.

Identity:

```text
User
Group
Role
```

Example:

```text
ApplicationRole
      |
S3ReadPolicy
```

---

# 13. Resource-based Policy

Policy directly resource par attach hoti hai.

Example:

```text
S3 Bucket
   |
Bucket Policy
```

It can specify a **Principal**.

Example concept:

```text
S3 Bucket
 |
Allow Account B
 |
Read objects
```

---

# 14. Identity Policy vs Resource Policy

| Identity-based               | Resource-based                 |
| ---------------------------- | ------------------------------ |
| User/group/role par attached | Resource par attached          |
| Principal usually implicit   | Principal explicitly specified |
| Example IAM policy           | Example S3 bucket policy       |
| "This identity can..."       | "This resource allows..."      |

---

# 15. Trust Policy

**Role ka trust policy batata hai ki ROLE KO KAUN ASSUME KAR SAKTA HAI.**

Ye bahut important distinction hai.

Example:

```text
EC2
 |
Can assume?
 ↓
IAM Role
```

Trust policy:

```text
EC2 service
→ allowed to assume role
```

### Remember:

```text
Trust Policy
= Who can assume this role?

Permission Policy
= After assuming role, what can it do?
```

---

# 16. Trust Policy vs Permission Policy

Interview favourite.

### Trust Policy

```text
WHO CAN ASSUME ROLE?
```

### Permission Policy

```text
WHAT CAN ROLE DO?
```

Example:

```text
EC2
 |
Trust Policy
 ↓
ApplicationRole
 |
Permission Policy
 ↓
S3:GetObject
```

---

# 17. AssumeRole

An identity can assume a role if trust/permissions allow it.

Example:

```text
Developer
    |
 AssumeRole
    ↓
ProductionRole
    |
    ↓
Production resources
```

This is common for cross-account access.

---

# 18. STS

STS = **AWS Security Token Service**

Provides temporary security credentials.

Concept:

```text
Role
 ↓
STS
 ↓
Temporary Credentials
 ↓
AWS Service
```

Temporary credentials generally consist of:

```text
Access Key ID
Secret Access Key
Session Token
```

### Why?

Temporary credentials are safer than distributing long-lived credentials.

---

# 19. IAM Role vs IAM User

| IAM User                                                 | IAM Role                      |
| -------------------------------------------------------- | ----------------------------- |
| Represents identity                                      | Assumable identity            |
| Often person/service identity                            | Temporary permissions         |
| Can have long-term credentials                           | Usually temporary credentials |
| Console/password/access keys possible                    | Assumed by trusted entity     |
| Applications generally shouldn't use hardcoded user keys | Preferred for AWS workloads   |

---

# 20. Least Privilege

**Give only the permissions actually required.**

Bad:

```text
Application
 ↓
AdministratorAccess
```

❌ Too much access.

Better:

```text
Application
 ↓
s3:GetObject
s3:PutObject
```

Only required permissions.

### Interview line:

> "We follow the principle of least privilege and grant only the minimum permissions required for the workload."

---

# 21. Wildcard permissions

Dangerous:

```text
Action: "*"
Resource: "*"
```

Means practically everything allowed depending on context.

Avoid unless genuinely required.

Better:

```text
Action:
s3:GetObject

Resource:
specific bucket/object path
```

---

# 22. Explicit Deny

This is **extremely important**.

Suppose:

```text
Policy A
Allow S3 Delete

Policy B
Deny S3 Delete
```

Final result:

```text
DENY
```

Because:

> **Explicit Deny overrides Allow.**

Remember:

```text
Explicit Deny
      ↓
wins
```

---

# 23. IAM Policy Evaluation — Simple Flow

When request comes:

```text
AWS Request
    |
Authentication
    |
Policies evaluated
    |
Is there explicit Deny?
    |
   YES → DENY
    |
   NO
    |
Is there applicable Allow?
    |
   YES → ALLOW
    |
   NO → DENY
```

Important default principle:

> **By default, access is denied unless an applicable Allow exists.**

---

# 24. MFA

MFA = Multi-Factor Authentication.

Example:

```text
Password
 +
Authenticator code
```

Even if password is compromised, attacker needs another factor.

Use especially for:

* privileged human access
* root account
* sensitive administrative operations

---

# 25. Root User

AWS account root user has extremely powerful permissions.

Best practice:

```text
Root
 ↓
Secure strongly
 ↓
Enable MFA
 ↓
Avoid everyday usage
```

Don't use root user for normal application/development operations.

---

# 26. Access Keys

Used for programmatic AWS API access.

```text
Access Key ID
+
Secret Access Key
```

### Never:

```text
GitHub
.properties
source code
Docker image
```

mein credentials commit/embed mat karo.

---

# 27. Temporary Credentials

Preferred for many workloads.

```text
IAM Role
 ↓
STS
 ↓
Temporary credentials
```

They expire automatically.

This reduces the risk associated with long-lived secrets.

---

# 28. Cross-account access

Suppose:

```text
Account A
Developer

        ↓ AssumeRole

Account B
Production
```

Common approach:

```text
Account B
ProductionRole
 |
Trust Account A
```

Developer assumes the role.

No need to permanently create a user in production account just for this access pattern.

---

# 29. Cross-account S3 example

```text
Account A
Application
    |
    | Assume Role
    ↓
Account B
S3 Access Role
    |
    ↓
S3 Bucket
```

Need to correctly configure:

```text
Trust policy
+
Permission policy
+
Resource policy where applicable
```

---

# 30. Secrets Manager

Application secrets securely store karne ke liye.

Examples:

```text
DB password
API key
OAuth secret
Application credential
```

Instead of:

```text
application.properties

password=MyPassword123
```

Use:

```text
Application
    |
Secrets Manager
    |
Secret
```

Application retrieves it securely with appropriate IAM permissions.

---

# 31. KMS

KMS = **Key Management Service**

Encryption keys create/manage/control karne ke liye.

Simple:

```text
Data
 ↓
Encryption
 ↓
KMS Key
 ↓
Encrypted Data
```

KMS commonly integrates with:

* S3
* EBS
* RDS
* Secrets Manager
* many other AWS services

---

# 32. Encryption at Rest vs in Transit

### At Rest

Stored data encrypted.

```text
Database
Disk
S3
Backup
```

### In Transit

Network ke through data encrypted.

```text
Client
  |
 HTTPS/TLS
  |
Server
```

Remember:

```text
At Rest     → stored data
In Transit  → moving data
```

---

# 33. KMS vs Secrets Manager

Common confusion.

### KMS

> Encryption keys manage karta hai.

### Secrets Manager

> Secrets store/manage karta hai.

Example:

```text
Secrets Manager
      |
DB password
      |
Encryption using KMS
```

---

# 34. CloudTrail

CloudTrail records AWS API activity/events.

Question:

> **Who changed this security group?**

CloudTrail can help answer:

```text
Who?
What?
When?
From where?
Which API call?
```

Example:

```text
Someone deleted IAM policy
        ↓
CloudTrail
        ↓
Find API event
```

---

# 35. IAM Access Analyzer

Helps identify unintended resource access, especially external/cross-account access.

Example:

```text
S3 Bucket
   |
Public access?
Cross-account access?
   ↓
Access Analyzer
```

Useful for finding overly broad access configurations.

---

# 36. Permission Boundaries

Advanced IAM concept.

Permission boundary sets the **maximum permissions** an IAM user/role can receive through identity-based policies.

Simple:

```text
Actual permissions
       ∩
Permission boundary
       ↓
Effective permissions
```

Example:

Developer creates a role and attaches:

```text
AdministratorAccess
```

But permission boundary limits it to:

```text
S3 + CloudWatch
```

So the role cannot exceed the boundary.

---

# 37. Service Control Policies — SCP

Used with **AWS Organizations**.

SCP sets permission guardrails for accounts/organizational units.

Important:

> SCP does **not itself grant permissions**. It can limit what permissions are available.

Concept:

```text
AWS Organization
       |
      SCP
       |
   Account
       |
 IAM policies
       |
Effective access
```

---

# 38. SCP vs IAM Policy

| IAM Policy                                        | SCP                                  |
| ------------------------------------------------- | ------------------------------------ |
| Grants/controls permissions for identity/resource | Organization-level guardrail         |
| User/Group/Role/resource                          | Account/OU                           |
| Can grant access                                  | Does not grant access                |
| Controls what identity can do                     | Limits maximum available permissions |

---

# 39. IAM Identity Center

For workforce users and centralized access to multiple AWS accounts, **IAM Identity Center** is commonly used.

Concept:

```text
Employee
   |
IAM Identity Center
   |
Permission Set
   |
AWS Account
```

Useful for centralized workforce access instead of maintaining separate IAM users in every account.

---

# 40. Permission Set

In IAM Identity Center, permission sets define what access users/groups receive in AWS accounts.

Example:

```text
Developer Permission Set
        |
   Read/Developer access
        |
Account A
Account B
Account C
```

---

# 41. AWS WAF

Networking mein already dekha tha, but security side se remember:

```text
Internet
   |
  WAF
   |
  ALB
   |
Application
```

Protect against web request patterns such as:

* SQL injection
* XSS
* malicious requests
* bot-related patterns
* IP/rate based rules

---

# 42. Security Group

Again security architecture mein:

```text
ALB SG
 ↓
App SG
 ↓
DB SG
```

Best practice:

```text
Internet
   ↓
ALB SG: 443
   ↓
App SG: only from ALB SG
   ↓
DB SG: only from App SG
```

This is much better than:

```text
DB SG
 ↓
0.0.0.0/0
```

---

# 43. IAM + Networking together — Real Architecture

Suppose enterprise hotel management application:

```text
                  Internet
                      |
                     WAF
                      |
                     ALB
                      |
                 ALB Security Group
                      |
              +-------+-------+
              |               |
            App-1           App-2
              |               |
         App Security Group
              |
          IAM Role
              |
       +------+-------+
       |              |
      S3           Secrets Manager
       |              |
      KMS            KMS
                      |
                     DB
                      |
                  DB Security Group
```

IAM controls:

```text
WHO CAN ACCESS AWS RESOURCES
```

Security Groups control:

```text
WHO CAN NETWORK TO THE RESOURCE
```

This distinction is **very important**.

---

# 44. IAM vs Security Group

Interviewer:

> "If IAM allows access, can application connect to database?"

**Not necessarily.**

IAM and network security are different layers.

```text
IAM
 ↓
AWS API authorization

Security Group
 ↓
Network connectivity
```

Example:

```text
IAM → S3:GetObject allowed

BUT

Network → DB port 5432 blocked
```

Application can have correct IAM permissions and still fail due to network configuration.

---

# 45. Real Troubleshooting Scenario #1

### Problem:

> EC2 application is getting AccessDenied while reading S3.

6-year experience answer:

```text
1. Check which IAM role is attached to EC2.
2. Verify application is actually using that role.
3. Check IAM policy.
4. Verify s3:GetObject permission.
5. Verify correct bucket/object ARN.
6. Check bucket policy.
7. Check for explicit Deny.
8. Check SCP if organization is used.
9. Check permission boundary.
10. Use CloudTrail/IAM policy analysis tools for evidence.
```

### Strong interview line:

> "I don't immediately modify the policy. First I identify the caller identity and exact AWS API action, then verify identity policy, resource policy, explicit denies, boundaries and organization-level restrictions."

**Ye experienced answer feel deta hai.**

---

# 46. Real Troubleshooting Scenario #2

### Problem:

> Application suddenly stopped accessing S3 after deployment.

Check:

```text
Old environment
     ↓
IAM Role A

New environment
     ↓
IAM Role B
```

Maybe deployment changed the role.

Then:

```text
Role B
 ↓
Missing S3 permission
```

Fix:

```text
Correct role
+
Minimum required permission
```

---

# 47. Real Troubleshooting Scenario #3

### Problem:

> Developer says "IAM role has S3 access, but S3 still gives AccessDenied."

Don't stop at role policy.

Check:

```text
Role policy
      ↓
Bucket policy
      ↓
Explicit Deny
      ↓
SCP
      ↓
Permission Boundary
      ↓
KMS permissions
      ↓
Object ownership/encryption configuration
```

Especially if S3 object is encrypted using KMS:

```text
S3 access
+
KMS permission
```

may both matter.

---

# 48. Real Troubleshooting Scenario #4

### Problem:

> EC2 application cannot retrieve secret.

Check:

```text
1. EC2 IAM Role
2. secretsmanager:GetSecretValue
3. Correct secret ARN
4. KMS permissions if customer-managed KMS key is involved
5. VPC endpoint/NAT/network connectivity
6. Region
7. Secret resource policy if applicable
8. CloudTrail
```

Notice this is a **security + networking** problem.

---

# 49. Real Troubleshooting Scenario #5

### Problem:

> Someone accidentally exposed an S3 bucket.

Experienced approach:

```text
1. Identify current bucket policy.
2. Check Block Public Access.
3. Check ACL/object ownership configuration where relevant.
4. Check Access Analyzer.
5. Review CloudTrail for the change.
6. Remove unintended public access.
7. Identify who/what made the change.
8. Add preventive guardrails.
```

Don't just say:

> "I'll make bucket private."

Explain **how you identify the root cause and prevent recurrence**.

---

# 50. 6-Year Experience — Golden IAM Answer

Interviewer:

> **How do you secure AWS applications?**

Answer:

> "We follow least privilege and avoid long-lived credentials for applications. For workloads running on AWS, we use IAM roles and temporary credentials. We separate access by environment and responsibility, use resource-level permissions where possible, and avoid wildcard permissions. For sensitive data we use encryption with KMS and store secrets in Secrets Manager rather than source code or configuration files. For human access, we use centralized identity and MFA, and CloudTrail for auditing. At the organization level, SCPs can provide additional guardrails."

That's a **strong 6-year-level answer**.

---

# 51. IAM Interview Questions You MUST Know

### Basic

1. What is IAM?
2. Authentication vs Authorization?
3. IAM User vs Role?
4. User vs Group?
5. What is IAM Policy?
6. What is ARN?
7. What is MFA?
8. What are access keys?

### Intermediate

9. What is IAM Role?
10. What is AssumeRole?
11. What is STS?
12. Trust policy vs permission policy?
13. Identity-based vs resource-based policy?
14. Managed vs inline policy?
15. Explicit Deny vs Allow?
16. What is least privilege?
17. How do you give EC2 access to S3?

### Advanced

18. How does IAM policy evaluation work?
19. Permission boundary kya hai?
20. SCP kya hai?
21. SCP vs IAM policy?
22. Cross-account access kaise implement karoge?
23. IAM Role vs Access Keys?
24. AccessDenied troubleshoot kaise karoge?
25. Application secret securely kaise store karoge?
26. KMS vs Secrets Manager?
27. IAM Identity Center kya hai?
28. How do you prevent privilege escalation?
29. How do you audit IAM activity?
30. How do you design IAM for multiple AWS accounts?

---

# 52. Sabse important mental model

AWS Security ko is tarah yaad rakho:

```text
                 AWS SECURITY
                      |
       +--------------+--------------+
       |              |              |
     IDENTITY       NETWORK         DATA
       |              |              |
      IAM             SG             KMS
      Role           NACL         Encryption
      Policy         WAF          Secrets
      STS            Firewall
       |
    Access
```

Aur request ka flow:

```text
User/Application
       |
       ↓
Authentication
       |
       ↓
IAM Authorization
       |
       ↓
Network Security
       |
       ↓
Resource Policy
       |
       ↓
Encryption/Key Permission
       |
       ↓
AWS Resource
```

## 🔥 10 things jo pakka yaad karo

```text
1. IAM = Identity + Access
2. Authentication = Who are you?
3. Authorization = What can you do?
4. Role = temporary/assumable access
5. Trust Policy = who can assume role
6. Permission Policy = what role can do
7. Explicit Deny overrides Allow
8. Least privilege = minimum required access
9. SCP limits permissions; it doesn't grant them
10. Production applications → Role, not hardcoded access keys
```

**Next logical topic:** **EC2 + Load Balancer + Auto Scaling**. Ye IAM + Networking ke saath combine karke **real production architecture aur troubleshooting** samajhne mein sabse zyada useful hoga.
========================
=================================
