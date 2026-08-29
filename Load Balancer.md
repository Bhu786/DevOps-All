Bilkul. **Load Balancer (LB)** ko ab surface-level nahi karte. Isko aise cover karte hain ki tum **architecture, Java application integration, AWS configuration, traffic flow, failure scenarios, troubleshooting aur interview cross-questioning** sab explain kar sako.

# AWS LOAD BALANCER — DEEP DIVE / MASTER NOTES

## 0. Sabse pehle: Load Balancer actually karta kya hai?

Simple:

> **Load Balancer incoming client traffic ko multiple healthy backend servers ke beech distribute karta hai.**

Without LB:

```text
1000 Users
    |
    ↓
  EC2-1
```

Problem:

```text
EC2-1
 ↓
Overloaded
 ↓
Application slow/down
```

With LB:

```text
                 1000 Users
                     |
                     ↓
              Load Balancer
              /      |      \
             ↓       ↓       ↓
          EC2-1    EC2-2    EC2-3
```

Traffic distribute hota hai.

But **LB ka kaam sirf traffic distribute karna nahi hai**.

Production mein LB additionally handles things such as:

```text
Traffic distribution
Health checks
Failure detection
TLS termination
Routing
Connection management
High availability
Cross-AZ distribution
Target registration
Access logging
Monitoring
```

---

# 1. AWS mein Load Balancer ke types

AWS Elastic Load Balancing family mein primarily:

```text
                    Elastic Load Balancing
                           |
             +-------------+-------------+
             |             |             |
            ALB           NLB           GWLB
             |
        HTTP/HTTPS
        Layer 7
```

### ALB

**Application Load Balancer**

Layer 7.

Best for:

```text
HTTP
HTTPS
REST API
Microservices
Web applications
```

---

### NLB

**Network Load Balancer**

Layer 4.

Best for:

```text
TCP
UDP
TLS
Very high throughput
Low latency
Static IP requirements
```

---

### GWLB

**Gateway Load Balancer**

Network virtual appliances ke liye.

```text
Firewall
IDS/IPS
Inspection appliance
Security appliance
```

---

# 2. ALB vs NLB — MOST IMPORTANT

|                    | ALB                      | NLB                               |
| ------------------ | ------------------------ | --------------------------------- |
| Layer              | L7                       | L4                                |
| Main protocols     | HTTP/HTTPS               | TCP/UDP/TLS                       |
| Routing            | URL/host/header etc.     | Connection/flow based             |
| HTTP awareness     | Yes                      | Limited at L4                     |
| Path-based routing | Yes                      | No                                |
| Host-based routing | Yes                      | No                                |
| Static IP          | Not the normal ALB model | Yes                               |
| Web apps           | Excellent                | Possible, but usually unnecessary |
| REST APIs          | Excellent                | Possible                          |
| TCP apps           | No                       | Excellent                         |

Memory:

```text
HTTP logic       → ALB
TCP/UDP logic    → NLB
Network appliance → GWLB
```

---

# 3. Very important: Layer 4 vs Layer 7

## Layer 4

Transport layer.

Think:

```text
IP
TCP
UDP
Port
```

Example:

```text
10.0.1.10:443
```

NLB can make decisions based on network/transport information.

---

## Layer 7

Application layer.

Think:

```text
HTTP
HTTPS
URL
Host
Headers
Cookies
```

Example:

```text
GET /booking/123
Host: api.hotel.com
```

ALB understands these HTTP concepts.

---

# 4. ALB Architecture

Suppose:

```text
                    Internet
                       |
                       ↓
                     ALB
                 /          \
                /            \
             AZ-1            AZ-2
              |                |
          Target-1          Target-2
              |                |
             EC2              EC2
```

ALB itself is deployed across multiple Availability Zones through enabled subnets.

---

# 5. ALB — Important Components

ALB architecture ko ye components mein divide karo:

```text
ALB
 |
 +-- Listener
 |
 +-- Listener Rules
 |
 +-- Target Group
 |
 +-- Targets
 |
 +-- Health Checks
 |
 +-- Security Group
 |
 +-- Attributes
 |
 +-- Access Logs
```

Agar ye 8 concepts master hain, ALB ka core samajh aa gaya.

---

# 6. Listener

**Listener waits for incoming traffic on a specific protocol and port.**

Example:

```text
ALB
 |
 +-- HTTPS :443
```

or:

```text
ALB
 |
 +-- HTTP :80
```

Example request:

```text
Client
 |
HTTPS :443
 |
ALB Listener
```

Listener receives the request.

---

# 7. Listener Rule

Listener ke baad ALB decide karta hai:

> **"Ye request kis target group ko bhejni hai?"**

Example:

```text
https://api.hotel.com/booking
                     |
                     ↓
                    ALB
                     |
             Listener :443
                     |
               Rule evaluation
                     |
                     ↓
             Booking Target Group
```

---

# 8. Host-based routing

Example:

```text
api.hotel.com
payment.hotel.com
admin.hotel.com
```

ALB:

```text
api.hotel.com
      ↓
Booking Service

payment.hotel.com
      ↓
Payment Service

admin.hotel.com
      ↓
Admin Service
```

This is **host-based routing**.

---

# 9. Path-based routing

Example:

```text
hotel.com/api/bookings
hotel.com/api/payments
hotel.com/api/customers
```

ALB:

```text
/api/bookings
      ↓
Booking Target Group

/api/payments
      ↓
Payment Target Group

/api/customers
      ↓
Customer Target Group
```

Very common in microservice architectures.

---

# 10. Header-based routing

ALB can also use HTTP headers for routing.

Example concept:

```text
Header:
X-Version: v2
```

Then:

```text
v2
 ↓
Version 2 Target Group
```

Useful for advanced routing/testing scenarios.

---

# 11. Query-string routing

ALB listener rules can also inspect query-string conditions.

Example concept:

```text
/api/search?version=beta
```

could route differently depending on configured conditions.

---

# 12. HTTP method routing

ALB listener rules can use HTTP request method conditions.

Example:

```text
POST
 ↓
Target Group A
```

```text
GET
 ↓
Target Group B
```

Use carefully; usually path/host routing is simpler and more maintainable.

---

# 13. Target Group

Target Group = **backend targets ka logical group**.

Example:

```text
Booking Target Group

+-- EC2-1
+-- EC2-2
+-- EC2-3
```

ALB doesn't simply say:

> "Send to any EC2."

It routes to **target groups**, and target groups contain targets.

---

# 14. Targets

Target can be different types depending on load balancer/target-group configuration.

For ALB commonly:

```text
EC2 instances
IP addresses
Lambda functions
```

ECS tasks can also register as IP targets in common ECS-on-ALB architectures.

---

# 15. Target Group is extremely important

Suppose:

```text
ALB
 |
 +-- Booking TG
 |      |
 |      +-- EC2-1
 |      +-- EC2-2
 |
 +-- Payment TG
        |
        +-- EC2-3
        +-- EC2-4
```

Listener rules determine which target group receives a request.

---

# 16. Health Check

This is one of the **most important LB concepts**.

ALB regularly checks whether targets are healthy.

Example:

```text
ALB
 |
Health Check
 |
GET /actuator/health
 |
EC2
```

If response is healthy:

```text
Healthy ✓
```

If not:

```text
Unhealthy ✗
```

ALB stops routing normal traffic to unhealthy targets.

---

# 17. Health Check is NOT same as application monitoring

Important.

Health check answers:

> "Can I successfully communicate with this target according to my configured health-check criteria?"

Monitoring asks broader questions:

```text
CPU?
Memory?
Latency?
Error rate?
JVM?
Database?
Business metrics?
```

So:

```text
ALB Health Check
≠
Complete application health monitoring
```

---

# 18. Spring Boot example

Suppose:

```text
GET /actuator/health
```

returns:

```json
{
  "status": "UP"
}
```

ALB can use a suitable health endpoint.

But be careful.

If `/actuator/health` returns UP even when an important dependency is broken, ALB may still consider the target healthy.

For critical applications, design health endpoints intentionally.

---

# 19. Health Check parameters

Important concepts:

```text
Protocol
Port
Path
Healthy threshold
Unhealthy threshold
Timeout
Interval
Success codes
```

Example:

```text
Protocol: HTTP
Port: 8080
Path: /actuator/health
```

ALB periodically checks.

---

# 20. Healthy threshold

Suppose:

```text
Healthy threshold = 3
```

Target may need 3 consecutive successful health checks before becoming healthy, depending on configuration/state.

---

# 21. Unhealthy threshold

Suppose:

```text
Unhealthy threshold = 2
```

If target fails enough consecutive checks according to configuration, it becomes unhealthy.

Then:

```text
ALB
 ↓
Stop routing traffic
 ↓
Bad target
```

---

# 22. Traffic flow — FULL ALB

This is the flow you should memorize:

```text
Client
  |
  | HTTPS :443
  ↓
Route 53
  |
  ↓
ALB
  |
  ↓
Listener
  |
  ↓
Listener Rule
  |
  ↓
Target Group
  |
  ↓
Healthy Target
  |
  ↓
Spring Boot Application
```

If you can explain this clearly, you can answer a huge number of LB questions.

---

# 23. DNS and ALB

Normally users don't call:

```text
ALB technical DNS name
```

directly.

Instead:

```text
api.hotel.com
       |
       ↓
Route 53
       |
       ↓
ALB
```

So:

```text
Domain
 ↓
DNS
 ↓
Load Balancer
 ↓
Application
```

---

# 24. ALB does not normally have one fixed public IP

This is a common interview trap.

ALB is accessed through a DNS name.

Its underlying IP addresses can change.

Therefore:

```text
Client
 ↓
DNS
 ↓
ALB
```

is the normal model.

If your requirement specifically needs static IP addresses, **NLB** is the more appropriate AWS LB choice.

---

# 25. Security Group with ALB

Production architecture:

```text
Internet
   |
   ↓
ALB
   |
ALB Security Group
   |
   ↓
App EC2
```

ALB SG:

```text
Inbound:
443 from Internet
```

App SG:

```text
Inbound:
8080 from ALB Security Group
```

Not:

```text
8080 from 0.0.0.0/0
```

This is a very good security practice.

---

# 26. ALB Security Group — Real Example

```text
ALB-SG

Inbound:
443 → 0.0.0.0/0
```

Application:

```text
APP-SG

Inbound:
8080 → ALB-SG
```

Database:

```text
DB-SG

Inbound:
5432 → APP-SG
```

So:

```text
Internet
   ↓ 443
ALB
   ↓ 8080
App
   ↓ 5432
DB
```

This creates controlled network layers.

---

# 27. ALB + Private EC2

Very common architecture:

```text
             Internet
                 |
                 ↓
             Public ALB
              /     \
             /       \
       Private EC2  Private EC2
             \       /
              \     /
              Database
```

The application servers don't need public IPs.

This is one of the biggest reasons to use an ALB.

---

# 28. TLS Termination

Very important.

Client sends:

```text
HTTPS
 |
ALB
```

ALB decrypts the TLS connection.

Then ALB can forward to backend:

```text
ALB
 |
HTTP :8080
 |
App
```

This is called:

> **TLS termination at the load balancer.**

Or you can configure HTTPS from ALB to backend as well.

---

# 29. HTTPS end-to-end

More secure architecture:

```text
Client
 |
HTTPS
 |
ALB
 |
HTTPS
 |
Application
```

Now traffic remains encrypted on both legs.

Whether you use HTTP or HTTPS between ALB and targets depends on security requirements and architecture.

---

# 30. TLS Certificate

ALB commonly integrates with **AWS Certificate Manager (ACM)**.

Concept:

```text
Client
  |
HTTPS
  |
ALB
  |
ACM Certificate
```

Certificate handles TLS identity for the domain.

---

# 31. Redirect HTTP → HTTPS

Common listener setup:

```text
Port 80
   |
   ↓
Redirect
   |
   ↓
HTTPS :443
```

So:

```text
http://hotel.com
       ↓
https://hotel.com
```

---

# 32. Connection termination

ALB can terminate the client connection and establish a separate connection to the target.

Conceptually:

```text
Client
   |
Connection A
   |
  ALB
   |
Connection B
   |
Target
```

This is important for understanding TLS termination and connection management.

---

# 33. Sticky Sessions

Normally ALB can distribute requests across healthy targets.

Example:

```text
User
 |
ALB
 |
 +-- Request 1 → EC2-1
 +-- Request 2 → EC2-2
 +-- Request 3 → EC2-3
```

But sometimes application wants the same client to continue going to the same target.

That's **session stickiness**.

```text
User A
  |
  ↓
EC2-1

User A again
  |
  ↓
EC2-1
```

---

# 34. Should you use sticky sessions?

In modern scalable applications:

**Prefer stateless applications when possible.**

Instead of:

```text
EC2-1
 |
Session
```

use:

```text
Application
 |
Shared session store / token-based state
```

Then any healthy instance can handle the request.

For Spring applications, distributed session storage or token-based authentication can help avoid instance-local session dependency.

---

# 35. Why sticky sessions can be problematic

Suppose:

```text
EC2-1
 ↓
User session
```

Then EC2-1 dies.

User may get:

```text
EC2-2
```

and session could be missing if it lived only on EC2-1.

Therefore:

```text
Stateless
 ↓
Better scaling
 ↓
Better failure tolerance
```

---

# 36. Cross-Zone Load Balancing

Suppose:

```text
AZ-1
EC2-1
EC2-2

AZ-2
EC2-3
```

ALB distributes traffic across enabled AZs/targets according to its load-balancing behavior and target configuration.

For architecture discussions, the key principle is:

> Deploy targets across multiple AZs and ensure the load-balancer/target setup supports resilient distribution.

---

# 37. Why multiple AZs?

If:

```text
AZ-1
 ↓
All applications
```

and AZ-1 fails:

```text
Application
 ↓
DOWN
```

Better:

```text
AZ-1            AZ-2
App-1           App-2
App-3           App-4
  \              /
   \            /
      ALB
```

One AZ fails:

```text
AZ-1 ❌

AZ-2 ✓
```

Application can continue serving traffic if capacity and dependencies remain healthy.

---

# 38. ALB + Auto Scaling

This is one of the most important production combinations.

```text
                 ALB
              /       \
             /         \
          EC2-1       EC2-2
             \         /
              Auto Scaling
```

Suppose traffic increases:

```text
100 users
 ↓
2 instances
```

Traffic increases:

```text
10,000 users
 ↓
Auto Scaling launches
EC2-3
EC2-4
```

They become registered/healthy targets, and ALB can route traffic to them.

---

# 39. Important: ALB doesn't create EC2 instances

Common confusion.

```text
ALB
→ distributes traffic

Auto Scaling
→ changes number of instances

EC2
→ runs application
```

They work together but have different responsibilities.

---

# 40. ALB + Auto Scaling full flow

```text
                    Users
                      |
                      ↓
                    ALB
                      |
              Target Group
              /     |      \
             ↓      ↓       ↓
           EC2-1  EC2-2   EC2-3
                      ↑
                      |
                 Auto Scaling
                      |
              CPU / traffic metrics
```

---

# 41. Scale-out scenario

Traffic increases:

```text
CPU = 80%
```

Auto Scaling decides:

```text
Launch EC2-3
```

Then:

```text
EC2-3
 ↓
Target Group
 ↓
Health Check
 ↓
Healthy
 ↓
ALB starts routing traffic
```

**Important:** Instance should be healthy/registered before receiving normal traffic.

---

# 42. Scale-in scenario

Traffic decreases:

```text
CPU = 20%
```

Auto Scaling may terminate one instance.

The target is removed/drained according to termination/connection-draining behavior before termination completes.

---

# 43. Connection Draining / Deregistration Delay

Very important.

Suppose:

```text
EC2-2
```

needs to be removed.

Existing request:

```text
User
 |
ALB
 |
EC2-2
 |
Long-running request
```

If EC2 is immediately killed:

```text
Request
 ↓
FAILED
```

Instead, deregistration/connection draining gives existing connections time to finish while new requests stop going to the target.

---

# 44. Slow application and ALB

Suppose:

```text
ALB
 |
EC2-1 → slow
EC2-2 → healthy
EC2-3 → healthy
```

Health check may still show EC2-1 healthy if it responds successfully.

So ALB may continue sending traffic to a technically healthy but overloaded/slow application.

Therefore:

```text
Health ≠ Performance
```

This is where CloudWatch application metrics matter.

---

# 45. 502 Bad Gateway

Very important troubleshooting.

ALB may return **502** when it cannot successfully get a valid response from the target or there is an issue in the target connection/response.

Possible causes include:

```text
Application crashed
Target connection failure
Backend closed connection unexpectedly
Protocol mismatch
Bad response
```

Don't automatically blame ALB.

---

# 46. 503 Service Unavailable

Often means ALB has no suitable healthy targets available for the request.

Example:

```text
Target Group

EC2-1 ❌
EC2-2 ❌
EC2-3 ❌
```

Then:

```text
ALB
 ↓
503
```

Check target health first.

---

# 47. 504 Gateway Timeout

Important.

ALB waited for the target but did not receive the expected response within the relevant timeout.

Example:

```text
Client
 ↓
ALB
 ↓
Java application
 ↓
DB query taking too long
```

Then:

```text
ALB
 ↓
504
```

Potential causes:

```text
Slow application
Slow DB
Downstream API
Network issue
Connection timeout
Thread pool exhaustion
```

---

# 48. 4xx vs 5xx

Simple mental model:

```text
4xx
→ request/client side issue

5xx
→ server/upstream/service side issue
```

But exact interpretation depends on where the response originated.

---

# 49. ALB Logs

ALB access logs are extremely useful.

You can investigate:

```text
Request
Client IP
URL
Status
Target response
Latency
```

Useful when:

```text
Users complain:
"API is slow"
```

You can inspect:

```text
Request latency
Target processing time
Response code
```

Then determine whether delay is at LB/target/application level.

---

# 50. ALB metrics

CloudWatch metrics are extremely important.

Common concepts:

```text
RequestCount
TargetResponseTime
HTTPCode_ELB_4XX_Count
HTTPCode_ELB_5XX_Count
HTTPCode_Target_4XX_Count
HTTPCode_Target_5XX_Count
HealthyHostCount
UnHealthyHostCount
RejectedConnectionCount
```

The exact metric set varies by LB/type and AWS feature.

---

# 51. VERY IMPORTANT — ELB 5xx vs Target 5xx

Suppose:

```text
ALB → Target
```

There are different places where a 5xx can originate.

Conceptually:

```text
ELB 5xx
→ Load balancer side

Target 5xx
→ Backend application side
```

Example:

```text
Java returns HTTP 500
       ↓
Target 5xx
```

Whereas a load-balancer-generated error may appear in ELB-side metrics.

This distinction is **very useful in production troubleshooting**.

---

# 52. TargetResponseTime

Suppose:

```text
TargetResponseTime = 4 seconds
```

Application is slow.

Break it down:

```text
ALB
 ↓
Java
 ↓
DB
 ↓
External API
```

You then investigate application and dependency latency.

---

# 53. Real Troubleshooting Scenario #1

## "Users are getting 503 from ALB."

Senior approach:

```text
1. Check Target Group.
       ↓
2. Check HealthyHostCount.
       ↓
3. Check UnHealthyHostCount.
       ↓
4. Check individual target health reason.
       ↓
5. Test health endpoint directly.
       ↓
6. Check application logs.
       ↓
7. Check Security Group.
       ↓
8. Check NACL / routing if relevant.
       ↓
9. Check target port.
       ↓
10. Check deployment/recent changes.
```

Possible root cause:

```text
ALB health check
GET /actuator/health
```

but application exposes:

```text
/health
```

Therefore:

```text
Health check → 404
Target → unhealthy
All targets → unhealthy
ALB → 503
```

Very realistic interview scenario.

---

# 54. Real Troubleshooting Scenario #2

## "ALB health check is failing."

Check:

```text
ALB
 |
Health Check Port
 |
Health Check Path
 |
Security Group
 |
NACL
 |
Application port
 |
Application endpoint
```

Example:

```text
ALB checks:
8080 /actuator/health

App actually listens:
8081
```

Result:

```text
Health check failure
```

---

# 55. Real Troubleshooting Scenario #3

## "Application works directly but fails through ALB."

This is an excellent interview question.

Direct:

```text
EC2:8080
 ↓
Works
```

Through ALB:

```text
Client
 ↓
ALB
 ↓
EC2
 ↓
Fails
```

Check:

```text
ALB listener
↓
Listener rule
↓
Target group
↓
Target port
↓
Security Group
↓
Health check
↓
Application host/header assumptions
↓
TLS/protocol
```

Most importantly:

```text
EC2 SG should allow traffic from ALB SG
```

not necessarily the whole internet.

---

# 56. Real Troubleshooting Scenario #4

## "One instance is slow but others are fine."

Architecture:

```text
ALB
 |
 +-- EC2-1 → 100ms
 +-- EC2-2 → 100ms
 +-- EC2-3 → 8sec ❌
```

Check:

```text
TargetResponseTime
EC2 CPU
Memory
JVM
GC
Thread pool
DB connections
Network
Application logs
```

Health check might still be:

```text
Healthy ✓
```

So ALB continues using it.

This shows:

> **Load balancer health checks don't replace application performance monitoring.**

---

# 57. Real Troubleshooting Scenario #5

## "After deployment, ALB shows 503."

Likely flow:

```text
Deployment
 ↓
New application version
 ↓
Application startup failure
 ↓
Health check fails
 ↓
Targets unhealthy
 ↓
ALB 503
```

Check:

```text
Deployment logs
Application startup logs
Health endpoint
Target health
Environment variables
Secrets
Database connectivity
Port
```

This is a very common production incident pattern.

---

# 58. Blue-Green Deployment with ALB

Very useful for senior interviews.

Suppose:

```text
ALB
 |
 +-- Blue TG → v1
 |
 +-- Green TG → v2
```

Initially:

```text
100%
 ↓
Blue
```

Test Green:

```text
Green
 ↓
Health check
 ↓
Smoke test
```

Then switch routing:

```text
100%
 ↓
Green
```

If problem:

```text
100%
 ↓
Blue
```

This gives quick rollback.

---

# 59. Canary Deployment with ALB

Concept:

```text
ALB
 |
 +-- 95% → v1
 |
 +-- 5%  → v2
```

Test new version with small traffic.

Monitor:

```text
Errors
Latency
Business metrics
```

Then increase gradually.

Important nuance: exact weighted-routing behavior depends on how you're implementing the deployment/routing mechanism; ALB target-group weighting can be used for controlled traffic distribution, but deployment tooling and failure semantics should be understood separately.

---

# 60. Microservices + ALB

This is probably most relevant to your Java experience.

Architecture:

```text
                    ALB
                     |
        +------------+------------+
        |            |            |
        ↓            ↓            ↓
    /booking      /payment     /customer
        |            |            |
 Booking TG      Payment TG   Customer TG
        |            |            |
       EC2          EC2          EC2
```

Spring Boot:

```text
Booking Service
Payment Service
Customer Service
```

ALB provides routing.

---

# 61. Path routing example

```text
/api/bookings/**
        ↓
Booking Service

/api/payments/**
        ↓
Payment Service

/api/customers/**
        ↓
Customer Service
```

This allows a single public endpoint:

```text
api.hotel.com
```

while internally routing to multiple services.

---

# 62. One ALB vs Multiple ALBs

### One ALB

```text
ALB
 |
 +-- Booking
 +-- Payment
 +-- Customer
```

Pros:

* Less infrastructure
* Centralized routing
* Lower cost

Cons:

* Shared blast radius
* More complex rules
* Potential scaling/organizational concerns

### Multiple ALBs

```text
Booking → ALB
Payment → ALB
Admin → ALB
```

Pros:

* Isolation
* Independent ownership
* Different security requirements

Cons:

* More cost
* More operational complexity

---

# 63. ALB + WAF

Production web architecture:

```text
Internet
   |
   ↓
AWS WAF
   |
   ↓
ALB
   |
   ↓
Application
```

WAF protects web requests.

ALB distributes them.

Different responsibilities:

```text
WAF
→ security filtering

ALB
→ traffic routing/distribution
```

---

# 64. ALB + CloudFront

Common architecture:

```text
User
 |
CloudFront
 |
WAF
 |
ALB
 |
Application
```

CloudFront:

```text
CDN/cache/global delivery
```

ALB:

```text
regional application load balancing
```

Don't confuse them.

---

# 65. ALB + Route 53 + CloudFront

Full internet-facing architecture:

```text
User
 |
Route 53
 |
CloudFront
 |
WAF
 |
ALB
 |
Target Group
 |
EC2/ECS
```

Each layer has a different job.

---

# 66. NLB Deep Dive

Now NLB.

NLB is Layer 4.

```text
Client
 |
TCP/UDP/TLS
 |
NLB
 |
Target
```

It doesn't operate like ALB's HTTP routing engine.

---

# 67. Why use NLB?

Use when requirements include:

```text
TCP
UDP
TLS pass-through/termination scenarios
Very high throughput
Very low latency
Static IP / Elastic IP requirements
PrivateLink endpoint services
```

---

# 68. NLB Target Types

Depending on configuration, NLB can target:

```text
Instance
IP
ALB
```

This is useful in architectures where L4 networking is needed in front of an ALB or other target.

---

# 69. NLB + ALB

Interesting architecture:

```text
Internet
   |
  NLB
   |
  ALB
   |
Application
```

Why?

NLB can provide capabilities such as static IP/network-level entry while ALB handles HTTP-aware routing.

This can be useful for specific architectures, but don't add it without a requirement—it increases complexity.

---

# 70. GWLB Deep Dive

Gateway Load Balancer:

```text
Traffic
   |
GWLB
   |
Firewall Appliance
   |
Application
```

It's designed for scaling and integrating virtual network/security appliances.

Examples:

```text
Firewall
IDS
IPS
Deep packet inspection
```

---

# 71. Load Balancer + Security Groups

Remember the layers:

```text
Internet
   |
WAF
   |
ALB SG
   |
ALB
   |
App SG
   |
EC2
```

The App SG should ideally reference the ALB SG as the source.

This means:

> "Only traffic coming through the ALB security group can access my application port."

---

# 72. Load Balancer + NACL

NACL is subnet level.

If ALB subnet or application subnet NACL blocks traffic:

```text
ALB
 ↓
NACL
 ↓
X
 ↓
EC2
```

Even if:

```text
Security Group ✓
```

the request can still fail.

Therefore troubleshooting:

```text
Route
+
SG
+
NACL
```

all matter.

---

# 73. Load Balancer + Private Subnet

Important architecture.

```text
              Internet
                  |
                  ↓
              Public ALB
              /       \
             /         \
       Private Subnet
        EC2          EC2
             \       /
              Private DB
```

Application servers don't need public IP addresses.

This is a standard security pattern.

---

# 74. Internal ALB

Not every ALB must be internet-facing.

You can have:

```text
Public ALB
```

and:

```text
Internal ALB
```

Internal ALB:

```text
VPC
 |
Internal ALB
 |
Private services
```

Useful for internal microservice communication.

---

# 75. Internet-facing vs Internal

| Internet-facing ALB         | Internal ALB                    |
| --------------------------- | ------------------------------- |
| Public clients              | Internal clients                |
| Public DNS/access path      | Private VPC networking          |
| Public-facing entry point   | Internal service entry point    |
| Often behind CloudFront/WAF | Often behind private networking |

---

# 76. Connection limits — practical thinking

Don't memorize random limits.

Think:

```text
Traffic
 ↓
ALB
 ↓
Targets
```

Performance depends on:

```text
Requests/sec
Connections
Payload size
TLS
Target capacity
Application latency
Network
```

If application is slow:

```text
Adding ALB
```

may not solve it.

You need to identify the bottleneck.

---

# 77. Load Balancer does NOT solve everything

Common misconception:

> "If application is slow, increase load balancer."

No.

If:

```text
Java
 ↓
DB
 ↓
Slow query
```

then:

```text
ALB
```

won't fix the database bottleneck.

Similarly:

```text
External API
 ↓
10 second latency
```

ALB won't magically make it fast.

---

# 78. LB and Stateless Architecture

Best architecture:

```text
             ALB
          /   |   \
        App  App  App
          \   |   /
        Shared services
```

Any request can go to any healthy instance.

Avoid:

```text
User → fixed EC2
```

unless there is a strong reason.

---

# 79. Real Java Spring Boot architecture

```text
                  Browser
                     |
                     ↓
                Route 53
                     |
                     ↓
                 CloudFront
                     |
                     ↓
                    WAF
                     |
                     ↓
                    ALB
                     |
              HTTPS Listener
                     |
              Path-based Rules
                     |
        +------------+-------------+
        |            |             |
        ↓            ↓             ↓
     Booking       Payment      Customer
        TG            TG            TG
        |             |             |
      EC2/ECS       EC2/ECS       EC2/ECS
        |             |             |
        +-------------+-------------+
                      |
                    RDS
```

This is an excellent architecture to discuss in a Java Full Stack interview.

---

# 80. Request flow — explain like a 6-year developer

Interviewer:

> "Explain request flow in your AWS application."

Answer:

> "The client resolves our application domain through Route 53. For a public application, traffic can go through CloudFront and WAF before reaching the Application Load Balancer. The ALB listener accepts HTTPS traffic, terminates TLS where configured, evaluates listener rules such as host or path conditions, and forwards the request to the appropriate target group. The target group contains healthy application instances or tasks. The ALB performs health checks and removes unhealthy targets from normal routing. Our application instances are in private subnets, and security groups allow application traffic only from the ALB security group."

That's a strong architecture answer.

---

# 81. Most important interview question

### "How does ALB know which server to send traffic to?"

Answer:

```text
Listener
 ↓
Listener Rule
 ↓
Target Group
 ↓
Healthy Targets
 ↓
ALB load-balancing algorithm
```

Not:

> "ALB randomly selects EC2."

---

# 82. Most important question

### "What happens if one EC2 goes down?"

```text
EC2 fails
   ↓
Health check fails
   ↓
Target becomes unhealthy
   ↓
ALB stops routing new traffic
   ↓
Other healthy targets handle traffic
```

Then:

```text
Auto Scaling
 ↓
May launch replacement
 ↓
New target registers
 ↓
Health check passes
 ↓
Traffic starts flowing
```

---

# 83. Most important question

### "What happens if all targets become unhealthy?"

```text
All targets
   ↓
Unhealthy
   ↓
No healthy target
   ↓
ALB cannot successfully route
   ↓
Likely 503
```

Investigate target health immediately.

---

# 84. Most important question

### "ALB vs API Gateway?"

Very common.

### ALB

```text
Load balancing
HTTP routing
Backend targets
```

### API Gateway

```text
API management
Authentication/authorization integrations
Throttling
API lifecycle features
Serverless/API front door
```

They can coexist.

---

# 85. ALB vs CloudFront

```text
CloudFront
→ CDN / caching / edge delivery

ALB
→ distribute requests across backend targets
```

Architecture:

```text
User
 ↓
CloudFront
 ↓
ALB
 ↓
Application
```

---

# 86. ALB vs Route 53

```text
Route 53
→ DNS

ALB
→ traffic distribution
```

Flow:

```text
api.hotel.com
 ↓
Route 53
 ↓
ALB
 ↓
App
```

---

# 87. ALB vs Auto Scaling

```text
ALB
→ distributes traffic

Auto Scaling
→ changes number of instances
```

Together:

```text
Traffic
 ↓
ALB
 ↓
EC2
 ↑
Auto Scaling
```

---

# 88. Golden Troubleshooting Flow

Tumhare previous SRE troubleshooting flow ke style mein LB ke liye ye yaad karo:

```text
CONFIRM
   ↓
RECENT CHANGES
   ↓
DNS
   ↓
LOAD BALANCER
   ↓
LISTENER
   ↓
RULE
   ↓
TARGET GROUP
   ↓
TARGET HEALTH
   ↓
SECURITY GROUP
   ↓
NACL / ROUTE
   ↓
APPLICATION
   ↓
DEPENDENCIES
   ↓
LOGS
   ↓
METRICS
   ↓
TRACE
   ↓
ROOT CAUSE
   ↓
FIX
   ↓
PREVENT
```

---

# 89. LB Troubleshooting Matrix

| Symptom                     | First things to check                                |
| --------------------------- | ---------------------------------------------------- |
| **503**                     | Target health / no healthy targets                   |
| **502**                     | Target connection/response/protocol/application      |
| **504**                     | Target response timeout / slow dependency            |
| Health check failed         | Path, port, SG, NACL, application                    |
| One target slow             | TargetResponseTime, CPU, JVM, DB                     |
| All targets unhealthy       | Deployment, app startup, health endpoint, networking |
| ALB unreachable             | DNS, listener, SG, subnet/routing                    |
| HTTPS problem               | Listener, certificate, TLS config                    |
| HTTP works, HTTPS fails     | 443 listener/certificate/SG                          |
| Direct EC2 works, ALB fails | Target port, SG from ALB, listener/rules             |
| New deployment fails        | Registration + health check + startup                |
| Random application failures | Target-specific health/performance                   |

---

# 90. 🔥 20 Questions You Should Be Able to Answer

After mastering this, you should be comfortable with:

1. What is a Load Balancer?
2. Why do we need it?
3. ALB vs NLB?
4. L4 vs L7?
5. What is a listener?
6. What is a listener rule?
7. What is a target group?
8. What is a target?
9. How does health checking work?
10. What happens when a target becomes unhealthy?
11. What is sticky session?
12. Why prefer stateless applications?
13. What is TLS termination?
14. ALB vs CloudFront?
15. ALB vs Route 53?
16. ALB vs API Gateway?
17. ALB + Auto Scaling kaise work karte hain?
18. Why put EC2 in private subnet behind ALB?
19. 502 vs 503 vs 504?
20. How do you troubleshoot ALB issues?

---

# 91. 🔥 ADVANCED QUESTIONS — 6 YEAR LEVEL

Ye especially prepare karo:

### Q1. One target is unhealthy. Others are healthy. What will you do?

```text
Target health reason
 ↓
Health endpoint
 ↓
Port
 ↓
SG
 ↓
NACL
 ↓
Application logs
 ↓
Recent deployment
```

---

### Q2. Health check is successful but users get 500.

Answer:

> "The target can be healthy from the load balancer's health-check perspective while the application can still return business or server errors. I'd distinguish target health from application error metrics and inspect target 5xx metrics, application logs and traces."

Excellent answer.

---

### Q3. ALB returns 504.

Think:

```text
ALB
 ↓
Target
 ↓
Application
 ↓
DB / external service
```

Find where latency is introduced.

---

### Q4. Application is working but ALB gives 503.

Check:

```text
Target Group
 ↓
Target registration
 ↓
Health check
 ↓
HealthyHostCount
 ↓
Security Group
 ↓
Port
```

---

### Q5. How do you achieve zero-downtime deployment?

One common approach:

```text
ALB
 ↓
Target Group
 ↓
Existing healthy instances

Deploy new version
 ↓
New instances
 ↓
Health checks
 ↓
Healthy
 ↓
Traffic shift
 ↓
Old instances drained
 ↓
Terminate old
```

Can be combined with:

```text
Blue-Green
Canary
Rolling deployment
```

---

# 92. The MASTER Mental Model

Don't memorize 50 isolated points.

Understand this:

```text
                         USER
                           |
                           ↓
                        DNS
                       Route53
                           |
                           ↓
                     CloudFront
                           |
                           ↓
                          WAF
                           |
                           ↓
                          ALB
                           |
                  +--------+--------+
                  |                 |
              Listener          Listener
                 :80               :443
                  |                 |
                  +--------+--------+
                           |
                    Listener Rules
                           |
              +------------+------------+
              |            |            |
              ↓            ↓            ↓
          Booking TG   Payment TG   Customer TG
              |            |            |
          Healthy       Healthy      Healthy
           Targets       Targets       Targets
              |            |            |
              ↓            ↓            ↓
           Spring       Spring       Spring
             Boot         Boot         Boot
              |            |            |
              +------------+------------+
                           |
                          DB
```

And security:

```text
Internet
   ↓
WAF
   ↓
ALB-SG
   ↓
ALB
   ↓
APP-SG
   ↓
EC2/ECS
   ↓
DB-SG
   ↓
RDS
```

And scalability:

```text
              ALB
               |
       +-------+-------+
       |       |       |
      App     App     App
       ↑       ↑       ↑
       +-------+-------+
               |
          Auto Scaling
```

And failure:

```text
App-1 ❌
   ↓
Health check fails
   ↓
ALB removes from routing
   ↓
App-2 / App-3 serve traffic
   ↓
Auto Scaling replaces App-1
   ↓
Health check passes
   ↓
New instance receives traffic
```

---

# 🧠 FINAL MEMORY FORMULA

**ALB ko ye sequence mein yaad karo:**

```text
DNS
 ↓
ALB
 ↓
Listener
 ↓
Rule
 ↓
Target Group
 ↓
Health Check
 ↓
Healthy Target
 ↓
Application
```

Aur production mein:

```text
Route 53
 ↓
CloudFront
 ↓
WAF
 ↓
ALB
 ↓
Private App
 ↓
Database
```

**ALB = traffic distribution + HTTP routing + health-based target selection + TLS termination (when configured).**

**NLB = L4 high-performance/network traffic + static IP-oriented use cases.**

**GWLB = network/security appliances.**

Agar tum is topic ko **master** karna chahte ho, next level par sabse useful exercise hoga: **"ALB ke 20 real production incidents — symptom → metrics/logs → exact investigation → root cause → fix"**. Isse theory actual **6-year DevOps/Java production interview answers** mein convert hogi.
