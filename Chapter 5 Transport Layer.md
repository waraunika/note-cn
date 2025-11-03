- located between the application layer and the network layer
- provides a process-to-process communication between two application layers
- one at local host and other at remote host
- communication is provided using a logical connection which may be located in different parts of the globe, assuming imaginary direct connection through which they can send and receive messages
- figure:
  ![|600][p2p_communication.png]
# 5.1 Transport Service
## A. Need
- provides host-to-host communication
- however, multiple applications or processes can run on a single host.
- the transport layer is needed to provide process-to-process communication
- this ensures data from one application on a source host reaches the correct application on a destination host
## B. Tasks
- Process-to-process communication:
	- Extends the network layer's host-to-host delivery to deliver data to correct application process using identifiers like port numbers
- Segmentation and Reassembly:
	- breaks large application messages into smaller segments for transmission and reassembles them at the destination
- Connection-Oriented Service:
	- provides reliable, in-order data delivery
	- involves:
		- connection control: establishes, maintains, and terminates a logical connection (handshaking)
		- error control: ensures data integrity through mechanisms like acknowledgements and re-transmission
		- flow control: prevents a fast sender from overwhelming a slow receiver
		- congestion control: prevents a sender from overwhelming the network
- Connection-less Service:
	- provides a minimal, low-overhead service for applications that prefer speed over reliability
	- does not guarantee delivery or order
- Multiplexing and Demultiplexing:
	- allows multiple application processes on a single host to use network services simultaneous.
## C. Services to Upper Layers
| Feature     | Connection-Oriented Service                                      | Connection-less Service                                                                   |
| ----------- | ---------------------------------------------------------------- | ----------------------------------------------------------------------------------------- |
| Concept     | establishes a logical connection before data transfer            | sends data without prior connection setup                                                 |
| Analogy     | telephone call                                                   | postal mail                                                                               |
| Reliability | reliable. guarantees delivery, correct order and error-free data | Unreliable. no delivery guarantee; packets can be lost, duplicated or arrive out of order |
| overhead    | high due to connection setup/termination, ACK, sequencing        | low                                                                                       |
| speed       | slower due to overhead                                           | faster due to lack of overhead                                                            |
| example     | TCP                                                              | UDP                                                                                       |
# 5.2 Transport Protocols
## A. UDP (User Datagram Protocol)
- UDP is a connection-less, lightweight and unreliable transport protocol
- provides minimal, low-overhead service for applications that prefer speed over guaranteed delivery
- used for real time traffics like video streaming, video chatting, VoIP, DNS queries
- header size of UDP Protocol is smaller than the header of TCP
  ![|500][udp_header.png]
- Header format: 8 Bytes Total
	- Source Port: 
		- 2 Byte
		- optional
		- when meaningful, it indicates the port of sending process and assumed to be port to which a reply should be addressed
		- if the field is not used, a value of zero is inserted
	- Destination Port:
		- 2 Byte
		- identifies the destination port
	- Length:
		- 2 Byte
		- length of UDP datagram (header + data)
		- minimum value is 8
	- checksum: 
		- 2 Byte
		- optional for IPv4, mandatory for IPv6
		- used for error-checking the header and data
## B. TCP (Transmission Control Protocol)
- connection-oriented, reliable, byte-stream protocol
- there is flow control with sequencing and ACK with sliding window
- provides ordered and error-checked delivery of a stream
- offers efficient control
- usually used for file transfers
- doesn't support multicasting because it is connection-oriented
- data in TCP is called segment that are obtained after breaking big file into small pieces
- header size of TCP is larger than of UDP
- Header fields can range from 20-60 bytes. 40 bytes are for options.
  ![|500][tcp_header.png]
- Fields:
	- Source Port:
		- This is a 16-bit field that holds the port address of the application that is sending data segment
	- Destination port address:
		- This is a 16-bit field that holds the port address of the application in the host that is receiving the data segment
	- Sequence number:
		- 32-bit field
		- byte number of the first data byte in this segment
		- used to reassemble the message at the receiving end if the segments are received out of order
	- Acknowledgement number: 
		- 32-bit field
		- next sequence number the receiver expects (cumulative ACK)
	- Header length (HLEN):
		- 4-bit field that indicates the length of the TCP header by number of 4-byte words in the header
		- if header is of 20 bytes, then this field holds 5 (5 x 4 = 20)
		- the maximum length being 60, it is capable of holding 15.
		- so value ranges from 5 to 15
	- Control flags:
		- These are 6 1-bit control bits that control connection establishment, termination, abortion, flow control, mode of transfer, etc.
		- URG: Urgent pointer is valid, the receiving TCP should interpret the urgent pointer field
		- ACK: Acknowledgement number is valid (used in case of cumulative acknowledgement)
		- PSH: Request for push
		- RST: Reset the connection
		- SYN: Synchronise sequence numbers
		- FIN: Terminate the connection (Finish)
	- Window size:
		- tells the window size of sending TCP in bytes
	- Checksum:
		- holds the checksum for error control
		- mandatory in TCP
	- Urgent Pointer:
		- this field is valid only if URG is set
		- used to point to data that is urgently required that needs to reach the receiving process at the earliest
		- value of this field is added to the sequence number to get the byte number of last urgent byte
	- Options:
		- provide additional functionality, like congestion control
## C. Why server process must run 1st?
- The server must be in a passive open state, listening on a specific port for incoming connection requests (SYN segments)
- If the server is not running, the client's SYN packet will have nowhere to go and will be resulting in a "Connection Refused" error
## D. Reliability of TCP
TCP ensures reliability through several integrated mechanisms:
1. Acknowledgements and Re-transmissions (ARQ):
	- the receiver sends ACKs for successfully received data
	- sender starts a re-transmission timer when segment is full
	- if an ACK is not received before the timer expires, the segment is resent
2. Sequence Numbers:
	- every byte of data is sequenced
	- this allows the receiver to detect lost segments
	- allows receiver to reorder out-of-order segments
3. Checksum:
	- checksum allows receiver to detect corrupted data
	- corrupted segments are silently discarded, triggering retransmission by sender's timer
4. Connection-Oriented Support:
	- the established connection provides a context for managing the sequence of data exchange and error recovery
## E. Difference
| Feature            | TCP                                           | UDP                          |
| ------------------ | --------------------------------------------- | ---------------------------- |
| Connection         | Connection-oriented                           | Connection-less              |
| Reliability        | Reliable                                      | unreliable                   |
| Ordering           | Guarantees in-order delivery                  | no ordering                  |
| flow control       | yes (sliding window)                          | no                           |
| congestion control | yes                                           | no                           |
| header size        | larger (20-60 bytes)                          | smaller (8 bytes)            |
| speed              | slower, more overhead                         | faster, less overhead        |
| use cases          | Web (HTTP), email (SMTP), File transfer (FTP) | DNS, VoIP, Streaming, Gaming |
# 5.3 Port and Socket
![|600][address_tcp.png]
## A. Port Addressing
- Definition: A port address is a 16-bit number, used in Transport Layer, to uniquely identify a specific application process, running on a host.
- When an IP address delivers data to the correct computer, a port address ensures it reaches the correct application (e.g., web browser, email client) on that computer
#### Significance:
- They enable multiplexing and demultiplexing, allowing a single host to run multiple network applications simultaneously
- fundamental mechanism to achieve process-to-process communication across a network
## B. IANA Ranges
| Range           | Port Numbers    | Description                                                                       | Examples                                                                             |
| --------------- | --------------- | --------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------ |
| Well-Known      | 0 - 1,023       | Assigned to universal network services<br>Require system privileges to use        | 80 (HTTP), 443 (HTTPS), 21 (FTP)                                                     |
| Registered      | 1,024 - 49,151  | Can be registered by software companies for their applications to avoid conflicts | 3306 (MySQL), 3389 (RDP)                                                             |
| Dynamic/Private | 49,152 - 65,535 | Used temporarily by client applications<br>Also called ephemeral/temporary ports  | A web browser uses a random port in this range to connect to a web server on port 80 |
## C. Socket
- A socket is application programming interface (API) that allows an application to access the network
- endpoint of a 2 way communication link between two programs running on the network
- uniquely identified by its IP and Port pair
#### Importance
- sockets are foundation of all network applications
- they abstract the complexities of the underlying network hardware and protocols, allowing programmers to build networked software by simply reading from and writing to these endpoints
## D. Port Vs. Socket
| Concept            | Port                                                              | Socket                                                                         |
| ------------------ | ----------------------------------------------------------------- | ------------------------------------------------------------------------------ |
| Definition         | 16-bit numerical identifier for a specific application or service | endpoint for communication formed by combining an IP address and a port number |
| Analogy            | apartment number in a building                                    | full address of the apartment                                                  |
| what it identifies | a service or process                                              | a specific process on a specific machine                                       |
| format             | single number, e.g., 80                                           | IP Address : Port Number, e.g., 192.168.1.5:80                                 |
## E. Implementation of TCP Socket for Communication
1. Server-Side:
	- Create socket: the server creates a socket
	- Bind: The server binds the socket to its IP address and a well-known port
	- Listen: the server socket listens for incoming connection requests
	- Accept: When a client connects, the `accept()` function creates a new socket specifically for that connection
2. Client-Side:
	- Create Socket: The client creates a socket
	- Connect: The client uses the `connect()` function, specifying the server's IP address and well-known port to initiate the 3-way handshake
3. Data Exchange:
	- Both sides use `send()` and `recv()` functions on the established socket to exchange data
4. Close
	- the connection is closed using `close()` function
# 5.4 Connection Management (TCP)
## A. Connection Establishment
The 3-way handshake synchronises sequence numbers and establishes a bidirectional connection.
1. SYN (Synchronise):
	- The client sends a segment to the server
	- The SYN flag is set to 1
	- It includes the client's random Initial Sequence Number (ISN = `x`)
2. SYN-ACK (Synchronise-Acknowledge):
	- The server responds with a segment
	- The SYN and ACK flags are set to 1
	- It includes the server's own random ISN (`y`)
	- The Acknowledgement Number is set to `x+1`, confirming receipt of the client's SYN and expecting the next byte from the client
3. ACK (Acknowledge):
	- The client sends a final segment
	- The ACK flag is set to 1.
	- The Acknowledgement Number is set to `y+1`, confirming receipt of server's SYN
	- Data transfer can now begin
**Purpose**:
- this handshake solves the "delayed duplicate" problem, ensuring that old, repeated connection requests do not accidentally establish a new invalid connection
**Figure**:
![|500][3_way_handshake.png]![|500][old_connection_request.png]
## B. Data Transfer
- Data is broken into segments
- each byte of data is tracked using sequence numbers
- the receiver sends acknowledgements (ACKs) to confirm successful receipt
- flow control using the window size field, and congestion control mechanism manage the rate of data transmission
## C. Connection Termination
The 4-step process is needed because connection is full duplex and each direction must be closed independently
1. FIN (Finish from Host A):
	- When Host A has no more data to send, it sends a segment with the FIN flag set to 1.
2. ACK (from Host B):
	- Host B receives the FIN and sends back an ACK to acknowledge it.
	- At this point data can still flow from Host B to Host A
3. FIN (Finish from Host B):
	- When Host B is also ready to close the connection, it sends its own segment with the FIN flag set to 1
4. ACK (from Host A) and Timer Wait
	- Host A sends a final ACK to confirm Host B's FIN
	- Host A then enters a TIME-WAIT state (typically 2 times the maximum segment lifetime) to ensure this final ACK was received
	- This prevents old, delayed segments from interfering with new connections
![|500][closing_connection.png]
# 5.5 Flow Control and buffering
## A. Flow Control
TCP uses a sliding window protocol for flow control to prevent a fast sender from overwhelming a slow receiver. The key mechanism is the receiver-advertised window
- **the receiver's role**: the receiver includes a Window Size value in every TCP segment it sends back to the sender. this value tells the sender how much free buffer space the receiver currently has
- **The sender's limitation**: The sender is not allowed to have more than a certain amount of unacknowledged data in transit. this amount is minimum of:
	1. The receiver's advertised window size (flow control)
	2. The congestion window (congestion control)
- **Dynamic Adjustment**: As the receiver's application reads data from its buffer, it frees up space. The receiver then sends new ACKs with an increased window size, which "slides" the window forward and allows the sender to transmit more data
This mechanism ensures the sender's transmission rate is always matched to the receiver's current ability to process data
## B. Buffering Strategies
| Strategy                                 | Description                                                            |
| ---------------------------------------- | ---------------------------------------------------------------------- |
| Chained Fixed-Size Buffers               | A pool of identically sized buffers, with one TCP segment per buffer   |
| Chained Variable-Sized Buffers           | Buffers of different sizes are allocated to fit each segment perfectly |
| One Large Circular Buffer per Connection | A dedicated, pre-allocated ring buffer for each connection             |
![|600][buffering_startegies.png]
- Since a single host manages many simultaneous TCP connections, efficient buffer management is crucial. 
- The choice of strategy involves a trade-off between performance and complexity
- optimal buffering strategy depends on the network traffic type
- a large file transfer benefits from a large circular buffer
- a chat application with fast messages might work with a pool of small, fixed-size buffers
# 5.6 Multiplexing and demultiplexing
#### Multiplexing
- The process of: 
	- gathering data from multiple application processes (sockets), 
	- encapsulating each piece of data into a transport-layer segment (by adding a header) and 
	- passing these segments down to the network layer 
	- over a single network connection
- Purpose:
	- allows efficient use of the network layer by consolidating data from various applications into one outgoing stream
#### Demultiplexing
- The process of:
	- receiving segments from the network layer
	- examining the header fields (destination port and IP address),
	- delivering the enclosed data to the correct waiting application process (socekt)
- Purpose:
	- Ensures that incoming data is directed to the appropriate application

The transport layer uses key fields in the segment header, primarily the destination port number, to identify target socket.
combination of ip address and port number uniquely identifies a specific process on a specific host.
# 5.7 Congestion control algorithm
- concept:
	- Congestion occurs when the number of packets sent to the network is greater than the capacity of the network
	- congestion will lead to a large queue length which results in buffer overflow and loss of packets
	- therefore congestion control is necessary in the network
- factors causing congestion:
	- Packet arrival rate exceeds the outgoing link capacity
	- burst traffic
	- insufficient memory to store arriving packets
	- slow processor
- congestion cannot be eliminated but can be controlled.
- two approaches of congestion control are:
	- Open loop control:
		- it is a prevention approach
		- tries to solve the problems by excellent design to prevent the congestion from happening
		- uses techniques like deciding
			- when to accept the new packets
			- when to discard pacekts
			- which packets are to be discarded
			- making scheduling decisions at various points
	- Closed Loop Control:
		- it uses some kind of feedback
		- based on 3 steps:
			- after congestion occurred, detect the congestion and locate it by monitoring the system
			- transfer the congestion information to places where action can be taken
			- adjust the system operations to correct the congestion
# 5.8 Traffic Shaping
- Concept:
	- Traffic shaping is a process of altering a traffic flow to avoid burst
	- is a congestion control technique that smooths out bursty network traffic,
	- regulates the average rate of data transmission to make data flow more predictable and manageable for the network
- two traffic shaping techniques are used to control congestion
## A. Leaky Bucket
- concept:
	- traffic shaping method designed to eliminate burstiness in data flows
	- models traffic using a bucket with hole
- analogy:
	- imagine a bucket with a small hole in the bottom.
	- data packets (water) can enter the bucket at any variable rate, but they exit (leak out) at a strictly constant, predefined rate
- Working:
	- this mechanism prevents network congestion
	- a critical limitation is that if the bucket's finite queue becomes full, any new incoming packets are discarded, providing no flexibility for handling legitimate traffic bursts
	- the bucket represents a finite queue
	- the network interface transmits packets at a fixed constant rate
- Algorithm:
	1. initialise a counter to n at the tick of the clock
	2. if n is greater than the size of the packet, send the packet and decrement the counter by the packet size
	3. repeat this step until n is smaller than the packet size
	4. reset the counter and go to step 1
- Figure
  1. Analogy
     ![|550][leaky_bucket.png]
  2. Implementation
     ![|550][leaky_bucket_implementation.png]
## B. Token Bucket
- concept:
	- provides a more flexible approach to traffic shaping by allowing for controlled bursts of data
- Operation:
	- tokens are generated at a constant rate, one token per $\Delta$T second
	- collected in a bucket upto a maximum capacity
	- to transmit a packet, a host must possess and remove a token from this bucket
	- this design allows an idle host to accumulate tokens
	- which it can later use to send, high-volume burst of packets up to the bucket's size limit
- differences with leaky bucket
	- unlike leaky bucket, this algorithm does not discard packets
	- if no tokens are available, packets are typically buffered and delayed until sufficient tokens are regenerated, making it more efficient with variable bandwidth needs
	- gives faster response to real burst of data packets
- token manipulation
	- the token bucket throws away a token when the bucket fills up, but never discards packets
	- the implementation of token bucket algorithm is just a variable count tokens
	- the counter is incremented by $\Delta$T second and decremented by one whenever one packet is sent.
	- When the counter hits zero, no packet can be sent.
- Figure:
  1. Token Bucket algorithm analogy:
     ![|550][token_bucket_analogy.png]
  2. Token Bucket Implementation:
       ![|550][token_bucket.png]
  

[[Chapter 6 Application Layer]]