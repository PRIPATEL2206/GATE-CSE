# Network Layer (IPv4, Routing, ICMP, NAT)

> Subject: Computer Networks
> GATE weight: **3–5 marks** every year. IPv4 addressing, subnetting, routing algorithms, ICMP/NAT.

---

## 1. Concept Explanation

### 1.1 Network Layer Functions

- **Logical addressing** (IP).
- **Routing** between networks.
- **Forwarding** packets at routers.
- **Fragmentation/reassembly.**
- **Best-effort delivery** (IP is connectionless).

### 1.2 IPv4 Address

32 bits, written in dotted decimal: `192.168.1.1`.

**Total addresses:** 2³² ≈ 4.3 billion.

### 1.3 Classful Addressing (legacy)

| Class | First octet | Default mask | # networks | # hosts |
|---|---|---|---|---|
| A | 0–127 | /8 | 128 | 16M |
| B | 128–191 | /16 | 16K | 65K |
| C | 192–223 | /24 | 2M | 254 |
| D (multicast) | 224–239 | — | — | — |
| E (reserved) | 240–255 | — | — | — |

### 1.4 CIDR (Classless Inter-Domain Routing)

`a.b.c.d/n` — n bits = network prefix.

Example: `192.168.1.0/24` → 256 addresses.

### 1.5 Subnetting

Borrow host bits → create subnets.

**# subnets** = 2^(borrowed bits).
**# hosts/subnet** = 2^(remaining host bits) − 2 (network + broadcast).

**Example:** /24 split into /26: 4 subnets × 62 hosts each.

### 1.6 Subnet Mask

`/24` = 255.255.255.0
`/26` = 255.255.255.192
`/30` = 255.255.255.252

### 1.7 Special Addresses

| Address | Purpose |
|---|---|
| 0.0.0.0/8 | "This network" |
| 127.0.0.0/8 | Loopback |
| 169.254.0.0/16 | Link-local |
| 224.0.0.0/4 | Multicast |
| 255.255.255.255 | Broadcast |
| Network address (all host bits 0) | Identify subnet |
| Broadcast (all host bits 1) | Subnet broadcast |

### 1.8 Private Address Ranges (RFC 1918)

| Class | Range |
|---|---|
| A | 10.0.0.0 – 10.255.255.255 (/8) |
| B | 172.16.0.0 – 172.31.255.255 (/12) |
| C | 192.168.0.0 – 192.168.255.255 (/16) |

### 1.9 IPv4 Header (20+ bytes)

```
| Ver(4) | IHL(4) | TOS(8) | Total Len(16) |
| Identification(16)  | Flags(3) | Frag Offset(13) |
| TTL(8) | Protocol(8) | Header Checksum(16) |
| Src IP (32) |
| Dst IP (32) |
| Options (0–40) |
| Data |
```

| Field | Description |
|---|---|
| Ver | 4 (IPv4) |
| IHL | Header length in 32-bit words (5–15) |
| TOS | Type of Service |
| Total Length | header + data |
| ID, Flags, Frag Offset | Fragmentation |
| TTL | Hop limit |
| Protocol | 6 = TCP, 17 = UDP |
| Header Checksum | Header integrity |

### 1.10 Fragmentation

If MTU < packet size, router fragments.
- **DF flag:** don't fragment.
- **MF flag:** more fragments.
- **Fragment Offset:** in 8-byte units.

Reassembly at destination only.

**Total fragments** = ⌈(packet_size − header) / max_data_per_fragment⌉.

### 1.11 Routing Concepts

| Term | Description |
|---|---|
| **Routing table** | Maps destination → next hop |
| **Default route** | Used when no specific match |
| **Longest prefix match** | Most specific route wins |
| **Static routing** | Manually configured |
| **Dynamic routing** | Protocol-based |

### 1.12 Routing Algorithms

| Algorithm | Approach |
|---|---|
| **Distance Vector (DV)** | Bellman-Ford; share distances with neighbors |
| **Link State (LS)** | Each node knows full topology; Dijkstra |
| **Path Vector** | Like DV but full path (BGP) |

### 1.13 Distance Vector Routing

Each router maintains distance vector to all destinations. Periodically share with neighbors.

**Issues:**
- **Count to infinity:** slow convergence on link failure.
- **Solutions:** split horizon, poisoned reverse.

**Protocols:** RIP (max 15 hops).

### 1.14 Link State Routing

Each router floods link state to all. Run **Dijkstra** locally.

**Protocols:** OSPF, IS-IS.

### 1.15 Path Vector Routing

Used between **autonomous systems** (BGP).

Carries entire path; avoids loops.

### 1.16 ICMP (Internet Control Message Protocol)

Error and diagnostic messages over IP.

| Type | Purpose |
|---|---|
| Echo Request/Reply | `ping` |
| Destination Unreachable | Various codes |
| Time Exceeded | `traceroute`; TTL = 0 |
| Redirect | Better gateway |
| Source Quench | (deprecated) |

### 1.17 NAT (Network Address Translation)

Map internal private IPs to single (or few) public IPs.

| Type | Description |
|---|---|
| **Static NAT** | 1:1 mapping |
| **Dynamic NAT** | Pool of public IPs |
| **PAT (NAPT)** | Many-to-one via port numbers |

Allows private networks to share public IP.

### 1.18 DHCP (Dynamic Host Configuration Protocol)

Automates IP assignment.

**Process (DORA):**
1. **Discover** (broadcast).
2. **Offer** (server).
3. **Request** (client picks).
4. **ACK** (server).

### 1.19 DNS Overview (preview, full in app/security)

Maps hostname → IP via hierarchical query.

### 1.20 IPv6

128-bit addresses.
- No fragmentation by routers (only sender).
- No header checksum.
- Streamlined header.

Format: `2001:0db8::1` (groups of 16-bit hex).

### 1.21 Subnetting Calculations

For `192.168.1.0/26`:
- Block size = 64.
- Subnets: 192.168.1.0, 192.168.1.64, 192.168.1.128, 192.168.1.192.
- Each: 62 hosts (64 − 2).

### 1.22 Common GATE Patterns

- Subnet calculations (block size, hosts).
- Route table lookup (longest prefix).
- Fragmentation (# fragments).
- ICMP message types.
- NAT scenario.

> **Summary:** IPv4 32-bit; CIDR /n. Subnetting: borrow bits, compute hosts. Routing: DV (RIP), LS (OSPF), PV (BGP). ICMP for diagnostics. NAT shares public IPs.

---

## 2. Important Points

- **IPv4** = 32 bits; **IPv6** = 128 bits.
- **CIDR** /n means n network bits.
- **Hosts per subnet** = 2^(host bits) − 2.
- **# subnets** = 2^(borrowed bits).
- **TTL** decremented at each hop.
- **MF flag** indicates more fragments.
- **Fragment offset** in 8-byte units.
- **Distance vector** → RIP.
- **Link state** → OSPF (Dijkstra).
- **Path vector** → BGP.
- **ICMP** used by ping, traceroute.
- **NAT** allows private addressing.
- **DHCP DORA** for IP assignment.
- **Longest prefix match** in routing.

---

## 3. Short Notes

```
NETWORK LAYER FUNCTIONS
 logical addressing, routing, forwarding,
 fragmentation, best-effort delivery

IPv4
 32 bits; dotted decimal
 4.3 billion addresses

CLASSFUL (legacy)
 A: 0-127 /8
 B: 128-191 /16
 C: 192-223 /24
 D: 224-239 multicast
 E: 240-255 reserved

CIDR /n: n network bits
hosts/subnet = 2^host_bits − 2
# subnets = 2^borrowed_bits

PRIVATE ADDRESSES (RFC 1918)
 10/8, 172.16/12, 192.168/16

SPECIAL
 127/8 loopback
 0.0.0.0 default
 255.255.255.255 broadcast
 169.254/16 link-local
 224/4 multicast

IPv4 HEADER (20 bytes min)
 Ver, IHL, TOS, Total Length
 ID, Flags, Frag Offset
 TTL, Protocol, Checksum
 Src IP, Dst IP

PROTOCOL: 6 = TCP, 17 = UDP

FRAGMENTATION
 DF (don't), MF (more), Frag Offset (8-byte units)

ROUTING ALGORITHMS
 distance vector (Bellman-Ford): RIP
 link state (Dijkstra): OSPF
 path vector: BGP

DV ISSUES: count to infinity
 fixes: split horizon, poisoned reverse

ICMP
 echo (ping), time exceeded (traceroute),
 dest unreachable, redirect

NAT
 static, dynamic, PAT (NAPT)
 allows private network sharing public IP

DHCP DORA
 Discover, Offer, Request, ACK

IPv6: 128 bits; no router fragmentation; no header checksum

ROUTING TABLE: longest prefix match
```

---

## 4. Formulas / Tricks

| # | Rule | Memorize Cold? |
|---|---|---|
| 1 | IPv4 = 32 bits; IPv6 = 128 bits | ✅✅ |
| 2 | Hosts per /n = 2^(32-n) − 2 | ✅✅✅ |
| 3 | Block size = 2^(32-n) | ✅✅ |
| 4 | Mask /24 = 255.255.255.0 | ✅✅ |
| 5 | Default routes table format | ✅ |
| 6 | RIP DV; OSPF LS; BGP PV | ✅✅ |
| 7 | DV count to infinity | ✅ |
| 8 | TTL decrements per hop | ✅✅ |
| 9 | ICMP types (echo, time exceeded) | ✅ |
| 10 | NAT for sharing public IP | ✅ |
| 11 | DHCP DORA | ✅ |
| 12 | Longest prefix match | ✅✅ |

### Tricks

- **Subnet block size:** 2^(32-n). Subnets are spaced by block size.
- **For broadcast address:** all host bits = 1.
- **For routing table lookup:** check most specific (longest prefix) first.
- **For fragmentation:** ⌈(payload) / (max per fragment)⌉; offset in 8-byte units.
- **For ICMP:** error generates ICMP message back to source.
- **For NAT scenario:** PAT uses port numbers to distinguish.

---

## 5. PYQs (with solutions)

### Q1. (GATE CSE 2017)
Hosts in /27:
**Solution.** 2^(32−27) − 2 = 30.

### Q2. (GATE CSE 2014)
RIP routing algorithm:
**Solution.** Distance vector.

### Q3. (GATE CSE 2018)
OSPF uses:
**Solution.** Link state (Dijkstra).

### Q4. (GATE CSE 2008)
TTL purpose:
**Solution.** Limits hops; prevents loops.

### Q5. (GATE CSE 2010)
Fragment offset units:
**Solution.** 8-byte units.

### Q6. (GATE CSE 2015)
ICMP traceroute uses:
**Solution.** Time exceeded (TTL = 0) messages.

### Q7. (GATE CSE 2013)
192.168.1.0/24 — # hosts:
**Solution.** 254.

### Q8. (GATE CSE 2007)
Class C default mask:
**Solution.** /24 = 255.255.255.0.

### Q9. (GATE CSE 2003)
NAT type 1:1:
**Solution.** Static NAT.

### Q10. (GATE CSE 2009)
DHCP DORA:
**Solution.** Discover, Offer, Request, ACK.

### Q11. (GATE CSE 2019)
IPv6 size:
**Solution.** 128 bits.

### Q12. (GATE CSE 2020)
Longest prefix match used in:
**Solution.** Routing table lookup.

### Q13. (GATE CSE 2021)
BGP type:
**Solution.** Path vector.

### Q14. (GATE CSE 2016)
Default gateway:
**Solution.** Used when no specific route.

### Q15. (GATE CSE 2011)
Count-to-infinity in DV:
**Solution.** Slow convergence after link failure; fixed by split horizon / poisoned reverse.

---

## 6. Practice Questions (20+)

### Easy

**P1.** IPv4 address size.

**P2.** /24 hosts.

**P3.** RIP type.

**P4.** OSPF type.

**P5.** TTL purpose.

**P6.** Private IP ranges.

**P7.** Loopback address.

**P8.** Default gateway.

**P9.** ICMP example.

**P10.** NAT purpose.

### Medium

**P11.** Subnet 192.168.1.0/24 into /26 — # subnets and hosts/subnet.

**P12.** Compute # fragments for 4500 byte packet, MTU 1500.

**P13.** Apply longest prefix match: routes /24, /16, /8.

**P14.** Distance vector after one round.

**P15.** Identify ICMP for `ping`.

**P16.** Convert 192.168.1.5/26 to network address.

**P17.** Calculate broadcast address for /25.

**P18.** DHCP renewal timing.

**P19.** Trace `traceroute` ICMP messages.

**P20.** NAT scenario: 5 private hosts → 1 public.

### Hard

**P21.** Detailed subnet planning for org.

**P22.** Compare RIP vs OSPF.

**P23.** Apply Dijkstra on link state.

**P24.** Detect routing loop in DV.

**P25.** IPv6 prefix.

**P26.** Implement NAT table.

**P27.** Multi-level subnetting.

---

### Answers + Brief Solutions

| # | Answer | Hint |
|---|---|---|
| P1 | 32 bits | direct |
| P2 | 254 | direct |
| P3 | DV | direct |
| P4 | LS | direct |
| P5 | hop limit | direct |
| P6 | 10/8, 172.16/12, 192.168/16 | direct |
| P7 | 127.0.0.1 | direct |
| P8 | route for unmatched | direct |
| P9 | ping | direct |
| P10 | private to public mapping | direct |
| P11 | 4 subnets, 62 hosts | direct |
| P12 | trace fragmentation | direct |
| P13 | /24 most specific | direct |
| P14 | trace | direct |
| P15 | echo request/reply | direct |
| P16 | 192.168.1.0 | direct |
| P17 | for /25 of 192.168.1.0: 192.168.1.127 | direct |
| P18 | T1 = 50% lease | direct |
| P19 | TTL 1, 2, ..., dest reached | direct |
| P20 | PAT | direct |
| P21 | recursive subnetting | direct |
| P22 | speed vs simplicity | direct |
| P23 | Dijkstra | direct |
| P24 | bad metric propagation | direct |
| P25 | /64 typical | direct |
| P26 | maintain mappings | direct |
| P27 | VLSM | direct |

---

## 7. Mistakes

| # | Trap | How to avoid |
|---|---|---|
| 1 | Forgetting -2 hosts | Subnet has network + broadcast. |
| 2 | RIP = OSPF | Different algorithms. |
| 3 | TTL is in seconds | It's hop count. |
| 4 | NAT requires multiple public IPs | PAT shares one. |
| 5 | Fragmentation reassembly at routers | Only at destination. |
| 6 | ICMP at transport layer | Network layer. |
| 7 | IPv6 has fragmentation by routers | Only by sender. |
| 8 | DHCP unicast | Discover is broadcast. |
| 9 | Path vector = link state | Different. |
| 10 | Static routing dynamic | Static is manual. |

---

## 8. Pattern Recognition

| If question says... | Then... |
|---|---|
| "Hosts in /n" | 2^(32-n) − 2. |
| "Subnet block size" | 2^(32-n). |
| "Routing algorithm DV/LS/PV" | RIP/OSPF/BGP. |
| "ICMP" | Network-layer diagnostics. |
| "NAT" | Private to public translation. |
| "TTL" | Hop limit. |
| "Fragmentation" | If MTU smaller than packet. |
| "Longest prefix match" | Routing decision. |
| "DHCP" | DORA process. |
| "Count-to-infinity" | DV problem. |

---

## 9. Quick Revision

```
IPv4 = 32 bits; CIDR /n
hosts/subnet = 2^(32-n) − 2
block size = 2^(32-n)

CLASSFUL (legacy): A /8, B /16, C /24

PRIVATE: 10/8, 172.16/12, 192.168/16
SPECIAL: 127/8 loopback, 0.0.0.0 default

IPv4 HEADER (20 B min)
 ver, IHL, TOS, total len
 ID, flags, frag offset
 TTL, protocol, checksum
 src IP, dst IP

PROTOCOL: 6=TCP, 17=UDP

FRAGMENTATION
 DF / MF flags
 frag offset (8-byte units)

ROUTING
 DV (Bellman-Ford): RIP
 LS (Dijkstra): OSPF
 PV: BGP

DV count-to-infinity → split horizon / poisoned reverse

ICMP: ping (echo), traceroute (time exceeded)

NAT: static / dynamic / PAT (NAPT)

DHCP: DORA (Discover, Offer, Request, ACK)

LONGEST PREFIX MATCH

IPv6: 128 bits; no router fragmentation
```
