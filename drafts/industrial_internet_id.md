# Industrial Internet Identification and Resolution

## Overview & Significance
In this course, we learned how to assign a globally unique digital identity to physical industrial devices and products, and how to resolve that identity to locate their data and services. In the IoT 3-layer hierarchy, this technology sits between the **Network Layer** and the **Application Layer**, acting like a **DNS (Domain Name System) for physical industrial assets**.

Why do we need this? There are two main reasons:
1. **Breaking Information Silos**: In real industrial sites, devices use heterogeneous protocols like ZigBee, Wi-Fi, and BLE. A **MAC address** only identifies a device locally at Layer 2, and an **IP address** can change dynamically. Neither carries business semantics like manufacturer or hardware version. Identification resolution provides a globally persistent ID across different factories and supply chains.
2. **Product Lifecycle Management (PLM)**: Industrial hardware nodes look identical in large deployments. By giving each node a "digital ID card," we achieve full lifecycle traceability from manufacturing and warehousing to on-site maintenance and recycling.

We covered this course in three main parts:
1. **Identification Systems and Carriers** (How to encode and attach the ID)
2. **Resolution Architecture and Process** (How to look up the ID)
3. **Course Project** (A traceability and monitoring system for CC2530 ZigBee nodes)

---

## 1. Identification Systems and Data Carriers

### Mainstream Identification Schemes
We studied three major global coding systems:
- **Handle System** (Core focus): Uses a **Prefix / Suffix** structure, such as `88.12345/IOT-CC2530-V2-0001`. It is decoupled from IP addresses, supports arbitrary metadata extension, and offers high security.
- **GS1 / EPC**: Includes retail barcodes (`EAN-13`) and **EPC (Electronic Product Code)**, widely used in supermarkets and supply chain logistics.
- **OID (Object Identifier)**: A hierarchical dot-separated tree standard (e.g., `1.2.156.xxxx`), mainly used in telecommunications (`SNMP`) and digital certificates.

**Tradeoff: Handle vs GS1**
- We prefer the **Handle System** in the Industrial Internet because GS1 is mainly designed for **category-level** commercial circulation (telling you *what kind of product* this is). In contrast, Handle supports **item-level** unique identity for every single machine or sensor and can directly resolve to dynamic RESTful APIs or monitoring URLs.

### Data Carriers: QR Code vs RFID
To read the ID in the physical world, we attach it using physical carriers:
- **QR Code (Quick Response Code)**: Optical carrier, extremely low cost, and easy to scan with a smartphone. However, it **requires line-of-sight** and can only be scanned one by one.
- **UHF RFID (Radio Frequency Identification)**: Uses wireless RF signals (860–960 MHz). It supports **non-line-of-sight and bulk reading** (anti-collision), making it ideal for harsh environments or reading through cardboard boxes. Its drawbacks are higher tag cost and sensitivity to metal or liquid interference.

---

## 2. Resolution Architecture and Process 

### Analogy to DNS
Just like DNS translates a domain name (`google.com`) into a server's IP address, **Industrial Internet Resolution** translates a product's identifier into its **static metadata** and **service redirect URL**.

### 4-Level Hierarchical Architecture
I would like to draw a structure showing the 4-level distributed hierarchy:
```
+-------------------------------------------------------+
|      International Root Node (Global Top Prefixes)    |
+-------------------------------------------------------+
                           |
                           v
+-------------------------------------------------------+
|       National Top Node (National Routing Center)     |
+-------------------------------------------------------+
                           |
                           v
+-------------------------------------------------------+
|    Secondary Node (Industry/Regional Hub: 88.12345)   |
+-------------------------------------------------------+
                           |
                           v
+-------------------------------------------------------+
|    Enterprise Node (Factory DB: Metadata & API URL)   |
+-------------------------------------------------------+
```
1. **International Root Node**: Manages global top-level prefixes across Handle, GS1, and OID.
2. **National Top Node**: Serves as the national routing hub and maintains top-level data synchronization.
3. **Secondary Node**: The industry-level or regional hub that assigns prefixes (like `88.12345`) to enterprises.
4. **Enterprise Node**: Deployed by the factory to store specific device metadata and service interfaces.
- Additionally, there is the **Public Recursive Node** (similar to DNS `8.8.8.8`), which receives queries from end users, caches frequent records, and performs step-by-step lookups.

### Resolution Workflow (Recursive vs Authoritative)
We learned two resolution behaviors: **Recursive Resolution** and **Authoritative Resolution**.
```
[Handheld Scanner / Client]
         |  1. Query: 88.12345/IOT-CC2530-V2-0001
         v
[Public Recursive Node]  <-- Does the "legwork" (Recursive)
         |
         +--> 2. Ask Root/Top Node --> Returns Secondary Node IP
         |
         +--> 3. Ask Secondary Node --> Returns Enterprise Node URL
         |
         +--> 4. Ask Enterprise Node (Authoritative) --> Returns JSON Metadata + Redirect URL
```
- The client sends a single request to the **Recursive Node**, which queries upward and downward across the **Authoritative Nodes** (Top $\rightarrow$ Secondary $\rightarrow$ Enterprise) and returns the final JSON result to the user.

---

## 3. Course Project: CC2530 ZigBee Node Traceability & Monitoring

In my final coursework, I designed a simplified product traceability and real-time monitoring system for **TI CC2530 ZigBee smart sensor nodes** used in industrial warehouse monitoring.

### 1. 5-Segment Handle Encoding Rule
I designed a structured Handle code: **`88.12345/IOT-CC2530-V2-0001`**
- `88.12345`: National secondary node prefix for the industry.
- `IOT`: Enterprise or lab organization code.
- `CC2530`: MCU hardware model and product category.
- `V2`: PCB hardware revision.
- `0001`: 4-digit production serial number.
- **Advantages**: Global uniqueness (prefix + serial), high extensibility (easy to update if switching to `CC2652` or `V3`), and direct human readability for engineers.

### 2. Extended IoT Data Template & Dual-Carrier Design
- **Extended Metadata**: Beyond standard fields (product name, batch, production date), I added IoT-specific attributes: **MAC Address**, **Z-Stack Network Role** (`Coordinator` or `EndDevice`), and **Firmware Version** (to support future OTA updates).
- **Dual-Carrier Strategy**: I combined both **QR Codes** and **UHF RFID** tags:
  - *QR Code* on the outer case allows field engineers to scan a single node with a mobile phone to check its firmware and status.
  - *UHF RFID* inside the housing allows warehouse staff to scan and inventory hundreds of boxed nodes in seconds without opening the packages.

### 3. RESTful API Verification & ThingsBoard Integration
To verify the system logic, I designed and tested two **RESTful APIs** using JSON:
- **Registration (`POST /api/identifier/register`)**: Called after manufacturing to write the node's identifier, MAC address, network role, and firmware version into the resolution database.
- **Query / Resolution (`GET /api/identifier/query?identifier=...`)**: Resolves the ID and returns static attributes along with a **`redirectUrl`** pointing to the **ThingsBoard** IoT platform.

**Static Metadata vs Dynamic Telemetry (Key Distinction)**:
- **Static Data** (MAC address, hardware batch, production date) is stored in the **Identification Resolution Server**.
- **Dynamic Telemetry** (temperature, humidity, RSSI signal strength) is collected by the CC2530 node and streamed via a ZigBee gateway to **ThingsBoard**, visualized with a temperature Gauge (with a 60°C alarm threshold), humidity Timeseries Line Chart, Network Role Card, and RSSI Bar Chart.
- The **identifier** acts as the bridge: resolving the static ID yields the `redirectUrl` that takes the user directly to the live dynamic dashboard.
