# CVE-2023-3460: Unauthenticated Privilege Escalation in WordPress Ultimate Member Plugin

## Overview
This repository documents a hands-on security assessment and proof-of-concept (PoC) demonstration for **CVE-2023-3460**, an unauthenticated privilege escalation vulnerability affecting the WordPress **Ultimate Member** plugin (versions < 2.6.7). 

The vulnerability stems from how WordPress handles user metadata keys. Attackers can manipulate requests during registration to inject restricted meta-keys—specifically `wp_capabilities`—allowing an unauthenticated user to register and elevate privileges to an **Administrator** or **Editor** role.

---

## Technical Summary
* **Vulnerability Type:** Unauthenticated Privilege Escalation / Improper Meta-Data Handling
* **Affected Software:** WordPress Ultimate Member Plugin (< 2.6.7)
* **Target Objective:** Perform a privilege escalation attack to acquire elevated privileges (Editor/Administrator) and retrieve the hidden flag from the restricted home page.
* **Primary Tools Used:** Burp Suite (Proxy & Repeater), Web Browser

---

## Methodology & Attack Walkthrough

1. **Reconnaissance & Target Analysis:**
   * Investigated the target web application (`https://test1.mohammadlotfi.com`).
   * Identified restricted content sections requiring an elevated role (such as `editor` or `administrator`) to view the hidden flag.

2. **Baseline Registration (Normal User):**
   * Registered a standard user account through the web interface (e.g., username `olivias`) to analyze standard traffic patterns and form parameters.

3. **Intercepting Requests with Burp Suite:**
   * Configured Burp Suite to intercept HTTP traffic.
   * Captured the registration and login POST requests to analyze parameter formatting, nonces, and user metadata fields.

4. **Exploitation via Parameter Manipulation:**
   * Registered a secondary test account while intercepting the request in Burp Suite.
   * Modified the POST request parameters to target user roles, mimicking the vulnerability structure outlined in the official advisory.
   * Forwarded the manipulated request to Burp Suite Repeater to adjust role assignment values to `editor`.

5. **Verification:**
   * Re-sent the crafted payload to validate server responses (`HTTP 200 OK`) and confirm successful privilege escalation.

---

## Getting Started & Prerequisites

To replicate this environment for educational and testing purposes locally:

### Prerequisites
* **Local Server Environment:** XAMPP (or local equivalent)
* **CMS:** WordPress (vulnerable version installed with the Ultimate Member plugin < 2.6.7)
* **Interceptor:** Burp Suite (Community or Professional Edition)

### Execution Steps
1. Spin up your local WordPress test environment.
2. Configure your browser proxy to route traffic through Burp Suite.
3. Navigate to the plugin registration page and follow the parameter manipulation steps outlined in the assessment documentation.

---

## Keywords
`Unauthenticated Privilege Escalation`, `WordPress`, `Burp Suite`, `Ultimate Member Plugin`, `CVE-2023-3460`, `KreativStorm`

---

## References & Resources
1. [WPScan Vulnerability Database: CVE-2023-3460](https://wpscan.com/vulnerability/694235c7-4469-4ffd-a722-9225b19e98d7/)
2. [Online URL Decoder](https://www.urldecoder.org)
3. [Online Unserialize Tool](https://www.unserialize.com/)