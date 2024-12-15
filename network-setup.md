# Network Setup Documentation

## **Devices in the Network**

### **Router**
- **Model**
- **Interface 0/0**:
  - IP Address: `168.90.0.1`
  - Subnet Mask: `255.255.0.0`
- **Interface 0/1**:
  - IP Address: `210.3.14.1`
  - Subnet Mask: `255.255.255.0`

### **Switches**
- **Switch 1**:
  - **Model**
  - Hosts connected: 3 PCs, 1 laptop, 1 server
- **Switch 2**:
  - **Model**
  - Hosts connected: 3 servers, 1 PC

### **Hosts and IP Addresses**

#### **Hosts Connected to Switch 1**
| Device   | Type    | Assigned IP Address |
|----------|---------|---------------------|
| PC3      | Desktop | `168.90.0.4`        |
| PC4      | Desktop | `168.90.0.5`        |
| Laptop0  | Laptop  | `168.90.0.3`        |
| Server0  | Server  | `168.90.0.2`        |
| PC0      | Desktop | `168.90.0.64`        |


#### **Hosts Connected to Switch 2**
| Device   | Type    | Assigned IP Address |
|----------|---------|---------------------|
| PC2      | Desktop | `210.3.14.3`        |
| Server1  | Server  | `210.3.14.4`        |
| Server2  | Server  | `210.3.14.2`        |
| PC5      | Desktop | `210.3.14.5`        |



# DHCP Configuration Details
## Steps to Configure DHCP on the Router
### 1. Access the Router CLI
- Open the router in Packet Tracer.
- Navigate to the **CLI** tab.

### 2. Enter Global Configuration Mode
- Use the following commands to enter global configuration mode:
```
enable 
configure terminal 
```

### 3. Assign IP Addresses to Router Interfaces
- Configure the router interfaces that connect to the switches with their respective IP addresses
```
interface GigabitEthernet0/0
ip address 168.90.0.1 255.255.0.0
no shutdown
exit

interface GigabitEthernet0/1
ip address 210.3.14.1 255.255.255.0
no shutdown
exit
```


### 4. Create a DHCP Pool for the First Network (168.90.0.0/16)
- Create a new DHCP pool named `NETWORK1`
- Specify the network address and subnet mask for this pool
- Define the default gateway for the second network
```
ip dhcp pool NETWORK1
network 168.90.0.0 255.255.0.0
default-router 168.90.0.1
exit
```

### 5. Create a DHCP Pool for the Second Network (210.3.14.0/24)
- Create a new DHCP pool named `NETWORK2`
- Specify the network address and subnet mask for this pool
- Define the default gateway for the second network

```
ip dhcp pool NETWORK2
network 210.3.14.0 255.255.255.0
default-router 210.3.14.1
exit
```

### 6. Verify the Configuration
- Exit configuration mode and verify the DHCP setup:
```
show running-config
```