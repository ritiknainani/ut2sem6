# 🎯 Mobile Computing (MCC) — Unit Test 2 (PT-II) Complete Guide
## Mumbai University | Computer Engineering | SEM 6 | REV-2019

---

# 📊 PART A: QUESTION BANK ANALYSIS & PRIORITY

## Exam Format (PT-II / Unit Test 2)
| Parameter | Detail |
|-----------|--------|
| **Total Marks** | 20 Marks |
| **Duration** | 1 Hour |
| **Syllabus Coverage** | Mobile IP, WLAN (IEEE 802.11), Bluetooth, Cellular IP |
| **Question Style** | Mostly theory + diagram-based |

---

## 🔥 Topic-Wise Priority

| Priority | Topic | Questions | Frequency |
|----------|-------|-----------|-----------|
| 🔴 **HIGHEST** | Mobile IP (Agent Discovery, Registration, Tunneling) | Q1-Q4 | **Almost Every Exam** |
| 🔴 **HIGHEST** | IEEE 802.11 Protocol Architecture | Q7 | **Every Exam** |
| 🟠 **HIGH** | Hidden & Exposed Terminal Problem | Q5 | **Very Frequent** |
| 🟠 **HIGH** | WLAN Security Threats | Q8 | **Frequent** |
| 🟡 **MEDIUM** | Infrastructure vs Ad-hoc Networks | Q6 | **Frequent** |
| 🟡 **MEDIUM** | Bluetooth (Piconet/Scatternet) | Q9 | **Frequent** |
| 🟢 **STANDARD** | Cellular IP | Q10 | **Moderate** |
| 🟢 **STANDARD** | IP Mobility in Wireless | Q11 | **Moderate** |

> [!TIP]
> **Exam Strategy**: Mobile IP questions (Q1-Q4) are **guaranteed**. Always draw diagrams for agent discovery, tunneling, and packet delivery — examiners award extra marks for diagrams.

---

# 📝 PART B: COMPLETE ANSWERS

---

# MOBILE IP

---

## Q.1) Agent Discovery / Advertisement Process

### Definition
**Agent Discovery** is the process by which a **Mobile Node (MN)** identifies whether it is on its **home network** or a **foreign network**, and discovers the available **mobility agents** (Home Agent or Foreign Agent).

### Two Methods of Agent Discovery:

### Method 1: Agent Advertisement (Passive Discovery)
- Mobility agents (HA/FA) **periodically broadcast** ICMP Router Advertisement messages
- These messages are **extended** with a **Mobility Agent Advertisement Extension**
- The MN listens for these advertisements to detect agents

### Method 2: Agent Solicitation (Active Discovery)
- If the MN does not want to wait, it can **actively send** an **ICMP Router Solicitation** message
- Any agent receiving this solicitation will immediately reply with an advertisement

---

### Agent Advertisement Message Format

```
┌────────────────────────────────────────────────────┐
│           ICMP Router Advertisement                │
│  (RFC 1256 base message)                           │
├────────────────────────────────────────────────────┤
│  Type = 9                                          │
│  Code = 0                                          │
│  Lifetime (how long ad is valid)                   │
│  Router Address(es)                                │
├────────────────────────────────────────────────────┤
│     Mobility Agent Advertisement Extension         │
│  ┌──────────────────────────────────────────┐      │
│  │ Type = 16                                │      │
│  │ Sequence Number                          │      │
│  │ Registration Lifetime                    │      │
│  │ Flags: R | B | H | F | M | G | V        │      │
│  │ Care-of-Address (COA)                    │      │
│  └──────────────────────────────────────────┘      │
└────────────────────────────────────────────────────┘
```

### Important Flags in Advertisement:

| Flag | Meaning |
|------|---------|
| **H** | Home Agent — the agent is offering HA services |
| **F** | Foreign Agent — the agent is offering FA services |
| **R** | Registration Required — MN must register with FA |
| **B** | Busy — FA will not accept new registrations |
| **M** | Minimal Encapsulation supported |
| **G** | GRE Encapsulation supported |
| **V** | Van Jacobson header compression supported |

### How MN Determines its Location:

```
MN receives Agent Advertisement
         │
         ▼
┌─────────────────────┐
│ Compare Network     │
│ Prefix of COA with  │
│ Home Network Prefix │
└────────┬────────────┘
         │
    ┌────┴─────┐
    ▼          ▼
 MATCH      NO MATCH
 (Home)     (Foreign)
    │          │
    ▼          ▼
 No action   Register
 needed      with FA
```

**Methods to detect movement:**
1. **Lifetime-based:** If MN doesn't receive ad from current agent within lifetime → moved
2. **Network prefix-based:** Compare IP prefix in ad with home network prefix
3. **Sequence number-based:** If sequence number resets or is lower → new agent

---

## Q.2) Agent Registration Process

### Definition
**Registration** is the process by which a Mobile Node (MN) **informs its Home Agent (HA)** of its current **Care-of-Address (COA)** so that packets can be forwarded correctly.

### When is Registration Needed?
- When MN moves to a **foreign network** → registers new COA
- When MN **returns home** → deregisters (removes COA binding)
- When **registration lifetime expires** → re-registration
- When MN moves to **another foreign network** → update registration

### Registration Process (via Foreign Agent):

```
┌──────┐         ┌──────┐         ┌──────┐
│  MN  │         │  FA  │         │  HA  │
└──┬───┘         └──┬───┘         └──┬───┘
   │                │                │
   │ 1. Reg Request │                │
   │───────────────>│                │
   │                │ 2. Reg Request │
   │                │───────────────>│
   │                │                │
   │                │  3. HA creates │
   │                │  mobility      │
   │                │  binding       │
   │                │  (HA ↔ COA)    │
   │                │                │
   │                │ 4. Reg Reply   │
   │                │<───────────────│
   │ 5. Reg Reply   │                │
   │<───────────────│                │
```

### Registration Request Message Fields:

| Field | Description |
|-------|-------------|
| **Type** | 1 (Registration Request) |
| **Flags** | S (simultaneous binding), B (broadcast), D (deregister) |
| **Lifetime** | Duration of registration (0 = deregister) |
| **Home Address** | MN's permanent home IP address |
| **Home Agent** | IP address of MN's Home Agent |
| **Care-of-Address** | Current temporary address of MN |
| **Identification** | 64-bit number for matching request/reply, replay protection |
| **Extensions** | Authentication (MN-HA, MN-FA, FA-HA) |

### Registration Reply Codes:

| Code | Meaning |
|------|---------|
| 0 | Registration accepted |
| 1 | Accepted, simultaneous bindings unsupported |
| 64 | Reason not specified (by FA) |
| 65 | Administratively prohibited (FA) |
| 69 | Requested lifetime too long (FA) |
| 128 | Reason not specified (by HA) |
| 131 | MN failed authentication |
| 133 | Registration ID mismatch |

### Deregistration (When MN Returns Home):
```
MN sends Registration Request with:
  - Lifetime = 0
  - COA = MN's home address

HA deletes the mobility binding → packets go directly to MN
```

---

## Q.3) Packet Delivery To and From Mobile Node

### Case 1: Packet Delivery TO Mobile Node (from CN)

```
Correspondent Node (CN) → sends packet to MN's HOME address
         │
         ▼
┌─────────────────┐
│   Internet       │
│   (normal        │
│    routing)      │
└────────┬────────┘
         │
         ▼
┌─────────────────┐
│  Home Agent (HA) │ ← intercepts packet (Proxy ARP)
│  Looks up        │
│  Mobility Binding│
│  MN → COA        │
└────────┬────────┘
         │ Tunnel: IP-in-IP Encapsulation
         ▼
┌─────────────────┐
│ Foreign Agent(FA)│ ← decapsulates packet
└────────┬────────┘
         │ delivers original packet
         ▼
┌─────────────────┐
│  Mobile Node(MN) │
└─────────────────┘
```

**Steps:**
1. CN sends packet to **MN's home IP** (CN doesn't know MN moved)
2. Packet reaches MN's **home network** via normal routing
3. **HA intercepts** the packet using **Proxy ARP**
4. HA looks up the **Mobility Binding Table** to find MN's current **COA**
5. HA **tunnels** (encapsulates) the packet to the **COA**
6. **FA decapsulates** the tunneled packet
7. FA delivers the **original packet** to MN

---

### Case 2: Packet Delivery FROM Mobile Node (to CN)

```
┌─────────────────┐
│  Mobile Node(MN) │
└────────┬────────┘
         │ sends directly — no tunnel needed
         ▼
┌─────────────────┐
│   Internet       │
│   (standard      │
│    routing)      │
└────────┬────────┘
         │
         ▼
┌─────────────────┐
│ Correspondent    │
│ Node (CN)        │
└─────────────────┘
```

**Steps:**
1. MN sends packet with **source = MN's home address**, **dest = CN's address**
2. Packet is routed **normally** (no tunneling needed)
3. CN receives the packet

> [!IMPORTANT]
> **Triangle Routing Problem:** Packets TO MN go via HA (indirect), but FROM MN go directly. This is inefficient. Solution: **Route Optimization** allows CN to learn MN's COA and send directly.

---

## Q.4) Tunneling and Encapsulation in Mobile IP

### Definition
**Tunneling** is the mechanism by which the HA forwards intercepted packets to the MN's current location by **encapsulating** the original IP packet inside a new IP packet addressed to the COA.

### How Tunneling Works:

```
Original Packet (from CN):
┌──────────────────────────────────────┐
│ IP Header                            │
│  Src: CN_IP    Dst: MN_Home_IP       │
├──────────────────────────────────────┤
│ TCP/UDP Header + Data (Payload)      │
└──────────────────────────────────────┘

         │ HA intercepts and encapsulates
         ▼

Tunneled Packet (HA → FA):
┌──────────────────────────────────────┐
│ NEW Outer IP Header                  │
│  Src: HA_IP    Dst: COA (FA_IP)      │
│  Protocol: 4 (IP-in-IP)             │
├──────────────────────────────────────┤
│ ORIGINAL Inner IP Header             │
│  Src: CN_IP    Dst: MN_Home_IP       │
├──────────────────────────────────────┤
│ Original TCP/UDP Header + Data       │
└──────────────────────────────────────┘

         │ FA decapsulates (removes outer header)
         ▼

Delivered to MN:
┌──────────────────────────────────────┐
│ IP Header                            │
│  Src: CN_IP    Dst: MN_Home_IP       │
├──────────────────────────────────────┤
│ TCP/UDP Header + Data (Payload)      │
└──────────────────────────────────────┘
```

### Types of Encapsulation:

| Type | Protocol # | Overhead | Description |
|------|-----------|----------|-------------|
| **IP-in-IP** | 4 | 20 bytes | Original packet wrapped in new IP header. **Mandatory**. |
| **Minimal Encapsulation** | 55 | 8-12 bytes | Reduced overhead by combining headers. Optional. |
| **GRE** | 47 | 24+ bytes | General-purpose. Supports multiple protocols. Optional. |

### Comparison:

| Feature | IP-in-IP | Minimal | GRE |
|---------|----------|---------|-----|
| **Overhead** | 20 bytes | 8-12 bytes | 24+ bytes |
| **Mandatory** | Yes | Optional | Optional |
| **Complexity** | Low | Medium | High |
| **Multi-protocol** | No (IP only) | No | Yes |
| **Flag in Agent Ad** | — | M flag | G flag |

---

# WLAN (Wireless LAN)

---

## Q.5) Hidden and Exposed Terminal Problems

### Hidden Terminal Problem

**Definition:** Two stations (A and C) cannot hear each other but both communicate with station B, causing **collisions at B**.

```
Station A          Station B          Station C
   ●──────range────────●──────range────────●
   
   A CANNOT hear C     B hears both       C CANNOT hear A
   
   A sends to B ──────→ B receiving
                        ← C also sends to B (doesn't know A is sending)
                        
   Result: COLLISION at B! ❌
```

---

### Exposed Terminal Problem

**Definition:** Station B **refrains from sending** to C because it hears A's transmission, even though B→C would **NOT cause interference**.

```
Station A          Station B          Station C
   ●──────range────────●──────range────────●
   
   A sending to LEFT   B wants to send     C is free
                       to C on RIGHT
   
   B hears A → thinks "medium busy" → WAITS unnecessarily ❌
```

---

### Solution: RTS/CTS (MACA Protocol)

```
┌──────┐         ┌──────┐         ┌──────┐
│  A   │         │  B   │         │  C   │
└──┬───┘         └──┬───┘         └──┬───┘
   │                │                │
   │ 1. RTS (A→B)   │                │
   │───────────────>│                │
   │                │                │
   │ 2. CTS (B→A)   │ 2. CTS heard   │
   │<───────────────│──────────────->│
   │                │                │
   │ 3. DATA (A→B)  │  C stays SILENT │
   │═══════════════>│  (heard CTS)    │
   │                │                │
   │ 4. ACK (B→A)   │                │
   │<───────────────│                │
```

| Problem | Cause | Solution |
|---------|-------|----------|
| **Hidden Terminal** | Senders can't hear each other | **CTS** alerts hidden nodes to stay silent |
| **Exposed Terminal** | Sender hears neighbor unnecessarily | **RTS/CTS** confirms if it's safe to send |

---

## Q.6) Infrastructure-Based vs Ad-Hoc Networks

| Parameter | Infrastructure-Based | Ad-Hoc |
|-----------|---------------------|--------|
| **Definition** | Fixed APs connected to wired backbone | Dynamic network, no fixed infrastructure |
| **Central Controller** | Yes (Access Point) | No (fully distributed) |
| **Backbone** | Required (wired) | Not needed |
| **Communication** | All traffic via AP | Direct peer-to-peer |
| **Range** | Extended via APs | Limited to node range |
| **Setup** | Planned deployment | Quick, on-the-fly |
| **Examples** | Office Wi-Fi, campus | Battlefield, disaster relief |
| **Routing** | Standard IP routing | AODV, DSR, DSDV |
| **Scalability** | Good (add more APs) | Limited |
| **Cost** | Higher | Lower |
| **Security** | Centralized (WPA2) | Distributed, harder |

```
INFRASTRUCTURE:                    AD-HOC:
                                   
  ┌─────────┐                      ●───────●
  │ Internet│                     / \     / \
  └────┬────┘                    ●   ●───●   ●
       │                          \       /
  ┌────┴────┐                      ●───●
  │   AP    │                     
  └────┬────┘                    All nodes are equal
      /│\                        No central controller
    ●  ●  ●                      Direct peer-to-peer
```

---

## Q.7) Protocol Architecture of IEEE 802.11

### Protocol Stack:

```
┌───────────────────────────────────────────┐
│          Higher Layers (IP, TCP, etc.)    │
├───────────────────────────────────────────┤
│           LLC (IEEE 802.2)               │  ← Logical Link Control
├───────────────────────────────────────────┤
│            MAC Layer                     │  ← Medium Access Control
│          (IEEE 802.11)                   │     (CSMA/CA, RTS/CTS)
├──────────────┬────────────────────────────┤
│  MAC Mgmt    │    MAC Sublayer            │
│  (MLME)      │    (frame handling,        │
│              │     access control)        │
├──────────────┼──────────┬─────────────────┤
│  PHY Mgmt    │  PLCP    │   PMD           │  ← Physical Layer
│  (PLME)      │  (conv.) │  (radio)        │
└──────────────┴──────────┴─────────────────┘
```

### 1. Physical Layer (PHY)

| Sublayer | Full Form | Function |
|----------|-----------|----------|
| **PLCP** | Physical Layer Convergence Protocol | Converts MAC frames into transmission format; adds preamble |
| **PMD** | Physical Medium Dependent | Handles actual radio transmission and modulation |

**PHY Standards:**

| Standard | Frequency | Max Speed | Modulation |
|----------|-----------|-----------|------------|
| 802.11a | 5 GHz | 54 Mbps | OFDM |
| 802.11b | 2.4 GHz | 11 Mbps | DSSS |
| 802.11g | 2.4 GHz | 54 Mbps | OFDM |
| 802.11n | 2.4/5 GHz | 600 Mbps | MIMO-OFDM |
| 802.11ac | 5 GHz | 6.9 Gbps | MU-MIMO |

### 2. MAC Layer — Two Access Mechanisms:

**(a) DCF — Distributed Coordination Function (Mandatory)**
- Based on **CSMA/CA** (Collision Avoidance)
- Uses **random backoff** timer
- Optional **RTS/CTS** handshake
- Works in both **ad-hoc and infrastructure** modes

```
DIFS → Backoff → DATA → SIFS → ACK

Station:   |DIFS|  Backoff  |====DATA====>|
Receiver:                                  |SIFS| ACK |
```

**(b) PCF — Point Coordination Function (Optional)**
- **Polling-based** — AP controls access
- **Contention-free** period
- Only in **infrastructure** mode
- For time-sensitive apps (voice, video)

### 3. MAC Management (MLME):
- Synchronization, Power Management, Association, Authentication

### MAC Frame Format:
```
┌──────┬─────────┬────────┬────────┬────────┬──────┬──────┬─────┐
│Frame │Duration │Addr 1  │Addr 2  │Addr 3  │Seq   │Frame │FCS  │
│Ctrl  │/ID      │(DA)    │(SA)    │(BSSID) │Ctrl  │Body  │     │
│2B    │2B       │6B      │6B      │6B      │2B    │0-2312│4B   │
└──────┴─────────┴────────┴────────┴────────┴──────┴──────┴─────┘
```

**Three frame types:** Data, Control (RTS/CTS/ACK), Management (Beacon/Probe/Auth)

---

## Q.8) Security Threats in WLAN and Solutions

### Major Threats:

| # | Threat | Description |
|---|--------|-------------|
| 1 | **Eavesdropping** | Passively intercepts wireless data (signals travel through air) |
| 2 | **Unauthorized Access** | Unauthorized users connect (weak/open authentication) |
| 3 | **Man-in-the-Middle** | Attacker intercepts/modifies data between sender and receiver |
| 4 | **Rogue Access Point** | Fake AP to lure users and capture data (Evil Twin) |
| 5 | **Denial of Service** | Flooding with traffic/deauth frames to disrupt service |
| 6 | **MAC Spoofing** | Attacker impersonates authorized device's MAC |
| 7 | **Replay Attack** | Captures and retransmits valid data |
| 8 | **WEP Cracking** | Exploiting WEP weakness to recover encryption key |

### Security Protocols Comparison:

| Feature | WEP | WPA | WPA2 | WPA3 |
|---------|-----|-----|------|------|
| **Encryption** | RC4 | RC4+TKIP | AES-CCMP | AES-GCMP |
| **Key Length** | 40/104 bit | 128 bit | 128 bit | 192 bit |
| **Auth** | Shared key | PSK/802.1X | PSK/802.1X | SAE |
| **Integrity** | CRC-32 | Michael | CBC-MAC | BIP-GMAC |
| **Security** | ❌ Broken | ⚠️ OK | ✅ Strong | ✅✅ Best |
| **Year** | 1997 | 2003 | 2004 | 2018 |

### Additional Security Measures:
- **MAC Filtering** — allow only pre-approved devices
- **SSID Hiding** — don't broadcast network name
- **VPN** — encrypt all traffic through tunnel
- **802.1X/RADIUS** — enterprise-grade authentication
- **Firewall + IDS/IPS** — filter and detect intrusions

---

# BLUETOOTH & CELLULAR IP

---

## Q.9) Piconet and Scatternet in Bluetooth

### Piconet

**Definition:** Basic Bluetooth network unit — **1 master + up to 7 active slaves** using the same channel.

```
              ┌──────┐
          ┌───│Master│───┐
          │   │ (M)  │   │
          │   └──────┘   │
          │       │      │
     ┌────┴──┐ ┌──┴───┐ ┌┴─────┐
     │Slave 1│ │Slave 2│ │Slave 3│
     └───────┘ └───────┘ └───────┘

  • 1 Master + up to 7 Active Slaves
  • Up to 255 parked (inactive) slaves
  • FHSS: 79 channels, 1600 hops/sec
  • TDD: Master sends even slots, slaves odd
  • Slaves only communicate WITH master
```

### Scatternet

**Definition:** **2+ piconets interconnected** via bridge devices participating in multiple piconets.

```
     Piconet 1                    Piconet 2
  ┌──────────────┐            ┌──────────────┐
  │  ┌──────┐    │  Bridge    │    ┌──────┐  │
  │  │  M1  │    │  Device    │    │  M2  │  │
  │  └──┬───┘    │    │       │    └──┬───┘  │
  │     │     ┌──┴──┐ │       │       │      │
  │  ┌──┴──┐  │ S2/ │─┘    ┌──┴──┐ ┌──┴──┐   │
  │  │ S1  │  │ S3  │      │ S4  │ │ S5  │   │
  │  └─────┘  └─────┘      └─────┘ └─────┘   │
  └──────────────┘            └──────────────┘

  Bridge = slave in both piconets (or master in one, slave in other)
  Cannot be master in two piconets simultaneously
```

### Comparison:

| Parameter | Piconet | Scatternet |
|-----------|---------|------------|
| **Piconets** | Single | 2+ connected |
| **Max Devices** | 8 active | Multiple × 8 |
| **Bridge** | Not needed | Required |
| **Coverage** | ~10m | Extended |
| **Complexity** | Simple | More complex |

---

## Q.10) Use of Cellular IP

### Definition
**Cellular IP** is a **micro-mobility** protocol for managing **local mobility** within one administrative domain without involving global Mobile IP for every small movement.

### Architecture:

```
              ┌──────────┐
              │ Internet │
              └────┬─────┘
                   │
          ┌────────┴────────┐
          │   Cellular IP   │
          │    Gateway      │ ← acts as Mobile IP Foreign Agent
          └───┬────┬────┬──┘
              │    │    │
          ┌───┴┐ ┌┴───┐┌┴───┐
          │BS-1│ │BS-2││BS-3│  ← Base Stations
          └─┬──┘ └─┬──┘└─┬──┘
            │      │     │
           MN₁    MN₂   MN₃

  MN moves BS-1→BS-2→BS-3: Cellular IP (fast, local)
  MN moves to different domain: Mobile IP (macro)
```

### Key Features:
- **Single gateway** connects domain to Internet (acts as FA)
- **Route caching** in base stations for fast packet forwarding
- **Paging** for idle nodes (saves battery)
- **Soft handoff** between base stations
- **Compatible** with Mobile IP at macro level

### Advantages:
- Fast local handoffs (no global re-registration)
- Reduces signaling overhead
- Supports paging for idle nodes
- Separates micro and macro mobility

---

## Q.11) IP Mobility in Wireless Networks

### What is IP Mobility?
The ability of a device to **maintain IP communication seamlessly** while **moving between networks**, without losing ongoing connections.

### The Fundamental Problem:
```
IP addresses serve TWO purposes:
  1. IDENTIFIER — uniquely identifies a host
  2. LOCATOR — tells routers where to deliver

When MN moves → location changes → but IP must stay same
(otherwise all TCP connections break!)

Solution: SEPARATE identity from location using Mobile IP
```

### Three Levels of Mobility:

```
┌──────────────────────────────────────────────┐
│           MACRO-MOBILITY (Mobile IP)         │
│      (between different networks)            │
│  ┌─────────────────────────────────────┐     │
│  │    MICRO-MOBILITY (Cellular IP)     │     │
│  │    (within same domain)             │     │
│  │  ┌─────────────────────────────┐    │     │
│  │  │  LINK-LAYER MOBILITY        │    │     │
│  │  │  (802.11 handoff, same      │    │     │
│  │  │   subnet)                   │    │     │
│  │  └─────────────────────────────┘    │     │
│  └─────────────────────────────────────┘     │
└──────────────────────────────────────────────┘
```

### Mobile IP Components:

| Component | Role |
|-----------|------|
| **Mobile Node (MN)** | Device that moves |
| **Home Agent (HA)** | Intercepts and tunnels packets on home network |
| **Foreign Agent (FA)** | Provides COA; decapsulates on visited network |
| **Care-of-Address** | Temporary address on foreign network |
| **Correspondent Node** | Device MN communicates with |

### Complete Flow:
```
1. MN at Home → CN sends directly to MN (normal routing)
2. MN moves → Agent Discovery → Registration (COA with HA)
3. Packet Delivery: CN → HA → tunnel → FA → MN
4. MN replies: MN → direct to CN (no tunnel)
5. MN returns → Deregistration (Lifetime=0)
```

### Challenges & Solutions:

| Challenge | Solution |
|-----------|---------|
| **Triangle Routing** | Route Optimization |
| **Handoff Latency** | Hierarchical MIP, Cellular IP |
| **Security** | Authentication extensions |
| **Firewall Issues** | Reverse tunneling |
| **Ingress Filtering** | Reverse tunneling |

---

# 📋 QUICK REVISION CHEAT SHEET

| Topic | Key Points |
|-------|------------|
| **Agent Discovery** | Advertisement (passive) + Solicitation (active); ICMP + mobility extension |
| **Registration** | MN→FA→HA (request); HA→FA→MN (reply); Lifetime=0 = deregister |
| **Packet Delivery** | TO MN: CN→HA→tunnel→FA→MN; FROM MN: direct to CN |
| **Tunneling** | IP-in-IP (20B, mandatory), Minimal (8-12B), GRE (24B+) |
| **Hidden Terminal** | A,C can't hear each other → collision at B; Fix: RTS/CTS |
| **Exposed Terminal** | B waits unnecessarily; Fix: RTS/CTS |
| **802.11 MAC** | DCF (CSMA/CA, mandatory) + PCF (polling, optional) |
| **WLAN Security** | WEP ❌ → WPA → WPA2 (AES) ✅ → WPA3 ✅✅ |
| **Piconet** | 1 Master + 7 Slaves; FHSS 1600 hops/sec; TDD |
| **Scatternet** | 2+ piconets linked by bridge; extends coverage |
| **Cellular IP** | Micro-mobility; CIP Gateway; fast local handoff |
| **IP Mobility** | Link-layer → Micro → Macro (Mobile IP) |

---

> [!IMPORTANT]
> ### Last-Minute Tips for MCC PT-II:
> 1. **Mobile IP = guaranteed questions** — know discovery, registration, tunneling.
> 2. **Draw diagrams everywhere** — packet flow, piconet, protocol stack, RTS/CTS.
> 3. **Hidden/Exposed terminal** — explain both + solution with diagram.
> 4. **Security table** (WEP→WPA→WPA2→WPA3) = easy marks.
> 5. **Time management**: 20 marks in 60 min = 3 min/mark.

---

*Prepared for: MU Sem 6 Mobile Computing (MCC) PT-II | Computer Engineering | REV-2019*
*Last Updated: April 7, 2026*
