# Lingo Leap - Secure Education Platform Architecture

**Live Deployment:** [https://lingo-leap.net](https://lingo-leap.net)

A high-performance, security-hardened web platform designed for a boutique language academy. This repository documents the architectural evolution of the platform: transitioning from a statically generated, monolithic-hosted site into a dynamic, AI-powered serverless edge application.

This project demonstrates a rigorous Defense-in-Depth approach to infrastructure, CI/CD pipeline troubleshooting, and advanced DNS management suitable for enterprise deployments.

## 🏗️ Current Technical Architecture (Phase 2)

* **Frontend:** Astro v6 & Tailwind CSS (TypeScript for type safety).
* **Compute / Backend:** Cloudflare Workers (Serverless Edge Computing with SSR).
* **Database:** Cloudflare D1 (Serverless SQLite at the Edge).
* **AI Integration:** Google Gemini API (Automated assessment & localized grading).
* **DNS & Networking:** Cloudflare (Advanced Routing, TLS Termination, Edge Caching).
* **CI/CD:** GitHub integrations paired with Cloudflare Wrangler CLI.

## 🚀 Phase 2: Edge Migration & AI Integration (May 2026)

To support a dynamic student placement test, the infrastructure was fully migrated away from legacy cPanel hosting to a modern Server-Side Rendered (SSR) edge environment.

### 1. Advanced DNS Decoupling & Zero-Downtime Migration
* Executed a live migration by decoupling legacy monolithic DNS records.
* Mapped root web traffic (A/CNAME records) directly to the Cloudflare Worker infrastructure while intentionally isolating and grey-clouding (DNS-only) MX and mail subdomains to legacy IP addresses, ensuring zero disruption to business email operations.

### 2. Serverless Backend & Database Implementation
* Deployed a Cloudflare D1 (SQLite) database to capture student lead data and test results globally.
* Integrated the Gemini AI API directly into the Astro SSR backend to instantly analyze test results, calculate CEFR levels (A1-C2), and generate personalized, localized (Vietnamese) feedback for prospective students.

### 3. DevSecOps & Pipeline Troubleshooting
* **Secret Management & Zero Trust:** Eliminated all hardcoded secrets. Database access is strictly governed by internal Cloudflare Bindings. External API keys (Gemini) are injected exclusively via encrypted Cloudflare Environment Variables.
* **SQL Injection Prevention:** Enforced parameterized queries for all database interactions.
* **CI/CD Debugging:** Troubleshot complex pipeline collisions between Astro's output configurations and Cloudflare's deployment engines (identifying and resolving `wrangler.toml` conflicts that caused legacy Pages vs. Workers routing errors). Managed remote database provisioning via `wrangler d1 execute` CLI commands.

**Evidence: Workers**

![Cloudflare Serverless](https://github.com/AlexPopCyberSec/lingo-leap-architecture/blob/main/workers.png)

**Evidence: D1 Database**

![D1-Cloudflare](https://github.com/AlexPopCyberSec/lingo-leap-architecture/blob/main/D1-Database.png)

**Evidence: AI output and grading**

![AI Result](https://github.com/AlexPopCyberSec/lingo-leap-architecture/blob/main/AI-feedback.png)

## 🛡️ Phase 1: Static Architecture & Baseline Hardening (Feb/Mar 2026)

The initial phase focused on deploying a blazing-fast static site while establishing a strict security baseline on a traditional cPanel/LiteSpeed web server.

### 1. Infrastructure Hardening
* **Security Headers:** Configured Apache/LiteSpeed directives (`.htaccess`) to strictly control browser behavior.
* **Strict-Transport-Security (HSTS):** Enforced HTTPS (1 Year Preload).
* **X-Frame-Options:** DENY (Full protection against Clickjacking).
* **Permissions-Policy:** Explicitly disabled access to Camera, Mic, and Geolocation to prevent spyware injection.
* **Transport Security:** Enforced TLS 1.2+ minimum via Cloudflare Edge to mitigate legacy protocol vulnerabilities (POODLE, BEAST).
* **Evidence:** SecurityHeaders.com Grade A
* **Evidence:** SSL Labs Grade A

### 2. Application Security
* **Bot Mitigation Strategy:**
    * *Layer 1 (Behavioral):* Custom CSS-hidden "Honeypot" fields to trap automated scripts without impacting UX.
    * *Layer 2 (Verification):* Google reCAPTCHA v2 integration enforced at the server level (EmailJS).
* **Input Sanitization:** Strict HTML5 Regex patterns on all form inputs to enforce data integrity and prevent injection.

### 3. Performance Optimization (SSG)
* **Score:** 100/100 Desktop, 95+ Mobile on PageSpeed Insights.
* **Technique:** Static Site Generation (SSG) combined with Cloudflare Edge Caching ensured sub-100ms Time to First Byte (TTFB).
* **Evidence:** PageSpeed Insights


**Evidence: SecurityHeaders.com Grade A**

![Security Headers Scan Result](https://github.com/AlexPopCyberSec/lingo-leap-architecture/blob/main/security%20headers.png)

**Evidence: SSL Labs Grade A**

![SSL Labs Scan Result](https://github.com/AlexPopCyberSec/lingo-leap-architecture/blob/main/qualys%20ssl.png)

**Evidence: PageSpeed Insights**

![PageSpeed Result](https://github.com/AlexPopCyberSec/lingo-leap-architecture/blob/main/page%20speed%20desktop.png)
![PageSpeed Result](https://github.com/AlexPopCyberSec/lingo-leap-architecture/blob/main/page%20speed%20mobile.png)

---
*Project engineered and maintained by Aleksandar Popov - IT Support & Cloud Infrastructure.*
