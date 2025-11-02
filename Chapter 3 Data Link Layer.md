# 3.1 Data Link Layer: Function and Services
**Functions**:
- Provides a well-defined services interface to the network layer
- synchronises frame for recognising the start and end of frame
- deals with transmission errors
- provides a flow control mechanism to avoid a fast transmitter from running a slow receiver
- has protocols to determine which of the devices has control over the link
**Services**:
- Unacknowledged connectionless services
	- the destination machine does not send back any acknowledgement of the receiving frame
	- if the frame is lost, no attempt is made to recover it
	- suitable for real time traffic
- Acknowledged connectionless services
	- improves reliability since in spite of being connectionless, acknowledgement is sent from receiver to transmit if the frame is not received within specified time
	- suitable for communication over unreliable channels
- Acknowledged connection-oriented services
	- the source and destination machines establish a connection before transferring the data
	- a specific number is given to each frame being sent and a data link layer guarantees that each transmitted frame is received.
	- 3 phases to be followed for data transfer: connection established, frame transfer and connection release
# 3.2 Framing
## A. Concept
- Definition: Breaking a raw bit-stream into manageable chunks called frames is known as framing
- it allows the receiver to detect the start and end of a frame within the continuous stream of bits.
- frame has following parts:
	- headers: contains the source and the destination addresses of the frame
	- payload field: contains the message to be delivered
	- trailer: it contains the error detection and error correction bits
## B. Framing Methods
1. Character Count
	- this method uses a field in the header to specify number of characters in the frame.
	- at destination, by seeing the character count, it knows how many characters follow and where the end of the frame is
	- but the problem can occur if the count is garbled in transit due to which the receiver will not know where to pick up and the sender will not know how much to resend.
	- this method is rarely used
	- figure:	  ![|650][character_count.png]
2. Flag Bytes with Byte Stuffing
	- In this method, frames begin and end with special bytes
	- Format is given in the figure:
	  ![|500][byte_stuffing_format.png]
	- flags are used as the start/end bytes which are often the same
	- during data transmission, if the receiver gets lost, it just looks for the pair of flag bytes to denote the end of one frame and the start of the next
	- a serious problem occurs with this method when flag byte's bit pattern occurs in the data
	- this is solved by inserting a special escape byte (ESC) just before each flag byte in the data.
	- this technique is called byte stuffing or character stuffing
	- the main drawback of this framing method is that we have to use 8 bits character and ASCII code
	- examples figure:
	  ![|600][byte_stuffing_method.png]
3. Starting and Ending Flags with Bit Stuffing
	- This new technique adds an arbitrary number of bits in data frames and character codes with an arbitrary number of bits per character
	- example: 
		- each frame begins and ends with a special bit pattern, 01111110 (in fact, a flag byte).
		- whenever the sender's data link layer encounters five consecutive 1s in the data, it automatically stuffs a 0 bit into the outgoing bit stream.
	- this process is called bit stuffing
	- example:
		- original data 01001111110111110
		- data stream after framing and bit stuffing:
		- 01111110 010011111**0**101111**0**0 01111110
		- bold bits are bit stuffing
4. Physical Layer Coding Violations
	- this method is only applicable to networks in which encoding on the physical medium contains some redundancy
	- when data is a series of 0, it appears as open circuit and when data is a series of 1, it appears as short circuit
	- to avoid this, it is put in transit (when 0 is the signal voltage is -5 to +5, and when 1 the signal voltage is +5 to -5). 
	- The combinations of low-low and high-high which are not used for data may be used for marking frame boundaries
### Comparison
| Aspect          | Flag Bytes with Byte Stuffing                                              | Flags with Bit Stuffing                                                  |
| --------------- | -------------------------------------------------------------------------- | ------------------------------------------------------------------------ |
| Delimiter       | special flag byte                                                          | special flag bit pattern                                                 |
| method          | byte-oriented.<br>inserts an extra ESC byte before a flag byte in the data | bit-oriented<br>inserts a '0' bit after five consecutive 1's in the data |
| Data Dependency | Dependent of 8-bit character codes (e.g., ASCII)                           | Independent of character code; works with any bit pattern                |
| Overhead        | depends on the frequency of the flag byte in the data                      | depends on the frequency of five consecutive 1's in the data             |
| flexibility     | less flexible, suited for text-based communication                         | highly flexible, used in modern protocols                                |
# 3.3 Error Control, Detection and Corrections
## A. Error Control
- Error control makes sure that all frames are eventually delivered to the network layer at the destination in proper order.
- Generally, feedback is sent by the receiving station to inform that a frame has been successfully received or not
- Error control in the data link layer is based upon the principle of request for automatic re-transmission (ARQ) of the missing, lost or damaged frame
- ARQ has three types
### A.1 Stop and Wait ARQ
- the sender sends one frame, stops until it receives confirmation from the receiver and then sends the next frame
- for retransmission, it keeps a copy of the lost frame that was sent
- the identification of data frame and ACK frame is 0 and 1 respectively.
- the sending device is equipped with a timer
- normal operation:
  ![[stop_n_wait_arq.png]]
- handles three cases of error:
	- damaged data frame
	- lost data frame
	- lost ACK/NAK frame
- the figure for the error cases are:
  ![[error_stop_n_wait.png]]
### A.2 Go Back N ARQ
- this form of error control is based on sliding window flow control
- a station may send a series of frames sequentially numbered with some maximum value
- in this method, acknowledgement (ACK) and negative acknowledgement (NAK) must be numbered.
- ACK carry the next frame to be expected and NAK carry current damaged frame
- if one frame is lost, or damaged, all frames are sent from the last frame acknowledgement are re-transmitted
- various cases for Go Back N ARQ:
  ![[go_back_n_arq.png]]
### A.3 Selective Repeat ARQ
- as in Go Back N ARQ, a station may send a series of frames sequentially numbered with some maximum value
- but in this method, only the specified damaged or lost frame is re-transmitted
- it is more efficient than Go Back N ARQ
	- as it minimises the amount of re-transmission
- A selective repeat system differs from the Go Back N ARQ method in following ways:
	- the receiver must contain some sorting logic to reorder frames
	- it must be able to store frames received after a NAK is sent until the damaged frame is replaced
	- Sender must contain a searching mechanism to find only the requested frame for transmission
	- Buffer in the receiver must be large enough to keep all previously received frame on hold until all retransmission has been stored.
- Figure for its operation:
![[selective_repeat.png]]  
## B. Error
#### Errors:
- different type of errors like bit altering, packet loss, data block missing, etc can occur during the transmission of data in a network
- these errors occur due to the fault in hardware or some other network limitations.
- so, various methods are applied for detection and correction of these errors to establish a perfect communication
#### Types of Errors:
- Content error: error in the content of a message
- Flow integrity error: when the message is delivered to the wrong destiation
Error can be further classified depending upon number of bit error:
- single bit error: if there is only bit which is corrupted
- multiple bit error: frame is received with more than one bit in corrupted state
- burst error: frame contains more than 1 consecutive bits that are corrupt

Error detection and correction are error control mechanism
## C. Error Detection
- for a given time, an error-detecting code (check bits) is calculated from data bits and it is appended to the data to send to a receiver
- in the receiver side, the incoming frame is separated into data bits and check bits and calculates check bits from received data bits
- then the calculated check bits are compared against received check bits and error is detected
- different techniques can be applied
### C.1 Parity Checking
- simplest technique for detecting the error
- a parity bit is added in the data bit
- then at the receiver side, the parity of data is compared with the parity bit for detection of error
- the sender while creating a frame counts the number of 1s in it
- for example, if even parity is used, and the number of 1s is even, then one bit with value 0 is added.
- this way, the number of 1s remain even
- if the number of 1s is odd, to make it even, a bit with value 1 is added
- operation figure:
  ![[parity_checking.png]]
- if a single bit flips in transit, the receiver can detect it by counting the number of 1s.
- but if double or even number of errors occurred, then it will not change the parity so error is unnoticed
- so, parity checks cannot correct errors but can detect odd numbers of errors
### C.2 Checksum
- checksum is used by the higher-layer protocol for error detection.
- here, all bytes in a message are added to generate a checksum which is then sent after all the messages
- then, when the receiver receives the message, it separately calculates the checksum and compares it with the one sent by the sender and detects error if no match occurs
- in a checksum error detection scheme:
	- the data is divided into k segments each of m bits
	- in the sender's end, the segments are added using 1's complement arithmetic to get the sum
	- the sum is complemented to get the checksum
	- the checksum segment is sent along the data segments
	- at the receiver's end, all received segments are added using 1's complement arithmetic to get the sum
	- the sum is complemented
	- if the result is zero, the received data is accepted; else discarded
- Operation's figure:
  ![[checksum.png]]
### C.3 Cyclic Redundancy Check (CRC)
- It is more powerful than parity and checksum
- it is based on division
- a sequence of redundant bits called CRC is generated by dividing the data with some specific byte and is appended at the of data which is used at the receiver side for error detection.
- Unlike the checksum scheme, which is based on addition, CRC is based on binary division
- in CRC, a sequence of redundant bits, called CRC bits are appended to the end of the data unit so that the resulting data unit becomes exactly divisible by a second, predetermined binary number
- At the destination, the incoming data unit is divided by the same number.
- if at this step, there is no remainder, the data unit is assumed to be correct and is therefore accepted
- a remainder indicates that the data unit has been damaged in transit and therefore must be rejected.
- figure for flowchart of operations:
  ![[crc.png]]
## D. Error Correction
- Error correction is the process of regeneration, of actual data from a noisy or faulty data.
- however, over copper wire retransmission is faster than error correction but in the case of very noisy networks, without error-correction, it will be hard to get anything through
- error-correcting codes are widely used on wireless links, which are very noisy and error prone when compared to copper wire or optical fibres.
- hamming code is one of the techniques used for error correction
- in the digital world, error correction can be done in two ways:
	- backward error correction: once the error is discovered, the receiver requests the sender to resend the entire data unit
	- forward error correction: in this case, the receiver uses the error correcting code which automatically corrects the errors
- to correct the error in the data frame, the receiver must know exactly which bit in the frame is corrupted.
- to locate the bit in error, redundant bits are used as parity bits for error detection

- in error correction techniques, codes are generated at the transmitter by adding a group of check bits
- the source generates the data in the form of a binary symbol.
- the encoder accepts these bits and adds the check bits to them to produce the code words which are transmitted towards the receiver
- the check bits are used by the decoder to detect and correct the errors
- these codes can be classified as block codes and convolution codes.
- Sometimes they can be classified as linear code and non-linear code according to their distinguishable properties
### D.1 Hamming Codes
- linear block codes
- proposed by R.W. Hamming
- Consider a message having four data bits which is to be transmitted as a 7-bit codeword by adding 3 error control bits. This would be called a (7, 4) code.
- A general method for constructing error-correcting codes by using a minimum distance of three
- every integer m, there is a (2$^m$ - 1) bit hamming code which contains m parity check bits and 2$^m$ - 1 - m information bits
- the 7-bits hamming code is as:
  D7  D6  D5  P4  D3  P2  P1
- Here, P1 P2 P4 = parity check bits
  D3 D5 D6 D7 = Data bits or Information bits
- If we number the positions from 1 to 2$^m$ -1, the bits in the position 2$^k$, where 0 $\le$ l $\le$ m - 1, and the bits int he remaining positions are information bits. Here, k is the message sequence to be transmitted
#### Calculating the Hamming Code
- The key to the Hamming Code is the use of extra parity bits to allow the identification of a single error.
- Code word is created as:
1. Mark all bit positions that are powers of 2 as parity bits (positions 1, 2, 4, 8, 16)
2. all other bit positions are for data to be encoded (positions 3,5,6,7,9,10,11,12 ...)
3. each parity bit calculates the parity for some of the bits in the code word. the position of the parity bit determines the sequence of bits that it alternately checks and skips
4. so:
   position 1: check 1 bit, skip 1 bit alternatively (1, 3, 5, 7, 9, 11 ...)
   position 2: check 2 bits, skip 2 bits alternatively (2,3, 6,7, 10,11, ...)
   position 4: check 4 bits, skip 4 bits alternatively (4,5,6,7, 12,13,14,15, 20,21,22,23 ...)
   position 8: check 8 bits, skip 8 bits alternatively (8-15, 24-31, ...)
5. while checking the parity, if the total number of 1's are odd, then write the value of parity bit as 1, which means the error is there
6. and if it is even, then the value of parity bit is 0, which means no error
#### Example of detection
- suppose seven bits hamming code is received as 1110111
- so, for checking parity bit p1, check one and skip one. so, we get: P1, D3, D5, D7 = 1 1 1 1. number of 1 is even, so we write the value of P1 as 0, no error
- Check for P2, check 2 and skip 2. so we get P2 D3 D6 D7 = 1 1 1 1. number of 1 is even, so we write the value of P2 as 0, no error
- Check for P4, check 4 and skip 4, so we get P4 D5 D6 D7 = 0 1 1 1. number of 1 is odd, we write value of P3 as 0, this means error.
- the error word is P4 P2 P1 = 1 0 0, so the 5th bit in the code-word is incorrect.
## E. Importance
of Error Detection and Correction Bits
- Ensures Data Integrity: They are the primary mechanism for verifying that the data received is identical to the data sent, preventing corrupted or altered information from being processed
- Maintains Reliable Communication: By detecting errors, the system can trigger re-transmissions (ARQ), ensuring that missing or damaged data is recovered and the communication link remains reliable
- Improves Overall System Efficiency: While adding some overhead, these bits prevent the waste of resources and time that would be spent processing corrupt data, propagating errors, or relying on higher-layer protocols to handle all data loss
- Enables Operation in Noisy Environments: error correction (FEC type) allows for successful data transmission over inherently unreliable and noisy channels, such as wireless networks where re-transmission is inefficient or impossible
- Supports Real-Time and Critical Systems: For applications like live video/audio streaming or financial transactions where retransmission delays are unacceptable, forward error correction is essential for maintaining a seamless and functional service
# 3.4 Flow Control
- deals with the issue where the sender sends data at higher rate than the receiver can receive
- flow control can be done by using the buffer on the receiver side.
- but, the main problem that occurs, in this case, is that the slower receiver cannot cope with the faster sender which causes overflow and loss of data
- Flow control tells the sender how much data should be sent to the receiver so that it is not lost
- this mechanism makes the sender wait for an acknowledgement before sending the next data
- there are two ways to control the flow of data
## A. Stop and Wait Protocol
- it is the simplest flow control method
- sender will send one frame at a time to the receiver
- then the sender will stop and wait for the acknowledgement from the receiver
- then it will send the next data packet to the receiver and wait for the acknowledgement again and this process will continue as long as the sender has data to send
- figure for timing diagram:
  ![[stop_and_wait.png]]
## B. Sliding Window Protocol
- **Concept**:
	- A method for reliable data transmission that allows the sender to transmit multiple frames before acquiring an acknowledgement, significantly improving efficiency over Stop and Wait
- **Components**:
	- Window Size (n): The maximum number of frames that can be sent outstanding (without ACK) at any time
	- Sequence Numbers: Framers are numbered modulo-m (often m > n) to identify them
	- Sender Window: Holds frames that have been sent but not yet acknowledged. The window *slides* forward as ACKs are received
	- Receiver Window: Holds the sequence numbers of frames it is prepared to accept. It slides forward as frames are delivered in order to the network layer
- **Working**:
	1. The sender can transmit all frames within its current window without waiting
	2. the receiver sends cumulative acknowledgements (e.g., ACK 4 means "I have received everything up to frame 3, expect frame 4 next)
	3. Upon receiving an ACK, the sender's window slides forward, freeing up space to send new frames
	4. This process creates a continuous pipeline of data, keeping the channel utilized
- **Purpose and Importance**:
	- Flow Control: Prevents a fast sender from overwhelming a slow receiver by limiting the number of unacknowledged frames
	- Efficiency: Maximises bandwidth usage by allowing multiple frames in transit, eliminating the idle time inherent in Stop and Wait
	- Reliability: Ensures data integrity through sequence numbers and re-transmission mechanisms (used in Go Back N and Selective Repeat ARQ)
- Figure for sender/receiver in sliding window protocol:
  ![Figure for sliding window operation in sender receiver][sliding_window.png]
- example is shown as:
  ![Sliding window example | 550][sliding_window_example.png]
# 3.5 Examples of Data Link Protocol
## A. HDLC (High Level Data Link Control)
#### Overview: 
- A bit-oriented, synchronous Data Link Layer protocol for serial links, supporting both connection-oriented and connection-less services.
- commonly used in WANs over leased lines
#### Stations, Configuration and Modes
| Category       | Types                                                                                                                                                                                                                                              | Description                                    |
| -------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------- |
| Stations       | Primary (issues commands), <br>Secondary (sends responses), <br>Combined (does both)                                                                                                                                                               | Defines the control hierarchy on the linnk     |
| Configurations | Unbalanced (1 primary, 1+ secondary), <br>Balanced (2+ combined stations)<br>Symmetric (other station linked to 1 primary and 1 secondary)                                                                                                         | Defines the physical and logical link          |
| Modes          | NRM (Normal Response Mode: secondary transmits only on command),<br>ABM (Asynchronous Balanced Mode: balanced, either station can initiate transmission)<br>ARM (Asynchronous Response Mode: unbalanced where secondary may initiate transmission) | Defines the rules for initiating communication |
#### HDLC Frame Types
- I-frames (Information): carries user data and piggybacked acknowledgements
- S-frames (supervisory): used for flow and error control (ACK, NAK)
- U-frames (unnumbered): used for link management (setup, disconnection)
#### HDLC Frame Format
- Flag (1 byte): Delimits the frame (01111110)
- Address (1+ byte): identifies the secondary station
- Control (1-2 bytes): manages flow/error control and defines the frame type
- Information (Variable): Carries upper-layer data (not in S/U frames)
- FCS (2-4 bytes): Frame Check Sequence for error detection (CRC)
## B. PPP (Point to Point Protocol)
- Overview: 
	- A Data Link Layer protocol for direct communication between two nodes
	- e.g., connecting a home computer to an ISP over dial-up or DSL
	- provides a standard framing method for transporting multi-protocol datagrams over point-to-point links
	- uses a suite of protocols: LCP (Link Control Protocol) for link establishment, testing and configuration, and NCP (Network Control Protocol) for configuring different network layer protocols (like IP).
- Frame Format:
	-  Flag: `01111110` (HDLC standard) for start/end.    
	- Address: Constant broadcast address (`11111111`).
	- Control: Constant value (`00000011`).
	- Protocol: Identifies the packet in the payload (e.g., IP, LCP, NCP).
	- Payload: The actual data (default 1500 bytes).
	- FCS: Frame Check Sequence for error detection.
- Connection Process:
	1. Link Establishment: LCP frames negotiate connection paramters
	2. Authentication: Optional step (using PAP/CHAP)
	3. Network Layer Setup: NCP configures the network layer (e.g., assigns an IP address)
	4. Data Transfer: Exchange of network layer packets
	5. Termination: LCP closes the link.
# 3.6 The Medium Access Sub-Layer
## A. Sub-layers of Data Link Layer
- Divided into two sub-layers to handle different responsibilities
	- Logical Link Control (LLC)
	- Media Access Control (MAC)
## B. Functions of each sub layer
| Sublayer | Primary Functions                                                                                                                                         |
| -------- | --------------------------------------------------------------------------------------------------------------------------------------------------------- |
| LLC      | - Error Control (using ARQ like mechanism)<br>- Flow control (using sliding window mechanism)<br>- provides an interface to the network layer             |
| MAC      | - Framing (encapsulating packets into frames)<br>- Physical Addressing (using MAC addresses)<br>- Multiple Access Control (managing shared medium access) |
## C. Significance of MAC Sub-Layer
- crucial because it solves a fundamental problem in broadcast networks (like Ethernet and WiFi): "Who gets to use the shared communication channel next?"
- it prevents data collisions and chaos by enforcing rules (protocols like CSMA/CD, CSMA/CA) that control how devices transmit onto a shared medium
- provides a unique, hardware-based MAC Address that identifies a device on the local network
## D. MAC Address vs IP Address
| MAC Address                             | IP address                                              |
| --------------------------------------- | ------------------------------------------------------- |
| Physical/Hardware Address               | Logical/Software Address                                |
| Flat Address (assigned by manufacturer) | Hierarchical Address (assigned by network)              |
| Permanent (burned into the NIC)         | Dynamic (can change)                                    |
| Function: identifies a specific device  | Function: Identifies a device's location on the network |
## E. Importance of Media Access
- The issue of media access is critically important because it directly determines the efficiency, fairness and stability of a network
	- without controlled access, multiple devices transmitting simultaneously on a shared channel cause data collision, corrupting all the data and making the network unusable
	- MAC protocols ensure that the shared channel is used effectively, providing orderly and fair access to all connected devices, which is the foundation of reliable local network's communication
# 3.7 The channel allocation problem
- Concept/Problem:
	- In a shared broadcast medium (like WiFi or classic Ethernet), if two or more devices transmit simultaneously, their signals collide, corrupting the data
	- the core challenge is: "how to allocate a single broadcast channel fairly and efficiently among multiple competing users?"
	- example: in a meeting, where everyone talks at once, no one gets their words through. a protocol is needed so that it can be decided who gets to talk for how much and when, so that communication gets done
## A. Static Channel Allocation
- Concept:
	- the channel's total capacity is divided into fixed, pre-assigned portions for each user
- Methods:
	- Frequency Division Multiplexing (FDM) and Time Division Multiplexing (TDM)
- Examples:
	- FDM: Traditional radio/TV stations, each assigned a specific frequency
	- TDM: Traditional telephone trunk lines, where each call gets a repeating time slot
- Inefficiency and its reasons:
	- wastes bandwidth: 
		- A portion of the channel is reserved for a user when they have no data to send.
		- this is highly inefficient for burst like traffic, which is common in computer network
	- Inflexible:
		- it cannot adapt to changes in the number of users or their traffic patterns.
		- if new user joins, the channel must be reconfigured
	- Limits scalability:
		- the number of users is fixed by the number of available frequency bands or time slots
## B. Dynamic Channel Allocation
- Concept:
	- the entire channel is available to all users
	- access is granted on-demand, based on who needs to transmit at any given moment
- Goal: to achieve much higher efficiency by allowing users to utilise the channel only when they actually have data to send
- Methods: Protocols like ALOHA, CSMA/CD (used in Ethernet), and CSMA/CA (used in WiFi). These protocols define rules for when a station can transmit and how to recover from collisions
# 3.8 Multiple Access Protocols
- Multiple access protocol is used to control/coordinate access to the link or link in a shared connection.
- nodes can regulate their transmission within the shared broadcast channel by using multiple access protocol.
- all the nodes can transmit a frame at the same time
- this may lend rise to collision, so to overcome this, Multiple Access Protocol is implemented.
- Categories:
	1. Random Access Protocols:
		1. ALOHA
		2. CSMA
		3. CSMA/CD
		4. CSMA/CA
	2. Controlled Access Protocols:
		1. Reservation
		2. Polling
		3. Token passing
	3. Channelisation Protocols:
		1. FDMA
		2. TDMA
		3. CDMA
# 3.9 Networks
## A. ALOHA
- earliest random access method, developed in the early 1970s.
- designed fro radio LAN but is also applicable for shared medium
- multiple stations can transmit data at the same time and can hence lead to collision and data being garbled
### A.1 Pure ALOHA
- original ALOHA protocol, where the stations transmit frames whenever they have data to send
- when two or more stations transmit simultaneously, there is collision and the frames are destroyed
- whenever any station transmits a frame, it expects the acknowledgement from the receiver.
- if acknowledgement is not received within specified time, the station assumes that the frame (or acknowledgement) has been destroyed.
- if the frame is destroyed for a random amount of time, and sends it again
- this waiting time must be random otherwise the same frames will collide again and again
- therefore, Pure ALOHA dictates that when the time-out period passes, each station must wait for a random amount of time before re-sending its frame
- this randomness will help avoid more collisions
### A.2 Slotted ALOHA
- was invented to improve the efficiency of pure ALOHA as chances of collision in pure ALOHA are very high
- the time of the shared channel is divided into discrete intervals called slots.
- the stations can send a frame only at the beginning of the slot and only one frame is sent in each slot
- if any station is not able to place the frame onto the channel at the beginning of the slot, i.e. it misses the time slot
	- then it has to wait until the beginning of the next time slot
- there is still a possibility of collision if two stations try to send at the beginning of the same time slot.
### A.3 Response
which has less delay at low load? pure aloha or slotted aloha?
-> Pure ALOHA has less delay at low load
- a station can transmit the moment it has a frame ready
- in slotted ALOHA, a station with a ready frame must wait for the beginning of the next time slot before it can start transmitting
- this forced waiting introduces a small delay even when the network is idle and no collisions are expected.
- at low load, this slot synchronisation delay makes slotted ALOHA slightly slower to respond than pure ALOHA
## B. VLAN
- logical grouping of network users and resources connected to administratively defined ports on a switch.
- can be considered as2 a local area network configured by software not by physical wiring.
- VLAN gives the ability to create smaller broadcast domains within a layer 2 switched inter-network by assigning different ports on the switches to different sub-networks
- grouping devices with a common set of requirements regardless of their physical location by VLAN can greatly simplify network design
- a VLAN has the same attributes as a physical LAN, but it allows for end stations to be grouped together more easily even if they are not on the same network switch.
- to setup a VLAN-based network, the network admin decides how many VLANs will be there, which computers will be on which VLAN and what VLANs will be called.
- VLAN assigns computers to LAN segments by using software
- VLANs are designed in two simple ways:
	- Single-switch VLANs: computers are connected using a large physical switch
	- Multi-switch VLANs: computers connected via different switches
## C. CSMA (Carrier Sense Multiple Access)
- CSMA is a significant improvement compared to ALOHA as it can only be used in lightly loaded networks.
- CSMA operates on the principle of carrier sensing before transmitting.
	- Station listens to see the presence of transmission on the cable and decides to act accordingly.
	- thus ensuring fewer collisions
- If it is idle, then it sends data, otherwise it waits till the channel becomes idle.
- However, there is still a chance of collision in CSMA due to propagation delay.
- Example:
	- if station A wants to send data, it will first sense the medium
	- if it finds the channel idle, it will send data
	- however, by the first bit of the data is sent, if station B requests to send data and senses that it is idle, it too will send data
	- this results in collision of transmitted data from A and B
- CSMA Access Modes:

| Mode           | Behavior                                                                                                                                              |
| -------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------- |
| Non-persistent | If busy, waits a random time before sensing again.<br>Reduces collisions but can be inefficient                                                       |
| 1-persistent   | If busy, continuously sense and transmit immediately when idle.<br>High collision risk                                                                |
| p-persistent   | If idle, transmit with probability p.<br>With probability 1-p, it waits till until the next slot and repeats.<br>A compromise between the earlier two |
### D. CSMA/CD
- Carrier Sense Multiple Access with Collision Detection
- widely used MAC protocol standardised by IEEE 802.3.
- stations listen before transmitting and also listen while transmitting to detect collision or to see if transmission was successful
- Collision Procedure:
	- Abort transmission immediately
	- Transmit a jam signal to ensure all stations know about the collision
	- Wait a random back-off time (which increases after repeated collisions)
	- Re-transmit the frame
- if so, the transmission is finished
- Limitation: Becomes inefficient as network speed and distance increase, as the "collision window" shrinks
### E. CSMA/CA
- Carrier Sense Multiple Access with Collision Avoidance
- since detecting collisions is difficult in wireless medium, it focuses on trying to prevent them.
- Why CSMA/CA over CMSA/CD?
	- Difficulty in detecting collisions due to nature of radio signals (easily interfered)
	- the hidden station problem: Node A and Node B might not hear each other, but both can transmit to node C. this causes collision at C, that neither A nor B can detect
- Collision Avoidance Strategies:
	- Inter-frame Space (IFS):
		- A station that finds the channel idle must wait a short prioritised IFS before transmitting
		- This gives priority frames like ACKs a chance to go first
	- Contention Window & Back-off:
		- If the channel is still idle after the IFS, the station doesn't transmit immediately.
		- Instead, it chooses a random back-off period (a number of time slots) to wait.
		- this randomises the transmission times and avoids collisions after a busy period
	- Acknowledgements: 
		- The receiver must send an ACK for every frame.
		- If the sender doesn't receive an ACK, it assumes a collision and re-transmits
## F. IEEE 802.3 (Ethernet)
- Overview:
	- the dominant standard for wired LANs.
	- defines the Physical Layer and MAC Sub-layer, 
		- using a local bus topology and CSMA/CD for media access
- Evolution (Generations):
	- Standard Ethernet: 10 Mbps
	- Fast Ethernet: 100 Mbps
	- Gigabit Ethernet: 1 Gbps
	- 10 Gigabit Ethernet: 10 Gbps 
#### Frame Format
| Field          | Size             | Purpose                                                       |
| -------------- | ---------------- | ------------------------------------------------------------- |
| Preamble       | 7 Bytes          | Alternating 1s/0/s (101010..) for synchronisation             |
| SFD            | 1 Byte           | Start Frame Delimiter (10101011) marks the start of the frame |
| DA             | 6 Byte           | MAC address of the destination address                        |
| SA             | 6 Byte           | MAC address of the sender's address                           |
| Length         | 2 Bytes          | Indicates the number of bytes in the Data Field               |
| Data & Padding | 46-1500<br>Bytes | Payload from upper layers. Padded to meet minimum frame size  |
| CRC            | 4 Bytes          | Cyclic Redundancy Check for error detection                   |
#### Cabling Techniques in IEEE 802.3
| Standard    | Common Name      | Data Rate | Cable Type                              | Max Segment Length                             | Topology      |
| ----------- | ---------------- | --------- | --------------------------------------- | ---------------------------------------------- | ------------- |
| 10Base5     | Thicknet         | 10 Mbps   | Thick Coaxial                           | 500 meters                                     | Bus           |
| 10Base2     | Thinnet          | 10 Mbps   | Thin Coaxial (RG-58)                    | 185 meters                                     | Bus           |
| 10Base-T    | -                | 10 Mbps   | Category 3+ UTP                         | 100 meters                                     | Star (hub)    |
| 100Base-TX  | Fast Ethernet    | 100 Mbps  | Category 5 UTP                          | 100 meters                                     | Star (switch) |
| 100Base-FX  | -                | 100 Mbps  | Multimode Fibre                         | 412 meters (half-duplex)<br>2 km (full-duplex) | Star          |
| 1000Base-T  | Gigabit Ethernet | 1 Gbps    | Category 5e/6 UTP                       | 100 meters                                     | Star (Switch) |
| 1000Base-SX | -                | 1 Gbps    | Multimode FIber (short-wave)            | 220-550 meters                                 | Star          |
| 1000Base-LX | -                | 1 Gbps    | Single-mode/Multimode Fiber (Long-wave) | 5 km                                           | Star          |
## G. IEEE 802.4 (Token Bus)
- Concept: A hybrid network that uses a physical bus topology (all stations connected to a single cable) but operates as a logical ring using a token for access control
- Operation (How multiple access is achieved):
	- Stations are arranged in logical ring based on their addresses, independent of their physical order on the cable
	- A special frame called a token circulates around this logical ring
	- Only the station holding the token is permitted to transmit data frames
	- After transmitting, the station passes the token to the next station within a predictable time, eliminating collisions
- Frame Format:
	- Preamble: clock synchronisation
	- Start Delimiter (SD): Marks the beginning of frame
	- Frame Control: used to claim token, Token lost, station with token dead, etc
	- Destination Address (DA): It specifies destination address
	- Source Address (SA): It specifies bytes source address
	- FCS: to detect transmission errors
	- End Delimiter (ED): marks the end of the frame
## H. IEEE 802.5 (Token Ring)
- Concept: A network that uses both a physical star and a logical ring topology. Stations are connected to a central device, but the data path forms a closed loop
- Operation:
	- A token circulates continuously around the logical ring
	- A station that needs to transmit must wait for the token to arrive
	- upon receiving the token, the station changes it to a data frame and transmits its data
	- The frame travels around the ring, and the destination station copies it
	- The frame continues back to the source station, which removes it from the ring and releases a new token
- This process ensures orderly, collision-free access to the shared medium
- Header Format:
	- Start Delimiter: Alerts each station of the arrival of a token (or data/command frame)
	- Access-control byte: contains the priority field (the most significant 3 bits) and the Reservation field (the least significant 3 bits)
	- End delimiter: Signals the end of the token or data/command frame
	- Destination and source addresses: Consists of two 6-byte address fields that identify the destination and source station addresses
	- Data: indicates the length of filed is limited by ring token holding time, which defines the maximum time a station can hold the token
	- FCS: for error detection
	- Frame Status: 1-byte field terminating a command/data frame. the FS field includes the address recognised indicator and frame-copied indicator
#### Difference between token bus vs ring
| Feature           | Token Bus                             | Token Ring                                            |
| ----------------- | ------------------------------------- | ----------------------------------------------------- |
| Physical Topology | Linear Bus (single cable)             | Star-Wired Ring (stations connected to a central MAU) |
| Cable Type        | Coaxial Cable                         | Twisted-Pair (Shielded or Unshielded)                 |
| Token Passing to  | next station in logical address order | physically adjacent station in the ring               |
| primary use case  | manufacturing/industrial networks     | traditional office LANs                               |
## I. IEE 802.11 (Wireless LAN)
- collection of standards set up for wireless networking.
- 802.11 lives in the physical layer and data link layer in the OSI
- 3 popular standards: 802.11a, 802.11b, 802.11g and latest one is 802.11n
- each standard uses a frequency to connect to the network and has a defined upper limit for data transfer speeds
- 2 types of services:
	- Basic Service Set (BSS)
		- IEEE 802.11 defines the BSS as the building blocks of a wireless LAN
		- BSS is made of stationary or mobile stations and optional central base station, AP>
	- Extended Service Set (ESS)
		- In ESS, the BSSs are connected through a distributed system, which is a wired or wireless network.
		- the distributed system connects the APs in the BSS.
## J. FDDI
- Concept:
	- high-speed, token-passing network technology that uses fibre-optic cable to create a highly reliable dual-ring topology
	- functions similar to Token Ring but operates at 100 Mbps
	- designed for backbone and high-performance networks
- Features:
	- Dual-Ring Architecture:
		- Consists of a Primary Ring (used for normal data transmission) and a Secondary Ring (used for backup or special information)
		- Rings are counter-rotating, meaning data flows in opposite directions
	- High Reliability & Fault Tolerance
		- if a cable breaks or station fails, the ring "wraps" at the point of failure, using the secondary ring to create a single continuous loop and maintain network operation
	- High Speed & Capacity:
		- Operates at 100 Mbps, making it significantly faster than early Ethernet and Token Ring
	- Large Geographical Coverage:
		- Supports a total ring length of upto 200 km, making it suitable for MANs and campus backbones
	- Station types:
		- SAS (Single Attachment Station): Connects to one ring (usually via a concentrator), e.g. PC's.
		- DAS (Dual Attachment Station): Connects directly to both rings. e.g., servers and routers
		- Concentrator: A hub-like device that allows multiple SAS devices to connect to the FDDI ring

[[Chapter 4 Network Layer]]