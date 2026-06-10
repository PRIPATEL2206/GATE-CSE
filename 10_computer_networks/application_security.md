# Application Layer & Network Security Basics

> Subject: Computer Networks
> GATE weight: **2–3 marks** every year. HTTP/DNS/SMTP/FTP, TLS/SSL, firewall, common attacks.

---

## 1. Concept Explanation

### 1.1 Application Layer

Top of TCP/IP stack. Provides services to user applications.

### 1.2 Common Application Protocols

| Protocol | Port | Transport | Purpose |
|---|---|---|---|
| HTTP | 80 | TCP | Web |
| HTTPS | 443 | TCP | Secure web |
| FTP | 20 (data), 21 (control) | TCP | File transfer |
| SMTP | 25 | TCP | Email send |
| POP3 | 110 | TCP | Email retrieve |
| IMAP | 143 | TCP | Email |
| DNS | 53 | UDP (small), TCP (zone transfer) | Name resolution |
| DHCP | 67 (server), 68 (client) | UDP | Auto-config |
| SSH | 22 | TCP | Secure shell |
| Telnet | 23 | TCP | Remote login |
| TFTP | 69 | UDP | Trivial FTP |
| SNMP | 161 | UDP | Network management |
| NTP | 123 | UDP | Time |

### 1.3 HTTP

| Feature | Description |
|---|---|
| Stateless | Each request independent |
| Methods | GET, POST, PUT, DELETE, HEAD, OPTIONS, PATCH |
| Status codes | 1xx info, 2xx success, 3xx redirect, 4xx client error, 5xx server error |
| Persistent connection | HTTP/1.1 keep-alive |
| HTTP/2 | Multiplexing, header compression |
| HTTP/3 | QUIC over UDP |

### 1.4 HTTP Status Codes

| Code | Meaning |
|---|---|
| 200 | OK |
| 301 | Moved Permanently |
| 302 | Found / Temporary Redirect |
| 304 | Not Modified |
| 400 | Bad Request |
| 401 | Unauthorized |
| 403 | Forbidden |
| 404 | Not Found |
| 500 | Internal Server Error |
| 502 | Bad Gateway |
| 503 | Service Unavailable |

### 1.5 DNS (Domain Name System)

Hierarchical name resolution: hostname → IP.

**Hierarchy:**
- Root.
- TLD (top-level: .com, .org, country codes).
- Authoritative.

### 1.6 DNS Query Types

| Type | Description |
|---|---|
| A | IPv4 address |
| AAAA | IPv6 |
| CNAME | Alias |
| MX | Mail server |
| NS | Authoritative name server |
| TXT | Text records |
| PTR | Reverse lookup |
| SOA | Start of Authority |

### 1.7 DNS Resolution Process

1. Local cache check.
2. Query local DNS server (recursive).
3. Server queries root, TLD, authoritative iteratively.
4. Answer returned, cached.

**Iterative vs Recursive:**
- Iterative: each server returns next-level server.
- Recursive: server fetches all and returns final.

### 1.8 Email Architecture

```
User → Mail User Agent (MUA) → SMTP → Mail Transfer Agent (MTA)
       → MTA → ... → Recipient MTA
       Recipient: POP3/IMAP → MUA
```

| Protocol | Direction |
|---|---|
| SMTP | Send |
| POP3 | Retrieve (download + delete) |
| IMAP | Retrieve (server-stored) |

### 1.9 FTP

Two channels:
- Control (port 21): commands.
- Data (port 20): file transfer.

**Modes:** active vs passive.

### 1.10 Web Caching / Proxies

**Cache** stores recent responses for reuse.
**Proxy server** intermediary; forwards requests.

Benefits: reduce load, latency, bandwidth.

### 1.11 TLS/SSL

**Transport Layer Security:** secures TCP communication.

**Handshake:**
1. Client Hello (cipher suites, random).
2. Server Hello (chosen suite, certificate, random).
3. Key exchange.
4. Finished.

Provides:
- **Confidentiality** (symmetric encryption).
- **Integrity** (HMAC).
- **Authentication** (certificates).

### 1.12 Public Key Infrastructure (PKI)

| Component | Description |
|---|---|
| Certificate Authority (CA) | Issues certificates |
| Certificate | Binds public key to identity |
| Chain of trust | Intermediate CAs |
| Certificate revocation | CRL, OCSP |

### 1.13 Common Network Attacks

| Attack | Description |
|---|---|
| **Sniffing** | Capture packets |
| **Spoofing** | Pretend to be another |
| **Man-in-the-Middle (MITM)** | Intercept + modify |
| **DoS / DDoS** | Overwhelm with traffic |
| **SYN flood** | TCP-specific DoS |
| **DNS poisoning** | Bad DNS replies |
| **ARP spoofing** | Bad ARP replies |
| **Phishing** | Fake site / email |
| **SQL injection** | Malicious SQL |
| **XSS** | Malicious scripts in web pages |
| **Buffer overflow** | Memory corruption |
| **Replay** | Resend captured |
| **Session hijacking** | Steal session token |

### 1.14 Firewalls

| Type | Description |
|---|---|
| **Packet filtering** | Per-packet rules |
| **Stateful** | Connection-aware |
| **Application proxy** | Application-layer inspection |
| **NAT firewall** | Hides internal IPs |

### 1.15 IDS / IPS

- **IDS (Intrusion Detection):** detect; alert.
- **IPS (Intrusion Prevention):** detect + block.

### 1.16 VPN

Encrypted tunnel over public network. Common: IPsec, OpenVPN, WireGuard.

### 1.17 Cryptography Recap

(See [io_protection.md](../08_operating_systems/io_protection.md) for OS-level treatment.)

| Type | Examples |
|---|---|
| Symmetric | AES, DES, 3DES |
| Asymmetric | RSA, ECC, DH |
| Hash | SHA-256, MD5 (broken) |
| MAC | HMAC |
| Signature | RSA-SHA, ECDSA |

### 1.18 Common Cryptographic Protocols

| Protocol | Purpose |
|---|---|
| TLS | Web security |
| IPsec | Network layer security |
| SSH | Secure remote shell |
| WPA2/3 | Wi-Fi security |
| Kerberos | Authentication |

### 1.19 SOCKS, Web Cookies, CDN

- **SOCKS:** generic proxy protocol.
- **Cookies:** state in HTTP (HTTP is stateless).
- **CDN:** content delivery network for low-latency access.

### 1.20 IPv6 Application Considerations

Most application protocols extend to IPv6. DNS uses AAAA records.

> **Summary:** Application protocols use TCP/UDP. HTTP stateless; DNS hierarchical. TLS provides confidentiality/integrity/authentication via PKI. Firewalls enforce policy. Common attacks: sniffing, MITM, DoS, injections.

---

## 2. Important Points

- **HTTP** stateless; uses cookies for state.
- **HTTPS** = HTTP over TLS.
- **DNS** hierarchical; UDP usually (53).
- **SMTP** sends; **POP3/IMAP** retrieves.
- **FTP** uses 2 ports (control 21, data 20).
- **TLS handshake** establishes secure channel.
- **PKI**: CAs issue certificates.
- **DDoS**: distributed denial of service.
- **SQL injection** via input sanitization.
- **XSS** via malicious scripts.
- **Firewall** types: packet, stateful, app proxy.
- **VPN** = encrypted tunnel.
- **HTTP/2** multiplexes; **HTTP/3** uses QUIC over UDP.

---

## 3. Short Notes

```
APPLICATION PROTOCOLS
 HTTP 80, HTTPS 443
 FTP 20/21
 SMTP 25, POP3 110, IMAP 143
 DNS 53 UDP
 DHCP 67/68 UDP
 SSH 22, Telnet 23
 SNMP 161 UDP, NTP 123 UDP

HTTP
 stateless, methods (GET/POST/PUT/DELETE)
 status: 1xx, 2xx, 3xx, 4xx, 5xx
 200, 301, 302, 304, 400, 401, 403, 404, 500, 502, 503
 HTTP/1.1 keep-alive
 HTTP/2 multiplex
 HTTP/3 QUIC over UDP

DNS
 hierarchy: root → TLD → authoritative
 record types: A, AAAA, CNAME, MX, NS, TXT, PTR, SOA
 iterative vs recursive

EMAIL
 SMTP send; POP3/IMAP retrieve
 MUA → MTA → … → MTA → MUA

FTP: 2 channels (control 21, data 20); active/passive

WEB CACHING / PROXY
 reduce load, latency, bandwidth

TLS/SSL
 handshake: client hello, server hello, key exchange, finished
 confidentiality + integrity + authentication

PKI: CA, certificate, chain, revocation

ATTACKS
 sniffing, spoofing, MITM, DoS/DDoS,
 SYN flood, DNS poisoning, ARP spoof,
 phishing, SQL injection, XSS, buffer overflow,
 replay, session hijack

FIREWALLS
 packet filter / stateful / app proxy / NAT firewall

IDS / IPS: detect / prevent

VPN: encrypted tunnel (IPsec, WireGuard, OpenVPN)

CRYPTO
 symmetric (AES, DES)
 asymmetric (RSA, ECC, DH)
 hash (SHA-256)
 MAC (HMAC)
 signature (RSA-SHA, ECDSA)

PROTOCOLS: TLS, IPsec, SSH, WPA2, Kerberos
```

---

## 4. Formulas / Tricks

| # | Rule | Memorize Cold? |
|---|---|---|
| 1 | HTTP 80; HTTPS 443; SSH 22; FTP 20/21; SMTP 25; DNS 53 | ✅✅✅ |
| 2 | HTTP stateless | ✅✅ |
| 3 | DNS hierarchical | ✅ |
| 4 | TLS provides confidentiality + integrity + authentication | ✅✅ |
| 5 | PKI uses CAs | ✅ |
| 6 | DDoS distributed | ✅ |
| 7 | SQL injection / XSS web vulns | ✅ |
| 8 | Firewall types | ✅ |
| 9 | VPN tunnel | ✅ |
| 10 | DHCP DORA | ✅ |

### Tricks

- **Memorize port numbers** (HTTP 80, HTTPS 443, SSH 22, FTP 20/21, DNS 53, SMTP 25, IMAP 143, POP3 110).
- **HTTP status family from first digit:** 2xx ok, 3xx redirect, 4xx client, 5xx server.
- **DNS** uses UDP for small queries, TCP for zone transfers.
- **TLS handshake** = key exchange + auth + cipher negotiation.
- **For attack identification:** match by description.

---

## 5. PYQs (with solutions)

### Q1. (GATE CSE 2017)
HTTP port:
**Solution.** 80.

### Q2. (GATE CSE 2014)
HTTPS port:
**Solution.** 443.

### Q3. (GATE CSE 2018)
DNS port:
**Solution.** 53.

### Q4. (GATE CSE 2008)
SMTP for:
**Solution.** Sending email.

### Q5. (GATE CSE 2010)
HTTP status 404:
**Solution.** Not Found.

### Q6. (GATE CSE 2015)
TLS provides:
**Solution.** Confidentiality, integrity, authentication.

### Q7. (GATE CSE 2013)
SQL injection prevention:
**Solution.** Input sanitization, prepared statements.

### Q8. (GATE CSE 2007)
Firewall types:
**Solution.** Packet filter, stateful, app proxy, NAT.

### Q9. (GATE CSE 2003)
DNS resolution:
**Solution.** Hierarchical; iterative or recursive.

### Q10. (GATE CSE 2009)
HTTP method to update:
**Solution.** PUT or PATCH.

### Q11. (GATE CSE 2019)
DDoS attack:
**Solution.** Distributed denial of service.

### Q12. (GATE CSE 2020)
Asymmetric crypto for:
**Solution.** Key exchange, signature.

### Q13. (GATE CSE 2021)
HTTP/2 features:
**Solution.** Multiplexing, header compression.

### Q14. (GATE CSE 2016)
SYN flood:
**Solution.** TCP SYN packets to exhaust connection table.

### Q15. (GATE CSE 2011)
DNS record types:
**Solution.** A, AAAA, CNAME, MX, NS, etc.

---

## 6. Practice Questions (20+)

### Easy

**P1.** HTTP port.

**P2.** HTTPS port.

**P3.** SSH port.

**P4.** FTP ports.

**P5.** DNS port.

**P6.** DNS hierarchy.

**P7.** Email send protocol.

**P8.** TLS purpose.

**P9.** SQL injection.

**P10.** XSS.

### Medium

**P11.** HTTP request format.

**P12.** HTTP response codes by class.

**P13.** DNS query types (A, MX, CNAME).

**P14.** TLS handshake steps.

**P15.** Firewall types.

**P16.** Compare POP3 vs IMAP.

**P17.** SYN flood mechanism.

**P18.** Buffer overflow defense.

**P19.** VPN protocols.

**P20.** Symmetric vs asymmetric crypto.

### Hard

**P21.** Detailed TLS handshake.

**P22.** PKI chain of trust.

**P23.** Detect MITM attack.

**P24.** Implement basic firewall rules.

**P25.** DNS poisoning scenario.

**P26.** HTTP/3 QUIC features.

**P27.** Stateless web with cookies + sessions.

---

### Answers + Brief Solutions

| # | Answer | Hint |
|---|---|---|
| P1 | 80 | direct |
| P2 | 443 | direct |
| P3 | 22 | direct |
| P4 | 20, 21 | direct |
| P5 | 53 | direct |
| P6 | root → TLD → auth | direct |
| P7 | SMTP | direct |
| P8 | secure transport | direct |
| P9 | input as code | direct |
| P10 | inject scripts | direct |
| P11 | method URI HTTP/1.1 + headers | direct |
| P12 | as in 1.4 | direct |
| P13 | A=IPv4, MX=mail, CNAME=alias | direct |
| P14 | client/server hello + key + finished | direct |
| P15 | packet/stateful/proxy/NAT | direct |
| P16 | download vs server-side | direct |
| P17 | many SYN, no ACK | direct |
| P18 | stack canary, ASLR, NX | direct |
| P19 | IPsec, WireGuard, OpenVPN | direct |
| P20 | speed vs key distribution | direct |
| P21 | full sequence | direct |
| P22 | root CA → intermediate → leaf | direct |
| P23 | certificate validation | direct |
| P24 | iptables example | direct |
| P25 | bad DNS reply | direct |
| P26 | UDP-based, multi-stream | direct |
| P27 | session ID via cookie | direct |

---

## 7. Mistakes

| # | Trap | How to avoid |
|---|---|---|
| 1 | HTTP stateful | It's stateless. |
| 2 | DNS only TCP | Mostly UDP. |
| 3 | SMTP retrieves | It sends. |
| 4 | TLS only encrypts | Also auth + integrity. |
| 5 | DDoS = DoS | Distributed. |
| 6 | SQL injection at app layer only | DB layer too. |
| 7 | Firewall blocks all | Selective. |
| 8 | VPN is unencrypted tunnel | Encrypted by definition. |
| 9 | HTTPS port 80 | 443. |
| 10 | DNS port 80 | 53. |

---

## 8. Pattern Recognition

| If question says... | Then... |
|---|---|
| "Port number" | Map protocol to port. |
| "HTTP status" | First-digit class. |
| "DNS" | Hierarchical resolution. |
| "Email send/retrieve" | SMTP / POP3, IMAP. |
| "TLS" | Confidentiality + integrity + auth. |
| "PKI" | Certificate-based trust. |
| "SQL injection / XSS" | Web vulnerabilities. |
| "Firewall type" | 4 types. |
| "VPN" | Encrypted tunnel. |
| "Symmetric vs asymmetric" | Speed vs key distribution. |

---

## 9. Quick Revision

```
APPLICATION PROTOCOLS
 HTTP 80, HTTPS 443
 FTP 20/21, SMTP 25, POP3 110, IMAP 143
 DNS 53 UDP, DHCP 67/68 UDP
 SSH 22, Telnet 23, SNMP 161 UDP, NTP 123 UDP

HTTP
 stateless; methods (GET/POST/PUT/DELETE)
 status: 1xx, 2xx, 3xx, 4xx, 5xx
 HTTP/1.1 keep-alive; HTTP/2 multiplex; HTTP/3 QUIC

DNS
 hierarchy: root → TLD → authoritative
 records: A, AAAA, CNAME, MX, NS, TXT, PTR
 iterative or recursive

EMAIL
 SMTP send; POP3/IMAP retrieve

FTP: 2 channels (control 21, data 20)

TLS
 handshake: client/server hello + key + finished
 confidentiality + integrity + authentication

PKI: CAs, certificate chain, revocation

ATTACKS
 sniff, spoof, MITM, DoS/DDoS,
 SYN flood, DNS poisoning, ARP spoof,
 phishing, SQL injection, XSS, buffer overflow

FIREWALLS: packet / stateful / proxy / NAT

VPN: IPsec / WireGuard / OpenVPN

CRYPTO
 symmetric (AES), asymmetric (RSA), hash (SHA-256), MAC, signature
```
