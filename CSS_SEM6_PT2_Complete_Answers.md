# 🎯 Cryptography & System Security (CSS) — Unit Test 2 Complete Guide
## Mumbai University | Computer Engineering | SEM 6 | REV-2019

---

# 📊 PART A: QUESTION BANK ANALYSIS & PRIORITY

## Exam Format (PT-II / Unit Test 2)
| Parameter | Detail |
|-----------|--------|
| **Total Marks** | 20 Marks |
| **Duration** | 1 Hour |
| **Syllabus** | Unit 2.3 (Key Distribution, Kerberos, PKI), Unit 3 (Hash Functions), Unit 4 (Auth & Digital Signatures), Unit 5 (Network Security) |
| **Style** | Theory + Diagrams + Numericals (Diffie-Hellman) |

---

## 🔥 Topic-Wise Priority

| Priority | Topic | Questions | Frequency |
|----------|-------|-----------|-----------|
| 🔴 **HIGHEST** | Kerberos Authentication Protocol | U2-Q1, U4-Q1 | **Almost Every Exam** |
| 🔴 **HIGHEST** | SSL Handshake Protocol | U5-Q3 | **Every Exam** |
| 🟠 **HIGH** | MD5 & SHA-1 (Hash Functions) | U3-Q1,Q2,Q4 | **Very Frequent** |
| 🟠 **HIGH** | Digital Signature / RSA DS | U4-Q2 | **Very Frequent** |
| 🟠 **HIGH** | DoS / DDoS Attacks | U5-Q2,Q6 | **Very Frequent** |
| 🟡 **MEDIUM** | HMAC & CMAC | U3-Q3 | **Frequent** |
| 🟡 **MEDIUM** | PKI & X.509 Certificate | U2-Q2,Q3 | **Frequent** |
| 🟡 **MEDIUM** | PGP | U5-Q4,Q5 | **Frequent** |
| 🟢 **STANDARD** | Diffie-Hellman Numerical | U2-Q4 | **Frequent** |
| 🟢 **STANDARD** | MITM on DH / KDC | U2-Q5,Q6 | **Moderate** |
| 🔵 **MODERATE** | Authentication Header (IPsec) | U5-Q1 | **Moderate** |
| 🔵 **MODERATE** | Firewall / IDS | U5-Q4 | **Moderate** |

---

# 📝 PART B: COMPLETE ANSWERS

---

# UNIT 2.3 — KEY DISTRIBUTION & MANAGEMENT

---

## U2-Q1 / U4-Q1) Kerberos Authentication Protocol

### Definition
**Kerberos** is a **network authentication protocol** that uses **symmetric key cryptography** and a **trusted third party (KDC)** to authenticate users and services securely, without sending passwords over the network.

### Components:

| Component | Role |
|-----------|------|
| **Client (C)** | User who wants to access a service |
| **Authentication Server (AS)** | Verifies client identity, issues TGT |
| **Ticket Granting Server (TGS)** | Issues service tickets based on TGT |
| **Service Server (SS/V)** | The service client wants to access |
| **KDC** | = AS + TGS + Database of secret keys |

### Kerberos Working (3 Exchanges):

```
┌────────┐      ┌─────────────────────┐      ┌──────────┐
│ Client │      │    KDC              │      │ Service  │
│  (C)   │      │  ┌─────┐  ┌─────┐  │      │ Server   │
│        │      │  │ AS  │  │ TGS │  │      │  (V)     │
└───┬────┘      │  └──┬──┘  └──┬──┘  │      └────┬─────┘
    │           └─────┼────────┼─────┘           │
    │                 │        │                  │
    │  ════════ Exchange 1: Authentication ═════  │
    │ 1. Request      │        │                  │
    │ (IDc, IDtgs)    │        │                  │
    │────────────────>│        │                  │
    │                 │        │                  │
    │ 2. Reply        │        │                  │
    │ (TGT + Session  │        │                  │
    │  Key Kc,tgs)    │        │                  │
    │<────────────────│        │                  │
    │                 │        │                  │
    │  ════════ Exchange 2: Ticket Granting ════  │
    │ 3. Request (TGT + IDv)   │                  │
    │─────────────────────────>│                  │
    │                          │                  │
    │ 4. Reply (Service Ticket │                  │
    │    + Session Key Kc,v)   │                  │
    │<─────────────────────────│                  │
    │                          │                  │
    │  ════════ Exchange 3: Client/Server ══════  │
    │ 5. Service Request (Ticket + Authenticator) │
    │────────────────────────────────────────────>│
    │                                             │
    │ 6. Server Authentication (optional)         │
    │<────────────────────────────────────────────│
```

### Detailed Steps:

**Exchange 1: Client ↔ AS (Authentication)**
```
Client → AS:    IDc, IDtgs, Timestamp
AS → Client:    E(Kc) [Kc,tgs || IDtgs || Timestamp || Lifetime || TGT]
                where TGT = E(Ktgs) [Kc,tgs || IDc || ADc || IDtgs || Timestamp || Lifetime]

- Client decrypts using its password-derived key Kc
- Obtains session key Kc,tgs and TGT (which client CANNOT read)
```

**Exchange 2: Client ↔ TGS (Ticket Granting)**
```
Client → TGS:   IDv || TGT || Authenticator
                 Authenticator = E(Kc,tgs) [IDc || ADc || Timestamp]
TGS → Client:   E(Kc,tgs) [Kc,v || IDv || Timestamp || Service Ticket]
                 Service Ticket = E(Kv) [Kc,v || IDc || ADc || IDv || Timestamp || Lifetime]
```

**Exchange 3: Client ↔ Service Server**
```
Client → V:     Service Ticket || Authenticator2
                 Authenticator2 = E(Kc,v) [IDc || ADc || Timestamp]
V → Client:     E(Kc,v) [Timestamp + 1]  (proves server knows Kc,v)
```

### Key Points for Exam:
- Password is **never sent** over network
- **TGT** avoids repeated password entry (Single Sign-On)
- **Timestamps** prevent replay attacks
- **Authenticators** prove client identity (fresh, one-time use)
- Uses **symmetric encryption** (typically AES or DES)

---

## U2-Q2) PKI (Public Key Infrastructure)

### Definition
**PKI** is a framework of **policies, hardware, software, and procedures** needed to create, manage, distribute, use, store, and revoke **digital certificates** and manage **public-key encryption**.

### Components of PKI:

```
┌──────────────────────────────────────────────────┐
│                      PKI                         │
│                                                  │
│  ┌──────────┐  ┌──────────┐  ┌──────────────┐   │
│  │    CA    │  │    RA    │  │ Certificate  │   │
│  │(Certifi- │  │(Regist-  │  │   Store      │   │
│  │ cate     │  │ ration   │  │              │   │
│  │Authority)│  │Authority)│  │              │   │
│  └──────────┘  └──────────┘  └──────────────┘   │
│                                                  │
│  ┌──────────┐  ┌──────────┐  ┌──────────────┐   │
│  │   CRL    │  │  Users/  │  │   Digital    │   │
│  │(Revoc.   │  │  End     │  │   Certifi-   │   │
│  │  List)   │  │  Entities│  │   cates      │   │
│  └──────────┘  └──────────┘  └──────────────┘   │
└──────────────────────────────────────────────────┘
```

| Component | Role |
|-----------|------|
| **CA (Certificate Authority)** | Issues, signs, and revokes digital certificates. Root of trust. |
| **RA (Registration Authority)** | Verifies identity of users before CA issues certificate |
| **Certificate Store/Repository** | Stores issued certificates and CRLs |
| **CRL (Certificate Revocation List)** | List of revoked certificates |
| **End Entities** | Users, servers, devices that use certificates |
| **Digital Certificate** | Binds a public key to an identity (signed by CA) |

### How PKI Works:
```
1. User generates public-private key pair
2. User submits public key + identity to RA
3. RA verifies identity → forwards to CA
4. CA creates digital certificate (signs with CA's private key)
5. Certificate is published in repository
6. Anyone can verify the certificate using CA's public key
```

### PKI Services:
- **Authentication** — proves identity
- **Confidentiality** — encryption using public keys
- **Integrity** — hash + digital signature
- **Non-repudiation** — sender cannot deny signing

---

## U2-Q3) Digital Certificate & X.509 Format

### What is a Digital Certificate?
A **digital certificate** is an electronic document that **binds a public key to an entity's identity**, signed by a trusted **Certificate Authority (CA)**.

### X.509 Certificate Format:

```
┌──────────────────────────────────────────┐
│           X.509 Certificate              │
├──────────────────────────────────────────┤
│  Version (V1, V2, or V3)                │
│  Serial Number (unique per CA)           │
│  Signature Algorithm ID (e.g., RSA-SHA256)│
│  Issuer Name (CA's distinguished name)   │
│  Validity Period                         │
│    ├─ Not Before (start date)            │
│    └─ Not After  (expiry date)           │
│  Subject Name (certificate owner)        │
│  Subject Public Key Info                 │
│    ├─ Algorithm (RSA, ECC, etc.)         │
│    └─ Public Key value                   │
│  Issuer Unique ID (V2+, optional)        │
│  Subject Unique ID (V2+, optional)       │
│  Extensions (V3, optional)               │
│    ├─ Key Usage                          │
│    ├─ Subject Alt Name                   │
│    └─ Basic Constraints                  │
├──────────────────────────────────────────┤
│  CA's Digital Signature                  │
│  (Hash of above fields, encrypted with   │
│   CA's private key)                      │
└──────────────────────────────────────────┘
```

### Certificate Chain of Trust:
```
Root CA Certificate (self-signed, trusted)
  └── Intermediate CA Certificate
        └── End Entity Certificate (website, user)

Verification: check each signature up the chain to root
```

---

## U2-Q4) Diffie-Hellman Key Exchange — Numerical

### Concept
Diffie-Hellman allows two parties to **establish a shared secret key** over an insecure channel, without any prior shared secret.

### Algorithm:

```
Public values:  p (large prime), g (generator/primitive root of p)

Alice:                              Bob:
  Choose secret a                     Choose secret b
  Compute A = g^a mod p               Compute B = g^b mod p
  Send A to Bob ──────────>           Send B to Alice
                 <──────────
  Compute:                            Compute:
  K = B^a mod p                       K = A^b mod p
       │                                    │
       └──── K = g^(ab) mod p ──────────────┘
              (SAME shared secret!)
```

### Numerical Example:
```
Given: p = 23, g = 5

Alice chooses: a = 6 (secret)
Bob chooses:   b = 15 (secret)

Step 1: Alice computes A
  A = g^a mod p = 5^6 mod 23
  5^1 = 5
  5^2 = 25 mod 23 = 2
  5^3 = 10
  5^4 = 50 mod 23 = 4
  5^5 = 20
  5^6 = 100 mod 23 = 8
  A = 8

Step 2: Bob computes B
  B = g^b mod p = 5^15 mod 23
  5^1  = 5
  5^2  = 2
  5^4  = 4
  5^8  = 4^2 = 16
  5^15 = 5^8 × 5^4 × 5^2 × 5^1
       = 16 × 4 × 2 × 5
       = 640 mod 23
       = 640 - 27×23 = 640 - 621 = 19
  B = 19

Step 3: Alice computes shared key
  K = B^a mod p = 19^6 mod 23
  19^2 = 361 mod 23 = 361 - 15×23 = 361 - 345 = 16
  19^3 = 19×16 = 304 mod 23 = 304 - 13×23 = 304 - 299 = 5
  19^6 = (19^3)^2 = 5^2 = 25 mod 23 = 2
  K = 2

Step 4: Bob computes shared key
  K = A^b mod p = 8^15 mod 23
  8^2  = 64 mod 23 = 18
  8^4  = 18^2 = 324 mod 23 = 324 - 14×23 = 2
  8^8  = 2^2 = 4
  8^15 = 8^8 × 8^4 × 8^2 × 8^1
       = 4 × 2 × 18 × 8
       = 1152 mod 23
       = 1152 - 50×23 = 1152 - 1150 = 2
  K = 2

┌──────────────────────────────────────────┐
│  Shared Secret Key K = 2                 │
│  Both Alice and Bob computed K = 2  ✅    │
└──────────────────────────────────────────┘
```

---

## U2-Q5) Man-in-the-Middle Attack on Diffie-Hellman

### How the Attack Works:

```
Alice                  Mallory (Attacker)              Bob
  │                        │                            │
  │ A = g^a mod p          │                            │
  │───────────────>        │                            │
  │         (Mallory intercepts A, computes own)        │
  │                        │  M1 = g^m mod p            │
  │                        │───────────────────────────>│
  │                        │                            │
  │                        │            B = g^b mod p   │
  │                        │<───────────────────────────│
  │         (Mallory intercepts B, sends own M2)        │
  │           M2 = g^m mod p                            │
  │<───────────────────────│                            │
  │                        │                            │
  │ K1 = M2^a mod p        │ K1 = A^m mod p             │
  │ (Alice thinks she      │ K2 = B^m mod p             │
  │  shares K with Bob)    │ (Mallory knows BOTH keys!) │
  │                        │                            │
  │ K2 = M1^b mod p        │                            │
  │                        │ (Bob thinks he shares      │
  │                        │  K with Alice)             │
```

**Problem:** DH provides **no authentication** — Alice and Bob can't verify who they're talking to.

### Solutions:
1. **Digital Signatures** — sign the DH values with private keys
2. **Digital Certificates** — use PKI to verify identities
3. **Station-to-Station (STS) Protocol** — authenticated DH
4. **Pre-shared keys** — use existing shared secret for verification

---

## U2-Q6) KDC (Key Distribution Center)

### Why is KDC Used?
- In a network of **n** users, each pair needs a unique key → **n(n-1)/2** keys total
- For 1000 users = ~500,000 keys — **impractical** to manage
- **KDC** reduces this: each user shares **one key** with KDC → only **n** keys needed

### What is KDC?
A **trusted third party** that generates and distributes **session keys** to users who want to communicate securely.

### How KDC Works:

```
┌──────┐         ┌──────┐         ┌──────┐
│  A   │         │ KDC  │         │  B   │
└──┬───┘         └──┬───┘         └──┬───┘
   │                │                │
   │ 1. Request to  │                │
   │ talk to B      │                │
   │───────────────>│                │
   │                │                │
   │ 2. KDC generates session key Ks │
   │    Sends:                       │
   │    E(Ka)[Ks, IDb]               │
   │    E(Kb)[Ks, IDa]  ← "ticket"  │
   │<───────────────│                │
   │                │                │
   │ 3. Forward ticket to B          │
   │    E(Kb)[Ks, IDa]              │
   │────────────────────────────────>│
   │                                 │
   │ 4. Communicate using Ks         │
   │<═══════════════════════════════>│

Ka = A's key shared with KDC
Kb = B's key shared with KDC
Ks = session key for this communication
```

### Advantages:
- Reduces key management from n(n-1)/2 to n keys
- Session keys are temporary (compromised key = limited damage)
- Centralized trust and control

### Disadvantage:
- **Single point of failure** — if KDC is compromised, entire system fails
- **Bottleneck** — all key requests go through KDC

---

# UNIT 3 — CRYPTOGRAPHIC HASH FUNCTIONS

---

## U3-Q1/Q2) Message Digest, MD5, and SHA-1

### What is a Message Digest?
A **message digest** (hash) is a **fixed-size output** produced from a variable-size input using a hash function. It serves as a digital "fingerprint" of the message.

### Goals of Message Digest:
1. **Data Integrity** — detect if message was modified
2. **Authentication** — verify sender identity (with HMAC)
3. **Non-repudiation** — used in digital signatures
4. **Password Storage** — store hash, not plaintext password
5. **Efficient Comparison** — compare hashes instead of full files

---

### MD5 (Message Digest 5)

| Property | Value |
|----------|-------|
| **Output** | 128-bit (16 bytes) hash |
| **Block Size** | 512 bits |
| **Rounds** | 4 rounds × 16 operations = 64 steps |
| **Designer** | Ronald Rivest (1991) |
| **Status** | ❌ Broken — collision attacks found |

**MD5 Steps:**
```
1. PADDING: Append bits so length ≡ 448 mod 512
   - Append '1' bit, then '0' bits
   - Last 64 bits = original message length

2. INITIALIZE: Four 32-bit registers (chaining variables)
   A = 0x67452301
   B = 0xEFCDAB89
   C = 0x98BADCFE
   D = 0x10325476

3. PROCESS: Each 512-bit block through 4 rounds
   Round 1: F(B,C,D) = (B AND C) OR (NOT B AND D)   — 16 steps
   Round 2: G(B,C,D) = (B AND D) OR (C AND NOT D)   — 16 steps
   Round 3: H(B,C,D) = B XOR C XOR D                — 16 steps
   Round 4: I(B,C,D) = C XOR (B OR NOT D)            — 16 steps

4. OUTPUT: Concatenate A || B || C || D = 128-bit digest
```

```
MD5 Block Diagram:

Message → [Padding] → [512-bit blocks]
                            │
                     ┌──────▼──────┐
                     │  A B C D    │ ← initial values
                     │  (128-bit)  │
                     ├─────────────┤
                     │  Round 1 (F)│ ← 16 steps
                     │  Round 2 (G)│ ← 16 steps
                     │  Round 3 (H)│ ← 16 steps
                     │  Round 4 (I)│ ← 16 steps
                     ├─────────────┤
                     │  Add to     │
                     │  previous   │
                     │  A B C D    │
                     └──────┬──────┘
                            │ (repeat for each block)
                            ▼
                     128-bit Hash Output
```

---

### SHA-1 (Secure Hash Algorithm 1)

| Property | Value |
|----------|-------|
| **Output** | 160-bit (20 bytes) hash |
| **Block Size** | 512 bits |
| **Rounds** | 4 rounds × 20 operations = 80 steps |
| **Designer** | NSA / NIST (1995) |
| **Status** | ⚠️ Deprecated — collision found (2017) |

**SHA-1 Steps:**
```
1. PADDING: Same as MD5 (length ≡ 448 mod 512)

2. INITIALIZE: Five 32-bit registers
   H0 = 0x67452301
   H1 = 0xEFCDAB89
   H2 = 0x98BADCFE
   H3 = 0x10325476
   H4 = 0xC3D2E1F0

3. PROCESS: Each 512-bit block through 80 steps
   Steps 0-19:  f(B,C,D) = (B AND C) OR (NOT B AND D)    K = 0x5A827999
   Steps 20-39: f(B,C,D) = B XOR C XOR D                 K = 0x6ED9EBA1
   Steps 40-59: f(B,C,D) = (B AND C) OR (B AND D) OR (C AND D)  K = 0x8F1BBCDC
   Steps 60-79: f(B,C,D) = B XOR C XOR D                 K = 0xCA62C1D6

4. OUTPUT: H0 || H1 || H2 || H3 || H4 = 160-bit digest
```

### MD5 vs SHA-1 Comparison:

| Feature | MD5 | SHA-1 |
|---------|-----|-------|
| **Digest Length** | 128 bits | 160 bits |
| **Block Size** | 512 bits | 512 bits |
| **Rounds** | 4 (64 steps) | 4 (80 steps) |
| **Registers** | 4 (A,B,C,D) | 5 (H0-H4) |
| **Speed** | Faster | Slower |
| **Security** | ❌ Broken | ⚠️ Deprecated |
| **Collision Resistance** | Weak | Better but broken |

---

## U3-Q3) HMAC and CMAC

### HMAC (Hash-based Message Authentication Code)

**Definition:** HMAC uses a **hash function + secret key** to provide both **message integrity** and **authentication**.

**Formula:**
```
HMAC(K, M) = H( (K ⊕ opad) || H( (K ⊕ ipad) || M ) )

where:
  K = secret key (padded to block size)
  M = message
  H = hash function (MD5, SHA-1, SHA-256)
  ipad = 0x36 repeated (inner padding)
  opad = 0x5C repeated (outer padding)
```

**Block Diagram:**
```
Key K ──┬──── K ⊕ ipad ──────┐
        │                     │
        │              ┌──────▼──────┐
        │              │ (K⊕ipad)||M │
        │              └──────┬──────┘
        │                     │
        │              ┌──────▼──────┐
        │              │   H (hash)  │ ← inner hash
        │              └──────┬──────┘
        │                     │
        └──── K ⊕ opad ──┐   │
                          │   │
                   ┌──────▼───▼──┐
                   │(K⊕opad)||H1 │
                   └──────┬──────┘
                          │
                   ┌──────▼──────┐
                   │   H (hash)  │ ← outer hash
                   └──────┬──────┘
                          │
                       HMAC output
```

### CMAC (Cipher-based MAC)

**Definition:** CMAC uses a **block cipher (like AES)** instead of a hash function to generate a MAC.

**How CMAC Works:**
```
Message M divided into n blocks: M1, M2, ..., Mn

       M1            M2            Mn ⊕ K1
       │              │              │
  0 ──►⊕         ┌───►⊕         ┌───►⊕
       │          │    │          │    │
   ┌───▼───┐     │┌───▼───┐     │┌───▼───┐
   │ AES-E │     ││ AES-E │     ││ AES-E │
   │  (K)  │     ││  (K)  │     ││  (K)  │
   └───┬───┘     │└───┬───┘     │└───┬───┘
       │         │    │         │    │
       └─────────┘    └─────────┘    ▼
                                   CMAC Tag (T)
       
K1 = derived subkey (from K using AES)
If last block is incomplete: pad and use K2 instead
```

### HMAC vs CMAC:

| Feature | HMAC | CMAC |
|---------|------|------|
| **Based on** | Hash function | Block cipher |
| **Example** | HMAC-SHA256 | AES-CMAC |
| **Speed** | Generally faster | Depends on cipher |
| **Key** | One key | One key + derived subkeys |
| **Output size** | Hash output size | Block cipher block size |

---

## U3-Q4/Q5/Q6) Properties of Secure Hash Functions

### Requirements / Properties:

| # | Property | Description | Why Needed |
|---|----------|-------------|------------|
| 1 | **Variable Input** | Accepts any length input | Flexibility |
| 2 | **Fixed Output** | Produces fixed-length output | Consistency |
| 3 | **Efficiency** | Easy and fast to compute H(x) for any x | Practical use |
| 4 | **Pre-image Resistance** | Given h, infeasible to find x such that H(x) = h | Can't reverse hash |
| 5 | **Second Pre-image Resistance** | Given x, infeasible to find y ≠ x such that H(y) = H(x) | Can't forge |
| 6 | **Collision Resistance** | Infeasible to find ANY pair x ≠ y where H(x) = H(y) | Strongest property |
| 7 | **Avalanche Effect** | Small change in input → drastic change in output | Security |

```
Property Hierarchy:
   Collision Resistance (strongest)
         ↓ implies
   Second Pre-image Resistance
         ↓ implies
   Pre-image Resistance (weakest of the three)
```

### Real-World Applications of Hash Functions:
1. **Password Storage** — store H(password), not plaintext
2. **Digital Signatures** — sign H(message) for efficiency
3. **Message Authentication (HMAC)** — verify integrity + sender
4. **File Integrity** — checksum verification (downloads)
5. **Blockchain** — proof of work, linking blocks
6. **Certificate Fingerprints** — identify certificates uniquely

---

# UNIT 4 — AUTHENTICATION & DIGITAL SIGNATURES

---

## U4-Q2) Digital Signature & RSA Digital Signature

### What is a Digital Signature?
A **digital signature** is a cryptographic mechanism that provides **authentication**, **integrity**, and **non-repudiation** by allowing a sender to sign a message using their **private key**.

### Properties:
1. **Authentication** — verifies sender's identity
2. **Integrity** — detects message tampering
3. **Non-repudiation** — sender cannot deny signing
4. **Unforgeable** — only private key holder can sign

### How Digital Signature Works:

```
SIGNING (Sender):                    VERIFICATION (Receiver):

Message M                           Message M + Signature S
    │                                    │           │
    ▼                                    ▼           ▼
┌────────┐                          ┌────────┐  ┌────────┐
│Hash H()│                          │Hash H()│  │Decrypt │
└───┬────┘                          └───┬────┘  │with    │
    │                                    │      │Sender's│
    ▼ h = H(M)                          │      │Public  │
┌────────┐                              │      │Key     │
│Encrypt │                              │      └───┬────┘
│with    │                              ▼          ▼
│Sender's│                          ┌────────────────┐
│PRIVATE │                          │  Compare h     │
│Key     │                          │  with decrypted│
│        │                          │  value         │
└───┬────┘                          ├────────────────┤
    │                               │ Match = VALID  │
    ▼                               │ No Match = BAD │
Signature S                         └────────────────┘
```

### RSA Digital Signature:

**Key Generation:**
```
1. Choose two large primes p, q
2. n = p × q
3. φ(n) = (p-1)(q-1)
4. Choose e: 1 < e < φ(n), gcd(e, φ(n)) = 1
5. Compute d: e × d ≡ 1 mod φ(n)
6. Public key = (e, n), Private key = (d, n)
```

**Signing:**
```
1. Compute hash: h = H(M)
2. Sign: S = h^d mod n  (encrypt hash with private key)
3. Send (M, S)
```

**Verification:**
```
1. Compute hash: h' = H(M)
2. Decrypt signature: h = S^e mod n  (decrypt with public key)
3. If h == h' → Signature is VALID ✅
   If h ≠ h' → Signature is INVALID ❌
```

### Attacks on Digital Signature:
1. **Key-only attack** — attacker has only public key
2. **Known message attack** — attacker has message-signature pairs
3. **Chosen message attack** — attacker gets signatures for chosen messages
4. **Existential forgery** — forge signature for some (possibly meaningless) message

---

# UNIT 5 — NETWORK SECURITY & APPLICATIONS

---

## U5-Q1) Authentication Header (AH) in IPsec

### Definition
**Authentication Header (AH)** is an **IPsec protocol** that provides:
- **Data integrity** — detects modification
- **Data origin authentication** — verifies sender
- **Anti-replay protection** — prevents replay attacks
- Does **NOT** provide confidentiality (no encryption)

### AH Header Format:
```
┌─────────────┬──────────┬─────────────────┐
│ Next Header │ Payload  │   Reserved      │
│  (8 bits)   │ Length   │   (16 bits)     │
│             │ (8 bits) │                 │
├─────────────┴──────────┴─────────────────┤
│ Security Parameters Index (SPI) — 32 bits│
├──────────────────────────────────────────┤
│ Sequence Number — 32 bits                │
├──────────────────────────────────────────┤
│ Integrity Check Value (ICV)              │
│ (variable length — HMAC-SHA1/MD5)        │
└──────────────────────────────────────────┘
```

### Anti-Replay Protection:
- Each packet has a **Sequence Number** (starts at 0, increments by 1)
- Receiver maintains a **sliding window** (default 64 packets)
- Packets with sequence number **left of window** → **rejected** (too old)
- Packets **within window** → checked if already received
- Packets **right of window** → accepted, window advances

```
Sliding Window:
                          Window (64 packets)
  Rejected ←──┤ ════════════════════════ ├──→ Accepted
          (too old)   (check if already      (advance
                       received)             window)
```

---

## U5-Q2/Q6) DoS, DDoS & Network Attacks

### Denial of Service (DoS)
**Definition:** An attack that makes a network service **unavailable** to legitimate users by overwhelming it with traffic or exploiting vulnerabilities.

### Types of DoS/DDoS Attacks:

**1. SYN Flood:**
```
Attacker sends many SYN packets with FAKE source IPs
Server allocates resources for each half-open connection
Server's connection table fills up → cannot accept legitimate connections

Attacker → SYN (fake IP) → Server
                             ↓ SYN-ACK → (nowhere)
                             ↓ Wait... timeout
                             ↓ Resources exhausted!

Solution: SYN Cookies, rate limiting, firewall rules
```

**2. ICMP Flood (Ping Flood / Smurf Attack):**
```
Attacker sends massive ICMP Echo Request packets
Server overwhelmed responding to pings
Smurf: send ping to broadcast address with spoofed source = victim
       → all hosts reply to victim → amplified flood

Solution: Block ICMP at firewall, disable broadcast responses
```

**3. UDP Flood:**
```
Attacker sends large number of UDP packets to random ports
Server checks for application → none found → sends ICMP "Destination Unreachable"
Server overwhelmed processing and responding

Solution: Rate limiting, deep packet inspection, firewall
```

**4. ARP Spoofing:**
```
Attacker sends fake ARP replies on local network
Maps attacker's MAC to victim's IP → traffic redirected to attacker
Used for MITM attacks or network disruption

Solution: Static ARP entries, Dynamic ARP Inspection (DAI), ARP monitoring
```

**5. Packet Sniffing:**
```
Attacker captures network packets using tools (Wireshark, tcpdump)
Can read unencrypted data (passwords, emails, etc.)
Works especially well on shared media or Wi-Fi

Solution: Encryption (SSL/TLS, VPN), switched networks, WPA2
```

### DDoS (Distributed DoS):
```
Attacker controls many compromised machines (Botnet)
All bots simultaneously attack the target
Much harder to defend — traffic comes from many legitimate-looking sources

        Bot1 ──────→ ┌──────────┐
        Bot2 ──────→ │  Target  │ ← Overwhelmed!
        Bot3 ──────→ │  Server  │
        ...  ──────→ └──────────┘
        BotN ──────→

Solutions: CDN, traffic scrubbing, rate limiting, blackholing, ISP cooperation
```

---

## U5-Q3) SSL/TLS Handshake Protocol

### Definition
**SSL (Secure Sockets Layer)** / **TLS (Transport Layer Security)** provides secure communication over the internet through **encryption, authentication, and integrity**.

### SSL Handshake — All Phases:

```
┌────────┐                              ┌────────┐
│ Client │                              │ Server │
└───┬────┘                              └───┬────┘
    │                                       │
    │ ──── Phase 1: Hello ────              │
    │                                       │
    │ 1. ClientHello                        │
    │ (version, random, cipher suites,      │
    │  session ID, compression methods)     │
    │──────────────────────────────────────>│
    │                                       │
    │                        2. ServerHello │
    │     (version, random, chosen cipher,  │
    │      session ID, compression method)  │
    │<──────────────────────────────────────│
    │                                       │
    │ ──── Phase 2: Server Auth ────        │
    │                                       │
    │                  3. Server Certificate │
    │                  (X.509 certificate)  │
    │<──────────────────────────────────────│
    │                                       │
    │              4. ServerKeyExchange     │
    │                  (if needed — DH)     │
    │<──────────────────────────────────────│
    │                                       │
    │          5. CertificateRequest        │
    │              (optional — mutual auth) │
    │<──────────────────────────────────────│
    │                                       │
    │              6. ServerHelloDone       │
    │<──────────────────────────────────────│
    │                                       │
    │ ──── Phase 3: Client Auth ────        │
    │                                       │
    │ 7. Client Certificate (if requested)  │
    │──────────────────────────────────────>│
    │                                       │
    │ 8. ClientKeyExchange                  │
    │ (pre-master secret encrypted with     │
    │  server's public key)                 │
    │──────────────────────────────────────>│
    │                                       │
    │ 9. CertificateVerify (if cert sent)   │
    │──────────────────────────────────────>│
    │                                       │
    │ ──── Phase 4: Finish ────             │
    │                                       │
    │ 10. ChangeCipherSpec                  │
    │    (switch to encrypted mode)         │
    │──────────────────────────────────────>│
    │                                       │
    │ 11. Finished (encrypted)              │
    │──────────────────────────────────────>│
    │                                       │
    │             12. ChangeCipherSpec      │
    │<──────────────────────────────────────│
    │                                       │
    │             13. Finished (encrypted)  │
    │<──────────────────────────────────────│
    │                                       │
    │ ═══ Encrypted Application Data ═══    │
    │<════════════════════════════════════=>│
```

### Summary of 4 Phases:

| Phase | Messages | Purpose |
|-------|----------|---------|
| **Phase 1** | ClientHello, ServerHello | Agree on version, cipher suite, exchange randoms |
| **Phase 2** | Certificate, KeyExchange, CertRequest, HelloDone | Server authentication, key parameters |
| **Phase 3** | Certificate, KeyExchange, CertVerify | Client authentication (optional), key exchange |
| **Phase 4** | ChangeCipherSpec, Finished | Switch to encryption, verify handshake integrity |

### Key Derivation:
```
Pre-Master Secret → Master Secret → Session Keys
  (from key exchange)   (using randoms)   (encryption, MAC, IV)
```

---

## U5-Q4/Q5) PGP, Firewall, IDS

### PGP (Pretty Good Privacy)

**Definition:** PGP provides **email security** through encryption, authentication, compression, and radix-64 encoding.

### PGP Operations for Email:

```
SENDING (Confidentiality + Authentication):

1. AUTHENTICATION:
   Sender hashes message → H(M)
   Signs hash with sender's private key → E(PRa)[H(M)]
   Prepend signature to message

2. COMPRESSION:
   Compress (signature + message) using ZIP

3. CONFIDENTIALITY:
   Generate random session key Ks
   Encrypt compressed data with Ks (symmetric: AES/3DES)
   Encrypt Ks with receiver's PUBLIC key → E(PUb)[Ks]

4. ENCODING:
   Convert to Radix-64 (Base64) for email compatibility

Output: E(PUb)[Ks] || E(Ks)[ZIP(Sign || M)]
```

```
PGP Flow Diagram:

Message ──→ [Hash] ──→ [Sign with Private Key] ──→ Signature
                                                      │
Message ──────────────────────────────────────────────┤
                                                      │
                                               ┌──────▼──────┐
                                               │  Compress   │
                                               │   (ZIP)     │
                                               └──────┬──────┘
                              Session Key Ks ─────────┤
                                                      │
                                               ┌──────▼──────┐
                                               │  Encrypt    │
                                               │  with Ks    │
                                               └──────┬──────┘
                              E(PUb)[Ks] ────────────┤
                                                      │
                                               ┌──────▼──────┐
                                               │  Base64     │
                                               │  Encode     │
                                               └──────┬──────┘
                                                      │
                                                   Email
```

### Firewall

**Definition:** A **firewall** is a network security device that **monitors and filters** incoming/outgoing network traffic based on predefined security rules.

| Type | How it Works |
|------|-------------|
| **Packet Filter** | Examines headers (IP, port) — fast but basic |
| **Stateful Inspection** | Tracks connection state — more secure |
| **Application Gateway (Proxy)** | Inspects application data — most secure but slow |
| **Circuit-Level Gateway** | Monitors TCP handshake — validates sessions |

### IDS (Intrusion Detection System)

**Definition:** IDS **monitors** network traffic for suspicious activity and **alerts** administrators.

| Type | Method |
|------|--------|
| **Signature-based** | Matches against known attack patterns (like antivirus) |
| **Anomaly-based** | Detects deviations from "normal" behavior baseline |
| **NIDS** | Network-based — monitors network traffic |
| **HIDS** | Host-based — monitors system files and logs |

**IDS vs IPS:**
- **IDS** = Detection only (alerts)
- **IPS** = Prevention (blocks attacks automatically)

---

# 📋 QUICK REVISION CHEAT SHEET

| Topic | Key Points |
|-------|------------|
| **Kerberos** | AS→TGT→TGS→Service Ticket→Server; 3 exchanges; timestamps prevent replay |
| **PKI** | CA + RA + CRL + Certificates; binds public key to identity |
| **X.509** | Version, Serial, Issuer, Validity, Subject, Public Key, CA Signature |
| **Diffie-Hellman** | A = g^a mod p, B = g^b mod p, K = g^ab mod p; NO authentication |
| **MITM on DH** | Attacker intercepts A,B; establishes separate keys; Fix: digital signatures |
| **KDC** | Reduces n(n-1)/2 keys to n; single point of failure |
| **MD5** | 128-bit output, 4 rounds, 64 steps; ❌ BROKEN |
| **SHA-1** | 160-bit output, 4 rounds, 80 steps; ⚠️ Deprecated |
| **Hash Properties** | Pre-image, Second pre-image, Collision resistance |
| **HMAC** | H((K⊕opad) \|\| H((K⊕ipad) \|\| M)); key + hash = MAC |
| **CMAC** | AES-based MAC; processes blocks sequentially with XOR |
| **Digital Signature** | Sign: S = H(M)^d mod n; Verify: H(M) = S^e mod n |
| **AH (IPsec)** | Integrity + Auth + Anti-replay; NO encryption; sequence number window |
| **SSL Handshake** | 4 phases: Hello → Server Auth → Client Auth → Finish |
| **PGP** | Hash→Sign→Compress→Encrypt→Base64; hybrid encryption |
| **DoS/DDoS** | SYN flood, ICMP flood, UDP flood, ARP spoofing |
| **Firewall** | Packet filter, Stateful, Application proxy, Circuit-level |
| **IDS** | Signature-based, Anomaly-based; NIDS vs HIDS |

---

> [!IMPORTANT]
> ### Last-Minute Tips for CSS PT-II:
> 1. **Kerberos diagram is GUARANTEED** — memorize 3 exchanges with message contents.
> 2. **SSL Handshake phases** — know all 4 phases and message flow.
> 3. **Diffie-Hellman numerical** — practice modular exponentiation.
> 4. **MD5 vs SHA-1 comparison table** = easy marks.
> 5. **Draw diagrams** for PGP, HMAC, Digital Signature — extra marks.
> 6. **DoS attack types** — memorize SYN, ICMP, UDP flood differences.

---

*Prepared for: MU Sem 6 CSS PT-II | Computer Engineering | REV-2019*
*Last Updated: April 8, 2026*
