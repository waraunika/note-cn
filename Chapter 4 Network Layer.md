Functions:
1. Routing:
	- When a packet reaches the router's input link, the router will move the packets to the next router
2. Logical Addressing:
	- the data link layer implements the physical addressing and the network layer implements logical addressing
	- logical addressing is also used to distinguish between source and destination system
	- the network layer adds a header to the packet which includes logical addresses of both the sender and the receiver
3. Internetworking:
	- main role of network layer
	- provides logical connection between different types of networks
4. Fragmentation:
	- the fragmentation is a process of breaking the packets into the smallest individual data units that travel through different networks
# 4.1 Internetworking and devices:
- process of interconnecting a set of independent networks is called internetworking
- routing between two networks of the same or different kinds is called internetworking
- devices and OSI Model:
  ![[devices_and_osi.png]]
## A. Repeaters
- physical layer device which is used to regenerate the signal between similar networks
- extends the distance over which a signal may travel
- require a small amount of time to regenerate the signal, which can cause propagation delay, which can affect network communication if multiple repeaters in a row
## B. Hubs
- aka multiport repeater is a physical layer device which transmits a received signal to all other ports and vice versa
- low-cost device and easy integration
- reduces the bandwidth
## C. Bridges
- aka two ports switch is a data link layer device that can divide an overloaded network into smaller, more efficient networks
- it maintains a MAC table with MAC address and port no. and decides whether to forward the frame or not
- bridges filter traffic based on the DA of the frame, and divides network into different LAN Segments
## D. Switches
- aka multiport bridge is a data link layer device which is a hub with some intelligence
- allows each workstation to transmit information based on physical address
- doesn't distribute the signal without verifying whether the signal needs to propagate to given port
## E. Router
- a network layer relay that connects multiple networks and uses routing, to forward data packets based on their IP addresses
- can be used to link two dissimilar LANs
- it receives a packet and selects the optimum path to forward the packet across the network
## F. Gateway
- software or combination of software and hardware, that works for exchanging data among networks which are using different protocols for sharing data
- used to connect multiple networks and pass packets from one network to the other network
- able to convert or translate the data format, although the data itself remains unchanged
# 4.2 Addressing
## A. Internet Protocol
- The network protocol in the Internet is called internet protocol.
- this is host to host network delivery protocol designed for the internet.
- IP is a connection-less datagram protocol with no guarantee of reliability
- IP can only detect the error and discard it if it is corrupted
### A.1 Internet Protocol Address
- An IP address is an identifier used in the IP layer of the TCP/IP protocol suite to identify the connection of each device to Internet.
- MAC address is a data link layer address also known as physical address that is recognised only in a local network.
- So, IP address is required for the globally recognised, also known as logical address.
- IP address is made of four bytes (32 Bits)
- Notation:
  Binary      10000000.00001011.00000011.00011111
  Decimal   128.11.3.31
- IP address is generally written in dotted decimal notation.
### A.2 Classes of IP Address
- There are 5 classes; A, B, C, D E
- Usage:
	- A, B, C: unicast
	- D: multicast
	- E: reserved
- each class occupies some part of the whole address space
- Nowadays, this concept has become obsolete and has been replaced with classless addressing.
- IP addresses, before 1993 used the classful addressing where classes have a fixed number of blocks and each block has a fixed number of hosts.
- In IPv4 addresses of class A, B, C, the first part of the address is considered as Network ID and the second part is called Host ID.
- The size of these parts varies with the classes
- Network ID: denotes the address of the network
- Host ID: denotes the address of the host attached to the corresponding network
- in Class A, the Network ID is defined by the first byte of the address, and the rest 3 bytes define the host ID
- in class B, the first 2 bytes, then class C, the first 3 bytes define the network address. remaining bytes define the Host ID
- figure demonstrating this:
  ![|600][classful_addresses.png]
### A.3 Calculation of IP Range
- Class A:
	- 00000000.00000000.00000000.00000000 to
	  01111111.11111111.11111111.11111111
	- i.e. 0.0.0.0 to 127.255.255.255
- Similarly,
	- Class B: 128.0.0.0 to 191.255.255.255
	- Class C: 192.0.0.0 to 223.255.255.255
	- Class D: 224.0.0.0 to 239.255.255.255
	- Class E: 240.0.0.0 to 255.255.255.255
### A.4 Address Distribution Concept
- Class A:
	- net.host.host.host
	- network bits = 7 bits
	- host bits = 24
	- total no. of networks = 2$^7$ = 128
	- total no. of hosts = 2$^{24}$ = 216,777,214
- Class B:
	- net.net.host.host
	- network bits = 14
	- host bits = 16
	- total no. of network = 2$^{14}$ = 16,384
	- total no. of hosts = 2$^{16}$ = 65,534
- and so on for C
- Class D:
	- used as multicast IP
	- it is a unique network that directs packets with that destination address to predefined groups for IP address.
- Class E:
	- reserved for future use
### A.5 Disadvantage of Classful Addressing
1. If we consider class A, the number of address in each block is more than enough for almost any organisation. So it wastes addresses
2. Same is the case with class B, probably an organisation receiving blocks from class B would not require that many addresses
3. A block in class C may be too small to fulfil the address requirement of an organisation
4. Each address in class D defines a group of hosts. Hosts need to multicast the address. So the address are wasted here too
5. address of class E are reserved for the future purpose which is also wastage of addresses
6. in classful addressing, addresses are not assigned according to user requirements, which means, a block of fixed size is assigned, and this will lead to excess or little addresses
### A.6 Types of IP address
- IP address is categorised into two types: Public IP and Private IP.
- Public IP: the number used on the Internet
- Private IP: any organisation can use an address out of this set without permission from the internet authorities. they are free to use
- They are:
	- 10.0.0.0 to 10.255.255.255, 2$^{24}$ 
	- 172.16.0.0 to 172.31.255.255, 2$^{20}$
	- 192.168.0.0 to 192.168.255.255, 2$^{16}$
### A.7 IP (IPv4) Header Format
- An IPv4 datagram consists of a header part and a body or payload part.
- the header has a 20-byte fixed part and a variable length optional part.
- every protocol follows a different header format for its data to be transmitted and received reliably
- the header format is shown below:
  ![|600][ipv4_header.png]
#### Description
| Field                  | Size     | Description                                                                                                                                                                                                           |
| ---------------------- | -------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Version                | 4 bits   | indicates the version number of the IP packet so that the revised version can be distinguished from previous version                                                                                                  |
| Internet Header Length | 4 bits   | specifies the length of the IP header in unit 32 bits.<br>in case of no option present in the header, IHL will have a value of 5<br>so, if the value of IHL > 5, then length of option field can be easily calculated |
| TOS                    | 8 bits   | Type of Service (e.g. text, audio, video)<br>specifies priority of the packets based on delay, throughput, reliability and cost requirements                                                                          |
| Total Length           | 16 bits  | This field specifies the number of bytes of the IP packet including header and data<br>As 16 bits are assigned to this field, the maximum length of the packet is 65,635 bytes                                        |
| Identification         | 16 bits  | used to identify which packet a particular fragment belongs to, so that fragments for different packets don't get mixed up                                                                                            |
| Flags                  | 3 bits   | deals with fragmentation and reassembly of packets of data units.<br>Unused bit, Don't fragment (DF) bit and More fragment (MF) bit                                                                                   |
| Fragment Offset        | 13 bits  | identifies the location of the fragment in a packet<br>the value measures the offset in a unit of 8 bytes, between the beginning of the packet to be fragmented and the beginning of the fragment                     |
| Time to Live           | 8 bits   | TTL indicates the amount of time in seconds a packet is allowed to remain in the network                                                                                                                              |
| Protocol               | 8 bits   | This field defines which upper layer protocol data are encapsulated in the datagram.<br>it selects the suitable protocol for next layer (e.g., connection-less or connection-oriented)                                |
| Header Checksum        | 16 bits  | This field verifies the integrity of the header of the IP packet                                                                                                                                                      |
| Source IP Address      | 32 bits  | literally the name                                                                                                                                                                                                    |
| Destination IP Address | 32 bits  | literally the name                                                                                                                                                                                                    |
| Options + Padding      | variable | rarely used to include special features such as security level, the route to be taken and time stamp at each router.<br>is used to make the header of a multiple of 32-bit words                                      |
| Data                   | variable | The data field must be an integer multiple of 8 bits in length.<br>the maximum length of the datagram (data field + header) is 65,535 octets                                                                          |
## B. Miscellaneous of IP
#### B.1 Optimisation of uses of IP address:
1. Classless Inter-Domain Routing (CIDR):
	- The primary solution. it eliminates the rigidity of IP address classes
	- Allows for variable-length subnet masking (VLSM), enabling the creation of subnets of almost any size, leading to highly efficient address allocation and reducing waste
2. Private IP Address and Network Address Translation (NAT):
	- Private Addresses: not routable on public internet. This allows every organisation to reuse the same internal addresses
	- NAT: a router with NAT function translates multiple private IP addresses into a single (or few) public addresses for internet communication. This is why home network has many devices, but only one public IP
3. Dynamic Host Configuration Protocol (DHCP):
	- Dynamically assigns IP to devices *only when they are connected to the network*
	- This mechanism means a company needs far fewer IP addresses than the total number of devices it owns, as not all devices are online simultaneously.
4. IP Address Conservation through Subnetting:
	- Breaking a large network into smaller subnets prevents the assignment of an entire large address block to a small network, ensuring addresses are allocated according to actual need.
#### B.2 Classful vs Classless Addressing
| Feature                  | Classful                                                                                               | Classless                                                                                                           |
| ------------------------ | ------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------- |
| Concept                  | original IPv4 address architecture, where the address space is divided into pre-defined, fixed classes | modern addressing scheme where the boundary between the network and host part is flexible and specified by a prefix |
| Determining Network/Host | Based on the first few bits of the IP address. The class itself defines the network/host boundary      | Based on a subnet mask (or prefix length) like `/24` which is explicitly provided                                   |
| Address Flexibility      | Inflexible. leads to wastage                                                                           | Highly flexible, allows efficient allocation                                                                        |
| Notation                 | Referred to by their class (e.g., "a class B network")                                                 | Referred to by their CIDR notation (e.g., 192.168.1.0/24)                                                           |
| Routing Updates          | Routing protocols like RIPv1 do not send subnet mask information                                       | Routing protocols like OSPF, RIPv2 send the subnet mask (prefix length)                                             |
| Modern Usage             | Obsolete. Replaced by classless in 1990's                                                              | Standard for all modern IP Network design                                                                           
## C. DHCP (Dynamic Host Configuration Protocol)
- DHCP is a client-server protocol in which the client sends a request message and the server returns a response message
- DHCP is used extremely in LANs and in residential internet access
- the operation can be summed up in the figure:
  ![|600][dhcp_operation.png]
- Operations:
	- client broadcasts a DHCP DISCOVER message to identify any available DHCP servers on the network.
	- A DHCP server replies with a DHCP OFFER message.
	- This message offers to the client a lease that contains such information as the IP Address and subnet mask to be assigned, the IP address of the DNS server, and the IP address of the default gateway.
	- After the client receives the lease, the received information must be renewed through another DHCP REQUEST message prior to the lease expiration
# 4.3 Subnetting
## A. Concept
- Subnetting is the technique of logical division of the large network into the smaller manageable sub-networks
- increases routing efficiency, enhances the security of the network, reduces the size of the broadcast domain.
- Adv:
	- Subnetting breaks large networks in smaller networks and smaller networks are easier to manage
	- reduces network traffic by removing collision and broadcast traffic, which overall improves performance
	- allows applications to apply network security policies at the interconnection between subnets
	- allows to save money by reducing the requirement for IP range
- Each IP class is equipped with its own default subnet mask which binds that IP class to have a pre-fixed number of networks and pre-fixed number of Hosts per network.
- CIDR or Classless Inter Domain Routing provides the flexibility of borrowing bits of Host part of the IP address and using them as Network in Network, called Subnet
- By using subnetting, one single class A IP Address can be used to have smaller sub-networks which provides better network management capabilities
## B. Subnet Mask
- 32 bit number that masks the IP address and divides the IP address into the network address and sub-network address from an IP address.
- For obtaining the subnet mask, assign all the network addresses as 1's and all the host's address as 0's.
- IP address AND'ed with the subnet mask gives the network ID
## C. Subnetting Process:
When subnetting a network following five things  should be determined
1. Maximum number of subnets = 2$^{\text{no. of subnet bits}}$
   Subnet bit is represented by '1'
2. Maximum number of hosts = 2$^{\text{no. of subnet bits}}$ - 2
   Host bit is represented by '0'
3. Valid subnets = 256-subnet mask = block size
4. Broadcast address for each subnet = number right before the value of the next subnet
5. Valid host = these are numbers between the subnet and broadcast address
# 4.4 Routing
## A. Concept
### A.1 Introduction
- process of selecting the best path for network traffic to travel from a source to a destination across one or more networks
- It involves two key functions inside a router
	- Forwarding: The process of sending a packet that has arrived at a router to the correct outgoing interface. This is a direct data-plane operation using a pre-built routing table
	- Routing (Protocol): The control-plane process of building and maintaining the routing table. This is where the routing algorithms and protocols (like OSPF, BGP) operate to dynamically learn network paths
- Core and main function of Network Layer
### A.2 Importance
- Interconnects Networks: It enables communication between different networks, forming the Internet and other large inter-networks. Without routing, devices could only talk to others on their own local network
- Finds Optimal Paths: Routing algorithms determine the most efficient path among many possible options, considering factors like speed, cost, reliability
- Provides Scalability: It allows the network to grow to a massive scale by breaking it into manageable segments (subnets, autonomous systems) that routers can intelligently connect
- Ensures Reliability and Adaptability: Dynamic routing protocols can automatically find alternative paths if a link fails or become congested, making the network robust and fault-tolerant
### A.3 Criteria for a Good Routing Algorithm
- Correct and simple: it must correctly deliver packets to their intended destination. The algorithm itself should be simple enough to operate with minimal overhead
- Robust and Stable: It must be able handle change in network topology (e.g., link failures) and varying traffic loads without crashing (robustness) and must converge to a stable state without oscillating or creating loops (stability)
- Fair and Efficient: It should provide a reasonable quality of service to all users (fairness) while optimising the use of network resources, such as bandwidth and router processing power (efficiency)
- Optimal: It should select the best path based on a specific metric (e.g., shortest path, lowest cost, highest speed) to improve overall network performance
## B. Techniques
## B.1 Static Routing
- **Concept**
	- network paths are manually configured by an administrator. The routing table is built and maintained by hand
- **Working**:
	- An administrator defines the specific routes for data to take.
	- these routes remain unchanged unless manually updated
- **Adv**:
	- Simple & Predictable: easy to implement in small network; traffic follows a fixed, known path
	- Secure & Efficient: no routing protocol messages are sent, revealing no network information and consuming no bandwidth for route updates
	- Low Resource Use: Requires minimal router CPU and memory
- **Disadv**:
	- Not Scalable: Managing manual configurations becomes impossible in large, complex networks.
	- Lack of Fault Tolerance: If a link fails, the network cannot automatically reroute traffic leading to an outage until an administrator manually intervenes
- **Best for**: Small networks, stub networks, and security-critical paths where traffic flow must be strictly controlled
### B.2 Dynamic Routing
- **Concept**:
	- Routers automatically discover remote networks and share routing information with each other using routing protocols (e.g., OSPF, EIGRP, BGP)
- **Working**: 
	- Routers exchange messages to build their own routing tables.
	- They dynamically update these tables when a network link fails or a new one is added
- **Adv**:
	- Scalable & Adaptive: Perfect for large networks; automatically adapts to topology changes like link failures
	- Fault Tolerant: If one path fails, the routing protocol automatically finds and uses an alternative path without manual intervention
	- Reduced Administrative Overhead: Once configured, the network manages itself
- **Disadv**:
	- Complexity: More complex to configure and troubleshoot than static routing
	- Resource Overhead: Uses router CPU, memory and network bandwidth to exchange routing updates
	- Less secure: Requires careful configuration to prevent unauthorised routers from participating and learning the network topology.
- **Best For**: Most modern networks, especially medium to large enterprise and the Internet core, where adaptability is essential
## C. Routing Table for classful address
- **Concept**: A routing table is a database stored in a router or network device that contains paths (routes) for directing data packets toward their final destination across an IP network
- **Key Components**:
	- Destination: target network or host IP address
	- next hop: the IP address of the next router to which the packet should be forwarded
	- Interface: the physical or logical port on the device used to reach the next hop
	- Metric: A value representing the "cost" of the path, used to select the best route when multiple paths exist
- **Working**:
	1. a device receives a packet and examines its destination IP address
	2. it performs a lookup in its routing table to find the best-matching entry
	3. the table entry provides the next hop IP address and the outgoing interface
	4. the device forwards the packet accordingly
- **Maintenance**:
	- Static Routing: Entries are manually added by a network administrator
	- Dynamic Routing: Entries are automatically learned and updated by routers using routing protocols (e.g., OSPF, BGP) allowing the network to adapt to changes
## D. Miscellaneous
#### Routed vs Routing Protocols
| Feature     | Routed Protocol                                                                                                                       | Routing Protocol                                                                                                               |
| ----------- | ------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------ |
| Definition  | protocol that defines the format and structure of data packets as they travel across a network.<br>it is the passenger in the network | protocol that allows routers to dynamically share information and build routing tables.<br>it is the map or GPS of the network |
| Function    | Provides the addressing that routers use to make forwarding decisions. <br>It carries user data                                       | Determines the best path for the routed protocol's packets to take.<br>it carries information between routers                  |
| Operates At | Network Layer                                                                                                                         | also at network layer, but its messages are exchanged between routers and do not carry end-user data                           |
| Example     | IP, IPv6, IPX                                                                                                                         | RIP, OSPF, EIGRP, BGP                                                                                                          |
#### Analogy
- Routed Protocol is like the car that carries the passenger
- routing protocol is the GPS navigation system that tells the car which roads to take
# 4.5 Routing Algorithms
## A. Shortest Path Algorithms
- **Purpose**:
	- to find the most efficient path between two nodes (routers) in a network, typically based on a "cost" metric like distance, delay or hop count
- **Concept**:
	- the network is modelled as a graph
	- where routers are nodes and communication links are edges with associated costs
	- the algorithm calculates the path with the lowest total cost between a source and destination
- **Dijkstra's Algorithm**:
	- most widely used shortest path algorithm.
	- it finds the shortest path from a single node to all other nodes in the network
- **Workings**:
	1. Initialisation: Start with the source node. Assign it a cost of 0 and mark it as permanent. All other nodes are marked as tentative with the initial cost of infinity.
	2. Examination: Examine all neighbours of the last permanent node. For each neighbour, calculate a new cumulative cost (current node's cost + link cost).  If this new cost is lower than the existing tentative cost, update it
	3. Selection: From all tentative nodes, selecting the one with the smallest cost and mark it as permanent. This node's shortest path is now confirmed
	4. Repetition: Repeat steps 2 and 3 until the destination node becomes permanent, or until all nodes are permanent
## B. Flooding
- **Concept**: A simple, brute-force routing algorithm where incoming packet is sent out on every outgoing link except the one it arrived on
- **Working**:
	1. A router receives a packet
	2. It immediately transmits a copy of that packet to all of its neighbours
	3. This process repeats at every router, effectively "flooding" the entire network with the packet
- **Key Mechanism to Prevent Infinite Loops**: Hop Count
	- A counter in the packet header is decremented at each hop. When it reaches 0, the packet is discarded.
	- This gives the packet a finite lifetime
	- Stops from infinite duplication of same message packet
- **Use**: While not used for standard routing, principle of flooding can be used in discovering routing information, wireless ad-hoc networks, etc.
  ![[flooding_1.png]]
  ![[flooding_2_3.png]]
## C. Distance Vector Routing
- **Concept**: 
	- A decentralised routing algorithm where each router maintains a table (a "vector") of the estimated distance (metric e.g., hop count) to every destination in the network
	- Routers periodically share their entire routing table only with their immediate neighbours
- **Working**
	- works on the principle of Bellman-Ford Equation
	- each router updates its table using the formula:
	- Destination Cost = min (Current Cost, Neighbour's Reported Cost + Link Cost to Neighbour)
	- If a neighbour updates to a router that there is a cheaper path to destination, then the router updates its table to send traffic via that neighbour.
- **Count-to-infinity Problem**:
	- Cause:
		- main problem is that no router ever has complete knowledge of the network path.
		- Routers only know the next hop and total cost, not the full route
		- this makes them vulnerable to forming routing loops when a link fails
	- Example:
		- Imagine four routers in a line: A --- B --- C --- D
		- initially, all routers know the correct hop count to D.
		- A's table: To reach D, next hop is B, cost  = 3
		  B's table: To reach D, next hop is D, cost = 2
		  C's table: To reach D, next hop is D, cost = 1
		  D's table: To reach D, cost = 0 (is directly connected)
		- Step 1: Link between C and D fails. now C marks its route to D as invalid (cost = $\infty$)
		- Step 2: Before C can advertise this, B sends its regular update to C, saying "I can reach D with a cost of 2"
		- Step 3: C thinks "B can reach D in 2 hops" and "B is my neighbour of 1 hop" so "i must be able to reach D with 2+1 = 3 hops". C updates its table to reach D via B of cost 3
		- Step 4: C now advertises to B: "I can reach D with a cost of 3"
		- Step 5: B undergoes same process as C, and reaches the conclusion: "Update my route to D via C with a cost of 4"
		- and this continues till the distance increasing to infinity from all router's perspective, since B also updates A about its increase of hop count
	- Solutions:
		1. Defining Infinity to max hop count
			- so that it will be considered unreachable
		2. split horizon:
			- rule: never advertise route back to the neighbour from which it was learned
		3. Route Poisoning & Poison Reverse:
			- when a link fails, the router immediately advertises that destination with an infinite metric, actively poisoning the route
## D. Link State Routing
-  **Concept**:
	- A routing algorithm where every router constructs a complete and identical map of the entire network topology
	- each router then independently calculates the shortest path to every destination using this map (typically with Dijsktra's algorithm)
- **5 steps of Link State Routing**:
	1. Discover Neighbours:
		- each router starts by identifying all other routers directly connected to it by sending a simple "hello" packet on each of its links
	2. Measure Link Cost:
		- the router actively measures the "cost" (e.g., delay, bandwidth) to each of its neighbours.
		- this cost becomes the weight of the link on the network map
	3. Build Link State Packet (LSP):
		- the router creates a packet (the LSP) containing its identity, a list of its neighbours and the cost to each one.
		- This packet represents its piece of the network's map
	4. Flood the LSP:
		- The router uses controlled flooding to distribute its LSP to every other router in the network.
		- Each router that receives a new LSP forwards it out on all links except the one it came from
		- This ensures every router gets a copy of every LSP
	5. Compute the shortest path:
		- Once a router has collected LSPs from all others, it has a complete graph of the network
		- it then runs Dijkstra's algorithm on this graph to compute the shortest path from itself to every other network node, building its routing table
## E. Internet Control Message Protocol (ICMP)
- network layer protocol that helps IP to handle some errors that may occur in the network layer delivery
- ICMP is used to test the internet, which works at Network Layer
- ICMP differs from transport protocols like TCP, UDP, in that it is not typically used to exchange data between systems, nor is it employed by end-user network applications
- exception being some diagnostic tools like ping and trace-route
- it is management protocol and messaging service provider for IP
- Some of the messages of ICMP are:
	- Destination unreachable: When router cannot locate the destination
	- Time exceeded: When a packet is dropped because of time out
	- Parameter Problem: If a router discovers a missing value in any field of the datagram, it discards the datagram and the messages is sent to source
	- Echo: used to see if a given destination is reachable alive
	- Echo reply: upon receiving an echo message, the destination is expected to send an Echo Reply message back
## F. ARP (Address Resolution Protocol)
- **Purpose**:
	- A critical protocol used to discover the Physical (MAC) Address of a device on the local network, when only its logical (IP) address is known
	- on a local network like Ethernet, data is delivered using MAC address, but applications use IP addresses. ARP bridges this gap.
- **Working**:
	- ARP Request (Broadcast)
		- A device that needs a MAC address creates an ARP Request packet
		- packet contains the target IP address and the sender's own IP and MAC address
		- this packet is broadcast to every device on the LAN
	- ARP Reply (Unicast)
		- all devices on the network receive the broadcast, but only the device with the matching IP address responds
		- that device sends back a directed ARP Reply packet (unicast) containing its MAC address
	- Cache the result
		- the original device receives the reply and stores the IP-to-MAC mapping in its ARP Cache (a temporary table in memory)
		- the next time it needs to send data to that IP, it can find the MAC address in its cache without another ARP request
- operation in figure:
  ![[arp_protocol.png]]
- **Caching & Management**:
	- ARP cache stores the recently learned IP-to-MAC mappings to improve efficiency and reduce network traffic
	- entries are not permanent. they are kept for a short period and then flushed out
	- if a device's NIC is replaced or its IP address changes, other devices' cached entries become invalid and the old entry will automatically be flushed
## G. RARP (Reverse Address Resolution Protocol)
- RARP is used to map the MAC address to the IP address.
- reverse of ARP
- to find the destination address the router broadcasts the MAC address by asking what is the logical address of the router having this MAC address
- then the router matching the mac address replies back to the source by sending the IP address
- working operation:
  ![[rarp_protocol.png]]
# 4.6 Routing Protocols
- routing protocol is the implementation of a routing algorithm in software or hardware
- a routing protocol uses metrics to determine which path to utilise to transmit a packet across an inter-network
- specifies how routers communicate with each other, disseminating information that enables them to select routes between any two nodes on a computer network.
- routing algorithms determine the specific choice of route.
- each route has a prior knowledge only of networks attached to it directly.
- Types:
	- Interior Gateway Routing Protocol (IGRP) or intra-AS Protocol
		- RIP
		- OSPF
	- Exterior Gateway Routing Protocol (EGRP) or inter-AS Protocol
		- BGP
#### Autonomous System
- a group of networks and routers under the authority of networks and routers under the authority of a single administration
- routing inside an autonomous system is referred to as interior routing
- routing between autonomous systems is referred to as exterior routing
- each AS can choose one or more routing protocols to handle routing inside the AS.
- however, only one inter domain routing protocol handles routing between AS's.
## A. Routing Information Protocol (RIP)
- **Overview**: 
	- RIP is a distance vector, interior gateway protocol (IGP) designed for small, stable networks.
	- it uses hop count as its sole metric to determine the best path
- **Characteristics**:
	- Metric: Hop Count (the number of routers a packet must pass through). The maximum allowed is 15, making RIP unsuitable for large networks
	- Update Mechanism: Routers broadcast their entire routing table to their immediate neighbours every 30 seconds.
- **Versions**:
	- RIPv1: Classful. Doesn't include subnet mask information in updates, so doesn't support VLSM or CIDR
	- RIPv2: Classless. Includes subnet masks, supports authentication and uses multicast for updates, making it more efficient and secure
	- RIPng: Designed for IPv6
- **Limitations of RIP**:
	- Increased network traffic: RIP checks with its neighbouring routers every 30 seconds, which increases network traffic
	- Maximum hop count: RIP has a maximum hop count of 15, which means that on large networks, other remote routers may not be able to be reached
	- Closest may not be shortest: Choosing the closest path by hop count doesn't necessarily mean that the fastest route was selected. RIP doesn't consider other factors when calculating the best path
	- RIP only updates neighbours so the updates for non-neighbouring routers are not first-hand information
## B. Open Shortest Path First (OSPF)
- **Overview**:
	- OSPF is a widely used link-state, IGP
	- unlike RIP, it uses a complex metric (primarily based on link cost, often inversely related to bandwidth) to determine the best path, 
	- making it suitable for large enterprise networks
- **Characteristics**:
	- Uses the link state routing algorithm and Dijkstra's SPF algorithm to calculate loop-free paths
	- floods Link State Advertisements (LSAs) immediately upon a topology change, allowing all routers to quickly recalculate routes
	- Divides a large network into areas to limit the scope of routing updates and reduce CPU/memory overhead on routers. Area 0 is mandatory backbone area
	- Fully supports VLSM CIDR.
- **Operation**:
	- OSPF routers from neighbour relationships by exchanging Hello packets. Not all neighbours become adjacent (fully synchronised).
	- adjacent routers synchronise their Link State Databases (LSDB) by exchanging LSAs which describe the state of the router's links
	- Each router runs the DIjkstra's algorithm on the synchronised LSDB to build a shortest path tree with itself as the root
	- The best paths from SPF tree are installed into the IP routing table.
- OSPF routers stores routing topology in 3 tables:
	- Neighbour table: stores information about OSPF neighbours
	- Topology table: stores the topology structure of the network
	- Routing table: stores the best routes
## C. Border Gateway Protocol (BGP)
- BGP is the exterior gateway protocol which is used for communicating information among AS on the Internet
- Neighbouring BGP routers i.e. BGP peers exchange detailed path information, widely used by ISP's.
- also called path vector routing algorithm
- the protocols are more concerned with reachability than optimality
- Unlike IGP, such as OSPF and RIP, BGP is EGP which controls route advertisement and selects optimal route between AS's then discovering or calculating routes
- BGP uses 4 types of messages for communication between BGP across the AS:
	- Open Message: open a BGP communication session between peer by TCP connection
	- Update message: used to provide routing updates to other BGP systems
	- Keepalive message: to inform BGP peers that a device is active
	- Notification: to alert an error condition or to close the session
## D. Unicast Routing
- simply unicast means one-to-one i.e. transmission is between two routers at a time.
- sender sends the message to one side and receiver receives the message to the other side
- simplest form of routing because destination is already known
- hence the router has to just look up the routing table and forward the packet to the next hop.
  ![[unicast.png]]
## E. Multicast Routing
- simply multicast means one-to-many i.e. the transmission is between more than 2 routers at a time. 
- there is one source and group of destinations. 
- In certain applications, a process has to send a message to a well-defined group which is small compared to network size. 
- Sending a message to such a group is multicasting and the routing algorithm used for multicasting is multicast routing
  ![[multicast.png]]
[[Chapter 5 Transport Layer]]
