# IoT Communication
1. Communication Theory
2. ZigBee Theory & Laboratory
3. Other Protocols

## Communication Protocols (WPAN & LPWAN)

|Protoco|Frequency|Speed|Distance|Power|Feature|
|---|---|---|---|---|---|
|ZigBee|2.4, 868, 915|low|short|low|low power, low latenct, high network capacity|
|Bluetooth|2.45 ISM|1Mb/s|
|RFID|
|NB-IoT|




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


