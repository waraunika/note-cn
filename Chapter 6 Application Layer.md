# 6.1 Web: HTTP and HTTPS
- Web is one of the major communication technologies that has changed the way people live and work
- WWW today is a distributed client-server service, in which a client using a browser can access a service using a server.
- The service provided is distributed over many locations called sites.
- The web today is a repository of information in which the documents, called web pages are linked together
## A. HTTP
- **Concept**:
	- Hyper Text Transfer Protocol
	- application-layer protocol that powers the web
	- it is request-response protocol where a client (browser) requests web pages and the server responds with requested data
- **Characteristic**:
	- Transport: Uses TCP on port 80 for reliable delivery
	- Stateless: each request is independent; the server does not retain information about previous requests
	- Pull Protocol: The client initiates all interactions; the server does not push data unsolicited
	- Operation: The browser establishes a TCP connection, sends an HTTP request message for an object (e.g., HTML file, image), and the server replies with an HTTP response message containing the object
- **Common HTTP Methods**:
	- GET: Requests data from a specified resource
	- POST: Submit data to be processed to a specified resource
	- PUT: replaces all current representations of the target resource with the uploaded content
	- DELETE: Removes the specified resource
- Figure:
  ![|500][http.png]
#### Web Server:
- A software program (e.g., Apache, Nginx) that hosts websites.
- listens on port 80 for incoming HTTP requests, processes them and returns the appropriate HTTP responses (web pages, images, etc)
## B. HTTPS
- **Concept**:
	- Hypertext Transfer Protocol Secure
	- not a separate protocol but HTTP layered on top of Secure Socket Layer / Transport Layer Security (SSL/TSL) to provide security
	- ensures communication between a client and server is encrypted and authenticated
- Figure:
  ![|500][https.png]
- **Working**:
	- Client initiates a connection to the server on port 443
	- server responds with SSL/TLS certificate to prove its identity
	- SSL/TSL handshake occurs where the client and server agree on encryption algorithms and exchange keys to establish a secure session
	- All subsequent HTTP communication is encrypted within this secure TLS tunnel, protecting it from eavesdropping and tampering
## C. HTTP vs HTTPS
| Aspect         | HTTP                                         | HTTPS                                                           |
| -------------- | -------------------------------------------- | --------------------------------------------------------------- |
| Security       | Not Secure<br>Data is sent in plain text     | Secure<br>Data is encrypted                                     |
| Port           | 80                                           | 443                                                             |
| Protocol       | HTTP over TCP                                | HTTP over SSL/TLS                                               |
| Authentication | None. Vulnerable to impersonation            | Sever is authenticated via certificate from a trusted authority |
| Use Case       | Non-sensitive information. e.g. reading news | sensitive transactions. e.g. banking, login, e-commerce         |
## D. HTTPS not used everywhere
While HTTPS usage is growing, HTTPS is not universally applied for all web traffic due to:
1. Computational Overhead: Encryption/Decryption process consume more server CPU resources
2. Cost and Complexity: Obtaining, installing and renewing certificates from trusted authorities requires effort and cost
3. Caching Inefficiency: Encrypted content cannot be cached by intermediate proxies as easily, which can slightly reduce performance for some users
# 6.2 File Transfer
- File transfer is a generic term for the act of transmitting files over a computer network like the Internet
- numerous ways and protocols to transfer files over a network
- Computer which provides a file transfer service is called file server
## A. FTP
- **Concept**:
	- FTP is a standard TCP/IP Protocol used for transferring files between a client and a server on a network.
	- Unlike HTTP, FTP is stateful and maintains a connection throughout a session
- **Working**: (Two Channel Architecture)
	- FTP uses two separate, parallel TCP connections to manage a file transfer session efficiently.
	1. Control Connection (Port 21):
		- This persistent connection is established first and remains open for the entire session
		- It is used to send commands (e.g., `LIST`, `GET`, `PUT`) and receive replies (status codes)
		- Handles user authentication (username/password)
	2. Data Connection (Port 20)
		- This connection is opened and closed for each individual file transfer or directory listing
		- It is used only for the actual transfer of file data or directory contents
- **FTP Server Working Principle and Data Transfer Process**:
	1. Connection Setup: The FTP client initiates a TCP connection to the FTP server on port 21 (the control connection)
	2. Authentication: the client sends the user's credentials (username and password) over the control connection
	3. Command Issuance: The user issues a command (e.g., `GET filename.txt` or `ls`)
	4. Data Connection Establishment:
		- For the actual transfer, the server opens a second TCP connection back to the client on port 20 (the data connection)
	5. Data Transfer: The requested file data or directory listing is sent over the connection.
	6. Connection Teardown: Once the transfer is complete, the data connection is closed. The control connection remains open, ready for the next command
- Figure:
  ![|500][control_and_data.png]
  ![|600][ftp_model.png]
#### TFTP (Trivial File Transfer Protocol)
- Concept: TFTP is simple, lockstep, connection-less file transfer protocol that uses UDP (Port 69) instead of TCP
- Key Characteristics (vs FTP):
	- No Authentication: It has no login mechanism and is inherently insecure
	- Minimal Overhead: It is a very basic protocol with a small code footprint
	- Uses UDP: Lacks the reliability of TCP, so it implements its own simple acknowledgement system for each data block
- Use Case: Primarily used for booting diskless workstations or transferring firmware/configuration files to network devices (e.g., routers) where a full FTP implementation is unnecessary
## B. PuTTY
- Concept:
	- PuTTY is a highly popular, free and open-source terminal emulator and network file transfer client
	- primarily functions as a client application for establishing secure remote connections to servers
- Key Functions and Protocols:
	- Terminal Emulation: provides a terminal to interact with a remote system's command line
	- Protocol Support: It acts as a client for several communication protocols, most notably: SSH (Secure Shell), Telnet, Rlogin, Raw Socket
- Platform Availability:
	- originally for MS Windows
	- has been officially ported to some Unix-like systems
	- unofficial ports and forks exist for other platforms, including macOS.
## C. WinSCP
- Concept:
	- WinSCP (Windows Secure Copy) is a popular free and open-source application for MS Windows, that provides secure file transfer between a logical computer and a remote server
- Core Function: its primary purpose is the graphical management and transfer of files with strong security
- Protocols and Techonlogy
	- Secure Protocols: uses SSH technology to enable encrypted file transfers. supports SSH File Transfer Protocol (SFTP), SCP (Secure Copy)
	- Standard Protocol: supports the standard, insecure FTP
- Technical foundation: leverages the PuTTY codebase for its SSH implementation
# 6.3 Electronic Mail
- Concept: 
	- Email is an asynchronous communication system, allowing users to send and read messages at their convenience.
	- its architecture is built on three  core components that work together
- Components
	- User Agent (UA):
		- the user-facing application (e.g., Outlook, Gmail Web Client)
		- allows users to compose, read, reply to, forward and manage emails in their mailbox
	- Message Transfer Agent (MTA):
		- The mail server's "postal service"
		- it is responsible for the routing and delivery of emails between servers
		- standard MTA protocol is SMTP, which is a push protocol
	- Message Access Agent (MAA):
		- The protocol that retrieves mail from the server
		- Since SMTP is a push protocol, a separate pull protocol is needed for the user agent to download messages (pulling) from the server mailbox.
		- Common MAAs are POP3 and IMAP
	- Figure:
	  ![|500][email_components.png]
- Architecture Flow:
  `Sender -> User Agent -> [MTA (SMTP)] -> ...` 
  `... -> [MTA (SMTP)] -> Receiver's Mail Server -> [MAA (POP3/IMAP)] -> User Agent -> Receiver
- Working Principle of an Email System:
	1. Composition & Submission:
		- the sender composes a message in their UA (e.g., Outlook) and hits `Send`
	2. Outgoing Transfer (SMTP):
		- The UA uses SMTP to push the message to the sender's designated outgoing MTA (SMTP server)
	3. Relay & Delivery (SMTP):
		- The sender's MTA finds the recipient's mail server and uses SMTP to forward it across the internet, potentially through various other MTAs, until it reaches the recipient's final final server.
		- the message is placed in the recipient's mailbox on that server
	4. Retrieval (POP3/IMAP):
		- The recipient's UA periodically checks their mail server
		- Uses a MAA protocol like POP3 or IMAP to pull the message to the recipient's device
	5. Reading: The recipient reads the message in their UA
	6. Figure:
	   ![|500][email_protocols.png]
- Mail Agents:
	- It is a collective term for the software components that handle amil.
	- The three primary agents are the User Agent (UA), Message Transfer Agent (MTA) and Message Access Agent (MAA)
	- each has a distinct role in the email delivery chain, from composition to final retrieval
## A. SMTP
- Concept:
	- SMTP is the standard application-layer protocol used for sending and relaying email across the internet
	- defines the communication between MTA's.
- Characteristics:
	- Push Protocol: SMTP is used to "push" emails from the sending server to the receiving server. It is not used to retrieve emails
	- Relies on TCP: Uses TCP port 25 for reliable, connection-oriented delivery
	- Text-Based: The protocol uses simple, human-readable commands and responses
- **Working**:
	- SMTP operates in a client-server model. A mail server acts as an SMTP client when sending mail and as an SMTP server when receiving it
	- Process:
		1. Submission: The sender's UA sends the composed email to its outgoing mail server (SMTP server), where it is placed in a message queue
		2. Connection Establishment: The sender's mail server (now acting as an SMTP client) establishes a TCP connection on port 25 to the recipient's mail server (the SMTP server)
		3. Handshake: The two servers perform an application-layer handshake. The client identifies the sender's and recipient's email addresses
		4. Message Transfer: The SMTP client sends the actual message over the established TCP connection
		5. Delivery: The recipient's SMTP server receives the message and places it in the recipient's mailbox
		6. Connection Closure: The TCP Connection is closed
## B. Mail Access Protocols (Pull Protocols)
- the two protocols, which transfer messages from receiver's mail server to the local PC are POP3 (Post Office Protocol Version 3) and IMAP (Internet Mail Access Protocol)
### B.1 POP3
- Concept:
	- POP3 is a simple, pull-based protocol used by a user's email client to retrieve messages from a remote mail server.
	- designed to download emails to a local device
- Characteristics:
	- Operation: Uses TCP port 110
	- Model: Follows a "download-and-delete" or "download-and-keep" model
	- Stateless: server does not track the state of messages after a session ends, beyond their deletion status
- Workings:
	1. Authorisation Phase
		- The client connects to the server on port 110
		- The client sends the username and password to authenticate and gain access to the mailbox
	2. Transaction Phase
		- The client can issue commands to list, retrieve, and delete messages from the server's mailbox
		- Messages are typically downloaded to local machine
	3. Update Phase:
		- occurs after the client issues the `QUIT` command
		- the server performs cleanup, permanently deleting any messages that were marked for deletion during transaction phase
- POP3 has two modes:
	- Delete Mode: the mail is deleted from the mailbox after each retrieval. Is used when the user is working at his permanent computer
	- Keep Mode: the mail remains in the mailbox after retrieval. This mode is used when the user accesses mail away from the primary computer.
- Disadvantages of POP3:
	- The user cannot have different folders on the server
	- The user cannot partially check the contents email before downloading
	- For nomadic user who would prefer to maintain a folder hierarchy on a remote server, that can be accessed from any computer, this is not possible
- Figure:
  ![|350][pop3.png]
### B.2 IMAP
- Concept:
	- IMAP is more advanced and feature-rich pull-based protocol for accessing email from a mail server.
	- Unlike POP3, it is designed to manage and synchronise emails directly on the server
	- making it ideal for accessing mail from multiple devices
- Characteristics:
	- Operation: Uses TCP port 143 (or port 993 for IMAPS - IMAP over SSL/TSL)
	- Model: Follows a online or synchronisation model. the server acts as the central repository
	- Stateful: the server maintains the state of the user's mailbox, including folders, read/unread status and message flags
- How IMAP Solves POP3's Limitation
	- No server-side folders: users can create, delete and rename folders/mailboxes on the server to organise mails
	- cannot preview emails: users can fetch and view email headers, like sender, subject or specific parts like body text before downloading the entire message
	- Poor for multiple devices: synchronises all actions across all devices, providing a consistent view
- Extra function:
	- Server-side Search: users can search for emails based on criteria (e.g., sender, subject, content) directly on the server without downloading all messages first
### B.3 Differences
| POP3                                                                                                                                                                                                          | IMAP                                                                                                                                  |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------- |
| When anyone opens the mail box, new mail is moved or downloaded permanently from the host server and saves on the computer.<br>Hence, if they want to see previous mail, they have to go to previous location | Mail is permanently stored in the server until user deletes it.<br>Thus, they can access them from various locations at various times |
| With POP, only one folder will be in the mail server i.e. index folder                                                                                                                                        | Mail stays on the server in multiple folders, some of which user creates                                                              |
| users cannot access their multimedia mail if on limited bandwidth                                                                                                                                             | if limited bandwidth, users can partially download e-mail content                                                                     |
| POP has only two modes: keep and delete                                                                                                                                                                       | users can create, delete or rename mailboxes on mail servers                                                                          |
| reading mail from multiple computers results in message scattering                                                                                                                                            | multiple computer can access the same                                                                                                 |
| message stored is limited only by the capacity of user's computer.                                                                                                                                            | message storage capacity is limited to 2 GB                                                                                           |
| lose all message if computer fails                                                                                                                                                                            | do not lose mails if computer fails                                                                                                   |
| Port 110 is used                                                                                                                                                                                              | port 143 is used                                                                                                                      |
| connection time required is small                                                                                                                                                                             | connection time required is large                                                                                                     |
| user backup mail boxes                                                                                                                                                                                        | ISP backs up mail boxes                                                                                                               |
# 6.4 DNS
- Concept:
	- DNS is the Internet's distributed directory service
	- Primary function is to translate human-friendly host names (e.g., www.google.com) into machine-readable IP addresses (e.g., 142.250.183.206)
	- it uses UDP Port 53
- why it is essential?
	- people use names
	- but network use IP addresses
	- DNS bridges this gap
	- makes internet usable for common people
## A. Working of DNS
1. A user's application (e.g., a browser) is given a host name
2. The application passes the host name to the DNS client (resolver) on the user's computer
3. The resolver sends a query to the Local DNS Server (typically provided by the user's ISP)
4. If the Local DNS Server doesn't have the answer cached, it begins a query process through the DNS hierarchy
	1. it queries a root DNS server
	2. The root server responds with the address of a Top-Level Domain (TLD) Server (e.g., for `.com`)
	3. The TLD server responds with the address of the Authoritative DNS server for the specific domain (e.g., google.com)
5. The local DNS Server finally queries the Authoritative DNS Server, which returns the IP address for the requested hostname
6. The local DNS Server sends the IP address back to the user's application which can now initiate a connection
7. Figure:
   ![600][dns_working.png]
**Why DNS is Distributive?**
- a single, central database for all internet names would be impossible to manage, maintain and scale
- a distributed system is fault-tolerant, scalable and avoids a single point of failure
## B. Domain Name Space & Hierarchy
The DNS namespace is hierarchical, inverted tree structure
- Root Domain: The top, represented by a dot (`.`)
- Top-Level Domains (TLDs): the next level, often 2-3 character codes of names (e.g., `.com`, `.org`, `.edu`, `.np`)
- Second-Level Domains: The unique part of a domain name that is purchased (e.g., `google` in `google.com`)
- FQDN (Fully Qualified Domain Name): The complete domain name, including the host and all domains (e.g., `mail.google.com`)
- PQDN (Partially Qualified Domain Name): if the label is not terminated by a null string
- Figure:
  ![|550][domain_name_label.png]
  ![|550][domain_name_hierarchy.png]
## C. Hierarchy of Name Servers
1. Root DNS Servers: Know the location of the TLD servers
2. Top-level domain Servers: TLD is one of the responsible for `com`, `org`, `net`, `edu`, etc and all top-level country domains `np`, `uk`, `jp`. they know the authoritative servers for domains under their TLD
3. Authoritative DNS servers: Holds the actual DNS records for IP address of specific domains
4. Local (Recursive) DNS servers: the first server a client contacts. It does the legwork of finding the answer
5. figure:
   ![|550][dns_server.png]
## D. DNS Query Types
- Recursive Query:
	- The client demands a final answer
	- the local DNS server bears the burden of finding the answer and returning it to the client
	- example: your computer asks your ISP's DNS server: what is the IP for `example.com`? and expects a final answer
- Iterative Query: 
	- A server responds with the best answer it has (e.g., a referral to another server). The query asking machine then contacts the next server itslef
	- example: Your ISP's DNS server asks a root server for `example.com`. the root server replies "I don't know but ask the `.com` TLD server at this address"
## E. DNS components
1. DNS Cache: can be the list of names and ip addresses that are already have been queried and have been resolved and are cached. the second meaning regards a dns server that simply performs recursive queries and caching without actually being an authoritative server itself
2. Resolvers: any hosts on the internet that need to look up domain information such as the computer you are using to read website
3. Name Servers: these are servers that contain the database of names and IP addresses and server DNS requests for clients
4. Name Space: database of IP addresses and their associated names
## F. DNS Records
DNS database is stored as Resource records (RRs). Key record types include:
- A (Address): Maps a hostname to an IPv4 address
- AAAA: Maps a hostname to an IPv6 address
- NS (Name Server): Specifies the authoritative DNS servers for a domain
- CNAME (Canonical Name): Creates an alias from one hostname to another
- MX (Mail exchange): Specifies the mail servers for a domain
## G. DNS/HTTP(s)
### G.1 Importance
1. DNS (The Address Book): When you type a URL, DNS is the first step. It translates the website's name (`www.example.com`) into an IP address. Without DNS, the browser wouldn't know where to find the website
2. HTTP/HTTPS (The conversation): Once the IP address is known, HTTP/HTTPS is usually used to actually fetch the website's content. HTTP retrieves the data, while HTTPS does so securely over an encrypted connection. Without HTTP(S), one couldn't download/view the web page
### G.2 Difference
| Feature  | DNS                                      | HTTP                                    |
| -------- | ---------------------------------------- | --------------------------------------- |
| Purpose  | Name Resolution                          | Content Transfer                        |
| Protocol | Primarily uses UDP (port 53)             | uses TCP (port 80/443)                  |
| Function | a support service for other applications | the core protocol for web page delivery |
# 6.5 P2P Applications
**NOT ASKED IN EXAM EVEN ONCE**
- Concept: 
	- A decentralised networking model where applications run on users' computers (peers), allowing them to connect directly to each other to share resources and services without a central server.
	- In P2P, each node acts as both a client and a server
- Characteristics and working:
	- Symmetrical Roles: Unlike client-server, there is no dedicated server. every peer can request and provide resources
	- Direct Communication: Peers connect directly to each other over the internet.
	- Efficient file sharing: a single file is broken into chunks. a user downloads different chunks from multiple peers simultaneously. the user also uploads chunks they already possess to other peers
	- Self-Organising: The networks must have mechanisms for peers to discover each other, query for content and share data
- Advantages:
	- Scalability: system becomes more robust and capable as more users join
	- cost effective: no need for expensive server infrastructure
	- fault tolerant: no single point of failure
	- efficient distribution: leverages the upload capacity of all users
- Disadvantage:
	- high bandwidth usage: can consume significant upload/download bandwidth
	- security risk: files may contain malware as they come from untrusted sources
	- copyright issues: notorious for facilitating the distribution of pirated content
	- management difficult: the decentralised nature makes it hard to control or manage
# 6.6 Socket Programming
- Socket Programming is a method for enabling network communication between two programs running on different computers (or the same computer) by using sockets as end points for sending and receiving data

- socket is a software endpoint that establishes a bidirectional communication channel between two machines.
- uniquely identified by the combination of IP address and a Port Number (e.g. 192.168.1.5:80)

- sockets are fundamental API that allows programs to use the network
- they abstract the underlying hardware and protocol complexities, letting developers build networked applications (web browsers, servers, chat apps) by simply reading from and writing to these end points.

- figures
  ![|550][process_communication.png]
###### Types of sockets:
| Type            | Protocol  | Characteristics                                                | Use Case                                           |
| --------------- | --------- | -------------------------------------------------------------- | -------------------------------------------------- |
| Stream Socket   | TCP       | Connection-oriented, reliable, in-order, error-checked         | Web browsing, email, file transfer                 |
| Datagram Socket | UDP       | Connection-less, unreliable, no ordering guarantees, faster    | Video streaming, DNS queries, online gaming        |
| Raw Socket      | Direct IP | Bypasses transport layer, allows direct IP packet manipulation | network diagnostics (e.g., ping), custom protocols |
# 6.7 Application server concept
## A. Proxy caching
- Concept:
	- A proxy server (web cache) is a network entity that acts as an intermediary, satisfying HTTP requests on behalf of clients.
	- stores copies of frequently requested web objects to improve performance and efficiency
- Working:
	- A user's browser or computer is configured to send all requests to the proxy server
	- For each request, the proxy checks its local cache:
		- HIT: if a fresh cached copy exists, the proxy returns it immediately to the client
		- MISS: If not, the proxy fetches the object form the origin server, stores a copy in its cache, and then forwards it to the client
- Function/Needs:
	- Performance (Reduced Latency): Serves cached content from local network, which is much faster than retrieving it from a distant origin server
	- Bandwidth Savings: Reduces an organisation's external bandwidth usage and costs by serving repeated requests internally
	- Load Reduction: Lessens the load on the origin server
	- Content Filtering & Access Control: Allows administrators to block access to specific websites
	- Anonymity & Privacy: Can hide the client's real IP address from the origin server
## Web/Mail/DNS server optimisation
# 6.8 Concept of traffic analyser
## MRTG
## PRTG
## SNMP
## Packet Tracer
## Wireshark
[[Chapter 7 Introduction to IPV6]]