# Wireshark Network Traffic Analysis

## 1. Objective

The main objective of this task was to use Wireshark to capture and analyze network traffic. I used Wireshark in a Kali Linux virtual machine and examined HTTP, DNS, and TCP traffic. I also looked at a TCP three-way handshake and identified unencrypted HTTP data.

## 2. Tools and Environment

- **Tool:** Wireshark
- **Operating System:** Kali Linux
- **Virtualization:** Oracle VirtualBox
- **Network Interface:** `eth0`
- **Network Mode:** VirtualBox NAT

## 3. Wireshark Installation

I installed Wireshark on Kali Linux using the following commands:

```bash
sudo apt update
sudo apt install wireshark -y
```

During installation, I selected **Yes** when asked whether non-superusers should be allowed to capture packets.

I then added my user to the Wireshark group and restarted the system:

```bash
sudo usermod -aG wireshark $USER
sudo reboot
```

After restarting, I opened Wireshark and selected the `eth0` network interface for packet capture.

## 4. Network Traffic Capture

I used Wireshark in my Kali Linux virtual machine to capture live network traffic. I selected the `eth0` interface and captured traffic for more than two minutes.

During the capture, I generated network activity using commands such as `nslookup` and `curl`. This helped me collect different types of packets for analysis.

## 5. HTTP Traffic Analysis

To find HTTP packets, I used the following display filter in Wireshark:

```text
http
```

I was able to identify an HTTP GET request in the captured traffic. By selecting the packet and expanding the HTTP section, I could see details such as the request method, requested path, host, and other HTTP headers.

### Unencrypted HTTP Data

The HTTP request was readable directly in Wireshark. This shows that HTTP does not encrypt the information being sent.

If someone is able to monitor the network traffic, they may be able to see information such as the requested URL, headers, or other data being transmitted.

### Why HTTPS is Safer

HTTPS uses TLS to encrypt communication between the client and the server. Because of this encryption, the actual contents of the communication cannot normally be read simply by capturing the network packets.

## 6. DNS Traffic Analysis

I used the following display filter to find DNS packets:

```text
dns
```

The capture showed DNS queries and responses. I generated DNS traffic using `nslookup` commands and then checked the packets in Wireshark.

The packets helped me understand how a domain name, such as `google.com`, is looked up and how the DNS response is returned.

## 7. TCP Three-Way Handshake

I used the `tcp` filter to examine TCP traffic and selected one TCP connection for closer analysis.

The TCP stream used for the analysis was:

```text
tcp.stream eq 8
```

I identified the following three packets:

- **Packet 174 – SYN**
- **Packet 178 – SYN-ACK**
- **Packet 181 – ACK**

These three packets form the TCP three-way handshake.

The process was:

```text
SYN → SYN-ACK → ACK
```

The SYN is sent by the client to request a connection. The server responds with SYN-ACK, and the client sends ACK to confirm the connection.

After these three steps, the TCP connection can be established and data can be exchanged.

## 8. Packet Analysis

While working with Wireshark, I checked different parts of the captured packets, including:

- Source IP address
- Destination IP address
- Source and destination ports
- Protocol
- TCP flags
- Packet contents

I also used the packet details section to understand what information was carried by different protocols.

This analysis helped me understand how network communication looks at the packet level and how Wireshark can be used to investigate network traffic.

## 9. Evidence

The following screenshots were collected during the task:

1. **HTTP Filter** – Shows HTTP traffic using the `http` display filter.
2. **DNS Filter** – Shows DNS queries and responses using the `dns` display filter.
3. **TCP Handshake** – Shows the SYN, SYN-ACK, and ACK packets of a TCP connection.

## 10. Files Included

The project contains:

```text
Wireshark-Task/
├── README.md
├── wireshark_capture.pcap
└── screenshots/
    ├── http-filter.png
    ├── dns-filter.png
    └── tcp-handshake.png
```

## 11. Glossary

### Packet
A packet is a small unit of data sent across a network.

### Protocol
A protocol is a set of rules that devices follow to communicate with each other.

### Port
A port is a logical communication endpoint used by network services and applications.

### Payload
The payload is the actual data carried inside a packet.

### Handshake
A handshake is a process used by two devices to establish communication. In TCP, this starts with SYN, followed by SYN-ACK, and then ACK.

## 12. Ethics and Authorization

Network traffic should only be captured on systems and networks that I own or have permission to monitor.

I performed this activity in my own Kali Linux virtual machine for learning and internship purposes. I did not capture traffic from public Wi-Fi, university networks, or other unauthorized networks.

## 13. Conclusion

This task gave me practical experience with Wireshark and helped me understand how network traffic can be viewed and analyzed at the packet level.

I learned how to filter HTTP and DNS traffic, identify a TCP three-way handshake, and understand why unencrypted HTTP traffic can be a security risk.

Wireshark is a useful tool for network troubleshooting, monitoring, and cybersecurity investigations.
