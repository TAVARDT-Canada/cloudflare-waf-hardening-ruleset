# Cloudflare WAF Hardening Ruleset & Edge Security Blueprint

[![Licence MIT](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)
[![Cloudflare WAF](https://img.shields.io/badge/Cloudflare-WAF%20Hardened-F38020.svg?logo=cloudflare)](https://cloudflare.com)
[![Language](https://img.shields.io/badge/Language-English%20(Canada)-green.svg)](README.md)
[![Diagnostics Suite](https://img.shields.io/badge/TAVARDT-Diagnostics-5b3cf5.svg)](https://tools.tavardt.com/ca/security-headers-check/)

Production-grade Cloudflare WAF custom ruleset and edge security blueprint aligned with PIPEDA requirements and CCCS baseline cyber security controls.

Engineered and maintained by the cybersecurity engineering group at **TAVARDT**.

> [!IMPORTANT]
> **Universal & Stack-Agnostic Architecture:** This repository is **not restricted to WordPress**. It is designed to safeguard **REST APIs, microservices, modern web apps (Next.js, React), and backend workloads (Node.js, Python, Go, PHP, Java)**. Blocking legacy CMS probes functions as an **active edge hygiene layer**, neutralizing automated reconnaissance and botnet scans at the Cloudflare edge (< 1ms) without taxing your origin compute.

***

### Multi-Stack Defense Matrix

| Defense Layer | Mitigated Vectors | Protected Environments & Stacks |
| :- | :- | :- |
| **Secret & Config Isolation** | Edge block on `.env`, `.git`, `.sql`, `package.json`, `composer.json` | **APIs, Next.js, Node.js, Python, Go, Laravel, React** |
| **Exploit Scanner Mitigation** | Block automated scanners (Nikto, SQLMap, Acunetix, Masscan, Nmap) | **Any production web service, microservice, or API** |
| **HTTP Verb Filtering** | Dropping dangerous diagnostic verbs (`TRACE`, `TRACK`, `DEBUG`) | **RESTful APIs and production backends** |
| **Privileged Route Gating** | Managed challenges protecting administration paths (`/admin`, `/login`) | **Administrative consoles, cloud dashboards, portals** |
| **Zero-Noise Edge Hygiene** | Dropping blind probes on `/xmlrpc.php` and amplification vectors | **Protection of origin CPU, memory, and TCP connections** |

***

## 1. Edge Security Architecture

This repository delivers hardened, production-tested Cloudflare edge firewall rules designed to prevent credential leaks, brute force attempts, and exposure of corporate assets:

* **Sensitive Asset & Environment Protection:** Absolute perimeter restriction for `.env` secrets, `.git` metadata directories, `.sql` database dumps, and application configurations (`composer.json`, `package.json`).
* **Automated Exploit Scanner Mitigation:** Real-time edge suppression of automated penetration scanners (Nikto, SQLMap, Acunetix, Masscan, Nmap, Gobuster, DirBuster).
* **CMS Perimeter Shielding:** Instant blocking of persistent attack targets like `/xmlrpc.php` and `/wp-trackback.php`.
* **HTTP Method Sanitisation:** Perimeter filtering of unsafe debugging methods (`TRACE`, `TRACK`, `DEBUG`).
* **Managed Challenges for Privileged Routes:** Adaptive challenge mechanics protecting administrative consoles (`/wp-login.php`, `/admin`).

***

## 2. Pre-Deployment Diagnostic Suite

Validate your domain's transport layer security and HTTP headers before deploying edge configuration rules in production:

* **Security Headers & SSL Diagnostic:** **TAVARDT Security Headers Audit**
* **Full Engineering Tools Suite:** **TAVARDT Tools Canada**

***

## 3. Deployment Instructions

### Option A: Ingestion via Cloudflare API v4

Deploy the ruleset directly using [`rules/ruleset.json`](rules/ruleset.json):

```bash
curl -X PUT "https://api.cloudflare.com/client/v4/zones/YOUR_ZONE_ID/rulesets/phases/http_request_firewall_custom/entrypoint" \
     -H "Authorization: Bearer YOUR_CLOUDFLARE_API_TOKEN" \
     -H "Content-Type: application/json" \
     -data @rules/ruleset.json
```

### Option B: Infrastructure-as-Code via Terraform

Use the declarative Terraform definition located in [`terraform/main.tf`](terraform/main.tf):

```bash
cd terraform
terraform init
terraform plan -var="zone_id=YOUR_ZONE_ID"
terraform apply -var="zone_id=YOUR_ZONE_ID"
```

***

## 4. Professional Advisory & Technical Support

Should your enterprise require in-depth security assessments, PIPEDA compliance validation, or autonomous agent hardening:

* **Corporate Portal:** **TAVARDT**
* **Technical Contact:** [Connect with Engineering](https://ag.tavardt.com/ca/contact/)

***

## Useful Links

* **Corporate Portal:** https://ag.tavardt.com/ca/
* **Diagnostic Suite:** https://tools.tavardt.com/ca/
* **Technical Contact:** https://ag.tavardt.com/ca/contact/

***

## Licence

Distributed under the open-source MIT Licence. Refer to the [`LICENSE`](LICENSE) file for more information.  
Copyright

***

© 2026 TAVARDT. All rights reserved.
