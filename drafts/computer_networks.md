# computer_networks

This course is located at the communication layer of IoT 3-layer hierarchy. We learned the top-down 5-layer protocol stack: Application, Transport, Network, Link, Physical. Each layer is responsible for different function, encapsulating and passing to next layer.

> **1. Application Layer (Top)**
This layer is closest to the user. It generates or receives the communicating message.
> 
> - *Core function*: Defining rules for user software to communicate.
> - *Key protocols*: **HTTP** for web browsing, **DNS** for translating domain names into IP addresses.
> - *Data unit*: **Message**.
> 
> **2. Transport Layer**
> This layer provides the service for application layer. The message from app. layer go through socket and received by transport layer, this process is called multiplexing.
> 
> - *Core function*: Deciding how data should be delivered.
> - *Two main protocols*: **TCP**, which is connection-oriented and reliable using handshakes and retransmissions; and **UDP**, which is connectionless and fast, prioritizing low latency over zero packet loss.
> - *Data unit*: Encapsulate the message with header to **Segment**.
> 
> **3. Network Layer**
> This layer moves data from **host to host** across multiple connected networks. So it’s inter-network transmission.
> 
> - *Core function*: Network layer is divided to 2 planes: Control plane for **routing** and data plane for **forwarding**.
> - *Key protocol & device*: **IP protocol** (IPv4 / IPv6). IP address is the location of the device in the global network.
> - *Data unit*: Encapsulate segment with header to **Datagram** (or Packet).
> 
> **4. Data Link Layer**
> This layer handles data transfer between **adjacent nodes** within the same local network.
> 
> - *Core function*: Error detection, and Node-to-node transmission by **MAC** address.
> - *Key protocols*: **Ethernet**, **ARP(Determine MAC from IP), CRC**.
> - *Data unit*: Encapsulate the datagram with header to **Frame**.
> 
> **5. Physical Layer (Bottom)**
> The base layer that transmit the bits in physical world.
> 

# Lab

> "In our lab lectures, we used **Cisco Packet Tracer** to complete two practical tasks: **IP Subnetting** and **TCP Three-Way Handshake Simulation**.
> 
> 
> **1: Subnet Division**
> We take the experiment of dividing a network to 2 subnets.
> 
> - Set the subnet mask as `255.255.255.0`, and assign IP for the devices: `192.168.0.x` for subnet 1, `192.168.1.x` for subnet 2.
> - This gave us two subnets: **Subnet 1** (`192.168.0.0/24`) and **Subnet 2** (`192.168.1.0/24`).
> - In Cisco Packet Tracer, ping the device in the same subnet, it’s okay. But there was a timeout in inter-subnet ping. Then, I set a router and connect host 0 and host 1 to port 0 and port 1, configure the **default gateway**. Now, the inter-subnet communication is okay.
> 
> **2: TCP Three-Way Handshake in Simulation Mode**
> To attest the 3-way handshake connection of TCP, I made a simulation in Packet Tracer.
> 
> - I added a Web Server in Subnet 2 and opened the Web Browser on a PC in Subnet 1.
> - I switched Packet Tracer from Realtime Mode to **Simulation Mode** and showed **TCP** and **HTTP**.
> - When I entered the server's IP in the browser and clicked 'Capture/Forward', I watched the three packets step-by-step:
>     1. **Step 1 (SYN)**: The PC sent a TCP segment with the **SYN** flag = 1 and an initial sequence number = ISN_A.
>     2. **Step 2 (SYN-ACK)**: The server replied with the flag **SYN = 1** and **ACK = 1**, Send initial sequence number = ISN_B, and ACK number = ISN_A + 1.
>     3. **Step 3 (ACK)**: The PC replied with **ACK = 1** and Sequence number = ISN_A + 1, ACK number = ISN_B + 1. Now the connection established.