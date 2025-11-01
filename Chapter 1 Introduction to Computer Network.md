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
# 1.4 OSI Model and TCP/IP Model
# 1.5 Comparison of OSI / TCP/IP
# 1.6 Data Encapsulation
# 1.6 Example Network: The internet, X.25, Frame Relay, Ethernet, VoIP, NGN, MPLS, xDSL
[[Chapter 2  Physical Layer]]