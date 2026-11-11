# IoT Communication
In this course, we learned the communication techniques of IoT. We covered ZigBee, WiFi, BLE, NB-IoT and RFID. We mainly focused on ZigBee and took some experiments about that. 

## Theory

### Protocols
These protocols have different features:
1. ZigBee is a short-range, low power protocol, so it's commenly used in Embedded System.
2. WiFi is a high-throughput, high power protocol which is able to access the internet.
3. BLE is a smartphone supported, low power, short range protocol, mainly used in P2P communication.
4. NB-IoT is a long-range, low power protocol, but it requires base sation and need to pay for that.
5. RFID is a passive (battery-free) protocol, commonly used in identity tag.

### Fundamental
ZigBee is based on the IEEE 802.15.4 standard. There're 4 layers: App. layer, Network layer, Data link layer and Physical layer. 
### Device
ZigBee devices functionally divided to 2 categories: FFD (Full-Function Device) and RFD (Reduced-Function Device) and logically divided to 3 categories: ZC (Coordinator), ZR (Router) and ZED (End Device). The topologic architecture includes multiple devices.

### Topology
There're 3 kinds of topologies of ZigBee network: Star, Tree and Mesh. 
Star topology is multiple ZED connect to the ZC, all the communications should go through ZC. 
Tree topology is level-by-level hierarchy, ZC is the root and multiple ZRs could be the parent nodes. Each node can only communicate with its parent or child. 
Mesh topology is inter-connected b/t ZC and multiple ZRs, so they could communicate to each other. 

### Address
The devices communicate via address. ZigBee address includes 16-bit short address and 64-bit extended address. Short address is just like IP address, assigned by its parent node. Extended address is like MAC address assigned by manufacturer and unchangeable.

## Laboratory
### 1. P2P Network Establishment
 We took the experiment of P2P network establishment on IAR workbench: 1 ZC and 1 ZED. Modify the PAN_ID for network and the Coordinator.c, Enddevice.c to implement:  
1.  for coordinator: Activate LED1_0 as the network established. Blink the LED1_1 as receiving the message "LED" from End device.
2. for End device: Detect the network status, send "LED" as the network established. 

### 2. Network Topology Attest
And we also took a experiment to attest the topologic architecture of ZigBee network. 1 ZC, 2ZR and 1 ZED. Connect PC to ZC via serial port. Modify the function of ZC: imput "get" in serial assistant, the nodes look up their association table and neighbors table, print back its short address and its parent's address via serial port. Then we could attest the topologic architecture based on that.