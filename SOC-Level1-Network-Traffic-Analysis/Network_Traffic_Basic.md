<div align="center">

# Network Traffic Basics

</div>

## Task 1 Introduction

## Network Traffic Analysis (NTA)


**Network Traffic Analysis (NTA)** is the process of monitoring, capturing, and examining network data packets to detect suspicious activity, security threats, performance issues, and policy violations.

In simple terms, it means analyzing the data that travels across a network to understand:

- Who is communicating
- What data is being transferred
- Where it is going
- Whether the activity is normal or malicious

---

##  What is Analyzed in NTA?

During network traffic analysis, the following elements are typically examined:

- **Source IP Address**
- **Destination IP Address**
- **Port Numbers (e.g., 80, 443, 22)**
- **Protocols (TCP, UDP, HTTP, DNS, HTTPS)**
- **Packet size and frequency**
- **Unusual traffic patterns**

---

## Why is Network Traffic Analysis Important?

Network Traffic Analysis helps in:

- Detecting malware infections
- Identifying command-and-control (C2) communication
- Preventing data exfiltration
- Detecting Distributed Denial of Service (DDoS) attacks
- Supporting Security Operations Center (SOC) monitoring
- Assisting in incident response investigations

---

##  Tools Commonly Used

Some popular tools used for Network Traffic Analysis include:

- **Wireshark** – Packet capture and deep packet inspection
- **tcpdump** – Command-line packet analyzer
- **Zeek** – Network security monitoring framework
- **Snort** – Intrusion Detection and Prevention System (IDS/IPS)

---

##  Example Scenario

If a workstation repeatedly sends traffic to an unknown external IP address on an unusual port (e.g., 4444), it may indicate:

- Malware infection
- Reverse shell connection
- Data exfiltration attempt

Network Traffic Analysis helps identify and investigate such behavior.

---

## Task 2 — What is the purpose of Network Traffic Analysis?

##  DNS Tunneling


**DNS Tunneling** is a cyberattack technique where attackers use DNS (Domain Name System) queries and responses to secretly transmit data between an infected system and an external server.

Since DNS traffic is usually allowed through firewalls and rarely blocked, attackers exploit it to bypass security controls.

---

###  How DNS Tunneling Works

1. A system becomes infected with malware.
2. The malware encodes data (often using Base64 or hexadecimal encoding).
3. The encoded data is placed inside DNS queries (usually in subdomains).
4. The DNS request is sent to an attacker-controlled domain.
5. The attacker extracts the hidden data from DNS logs.

---

###  Why DNS Tunneling is Dangerous

- DNS traffic is commonly trusted and allowed.
- It can bypass firewall restrictions.
- It enables data exfiltration without triggering alerts.
- It can maintain hidden command-and-control (C2) communication.

---

###  Indicators of DNS Tunneling

- Unusually long or random-looking domain names
- High entropy subdomains
- Large number of DNS requests to a single domain
- DNS traffic with unusual record types (e.g., TXT records)

---

## Beaconing


**Beaconing** refers to periodic communication between an infected system and a Command-and-Control (C2) server.  
It acts as a “check-in” mechanism that allows attackers to maintain control over compromised systems.

---

###  How Beaconing Works

1. Malware infects a device.
2. The malware sends regular network requests to a C2 server.
3. The attacker sends commands or receives data through this communication channel.

---

###  Common Characteristics of Beaconing

- Regular time intervals (e.g., every 30 or 60 seconds)
- Communication to the same IP address or domain
- Consistent packet sizes
- Low but persistent data transfer

---

##  Difference Between DNS Tunneling and Beaconing

| Feature | DNS Tunneling | Beaconing |
|----------|---------------|-----------|
| Purpose | Hide data inside DNS traffic | Maintain connection with C2 server |
| Protocol Used | DNS | Any protocol (HTTP, HTTPS, DNS, TCP) |
| Pattern | Encoded subdomains | Periodic communication |
| Main Risk | Data exfiltration | Remote command execution |

---

##  Role in Network Security

Both DNS Tunneling and Beaconing are commonly used in advanced cyberattacks.  
Detecting them is a critical task in:

- Security Operations Centers (SOC)
- Threat Hunting
- Incident Response
- Network Traffic Analysis

Proper monitoring of DNS logs, traffic patterns, and periodic connections helps detect these threats early.

**Q1** What is the name of the technique used to smuggle C2 commands via DNS?

![Network Traffic Basics](screenshot2/NTB1.png)

Answer: DNS tunneling

---

## Task 3 — What network traffic can we observe?


## 1 Web Traffic (HTTP / HTTPS)

- Protocols: HTTP (Port 80), HTTPS (Port 443)
- Used for browsing websites and web applications
- Can reveal:
  - Requested URLs
  - User-Agent information
  - Server responses
  - Encrypted sessions (HTTPS metadata only)

---

## 2 Email Traffic (SMTP / POP3 / IMAP)

- SMTP (Port 25) – Sending emails  
- POP3 (Port 110) – Retrieving emails  
- IMAP (Port 143) – Email synchronization  

Can help detect:
- Phishing attempts
- Malicious attachments
- Suspicious sender domains

---

## 3 File Transfer Traffic (FTP / SFTP / SMB)

- FTP (Port 21)
- SFTP (Port 22)
- SMB (Port 445)

Used for transferring files across systems.  
Important for detecting:
- Unauthorized file downloads/uploads
- Data exfiltration
- Lateral movement inside a network

---

## 4 DNS Traffic

- Protocol: DNS (Port 53)
- Used to resolve domain names to IP addresses

Useful for identifying:
- Suspicious domains
- DNS tunneling
- Command-and-Control (C2) communication

---

## 5 Remote Access Traffic

- SSH (Port 22)
- RDP (Port 3389)

Helps detect:
- Unauthorized remote logins
- Brute-force attacks
- Privilege escalation attempts

---

## 6 ICMP Traffic

- Used for ping and network diagnostics
- Can indicate:
  - Network scanning
  - Host discovery
  - ICMP tunneling (in rare cases)

---

## 7 Suspicious / Malicious Traffic Patterns

While analyzing traffic, we observe:

- Repeated connections at fixed intervals (Beaconing)
- Large outbound data transfers (Possible data exfiltration)
- Connections to blacklisted IPs/domains
- Unusual port usage
- High DNS query volume

---

**Q2** Look at the HTTP example: what is the size of the ZIP attachment included in the HTTP response?

![Network Traffic Basics](screenshot2/NTB2.png)

Answer: 10485760 bytes

**Q3** Which attack do attackers use to try to evade an IDS?

Answer : fragmentation

**Q4** What field in the TCP header can we use to detect session hijacking?

![Network Traffic Basics](screenshot2/NTB3.png)

 Answer: sequence number

 ---

## Task 4 — Network Traffic Sources and Flows

##  Network Traffic Sources

Network traffic originates from various devices and services within and outside an organization.

## 1️ End-User Devices
- Laptops
- Desktops
- Mobile devices
- Tablets

These generate traffic through:
- Web browsing
- Email communication
- File downloads/uploads
- Remote access sessions

---

## 2️ Servers
- Web servers
- Application servers
- Database servers
- Mail servers

Servers handle:
- Client requests
- Data storage and retrieval
- API communication
- Authentication services

---

## 3️ Network Infrastructure Devices
- Routers
- Switches
- Firewalls
- Load balancers

These devices generate:
- Routing updates
- ARP traffic
- ICMP messages
- Log and monitoring data

---

## 4️ Cloud Services
- SaaS applications
- Cloud storage
- Virtual machines
- CDN services

Cloud sources may generate:
- API calls
- Sync traffic
- Authentication requests
- External service communication

---

## 5️ External Internet Sources
- Public websites
- Third-party APIs
- Threat actors
- Unknown external IP addresses

These can include:
- Normal inbound requests
- Malicious scanning
- Brute-force attempts
- Command-and-Control (C2) communication

---

## Flow Examples

Let's have a visual look at some of the network flows mentioned above.

### HTTPS

There are different variations of HTTPS network traffic flows. Let's examine a flow where the web proxy does TLS inspection:
A host requests a website; this request is sent to the NGFW, which includes a web proxy. The web proxy will act as the web server and simultaneously establish a new TCP session with the actual web server and forward the clients' requests. When the web proxy receives the answer from the web server, it inspects its contents and then forwards it to the host if deemed safe. To summarize, we have two sessions, one between the client and the proxy and the other between the proxy and the web server. From the client's point of view, it has established a session with the web server.

![Network Traffic Basics](screenshot2/NTB4.png)

### External DNS
DNS traffic within a corporate network starts when a host sends a DNS query. The host sends the query to the internal DNS server on port 53, which will then act on behalf of the host. First, it will check if it has an answer to the query in its cache; if not, it will send the query via the router, through the firewall, to the configured DNS servers. The answer will then follow the same path to the internal DNS server, which will then forward it to the host. The network diagram below shows a simplified flow.

![Network Traffic Basics](screenshot2/NTB5.png)

### SMB with Kerberos

When a host opens a share to, for example, \\FILESERVER\MARKETING, an SMB session is set up. First, authentication is done via Kerberos. When a user logged in on the host, it authenticated with the Key Distribution Center on the Domain Controller and received a Ticket Granting Ticket to request "service authentication tickets". Now, the host requests a service ticket using the Ticket Granting Ticket it received earlier. The host then uses this ticket to establish the SMB connection. Once the SMB session is set up, the host can access the share. Below we see a simplified network diagram of the flow.

![Network Traffic Basics](screenshot2/NTB6.png)

**Q5** Which category of devices generates the most traffic in a network?

Answer: endpoint devices

**Q6** Before an SMB session can be established, which service needs to be contacted first for authentication?

![Network Traffic Basics](screenshot2/NTB6.png)

 Answer: Kerberos

 **Q7** What does TLS stand for?

 Answer: Transport Layer Security

 ---

 ## Task 5 — How can we observe network traffic?

**Q8** What is the flag found in the HTTP traffic in scenario 1?

How it was found (step-by-step)

- Open the static lab page and click Start.
- Drag the topology file onto the diagram and locate the WP1 device (or follow the lab instructions to start the simulated capture).

![Network Traffic Basics](screenshot2/NTB7.png)

Click through the packet table pages (paging button) until the last page. On the last page, last row shows the HTTP GET for 200 OK (application/zip) with a size of 10485760.

![Network Traffic Basics](screenshot2/NTB8.png)

- Expand that row and view the Body Preview the captured HTTP response body contains the flag:

Answer:  THM{FoundTheMalware}

