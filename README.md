# Project: CVE-2023-3460 WordPress Privilege Escalation Assessment

## 📋 Executive Summary
Completed a hands-on cybersecurity training assignment with KreativStorm to investigate and exploit CVE-2023-3460, an unauthenticated privilege escalation vulnerability affecting the WordPress Ultimate Member plugin (< 2.6.7). Utilized Burp Suite and request parameter manipulation to inject restricted meta-keys (`wp_capabilities`), successfully escalating privileges to an administrative role to retrieve the hidden flag from the restricted homepage.

---

## 🛠️ Architecture & Tech Stack
* **Target Environment:** Local WordPress test environment / Web Application (`https://test1.mohammadlotfi.com`)
* **Vulnerable Component:** WordPress Ultimate Member Plugin (< 2.6.7)
* **Exploitation & Interception Tool:** Burp Suite (Proxy and Repeater modules)
* **Supporting Tools:** Web Browser, URL Decoder, Unserialize tools

---

## ⚙️ Step-by-Step Implementation

### Step 1: Environment Setup & Reconnaissance
* Investigated the target web application and identified restricted content sections that required an elevated role (`editor`) to view the hidden flag.
* Reviewed the source code and vulnerability proof-of-concept guidelines detailing how improper meta-data handling permits attackers to update restricted fields like `wp_capabilities`.

```bash
# Example reference structure for vulnerability analysis mapping via WPScan advisory
https://wpscan.com/vulnerability/694235c7-4469-4ffd-a722-9225b19e98d7/
```

### Step 2: Baseline Registration & Traffic Interception
* Registered a standard user account through the web interface (e.g., username `olivias`) to understand standard parameter behavior.
* Configured Burp Suite as an intercepting proxy to capture login and registration POST requests.
* Analyzed the captured parameters, form nonces, and metadata fields to prepare for payload injection.

### Step 3: Parameter Manipulation & Privilege Escalation
* Initiated a secondary registration attempt while intercepting the traffic in Burp Suite.
* Copied and modified the POST request parameters, replacing standard user variables to target role assignments.
* Forwarded the modified request to Burp Suite Repeater, altering the parameters to map user roles to an `editor` privilege level.

### Step 4: Verification & Flag Retrieval
* Sent the crafted payload and verified the server response (`HTTP 200 OK`) to confirm successful execution of the vulnerability.
* Authenticated using the escalated credentials to bypass access controls and retrieve the target flag from the restricted homepage.

---

## 🧪 Testing & Validation
* Validated the exploit workflow by observing how unauthenticated user registration inputs processed metadata without adequate sanitization.
* Confirmed that injecting `wp_capabilities` during the registration lifecycle successfully bypassed default role assignment constraints.

---

## 💡 Key Learnings & Challenges
* **Challenge:** Understanding how WordPress treats metadata keys and how improper validation can allow unauthorized modification of sensitive attributes like `wp_capabilities`.
* **Solution:** Used Burp Suite Proxy and Repeater to precisely isolate, modify, and replay registration POST parameters.
* **Key Takeaway:** Gained a practical understanding of unauthenticated privilege escalation mechanics in content management systems and the importance of secure meta-data handling.

---

## 🚀 Future Improvements
* Implement automated vulnerability scanning to detect outdated WordPress plugins in staging environments.
* Explore remediation strategies by patching the Ultimate Member plugin to version 2.6.7 or higher and enforcing strict Role-Based Access Control (RBAC).