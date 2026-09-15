# Common Network Security Threats

**OASIS Infobyte SIP – Security Analyst Track**  
**Task 4: Research Report – Common Network Security Threats**

## 1. Introduction

Network security threats are attacks or activities that can affect the confidentiality, integrity, or availability of systems and data connected to a network. Modern organisations depend on networks for communication, applications, cloud services, and business operations, so a successful network attack can cause service disruption, data exposure, financial loss, and reputational damage. Understanding common threats and applying layered security controls helps organisations reduce risk and respond to attacks more effectively.

## 2. Denial-of-Service (DoS) and Distributed Denial-of-Service (DDoS) Attacks

### How the attack works

A Denial-of-Service (DoS) attack attempts to make a service unavailable by overwhelming a system, application, or network resource with excessive traffic or requests. A Distributed Denial-of-Service (DDoS) attack uses many systems at the same time, often a botnet, making the attack larger and harder to block based on a single source.

### Real-world example

In February 2018, GitHub experienced a very large DDoS attack that reached approximately 1.35 Tbps. The incident was associated with abuse of memcached servers and spoofed traffic. GitHub was able to mitigate the attack using its DDoS protection and traffic filtering infrastructure.

### Impact

- Websites and online services may become unavailable.
- Legitimate users may be unable to access applications.
- Organisations can lose revenue and productivity.
- Incident response and recovery can require significant resources.
- Repeated attacks can damage customer trust.

### Mitigation strategies

1. **DDoS protection and traffic filtering:** Use a DDoS mitigation service, CDN, or network filtering solution to absorb and filter malicious traffic.
2. **Rate limiting:** Limit the number of requests that a client or source can make within a defined period.
3. **Redundancy and capacity planning:** Use scalable infrastructure and redundant services so that one overloaded component does not cause complete service failure.

## 3. Man-in-the-Middle (MITM) Attacks

### How the attack works

A Man-in-the-Middle attack occurs when an attacker secretly positions themselves between two communicating parties. The attacker may intercept, modify, or relay communication while attempting to remain unnoticed. Unsecured public Wi-Fi, weak authentication, malicious network devices, and improperly validated certificates can increase the risk.

### Real-world example

In 2011, the DigiNotar certificate authority was compromised. Fraudulent certificates were issued, including certificates for major websites. The incident demonstrated how compromise of certificate infrastructure can enable attackers to impersonate trusted services and potentially intercept communications.

### Impact

- Login credentials or sensitive information may be exposed.
- Data can be modified while in transit.
- Users may be redirected to fraudulent services.
- Session information can potentially be stolen.
- Confidential business communications may be compromised.

### Mitigation strategies

1. **Use HTTPS/TLS:** Encrypt sensitive communications and ensure certificates are properly validated.
2. **Use secure authentication:** Apply multi-factor authentication (MFA) so stolen credentials alone are less useful.
3. **Secure network access:** Avoid untrusted networks for sensitive activity and use properly configured VPNs where appropriate.

## 4. IP Spoofing

### How the attack works

IP spoofing occurs when an attacker manipulates the source IP address in network packets so that the traffic appears to originate from another address. Because the source address can be forged, systems should not treat it as proof of identity.

IP spoofing can be used in reflection/amplification attacks, some forms of denial-of-service, and attempts to bypass poorly designed network access controls.

### Real-world example

The 2018 GitHub DDoS incident used spoofed source addresses in traffic generated through vulnerable memcached servers. Spoofing helped the attacker cause responses from third-party servers to be directed toward the target.

### Impact

- Attack sources can be difficult to identify from packet source addresses alone.
- Spoofed traffic can contribute to DDoS and reflection attacks.
- Weak IP-based access controls may be bypassed.
- Network monitoring can become more difficult.

### Mitigation strategies

1. **Ingress and egress filtering:** Apply network filtering practices such as source-address validation to reduce spoofed traffic.
2. **Do not rely only on IP addresses for authentication:** Use strong identity and authentication mechanisms.
3. **Use anti-DDoS controls:** Deploy filtering and rate-limiting controls to detect and reduce spoofed or abnormal traffic.

## 5. DNS Poisoning / DNS Spoofing

### How the attack works

The Domain Name System (DNS) translates domain names into IP addresses. DNS poisoning or spoofing attempts to provide a false DNS response so that a user is directed to an incorrect or malicious destination.

An attacker may target DNS caches, DNS infrastructure, or the communication between a user and a DNS resolver. DNS manipulation can therefore redirect users without changing the visible domain name they intended to visit.

### Real-world example

The 2019 Sea Turtle campaign demonstrated the risk of DNS-related infrastructure compromise. Attackers targeted organisations involved in DNS and network infrastructure and used compromised credentials and DNS manipulation to redirect traffic and capture information.

### Impact

- Users may be redirected to malicious websites.
- Credentials and other sensitive information may be stolen.
- Business traffic may be redirected or disrupted.
- Users can lose trust in affected online services.

### Mitigation strategies

1. **Use DNSSEC where appropriate:** DNSSEC provides cryptographic validation of DNS data and helps detect tampered responses.
2. **Secure DNS infrastructure:** Protect registrar, DNS provider, and administrator accounts with strong passwords and MFA.
3. **Monitor DNS changes:** Alert on unexpected modifications to DNS records and investigate suspicious domain-resolution behaviour.

## 6. Comparison Table

| Threat | Attack Vector | Who Is at Risk? | Difficulty to Execute | Ease of Mitigation |
|---|---|---|---|---|
| DoS/DDoS | Excessive traffic or requests | Websites, servers, online services | Medium to High | Medium |
| MITM | Intercepted or manipulated communication | Users and organisations using vulnerable networks/services | Medium | Medium |
| IP Spoofing | Forged source IP addresses | Networks and Internet-facing services | Medium | Medium |
| DNS Poisoning/Spoofing | Manipulated DNS responses or DNS infrastructure | Users, websites, organisations | Medium to High | Medium |

## 7. Key Prevention Practices

Organisations should use a layered security approach rather than depending on a single control. Important practices include:

- Keep operating systems, applications, network devices, and security software updated.
- Use strong authentication and enable MFA for important accounts.
- Encrypt sensitive communication using properly configured TLS.
- Segment networks so that compromise of one area has limited impact.
- Monitor network traffic, DNS activity, authentication events, and configuration changes.
- Maintain tested backups and an incident response plan.
- Apply least-privilege access to administrative systems.
- Regularly review firewall, DNS, router, and cloud security configurations.
- Train employees to recognise suspicious network and social-engineering activity.

## 8. Conclusion

Three key takeaways for a network administrator are:

1. **Use defence in depth:** No single security control can prevent every network attack.
2. **Protect critical infrastructure:** DNS, network devices, authentication systems, and public-facing services should receive strong security controls and continuous monitoring.
3. **Prepare for disruption:** DDoS protection, incident response procedures, redundancy, monitoring, and tested recovery plans help organisations continue operating when attacks occur.

## 9. References

1. National Institute of Standards and Technology (NIST) – Computer Security Resource Center: https://csrc.nist.gov/
2. Cybersecurity and Infrastructure Security Agency (CISA) – Cybersecurity Resources: https://www.cisa.gov/
3. MITRE ATT&CK – Enterprise Techniques and Tactics: https://attack.mitre.org/
4. SANS Institute – Information Security Resources: https://www.sans.org/white-papers/
5. GitHub Engineering – 1.35 Tbps DDoS Attack: https://github.blog/engineering/infrastructure/ddos-incident-report/
6. KrebsOnSecurity – Sea Turtle DNS Hijacking Campaign: https://krebsonsecurity.com/2019/04/dns-hijacking-campaign-targeted-middle-east/
