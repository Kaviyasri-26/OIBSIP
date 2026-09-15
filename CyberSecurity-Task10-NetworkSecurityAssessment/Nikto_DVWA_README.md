# Nikto Vulnerability Scanning with DVWA

## 1. Objective

The objective of this task was to learn how to perform a basic web vulnerability scan using Nikto. I used DVWA (Damn Vulnerable Web Application) as a deliberately vulnerable web application in my own local environment. The scan helped me identify common web server and security configuration issues.

> **Ethical note:** This scan was performed only against my own local DVWA environment (`127.0.0.1`). Nikto should only be used on systems where you have permission to perform security testing.

## 2. Tools and Environment

- **Operating System:** Kali Linux
- **Virtualization:** Oracle VirtualBox
- **Web Application:** DVWA (Damn Vulnerable Web Application)
- **Scanner:** Nikto
- **Target:** `http://127.0.0.1:8080`
- **Nikto Version:** 2.6.0

## 3. What is Nikto?

Nikto is an open-source web server scanner. It checks a web server for potentially dangerous files, outdated components, insecure HTTP headers, configuration problems, and other known issues.

Nikto is useful during security testing because it can quickly identify areas that may need further investigation.

## 4. What is DVWA?

DVWA stands for **Damn Vulnerable Web Application**. It is an intentionally vulnerable web application used for learning web application security.

I ran DVWA locally so that the vulnerability scanning could be performed safely without targeting an external website.

## 5. Setting Up the Test Environment

I used Kali Linux in Oracle VirtualBox and ran DVWA locally.

The local target address used for testing was:

```text
http://127.0.0.1:8080
```

The IP address `127.0.0.1` refers to the local machine, so the scan remained inside my test environment.

## 6. Performing the Nikto Scan

After starting the DVWA environment, I checked that the application was available on the local port.

I then ran Nikto against the local DVWA target using:

```bash
nikto -h http://127.0.0.1:8080
```

The scan checked the web server and application for several common security issues.

To save the scan output for documentation, the result can also be saved with:

```bash
nikto -h http://127.0.0.1:8080 -o nikto_scan.txt
```

## 7. Scan Results

The Nikto scan identified several security-related findings in the local DVWA environment.

Some of the findings included:

- Cookies were set without the `HttpOnly` attribute.
- The `Strict-Transport-Security` (HSTS) header was missing.
- The `Permissions-Policy` header was missing.
- The `Referrer-Policy` header was missing.
- The `X-Content-Type-Options` header was missing.
- The `Content-Security-Policy` (CSP) header was missing.
- A potentially interesting `/icons/README` resource was detected.
- `/login.php` was identified as an accessible login-related page.

These findings do not automatically mean that every item is a directly exploitable vulnerability. They are security observations that should be reviewed and tested further.

## 8. Explanation of Important Findings

### 8.1 Cookie Without HttpOnly

The scan reported cookies that did not have the `HttpOnly` attribute.

The `HttpOnly` attribute helps prevent client-side JavaScript from directly accessing a cookie. Without it, a successful cross-site scripting (XSS) attack could potentially make it easier for an attacker to access certain session cookies.

**Recommendation:** Set the `HttpOnly` attribute on sensitive session cookies where appropriate.

### 8.2 Missing HSTS Header

Nikto reported that the `Strict-Transport-Security` header was missing.

HSTS tells browsers to use HTTPS for a website instead of making normal HTTP connections.

**Recommendation:** For production websites that are fully configured for HTTPS, enable HSTS with an appropriate policy.

Example:

```text
Strict-Transport-Security: max-age=31536000
```

### 8.3 Missing Content-Security-Policy

The `Content-Security-Policy` (CSP) header was not present.

CSP can reduce the risk and impact of some cross-site scripting and other content injection attacks by controlling which sources of content a browser is allowed to load.

**Recommendation:** Create and deploy a CSP that matches the application's actual requirements.

### 8.4 Missing X-Content-Type-Options

The scan reported that the `X-Content-Type-Options` header was missing.

This header can help prevent browsers from MIME-sniffing responses when set to:

```text
X-Content-Type-Options: nosniff
```

**Recommendation:** Add the `X-Content-Type-Options: nosniff` response header where appropriate.

### 8.5 Missing Referrer-Policy

The `Referrer-Policy` header was missing.

This header controls how much referrer information is included when a browser makes requests to another resource.

**Recommendation:** Configure a suitable Referrer-Policy based on the application's privacy and functionality requirements.

### 8.6 Missing Permissions-Policy

Nikto also identified a missing `Permissions-Policy` header.

Permissions Policy allows websites to control access to certain browser features.

**Recommendation:** Configure a suitable policy and disable browser features that the application does not need.

### 8.7 `/icons/README`

Nikto identified an accessible `/icons/README` resource.

Publicly accessible documentation or server-related files can sometimes reveal useful information about the server configuration or software.

**Recommendation:** Remove unnecessary files and directories from production web servers, or restrict access to them when they are not required.

### 8.8 `/login.php`

Nikto identified `/login.php` as an accessible login-related resource.

A login page itself is not necessarily a vulnerability. However, authentication pages should be protected with secure authentication controls, HTTPS, appropriate session management, and protection against common attacks.

**Recommendation:** Use HTTPS, secure cookies, strong authentication controls, input validation, rate limiting, and appropriate session management.

## 9. Why These Findings Matter

Security headers and secure cookie settings add important layers of protection to web applications.

Missing headers do not always create an immediate vulnerability by themselves. However, they can reduce the browser's security protections and may increase the impact of other vulnerabilities.

Nikto is therefore useful as an initial security check, but its findings should be manually reviewed and validated before considering them confirmed vulnerabilities.

## 10. Evidence

The project should include screenshots showing the work performed.

Suggested screenshots:

```text
screenshots/
├── dvwa-running.png
├── nikto-scan.png
└── nikto-results.png
```

### Screenshot 1 – DVWA Running

Shows that DVWA was running locally before the scan.

### Screenshot 2 – Nikto Scan

Shows the Nikto command and the target:

```text
http://127.0.0.1:8080
```

### Screenshot 3 – Nikto Results

Shows the findings reported by Nikto, including missing security headers and other observations.

## 11. Files Included

A recommended project structure is:

```text
Nikto-DVWA-Task/
│
├── README.md
├── nikto_scan.txt
│
└── screenshots/
    ├── dvwa-running.png
    ├── nikto-scan.png
    └── nikto-results.png
```

The `nikto_scan.txt` file should contain the raw output generated by the Nikto scan.

## 12. Recommendations

Based on the scan results, the following general security improvements are recommended for a production web application:

1. Use HTTPS and configure HSTS after HTTPS is correctly deployed.
2. Set secure attributes such as `HttpOnly` and `Secure` on sensitive cookies.
3. Configure a suitable Content-Security-Policy.
4. Add security headers such as `X-Content-Type-Options`.
5. Configure an appropriate Referrer-Policy.
6. Configure Permissions-Policy where appropriate.
7. Remove unnecessary files and directories from the web server.
8. Protect login pages with secure authentication and session-management controls.
9. Perform manual validation of scanner findings.
10. Keep the web server and application components updated.

## 13. Limitations

Nikto is a useful web server scanning tool, but it does not find every possible web application vulnerability.

A Nikto scan should not be treated as a complete penetration test. Other security testing methods and tools may be required to identify issues such as application logic flaws, authentication problems, authorization issues, and complex injection vulnerabilities.

## 14. Ethics and Authorization

This activity was performed only in a controlled environment using a locally hosted DVWA instance.

Security scanning can generate traffic and may affect systems if performed incorrectly. Therefore, scanning should only be performed against systems that I own or have explicit permission to test.

I did not use Nikto to scan public websites, public Wi-Fi, university networks, or other unauthorized systems.

## 15. Conclusion

This task gave me practical experience with Nikto and basic web vulnerability scanning.

I learned how to scan a local web application, save scan results, and understand common security configuration findings such as missing security headers and insecure cookie settings.

The task also helped me understand that automated scanners are useful for finding potential security issues, but their results should always be reviewed and validated before drawing final conclusions.
