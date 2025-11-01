# 1.1 Computer Network & Uses
## Concept
- definition: Computer network is defined as an interconnected collection of autonomous computers that are capable of exchanging information and resources with one another
- Fundamental requirement is that the computers must be able to communicate and share data
- This interconnection is facilitated through various transmission media, including:
	- guided media: copper wires, fibre optics
	- unguided media: microwaves, infrared waves and communication satellites.
- network enables computers to function not as isolated systems but as a cohesive, integrated unit
## Advantages
1. Resource sharing: 
	- primary advantage
	- allows multiple users to share expensive hardware devices such as printers, plotters and scanners
	- enables the centralised storage and sharing of data and software applications
	- eliminates duplication and ensures consistency
2. Enhanced Communication and Collaboration:
	- Networks provide a powerful and rapid communication medium.
	- They facilitate the exchange of information via email, instant messaging and video conferencing
	- they enable collaboration among individuals, and teams, regardless of their physical location
3. Improved Reliability and Data Integrity: 
	- Networks allow for data redundancy through centralised backup systems on network servers.
	- if one system fails, data can be recovered from another location, improving reliability.
	- centralised data management also reduces the risk of inconsistent or duplicated information
4. Cost Efficiency
	- by sharing resources and infrastructure, organisations can avoid redundant purchases of hardware and software, leading to substantial cost savings
	- networks also reduce communication costs by leveraging internal systems and internet-based communication over traditional methods
5. Centralised Management and Security:
	- System administrators can manage software developments, updates and security policies from a central server for all connected computers.
	- this simplifies network administration, ensures uniformity, and allows for the implementation of robust, centralised security measures like firewalls and access control
6. Scalability and Flexibility:
	- Networks can be easily scaled by adding new computers and devices without significant overhead and disruption to existing services
	- allows an organisation to grow it computing capacity incrementally as needed
## Applications
1. **Business applications**
	- Resource and Infrastructure Sharing: Networking allows for the sharing of expensive hardware resource like high-speed printers, large-capacity storage arrays and powerful servers across an entire organisation, leading to significant cost savings
	- Enterprise Communication Systems: Networks provide the backbone for powerful communication tools such as email, instant messaging for quick collaboration, video conferencing for remote meetings and shared online documentation
	- E-Business and E-Commerce: Manufacturers and businesses use networks (primarily the internet) for electronic procurement from suppliers (E-business) and for direct selling of products and services to consumers over the internet (E-commerce)
2. **Home applications**
	1. Access to Remote Information: This includes browsing world-wide news platforms, accessing online libraries and databases, and using search engines for a multitude of purposes, reducing reliance on physical media
	2. Person-to-Person Communication: Networks host a multitude of connection channels, including social media platforms, instant messaging applications, online chat rooms and voice/video over VoIP services
	3. Entertainment: This is a major driver, encompassing video-on-demand services, online gaming, streaming music and podcasts and digital media distribution
	4. Home E-Commerce and Finance: This involves online shopping through vast digital catalogues, electronic banking for managing accounts and paying bills and handling personal investments through online brokerages
3. **Mobile applications**
	- Portable and Ubiquitous Access: mobile networks allow users with devices like smartphones, tablets and laptops to access the internet, corporate data and communication services from virtually anywhere, enabling a "always-connected" lifestyle
	- Location-based services: Networks enable applications like GPS Navigation, finding nearby services (restaurants, fuel stations), and receiving location-specific alerts and information
## Part of Life
1. Digital Financial Transactions and Management
	- Networks are the foundation of modern finance
	- everytime an individual also uses online banking to transfer funds, pay utility bills or manage their investment portfolio through a trading app, they are leveraging a secure computer network
	- point-of-sale (POS) terminals in retail stores use networks to verify debit/credit card transactions in real-time with banking servers.
	- the entire digital payment ecosystem, including services like mobile wallets and UPI, operates over complex, secure networks
2. On-Demand Entertainment and Media Consumption
	- The paradigm of entertainment has shifted entirely to network-based delivery
	- streaming services for movies and series, music platforms, and online gaming are all facilitated by high-speed computer networks.
	- provides instant, on-demand access to a vast global library of content, eliminating the need for physical media like DVDs or CDs and allowing for personalised entertainment experiences
3. Ubiquitous Personal and Professional Communication
	- Networks are the central nervous system of modern communication
	- daily activities such as sending and receiving mails, using instant messaging applications for personal and group chats, and participating in video conference calls for work or family (e.g., Zoom, Microsoft Teams) are all network-dependent.
	- Social media platforms, which are entirely hosted on massive global networks, have redefined social interaction and information dissemination
4. E-Commerce and the Digital Marketplace
	- entire process of online shopping is a manifestation of computer networks.
	- from browsing extensive digital catalogues on e-commerce websites, comparing prices across different vendors, reading user reviews, and making secure electronic payments, to tracking the shipment of the order through logistics networks
	- every single step relies on seamless integration of multiple computer networks to function efficiently and provide a seamless consumer experience
5. Civic Services, Information and Education
	- public life is increasingly managed through networks
	- accessing government services and information portals
	- using gps and online maps for navigation
	- proliferation of online learning platforms and distance education programs are all prime examples.
	- even routine activities like checking the weather forecast on smartphone app involve fetching data from remote servers over a network, demonstrating how deeply networks are embedded in daily decision-making and access to public utilities.
# 1.2 Networking model: C/S, P2P, active network
## Client Server Model
- definition: A distributed application structure that partitions tasks or workloads between the providers of a resource or service, called **servers**, and service requesters, called **clients**.
- Figure:
  ![[client_server_model.png]]
- **Workings**:
	- Centralised Servers: Powerful, dedicated computers (servers) host resources like data, applications, or services
	- Client Requests: Simpler machines (clients) send a request message over the network to a server process to access a resource
	- Server Processes & Replies: The server process listens for requests, performs the required work (e.g., fetching data, running a computation), and sends back a reply message
	- Client Waits: The client process waits for and then processes the server's reply
	- Figure:
	  ![[client_server_processes.png]]
- **Key Features**:
	- Centralised Management: Data and security policies are managed centrally on the server
	- Asymmetrical Roles: Clear distinction between client (consumer) and server (provider)
	- Scalability: Can handle many clients by upgrading server hardware or adding more servers
	- High Security: Access control and security are enforced at the server
	- Dedicated Resources: Servers are often optimised for reliability and high availability
- **Examples**:
	- Web Browsing:
		- Client: Web browser, Server: Web Server
	- Email
		- Client: Outlook/Gmail app, Server: Email server like Gmail/Exchange
	- Online banking
		- Client: Browser/app, Server: Bank's central server
## Peer-to-peer Model
- Definition: A decentralised model where each device (called a peer) can act as both a client and a server, sharing resources and responsibilities directly with other peers without a central server.
- Figure:
  ![[peer2peer.png]]
- **Workings**:
	- No central server: peers form a loose, often temporary, network
	- equal capabilities: each peer has equal status and can initiate communication or provide resources.
	- direct sharing: peers connect directly to each other to share files, processing power or bandwdith
	- dynamic membership: peers can join or leave the network freely
- **Key Features**:
	- Decentralisation: No single point of failure or control
	- Self-scaling: More users (peers) bring more resource to the network
	- cost-effective: no need for expensive server infrastructure
	- easy setup: relatively simple to setup for small groups
- **Examples**:
	- File sharing: BitTorrent, Torrent clients
	- Blockchain/Cryptocurrencies: Bitcoin, Ethereum
	- Early Internet Applications: Napster, Skype (originally)
	- Collaborative Platforms: Some features of MS Teams, or Slack for direct file sharing
## Differences of CS/P2P model

| Attribtue      | Client-Server                                                                  | Peer-to-Peer                                                   |
| -------------- | ------------------------------------------------------------------------------ | -------------------------------------------------------------- |
| architecture   | centralised, hierarchical                                                      | decentralised, flat                                            |
| setup          | difficult to set up                                                            | easy                                                           |
| installation   | expensive to install                                                           | cheaper                                                        |
| OS requirement | clients: variety of OS is supported<br>server: OS that supports the networking | wide range of OS can be used                                   |
| maintenance    | less time consuming, maintenance done from server side                         | more time consuming, computers have to be managed individually |
| security       | high, controlled from server                                                   | very low or none                                               |
| limit          | no limit to no. of computers                                                   | ideal for 10 or less                                           |
| server         | requires a server, running Server OS                                           | no server required                                             |
| skill          | requires high level of IT skills                                               | moderate level of skill                                        |
## Active Network
- Definition: A networking paradigm where the network infrastructure (routers, switches) is programmable and can perform customised computations on the data packets flowing through them, rather than just passively forwarding them
- Concept: Packets don't just carry data; they also carry small programs or code that tells the network nodes what to do with them
- **Key Features**:
	- Flexibility: Enables rapid deployment of new network services and protocols without upgrading hardware
	- Custom processing: Network nodes can modify, filter or process data in transit based on the carried code
	- network awareness: devices become more aware of the data they are handling
	- performance: aims to enable faster service development and potentially more efficient data handling
# 1.3 Network Software, Protocols and Standards
## Protocols
- Definition: A protocol is a set of rules and conventions that govern how devices on a network communicate
- defines the format, order, timing of data exchange as well as error control mechanisms
## Connection oriented / Connection less service
### A. Connection Oriented Service
- a service in which a connection (real or virtual) is setup and maintained for the duration of the communication
- typically used to transport data at session layer
- modelled after the telephone system
- to talk to someone, one picks up the phone, dials the number, talks and then hangs up.
- similarly, the service user first establishes a connection, and then uses it and then releases the connection
- essential aspect: it acts like a tube: the sender pushes objects (bits) at one end, and the receiver takes them out at the other end
### B. Connection-less Service
- a service in which a connection is not present and maintained throughout the communication
- modelled after postal system
- each message carries the full destination address and each one is routed through the system, independent of each other
- normally, when two messages are sent to same destination, 1st one sent will be 1st one to arrive
### C. Difference

| Feature     | Connection-Oriented                                          | Connection-less                                    |
| ----------- | ------------------------------------------------------------ | -------------------------------------------------- |
| Concept     | establishes a dedicated connection path before data transfer | sends data immediately without establishing a path |
| Analogy     | Telephone Call                                               | Postal mail                                        |
| Reliability | Reliable. guarantees delivery and order                      | Unreliable. No delivery/order guarantee            |
| Overhead    | High                                                         | Low                                                |
| Data flow   | like in a tube                                               | like individual letters                            |
| Use Case    | File transfer, web browsing, email                           | Video streaming, DNS queries, VoIP                 |

## Network Architecture
- fundamental structure and design of a computer network, defining how devices connect, interact and communicate
- a set of layers and protocols is called network architecture
- **Key Examples**:
	- TCP/IP Suite: The foundational architecture of the modern internet
	- OSI Model: A theoretical 7-layer model for understanding network functions
## Layers:
- in a network, layer refers to:
	- a distinct level of hierarchical system of protocols used to manage communication between distributed computer systems
- each layer provides specific functions and services that contribute to the overall communication process and it interacts only with layers directly above it or below it
### Need for layering:
- Manages Complexity: Breaks down the complex process of communication into smaller, more manageable tasks (layers)
- Modularity & ease of development: Developers can work on one layer without needing to understand the details of others
- Simplifies Troubleshooting: Problems can be isolated to a specific layer, making debugging easier
- Promotes Interoperability: Different vendors can create hardware/software for different layers, and as long as they adhere to the standard interfaces, they will work together
### Need for Layered protocol architecture:
- needed to structure the communication protocols used in networking in a clear and organised manner
- protocols define the rules and conventions for data exchange, and when arranged into layers, each protocol in a given layer only interacts with the protocols in adjacent layers
- this architecture allows for:
	- abstraction: hiding complexity from layers above
	- interoperability: systems and devices built by different vendors can work together as long as they conform to standard protocols
	- re-usability and modularity: protocols can be designed or updated or replaced by other protocol within the same layer
	- scalability: networks can grow without a need to overhaul the entire protocol stack
	- troubleshooting and maintenance: issues can be isolated to specific layers, simplifying diagnosis and repair
## Design Issues for Layers
- Addressing: 
	- For every layer, it is necessary to have a mechnism for identifying senders and receivers. 
	- since, there are multiple possible destinations, some form of addressing is required in order to specify a specific destination
- direction of transmission:
	- based on whether the system communicates only in one direction or both, communication systems are classified as simplex, half duplex and full duplex systems
- error control:
	- error controls and detection both are essential since physical communication circuits are not perfect.
	- the receiver must have some ways of telling the sender which messages have been correctly received and which are not
- flow control:
	- all communication channels cannot preserve the order in which messages are sent on it
	- so some kind of coordination must be maintained to keep a fast sender from overwhelming a slow receiver with data
- multiplexing: 
	- multiplxeing and demultiplexing is to be shared the same channel by many sources simultaneously.
	- it can be used for any layer
	- it is mostly needed in physical layer
	- where all the traffic has to be sent over few physical circuits
- routing
	- when there are multiple paths between source and destination, a proper route should be chosen
	- routing uses the best path in each network
1. define protocol
2. explain about connection oriented and connection less service
3. what do you mean by network architecture
4. why do you need layering
5. why do we need layered protocol architecture
6. what are the reasons for using layered network architecture
7. why layering is important
8. what are the layer design issues
9. explain design issues for layers in detail
10. explain about the design issues of computer network software
# 1.4 OSI Model and TCP/IP Model
# 1.5 Comparison of OSI / TCP/IP
# 1.6 Data Encapsulation
# 1.6 Example Network: The internet, X.25, Frame Relay, Ethernet, VoIP, NGN, MPLS, xDSL
[[Chapter 2  Physical Layer]]