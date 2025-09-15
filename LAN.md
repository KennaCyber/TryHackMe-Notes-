# Introducing LAN Topologies

- Topology refers to the design or look of the network at hand.
  
**Star Topology**
  
- Devices are individually connected via a central networking device (switch or hub). 

- It's the most common one because of its reliability and scalability despite the cost.

- Any info is sent to the central device.

- It's more expensive because more cabling and dedicated networking equipment are required.
  
- However, it's more scalable (easy to add more devices).

- The more it scales, the more maintenance is required to keep it functional. This can make troubleshooting faults harder.

- If the centralized hardware that connects devices fails, the devices can't receive/transmit data (but they're often robust).

**Bus Topology**

- Relies on a single connection called the backbone cable.

- All data for each device travels along the same cable, and it's prone to becoming slow and bottlenecked (a lot of traffic in a narrow area).

- Bottleneck causes difficult troubleshooting since it's hard to identify which device is having issues, since data is traveling along the same route.

- It's easier and more cost-efficient

- If the cable breaks, the data can't be received/transmitted

**Ring Topology**

- Devices are connected directly to each other to form a loop, so little cabling is required and less dependence on dedicated hardware.

- Data is sent across the loop until it reaches the destined device, so they act like mini post offices.

- When it receives a data packet, it first checks if it's for itself. If yes, it reads it. If it's for another device, it will then forward it along the ring.

- If it has its own data to send, it will prioritize sending it first, and then it can forward data for other devices.

- This prevents devices from endlessly forwarding others' data without getting to send their own.
  
- It's easier to troubleshoot since  there's only one direction for data to travel. However, the data has to visit multiple devices.
  
- They are less prone to bottlenecks; however, a broken device or cable issue can break the entire network.

**What is a Switch?**

- Dedicated devices within a network that connect multiple devices using Ethernet cables.

- The devices are plugged into a switch's port (where the cable is inserted).
  
- Usually found in larger networks (businesses, schools, etc.).
  
- Switches can connect a large number of devices with multiple ports to plug into (4, 8, 16, 24, 32, and 64).
  
- More efficient than hubs and repeaters. They keep track of what device is connected to which port. Due to this, packets are sent to the intended target (which reduces network traffic).

**What is a Router?**

- A router connects networks and passes data between them by using routing.

    - Ex. Home network to the internet.

- Routing refers to the method of transferring data between different networks.

- This process involves selecting a path for the data to follow, so the router creates a path between networks to deliver data.
  
- This helps when many paths connect devices.
  
- Switches and routers can be connected, and this increases the redundancy of a network since it adds more pathways.
  
- Since there are multiple paths for data, it may take a longer route/travel through more devices, which can cause slower performance.
  
- When one path fails, another is available (the network stays online).
---
**A Primer on Subnetting**

- Subnetting is splitting up a network into smaller, miniature networks within itself.

    - Everyone wants cake, but there's scarcity, so you slice it up
      
    - Businesses have different departments (Accounting, Finance, Human Resources)
      
- Network administrators use subnetting to categorize and assign specific parts of a network.
  
- Networks need to know which group of devices to send data to, so they must be organized.
  
    - A subnet is represented by a number(subnet mask)
 
- Recall: An IP address is made up of 4 octets (32 bits), and so is a subnet mask, ranging from 0 to 255.
  
- Subnets use IP Addresses to identify the network address, host address, and default address.
  
- Network Address: Entire subnet or network (starting point of a network range)
  
    - Device with IP 192.168.1.100 belongs to the network 192.168.1.0
      
- Host Address: Specific device within a subnet
  
    - Device 192.168.1.100 within 192.168.1.0/24 network
      
- Default Gateway: Connects your local network to other networks, acts as an exit point for your network
  
    -  Device 192.168.1.100 wants to reach 8.8.8.8 (Google DNS), so the device sends the data to the default gateway (maybe 192.168.1.254). It then forwards it to the internet. Can use any host address, but usually use the first or last (.1 or .254).
      
- In small networks (home), you will be on one subnet, and it's unlikely you need more than 254 devices connected simultaneously.
  
    - Businesses and offices will have more devices (PCs, printers, cameras, sensors) for subnetting
      
- Subnetting provides efficiency, security, and full control.
---
**ARP**

- Recall: A MAC Address and an IP address are responsible for identifying themselves on a network.

- ARP (Address Resolution Protocol) links an IP address to a MAC address.
  




  
