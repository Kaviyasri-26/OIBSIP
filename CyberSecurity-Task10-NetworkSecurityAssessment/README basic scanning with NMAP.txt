Basic Network Scanning with Nmap

1. Objective

The objective of this task was to perform basic network scanning using Nmap and understand what network services are exposed on a local machine. I used my Kali Linux virtual machine in Oracle VirtualBox as the test environment.

I performed a basic scan, service version detection, and OS detection. I then documented the results and analyzed the security implications.

2. Tools and Environment

- Tool:** Nmap 7.99
- Operating System:** Kali Linux
- Virtualization:** Oracle VirtualBox
- Target IP:** 10.0.2.15
- Environment:** Local virtual machine

3. What is Nmap?

Nmap (Network Mapper) is a network scanning and security auditing tool. It can be used to discover hosts, identify open ports, detect running services, and gather information about operating systems.

Nmap is commonly used by network administrators and security professionals to understand which services are accessible on a system.

4. Why Network Scanning Matters

Network scanning helps identify services that are exposed on a network. An unnecessarily open port or service can increase the attack surface of a system.

By scanning a system, administrators can identify exposed services, check whether they are required, and take appropriate security measures such as firewall configuration and service hardening.

5. Nmap Installation

Nmap was already available in my Kali Linux installation.

I checked the installed version using:

```bash
nmap --version

The installed version was:

Nmap version 7.99
6. Finding the Target IP

I checked the network interfaces using:

ip addr

The eth0 interface had the following IPv4 address:

10.0.2.15

I used this local Kali VM address as the target for the scan.

7. Basic Nmap Scan

I performed a basic scan using:

nmap 10.0.2.15
Result

The host was up, but Nmap reported that all 1000 scanned TCP ports were in ignored states.

The output showed:

Host is up.
All 1000 scanned ports on 10.0.2.15 are in ignored states.
Not shown: 1000 filtered tcp ports (no-response)
Finding

No open TCP ports were identified by the basic scan.

The ports were reported as filtered, which means Nmap did not receive a response from them. This can happen when traffic is being blocked or filtered by a firewall or other network filtering mechanism.

8. Service Version Scan

I performed service and version detection using:

nmap -sV 10.0.2.15
Result

The host was up, but all 1000 scanned TCP ports were filtered.

The scan reported:

All 1000 scanned ports on 10.0.2.15 are in ignored states.
Not shown: 1000 filtered tcp ports (no-response)
Service detection performed.

No open services or service versions were identified.

Finding

Since no open TCP ports were detected, Nmap could not identify any running TCP services on the scanned ports.

9. OS Detection Scan

I performed OS detection using:

sudo nmap -O 10.0.2.15
Result

The scan reported:

Host is up.
All 1000 scanned ports on 10.0.2.15 are in ignored states.
Not shown: 1000 filtered tcp ports (no-response)
Too many fingerprints match this host to give specific OS details
Network Distance: 0 hops
Finding

Nmap could not identify the specific operating system because the available responses were not sufficient for reliable OS fingerprinting.

I did not assume or manually assign an OS based on this scan result.

10. Open Port Analysis

Based on the three scans:

Port	State	Service	Security Risk
None identified	Filtered	None identified	No exposed TCP service was identified

The scans did not identify any open TCP ports among the default 1000 ports tested.

Because no open services were found, there were no specific exposed services to analyze in this scan.

11. Security Analysis

The scan showed that the tested TCP ports were filtered and did not provide responses to Nmap.

This can reduce the externally visible attack surface because services are not responding through the scanned ports.

However, filtered ports do not automatically mean that the system is completely secure. Other ports, protocols, network interfaces, or application-level vulnerabilities may still exist.

Regular network scanning can help administrators identify unexpected services and verify firewall configurations.

12. Screenshots

The following screenshots were captured as evidence:

Basic Scan

nmap-basic-scan.png

Shows the result of:

nmap 10.0.2.15
Service Version Scan

nmap-service-version.png

Shows the result of:

nmap -sV 10.0.2.15
OS Detection

nmap-os-detection.png

Shows the result of:

sudo nmap -O 10.0.2.15
13. Ethical Use

Nmap should only be used against systems that you own or have explicit permission to scan.

For this task, I used my own Kali Linux virtual machine as the target. I did not scan external websites, public networks, university networks, or systems without authorization.

Unauthorized network scanning can cause disruption and may violate organizational policies or laws.

14. Conclusion

This task gave me practical experience with Nmap and basic network reconnaissance.

I learned how to perform a basic port scan, service version detection, and OS detection. The scans showed that the target host was reachable but the 1000 default TCP ports tested were filtered.

The task also helped me understand that network scanning is useful for identifying exposed services and checking the network attack surface of a system