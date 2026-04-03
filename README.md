# 📡 Network Traffic Analysis & Threat Detection using Wireshark

## 🔍 Problem Statement

Understanding real network behavior and detecting malicious activity is a critical skill for cybersecurity and cloud security engineers. Most learners rely on theoretical knowledge without analyzing real packet-level data.

This project focuses on analyzing live network traffic using Wireshark to understand protocol behavior and detect common attack patterns.

---

## 🎯 Objectives

* Understand TCP/IP, DNS, and TLS at packet level
* Analyze real network traffic
* Identify normal vs suspicious behavior
* Detect common attacks:

  * Port Scanning
  * DNS Tunneling patterns
  * SYN Flood (DoS)

---

## 🏗️ Architecture Overview

```
User Action (Browser / CLI)
        ↓
Network Traffic Generated
        ↓
Wireshark Capture Interface
        ↓
Packet Analysis (DNS / TCP / TLS)
        ↓
Pattern Detection
        ↓
Security Insights
```

---

## 🧠 Methodology

### Phase 1: Traffic Observation

Captured normal traffic and identified:

* DNS resolution
* TCP 3-way handshake
* TLS handshake

---

### Phase 2: Packet Dissection

#### 🌐 IP Layer

* TTL (hop-based lifetime)
* Protocol identification
* Fragmentation flags

#### 🔗 TCP Layer

* Sequence & Acknowledgment numbers
* Window size (flow control)
* Flags (SYN, ACK, RST)

#### 📡 DNS Layer

* Query/Response structure
* Recursion flags (RD, RA)
* TTL for caching

---

### Phase 3: Attack Simulation & Detection

#### 🚨 1. Port Scanning (Nmap)

**Command:**

```bash
nmap scanme.nmap.org
```

**Observations:**

* Multiple SYN packets sent
* Different destination ports targeted
* SYN-ACK (open ports) vs RST (closed ports)
* Incomplete TCP handshake

**Detection Logic:**
**Port Scan**
* Multiple SYN packets from single source
* Different destination ports
* No handshake completion

**Analysis:**
Multiple SYN packets across ports indicate a SYN scan used to identify open services.

---

#### 🚨 2. DNS Suspicious Traffic

**Command:**

```bash
nslookup verylongrandomstringexampletestdomain123456.com
```

**Observations:**

* Long and random domain names
* Repeated DNS queries
* NXDOMAIN responses

**Detection Logic:**
**DNS Tunneling**
* Long/random domain names
* Repeated queries
* NXDOMAIN responses

**Analysis:**
Such patterns may indicate DNS tunneling or data exfiltration via encoded subdomains.

---

#### 🚨 3. SYN Flood Attack

**Command:**

```bash
hping3 -S --flood --rand-source -p 80 <target-ip>
```

**Observations:**

* Extremely high volume of SYN packets
* Random source IPs (spoofed)
* No TCP handshake completion

**Detection Logic:**
**SYN Flood**
* High rate of SYN packets
* Random source IPs
* Half-open connections

**Analysis:**
Indicates a SYN flood attack where half-open connections exhaust server resources.

---

## 📊 Key Findings

* Network communication flow:

  ```
  DNS → TCP → TLS → Encrypted Data
  ```

* Packet-level analysis helps identify:

  * Connection states
  * Service availability
  * Attack patterns

---

## ⚠️ Limitations

* Encrypted traffic cannot be inspected without decryption
* Manual analysis (not automated)
* Limited to local lab environment

---

## 🔐 Security Learnings

* Networks are highly observable at packet level
* TLS encryption protects sensitive data
* Attack patterns can be identified through traffic behavior

---

## 🧰 Tools Used

* Wireshark
* Nmap
* hping3

---

## ⚖️ Ethical Considerations

All testing was performed in a controlled lab environment (local system/network). No unauthorized scanning was conducted.
