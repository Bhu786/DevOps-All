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
Networking
=====================
