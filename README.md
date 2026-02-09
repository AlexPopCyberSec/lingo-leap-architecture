# Lingo Leap - Secure Education Platform Architecture

**Live Deployment:** [https://lingo-leap.net](https://lingo-leap.net)

A high-performance, security-hardened web platform designed for a boutique language academy. This project demonstrates a **"Defense-in-Depth"** approach to infrastructure, moving beyond default configurations to a hardened production environment suitable for enterprise deployment.

## 🏗️ Technical Architecture

* **Frontend:** Astro (Static Site Generation) & TypeScript for type safety.
* **Web Server:** LiteSpeed Enterprise (cPanel) for high-concurrency performance.
* **Edge Network:** Cloudflare (DNS, TLS Termination, Edge Caching).
* **CI/CD:** Manual hardened deployment pipeline (Audit -> Build -> Deploy).

---

## 🛡️ Security Implementation (DevSecOps)

### 1. Infrastructure Hardening
* **Security Headers:** Configured Apache/LiteSpeed directives (`.htaccess`) to strictly control browser behavior.
    * `Strict-Transport-Security` (HSTS): Enforced HTTPS (1 Year Preload).
    * `X-Frame-Options: DENY`: Full protection against Clickjacking.
    * `Permissions-Policy`: Explicitly disabled access to Camera, Mic, and Geolocation to prevent spyware injection.
* **Transport Security:** Enforced **TLS 1.2+** minimum via Cloudflare Edge to mitigate legacy protocol vulnerabilities (POODLE, BEAST).

**Evidence: SecurityHeaders.com Grade A**
![Security Headers Scan Result](https://github.com/AlexPopCyberSec/lingo-leap-architecture/blob/main/security%20headers.png)

**Evidence: SSL Labs Grade A**
![SSL Labs Scan Result](https://github.com/AlexPopCyberSec/lingo-leap-architecture/blob/main/qualys%20ssl.png)

### 2. Application Security
* **Secret Management:** Zero hardcoded credentials. All API keys (EmailJS, reCAPTCHA) are managed via **Environment Variables** (`.env`) and injected strictly at build time.
* **Bot Mitigation Strategy:**
    * **Layer 1 (Behavioral):** Custom CSS-hidden "Honeypot" fields to trap automated scripts without impacting UX.
    * **Layer 2 (Verification):** Google reCAPTCHA v2 integration enforced at the server level (EmailJS).
* **Input Sanitization:** Strict HTML5 Regex patterns on all form inputs to enforce data integrity and prevent injection.

### 3. Supply Chain Security
* Dependency lifecycle managed via `package-lock.json` to ensure reproducible builds.
* Pre-deployment vulnerability scanning via `npm audit` (0 Vulnerabilities).

---

## ⚡ Performance Optimization

* **Score:** 100/100 Desktop, 95+ Mobile on PageSpeed Insights.
* **Technique:** Static Site Generation (SSG) combined with Cloudflare Edge Caching ensures sub-100ms Time to First Byte (TTFB).

**Evidence: PageSpeed Insights**
![PageSpeed Result](https://github.com/AlexPopCyberSec/lingo-leap-architecture/blob/main/page%20speed%20desktop.png)
![PageSpeed Result](https://github.com/AlexPopCyberSec/lingo-leap-architecture/blob/main/page%20speed%20mobile.png)

---

*Project maintained by Aleksandar Popov - IT Support Specialist and Aspiring Cybersecurity Professional*
