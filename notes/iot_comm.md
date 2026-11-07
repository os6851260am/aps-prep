# IoT Communication
1. Communication Theory
2. ZigBee Theory & Laboratory
3. Other Protocols

## Communication Protocols (WPAN & LPWAN)|
1. ZigBee  
    Short-range, low power, no fee
2. Wi-Fi  
    High Throughput, High power, internet access
3. BLE  
    Low Power, short-range, P2P
4. NB-IoT  
    Long-range, fees, Low power  
5. RFID  
    Passive (Battery-free), Identity Tag
## ZigBee Theory
### Basic Theory
1. IEEE 802.15.4
2. Frequency: 2.4GHz, 868MHz, 915MHz.
3. 4-Layers:  
Application
Network
Data Link (MAC)
Physical

### Devices Categories  
1. Function  
    FFD: Full Function
    RFD: Reduced Function
2. Logical Device Role
    Coordinator: ZC
    Router: ZR
    End_Device: ZED

### Network Topology
1. Star
    1 ZC, multiple ZEDs
2. Tree
    1 ZC, multiple ZRs (connect to ZC), multiple ZEDs
3. Mesh
    1 ZC, multiple ZRs (inter-connect allowed), multiple ZEDs

### Address
1. 16-bit short address  
    assigned by parent node (ZR or ZC)  as joining the network  
    like IP address
2. 64-bit extended address  
    assigned by manufacturer, unmodifiable
    like MAC address

### Establishment of Network
1. initialized ZC scan the channel, build the PAN_ID, set its own address: 0x0000
2. new node broadcast and replied by the ZC/ZR  
new node compare the link quality and choose the best one as its parent

### Communication
1. Sender node: sender encapsulates the short address & endpoint # (like port number)
2. intermediate nodes: pass the message (routed by the routing table)  
    if routing table has no path:  
        AODVjr algorithm
3. receiver node: communicate with its parent spasmodically via polling

## ZigBee Laboratory
### 1. P2P Network Establishment
We took the experiment that 1 coordinator and 1 enddevice establishing network. 
1. Set the PAN_ID of the coordinator
3. Modify the "Coordinator.c" and "Enddevice.c": activate the LED as network established (via network state judgement), end device send a message and blink the LED after coordinator receiving and validating.

### 2. Topology Experiment
1. We used 1 ZC, 2 ZRs and 1 ZED.
2. We established the network b/t the 4 devices and attested the topology via ZC serial port output.
3. Modify the HAL function: when receive the "get" through serial port, look up the association table and neighbors table, print the address and parent node's address of each node.
4. According to the content printed, we could attest the topologic architecture.
