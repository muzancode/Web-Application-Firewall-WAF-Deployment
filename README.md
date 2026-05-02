# WEB APPLICATION FIREWALL (WAF) DEPLOYMENT

**Author:** Muzan Abbas

A web application security lab built to study how web-based attacks are detected, analyzed, and mitigated using a modern Web Application Firewall (WAF). Simulated real attacker behavior against a vulnerable application and evaluated WAF effectiveness through rule tuning and defensive controls.

---

## Lab Architecture

```
┌─────────────────┐        ┌─────────────────┐        ┌─────────────────┐
│   Attacker VM   │──────▶│       WAF        │──────▶│  App Server     │
│   Kali Linux    │  HTTP  │  Reverse Proxy   │  HTTP  │  Ubuntu (LAMP)  │
│                 │        │  TLS Termination │        │  DVWA           │
└─────────────────┘        └─────────────────┘        └─────────────────┘
```

All systems isolated in a controlled lab environment on the same network.

---

## Objectives

- Understand how WAFs inspect, classify, and block malicious HTTP traffic
- Study attacker behavior against vulnerable web applications
- Evaluate the effectiveness of automated and custom WAF rules
- Gain hands-on experience with secure server deployment, TLS, and traffic inspection
- Develop documentation and analysis skills relevant to security research

---

## Part 1 – Lab Environment

| Component | Details |
|---|---|
| Attacker VM | Kali Linux |
| Application Server | Ubuntu Server (LAMP stack) |
| Vulnerable App | Damn Vulnerable Web Application (DVWA) |
| Security Layer | WAF deployed as reverse proxy |
| Network | Isolated lab network |

---

## Part 2 – Vulnerable Application Deployment

A deliberately vulnerable web application (DVWA) was deployed on the Ubuntu server running Apache, PHP, and MySQL. The application was intentionally misconfigured to expose common vulnerabilities such as SQL injection, providing a realistic attack surface for controlled testing.

Custom data was added to the backend database to simulate realistic application content and improve attack visibility during testing.

---

## Part 3 – Network, DNS, and TLS Configuration

- Application moved to a non-default port to simulate production routing
- Local DNS configured for hostname-based access and realistic WAF policy enforcement
- Self-signed SSL certificate generated and deployed to enable HTTPS inspection
- All traffic routed through the WAF — no direct backend access during testing

---

## Part 4 – WAF Deployment

The WAF was deployed in **reverse-proxy mode** in front of the vulnerable application.

**WAF Responsibilities:**
- Terminate TLS connections
- Inspect inbound HTTP requests
- Apply security rules before forwarding to backend
- Log and block malicious behavior

---

## Part 5 – Attacks Performed

| Attack Type | Description |
|---|---|
| SQL Injection | Malicious payloads injected into application input fields |
| Authentication Abuse | Repeated login attempts and credential manipulation |
| HTTP Flood | High-frequency requests simulating volumetric abuse |

These attacks reflect common techniques used in real-world web exploitation scenarios.

---

## Part 6 – WAF Detection and Telemetry

During attack execution, the WAF:
- Identified malicious payloads in HTTP requests
- Blocked requests matching known attack signatures
- Logged detailed information including attack type, source IP, and rule triggered

> **Key Insight:** Effective web defense relies on traffic behavior and context, not just static signatures. Even simple attacks generated rich metadata usable for monitoring and alerting.

---

## Part 7 – Advanced Defensive Configurations

### HTTP Flood Defense
Rate-limiting and flood protection mechanisms were configured and validated by generating bursts of requests from the attacker system.

### Authentication Gatekeeping
An authentication layer was applied at the WAF level to restrict backend access independently of application logic.

### Custom Deny Rules
Custom rules were created to block traffic from specific sources, demonstrating fine-grained policy control and active enforcement.

---

## Part 8 – Challenges and Troubleshooting

| Challenge | Resolution |
|---|---|
| Reverse proxy misconfiguration | Debugged backend routing and proxy pass settings |
| TLS certificate trust issues | Configured certificate properly on WAF and client |
| DNS resolution inconsistencies | Set up local `/etc/hosts` entries across all VMs |
| WAF blocks vs application errors | Reviewed WAF logs to differentiate block types |

---

## Key Takeaways

- WAFs provide critical visibility into application-layer attacks
- Secure deployment requires careful coordination between networking, TLS, and application configuration
- Behavior-based detection and policy tuning are essential for effective defense
- Hands-on experimentation is invaluable for understanding how defensive systems operate in practice
