# LAN Technologies, Switching & MAC

> Subject: Computer Networks
> GATE weight: **2–4 marks** every year. Ethernet, CSMA/CD, switching, ARP, VLAN.

---

## 1. Concept Explanation

### 1.1 LAN (Local Area Network)

Network covering small geographic area (building, campus). Common technologies:
- **Ethernet** (IEEE 802.3) — wired, dominant.
- **Wi-Fi** (IEEE 802.11) — wireless.
- **Token Ring** (legacy).
- **FDDI** (legacy fiber).

### 1.2 Ethernet Frame Format

```
| Preamble (7) | SFD (1) | Dst MAC (6) | Src MAC (6) | Type (2) | Data (46-1500) | FCS (4) |
```

- **MAC address:** 48 bits = 6 bytes.
- **Type/Length:** identifies upper protocol or length.
- **Min frame size:** 64 bytes (without preamble) for collision detection.
- **Max payload:** 1500 bytes (MTU).

### 1.3 MAC Address

48-bit globally unique address per NIC.

Format: `00:1A:2B:3C:4D:5E` (hex).

First 24 bits = OUI (manufacturer ID).
Last 24 bits = device-specific.

**Special:**
- All 1's (FF:FF:FF:FF:FF:FF) = broadcast.
- First octet bit set = multicast.

### 1.4 MAC Sublayers

| Sublayer | Description |
|---|---|
| **LLC (802.2)** | Upper sublayer; SAP, link control |
| **MAC** | Lower sublayer; framing, addressing |

### 1.5 Medium Access Control (MAC)

Strategies for shared medium:

| Method | Description |
|---|---|
| **ALOHA** (pure) | Send anytime; collide → retry |
| **Slotted ALOHA** | Send at slot start |
| **CSMA** | Listen before transmit |
| **CSMA/CD** (Ethernet) | + collision detection |
| **CSMA/CA** (Wi-Fi) | + collision avoidance |
| **Polling** | Master polls each station |
| **Token passing** | Token grants access |

### 1.6 ALOHA Efficiency

- **Pure ALOHA:** max efficiency = 1/(2e) ≈ 18.4%.
- **Slotted ALOHA:** max efficiency = 1/e ≈ 36.8%.

Throughput peaks when offered load = 1/2 (slotted) or 1 (pure).

### 1.7 CSMA Variants

| Type | Description |
|---|---|
| **1-persistent** | Sense; if idle, transmit immediately |
| **Non-persistent** | Sense; if busy, wait random time |
| **p-persistent** | Sense; if idle, transmit with probability p |

### 1.8 CSMA/CD (Ethernet)

1. **Listen** before transmit.
2. **Transmit** if idle.
3. **Detect collision** (signal abnormality).
4. **Send jam signal**.
5. **Backoff** (binary exponential): wait random k slots, k ∈ [0, 2^n − 1].
6. Retry.

After 16 attempts, give up.

### 1.9 Minimum Frame Size for Collision Detection

For collision to be detectable before frame ends:
`Frame size ≥ 2 × bandwidth × propagation_delay`

**Ethernet:** min 64 bytes for 10 Mbps and 2500 m segment.

### 1.10 CSMA/CA (Wi-Fi)

Cannot detect collisions while transmitting (radio half-duplex).

Uses:
- **DIFS, SIFS** wait times.
- **RTS/CTS** handshake.
- **Random backoff.**

### 1.11 Switching

| Method | Description |
|---|---|
| **Circuit switching** | Dedicated path (telephone) |
| **Packet switching** | Datagrams (Internet) |
| **Message switching** | Store-and-forward (legacy) |

### 1.12 Switching at Layer 2

**Switch (bridge):** forwards frames based on MAC addresses.

| Operation | Description |
|---|---|
| **Learning** | Build MAC table from source addresses |
| **Forwarding** | Lookup destination; forward to specific port |
| **Flooding** | If unknown destination, send to all ports (except source) |
| **Filtering** | Drop frames going back to source segment |

### 1.13 Switch vs Hub vs Router

| Device | Layer | Function |
|---|---|---|
| **Hub** | 1 | Repeater; broadcasts to all ports |
| **Switch / Bridge** | 2 | MAC-based forwarding |
| **Router** | 3 | IP-based routing |
| **Gateway** | 7 | Application-level translation |

### 1.14 Spanning Tree Protocol (STP, 802.1D)

In switched networks with redundant links, prevents loops.

**Algorithm:**
1. Elect **root bridge**.
2. Each switch finds shortest path to root.
3. Block redundant links.

### 1.15 Collision Domain vs Broadcast Domain

| Domain | Definition |
|---|---|
| **Collision** | Set of devices sharing medium (collisions between them) |
| **Broadcast** | Set receiving same broadcast |

**Hub:** one big collision + broadcast domain.
**Switch:** each port = collision domain; switch = one broadcast domain.
**Router:** separate broadcast domains.

### 1.16 VLAN (Virtual LAN, 802.1Q)

Logical grouping of devices regardless of physical location.

VLAN tag in Ethernet frame (4 bytes):
- VLAN ID (12 bits).
- Priority (3 bits).

Inter-VLAN routing requires router.

### 1.17 ARP (Address Resolution Protocol)

Maps IP → MAC.

**Operation:**
1. Host wants to send to IP X.
2. ARP request broadcast.
3. Host with IP X replies with MAC.
4. Cache mapping.

### 1.18 Reverse ARP (RARP)

MAC → IP. Mostly replaced by DHCP.

### 1.19 Ethernet Speeds

| Standard | Speed |
|---|---|
| 10BASE-T | 10 Mbps |
| 100BASE-TX (Fast Ethernet) | 100 Mbps |
| 1000BASE-T (Gigabit) | 1 Gbps |
| 10GBASE-T | 10 Gbps |

### 1.20 Wi-Fi Speeds (overview)

| Standard | Max Speed |
|---|---|
| 802.11b | 11 Mbps |
| 802.11g | 54 Mbps |
| 802.11n | 600 Mbps |
| 802.11ac | 6.9 Gbps |
| 802.11ax (Wi-Fi 6) | 9.6 Gbps |

### 1.21 Bridges and Bridging

**Transparent bridges** are auto-learning switches. Use STP for loop prevention.

### 1.22 Common GATE Calculations

- Min frame size for given bandwidth and propagation.
- ALOHA efficiency.
- CSMA/CD backoff.
- ARP transaction.

> **Summary:** Ethernet uses CSMA/CD. ALOHA gives 18.4% / 36.8% efficiency. Switch operates at L2 (MAC-based), router at L3 (IP-based). STP prevents loops. ARP maps IP → MAC.

---

## 2. Important Points

- **Ethernet frame min 64 bytes**, max 1518 bytes (incl. headers).
- **MAC address** = 48 bits.
- **Pure ALOHA efficiency:** 1/(2e) ≈ 18.4%.
- **Slotted ALOHA:** 1/e ≈ 36.8%.
- **CSMA/CD** detects collisions during transmission.
- **CSMA/CA** avoids via RTS/CTS (Wi-Fi).
- **Min frame size** = 2 × bandwidth × propagation_delay.
- **Switch** learns MAC table; floods unknown.
- **Hub** broadcasts everything.
- **Router** separates broadcast domains.
- **STP** prevents loops in switched networks.
- **VLAN** logical grouping; tagged frame 4 extra bytes.
- **ARP** broadcast for IP → MAC.

---

## 3. Short Notes

```
LAN: Ethernet (802.3), Wi-Fi (802.11)

ETHERNET FRAME
 preamble(7) + SFD(1) + dst MAC(6) + src MAC(6)
 + Type/Length(2) + Data(46–1500) + FCS(4)
 min = 64 bytes (no preamble)

MAC ADDRESS: 48 bits

MAC SUBLAYERS
 LLC (802.2): upper
 MAC: lower (framing, addressing)

MAC METHODS
 ALOHA / slotted ALOHA
 CSMA (1-persistent, non-persistent, p-persistent)
 CSMA/CD (Ethernet)
 CSMA/CA (Wi-Fi)
 polling, token

ALOHA EFFICIENCY
 pure: 1/(2e) ≈ 18.4%
 slotted: 1/e ≈ 36.8%

CSMA/CD
 listen → transmit → detect collision → jam → backoff
 binary exponential backoff: 0..2^n − 1 slots
 max 16 attempts

MIN FRAME SIZE = 2 × BW × T_p

CSMA/CA: DIFS/SIFS, RTS/CTS, backoff

SWITCHING
 circuit / packet / message

L2 SWITCH
 learn (source MAC)
 forward (dest MAC lookup)
 flood (unknown)
 filter

DEVICES
 hub (L1) / switch (L2) / router (L3) / gateway (L7)

COLLISION DOMAIN vs BROADCAST DOMAIN
 hub: 1 + 1
 switch: per port + 1
 router: per port + per port

STP (802.1D): prevent loops; elect root bridge

VLAN (802.1Q)
 4-byte tag in frame
 VLAN ID 12 bits

ARP: IP → MAC (broadcast request)
RARP: MAC → IP (replaced by DHCP)
```

---

## 4. Formulas / Tricks

| # | Rule | Memorize Cold? |
|---|---|---|
| 1 | Pure ALOHA: 1/(2e) ≈ 18.4% | ✅✅ |
| 2 | Slotted ALOHA: 1/e ≈ 36.8% | ✅✅ |
| 3 | Min Ethernet frame: 64 bytes | ✅✅ |
| 4 | Min frame ≥ 2·BW·T_p | ✅✅ |
| 5 | CSMA/CD backoff: random in [0, 2^n − 1] | ✅ |
| 6 | MAC = 48 bits | ✅ |
| 7 | IP MTU = 1500 bytes (Ethernet) | ✅ |
| 8 | Switch learns from source MAC | ✅✅ |
| 9 | Hub = L1; Switch = L2; Router = L3 | ✅✅ |
| 10 | STP for loop prevention | ✅ |
| 11 | VLAN tag = 4 bytes | ✅ |
| 12 | ARP broadcast | ✅✅ |

### Tricks

- **For min frame size:** double the propagation delay for round-trip detection.
- **For ALOHA peak:** offered load = 1/2 (slotted), 1 (pure).
- **For switch learning:** trace source MAC observed.
- **For collision detection:** transmission time ≥ 2 × propagation.
- **For VLANs:** different VLAN = different broadcast domain.

---

## 5. PYQs (with solutions)

### Q1. (GATE CSE 2017)
Pure ALOHA max throughput:
**Solution.** 1/(2e) ≈ 0.184.

### Q2. (GATE CSE 2014)
Min Ethernet frame (without preamble):
**Solution.** 64 bytes.

### Q3. (GATE CSE 2018)
MAC address bits:
**Solution.** 48.

### Q4. (GATE CSE 2008)
Switch operates at:
**Solution.** Layer 2 (data link).

### Q5. (GATE CSE 2010)
ARP maps:
**Solution.** IP → MAC.

### Q6. (GATE CSE 2015)
Slotted ALOHA efficiency vs pure:
**Solution.** Slotted is twice (≈36.8% vs 18.4%).

### Q7. (GATE CSE 2013)
Hub vs switch:
**Solution.** Hub broadcasts; switch learns + forwards.

### Q8. (GATE CSE 2007)
CSMA/CD min frame size requirement:
**Solution.** 2 × BW × propagation.

### Q9. (GATE CSE 2003)
STP purpose:
**Solution.** Prevent loops.

### Q10. (GATE CSE 2009)
VLAN tag bytes:
**Solution.** 4 bytes.

### Q11. (GATE CSE 2019)
Router functions at:
**Solution.** Layer 3 (network).

### Q12. (GATE CSE 2020)
CSMA/CA used in:
**Solution.** Wi-Fi (802.11).

### Q13. (GATE CSE 2021)
Ethernet 1 Gbps with 200 m segment, signal speed 2×10⁸ m/s. Min frame:
**Solution.** T_p = 200 / 2×10⁸ = 10⁻⁶ s; 2 · 10⁹ · 10⁻⁶ = 2000 bits = 250 bytes.

### Q14. (GATE CSE 2016)
ALOHA throughput at G = 0.5 (offered load):
**Solution.** Slotted: G·e⁻ᴳ = 0.5 · e⁻⁰·⁵ ≈ 0.303.

### Q15. (GATE CSE 2011)
Bridge operates at:
**Solution.** Layer 2.

---

## 6. Practice Questions (20+)

### Easy

**P1.** OSI layer of switch.

**P2.** OSI layer of router.

**P3.** ALOHA pure efficiency.

**P4.** ALOHA slotted efficiency.

**P5.** MAC address size.

**P6.** Ethernet min frame.

**P7.** ARP purpose.

**P8.** STP purpose.

**P9.** VLAN tag size.

**P10.** CSMA/CD vs CSMA/CA.

### Medium

**P11.** Compute min frame size for 100 Mbps, 200 m, speed 2×10⁸.

**P12.** ALOHA throughput at offered load G.

**P13.** Switch flooding behavior.

**P14.** ARP request format.

**P15.** Distinguish collision and broadcast domain.

**P16.** Compute # collision domains in a switched LAN.

**P17.** Frame format Ethernet.

**P18.** Wi-Fi RTS/CTS purpose.

**P19.** Spanning Tree root bridge election.

**P20.** Apply VLAN tagging.

### Hard

**P21.** Compute Slotted ALOHA optimal load and throughput.

**P22.** CSMA/CD backoff trace.

**P23.** Compute throughput Ethernet at saturation.

**P24.** Compare hub-only LAN with switched LAN.

**P25.** Routing decisions in VLAN.

**P26.** Address learning in multi-switch network.

**P27.** Detect ARP spoofing scenario.

---

### Answers + Brief Solutions

| # | Answer | Hint |
|---|---|---|
| P1 | 2 | direct |
| P2 | 3 | direct |
| P3 | 1/(2e) | direct |
| P4 | 1/e | direct |
| P5 | 48 bits | direct |
| P6 | 64 bytes | direct |
| P7 | IP → MAC | direct |
| P8 | prevent loops | direct |
| P9 | 4 bytes | direct |
| P10 | wired with CD vs wireless with CA | direct |
| P11 | 2·10⁸·10⁻⁶ ms? actually 2·100·10⁶·10⁻⁶ = 200 bits | direct |
| P12 | G·e⁻²ᴳ pure; G·e⁻ᴳ slotted | direct |
| P13 | flood unknown | direct |
| P14 | request, reply | direct |
| P15 | hub: 1; switch: many | direct |
| P16 | per port | direct |
| P17 | as in 1.2 | direct |
| P18 | hidden node | direct |
| P19 | lowest bridge ID | direct |
| P20 | tag inserted | direct |
| P21 | G=1 → 1/e | direct |
| P22 | random backoff | direct |
| P23 | depends on collisions | direct |
| P24 | switch isolates | direct |
| P25 | router needed | direct |
| P26 | each switch learns | direct |
| P27 | conflicting ARP replies | direct |

---

## 7. Mistakes

| # | Trap | How to avoid |
|---|---|---|
| 1 | ALOHA pure = slotted | Different. |
| 2 | Switch broadcasts | Only floods unknown. |
| 3 | Hub at layer 2 | Layer 1. |
| 4 | MAC = IP | Different. |
| 5 | Min frame independent of speed | Depends on propagation. |
| 6 | ARP for hostname | DNS does that. |
| 7 | RARP same as ARP | Reverse direction. |
| 8 | VLAN crosses switches | Trunk tagging required. |
| 9 | CSMA/CA doesn't detect collisions | Avoids via timing. |
| 10 | STP doesn't elect root | It does (lowest bridge ID). |

---

## 8. Pattern Recognition

| If question says... | Then... |
|---|---|
| "ALOHA throughput" | G·e⁻²ᴳ or G·e⁻ᴳ. |
| "Min Ethernet frame" | 64 bytes (or 2·BW·T_p). |
| "Switch operation" | Learn / forward / flood / filter. |
| "Hub vs switch" | L1 broadcasts vs L2 learns. |
| "ARP" | IP → MAC broadcast. |
| "STP" | Spanning tree prevents loops. |
| "VLAN" | Logical isolation; 4-byte tag. |
| "CSMA/CD" | Wired Ethernet collision detection. |
| "CSMA/CA" | Wireless avoidance. |
| "Backoff" | Random in [0, 2^n−1]. |

---

## 9. Quick Revision

```
ETHERNET
 frame min 64 bytes; MAC 48 bits
 CSMA/CD: listen → transmit → detect collision → jam → backoff
 binary exponential backoff [0, 2^n−1]
 min frame ≥ 2 · BW · T_p

WI-FI: CSMA/CA
 RTS/CTS, DIFS/SIFS

ALOHA
 pure: 1/(2e)
 slotted: 1/e
 throughput: G·e⁻²ᴳ pure; G·e⁻ᴳ slotted

DEVICES
 hub (L1) / switch (L2) / router (L3) / gateway (L7)

L2 SWITCH
 learn / forward / flood / filter

COLLISION vs BROADCAST DOMAIN
 hub: 1 + 1
 switch: per port + 1
 router: per port + per port

STP: prevent loops; elect root bridge

VLAN (802.1Q): 4-byte tag

ARP: IP → MAC (broadcast)
RARP: MAC → IP (DHCP modern)

ETHERNET SPEEDS: 10/100/1000/10G Mbps
WI-FI: 802.11 a/b/g/n/ac/ax
```
