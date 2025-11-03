IPv6 is the most recent version of the Internet Protocol (IP), the communications protocol that provides an identification and location system for computers on that networks and routes traffic across the Internet
IPv6 was developed by the Internet Engineering Task Force (IETF) to deal with the long-anticipated problem of IPv4 address exhaustion
IPv6 is intended to replace IPv4
**Address Space**
- uses 128-bit address that is very large space compared to 32-bit of IPv4
- uses a special notation called Hexadecimal Colon Notation
- Here 128 bits are divided into 8 sections, each one 16 bits long.
- Example:
	- `FE80:0000:0000:0001:0800:23E7:F5DB`
**Limitations**
- network layer protocol in the TCP/IP protocol suite is currently IPv4 (Internetworking Protocol, version 4)
- IPv4 provides host-to-host communication between systems in the Internet
- Although IPv4 is well designed, data communication has evolved since the inception of IPv4 in the 70's.
- IPv4 has some deficiencies that make it unsuitable for fast growing internet:
	- Despite all short-term solutions such as subnetting, classless addressing, and NAT, addressing depletion is still a long-term problem in the Internet
	- The Internet must accommodate real-time audio and video transmission. This type of transmission requires minimum delay strategies and reservation of resources not provided in the IPv4 design
	- The Internet must accommodate encryption and authentication of data for some applications. No encryption or authentication is provided by IPv4
# 7.1 IPv6 - Advantages
1. Larger Address space:
	   The address space of IPv6 contains 2$^{128}$ addresses. This is very large in comparison to IPv4 containing only 2$^{32}$ addresses. Nearly $8 \cdot 10^{28}$ times larger
2. Better header format:
	   IPv6 uses a new header format in which options are separated from the base header and inserted when needed. This reduces processing delay due to fixed header size and there is no header checksum
3. Possibility of extension
	   IPv6 has been designed in such a way that there is possibility of extension of protocol if required
4. Reduction in routing table
	   Globally unique and hierarchical addressing, based on prefixes rather than address classes to keep routing tables small and backbone routing efficient
5. Support for more security
	   The encryption and authentication options in IPv6 provide confidentiality and integrity of the packet
6. Support for resource allocation
	   In IPv6, the type of service field has been removed, but a mechanism has been added to enable the source to request special handling of the packet. This mechanism can be used to support traffic such as real-time audio and video
7. It aids multicasting by allowing scopes to be specified
# 7.2 Packet Formats
| Field               | size     | Function                                                                                                                                                                                                                                                  |
| ------------------- | -------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Version             | 4 bits   | - used to indicate the version of IP<br>- set to 6                                                                                                                                                                                                        |
| Traffic Class       | 8 bits   | - same function as ToS in IPv4<br>- distinguish different real-time delivery requirement                                                                                                                                                                  |
| Flow label          | 24 bits  | - identifies a flow<br>- it is intended to enable the router to identify packets that should be treated in a similar way without the need for deep lookups within those packets.<br>- set by the source and not changed by routers in path to destination |
| Payload Length      | 16 bits  | - only the length of the payload<br>- header length is fixed to 40 bytes                                                                                                                                                                                  |
| Next Header         | 8 bits   | - indicates either the first extension header (if present) or the protocol in the upper layer PDU                                                                                                                                                         |
| Hop Limit           | 8 bits   | - IPv4 TTL was appropriately renamed Hop Limit<br>- is decremented at each hop                                                                                                                                                                            |
| Source Address      | 128 bits | - stores IPv6 address of originating host                                                                                                                                                                                                                 |
| Destination Address | 128 bits | - stores the IPv6 address of the current destination host                                                                                                                                                                                                 |
Figure:
![[ipv6_header.png]]
#### Comparison with IPv4 header
Figure:
![[ipv4_ipv6.png]]
1. Few fields have been removed:
	1. Identification, flags, fragmentation offset
	2. TOS, header length
	3. Header checksum
2. Some of the name of the fields have been changed
	1. Total length -> payload length
	2. Protocol -> Next header
	3. Time to Live -> Hop limit
3. Added some fields
	1. Traffic class
	2. Flow label
4. Major improvements:
	1. No option field: replaced by extension header. result in a fixed length, 40 byte header
	2. No header checksum: result in fast processing
	3. No fragmentation at intermediate nodes: result in fast IP forwarding
#### Comparison of IPv4 and IPv6
| Aspect                 | IPv4                                                | IPv6                                                                                                                |
| ---------------------- | --------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------- |
| address length         | 32-bit                                              | 128-bit                                                                                                             |
| DHCP support           | supports manual and DHCP address configuration      | - does not require manual and DHCP address configuration. <br>- supports auto and renumbering address configuration |
| end-to-end integrity   | end to end connection integrity is unachievable     | achievable                                                                                                          |
| Security               | Security features are dependent on application      | IPSec is an inbuilt security feature in the IPv6                                                                    |
| Address representation | in decimal                                          | in hexadecimal                                                                                                      |
| Fragmentation          | performed by sender and forwarding routers          | only by sender                                                                                                      |
| flow identification    | flow identification not available                   | is available, and uses flow label field in the header                                                               |
| checksum               | checksum is available                               | checksum field is not available                                                                                     |
| message transmission   | It has broadcast Message Transmission Scheme        | multicast and anycast message transmission scheme is available                                                      |
| security facilities    | encryption and authentication facility not provided | provided                                                                                                            |
| header length          | 20 - 60 bytes                                       | 40 bytes fixed                                                                                                      |
# 7.3 Extension headers
- **Concept**: 
	- a flexible and efficient mechanism to add optional feature to an IPv6 datagram without bloating the base header
	- Unlike IPv4 fixed options field, IPv6 uses a chain of separate headers, each dedicated to a specific function
- Needed because:
	- **Efficiency**:
		- most datagrams don't need all advanced features (e.g., fragmentation, security)
		- including fixed fields for every feature in the base header would be wasteful
	- **Flexibility**:
		- Senders can include only the necessary headers, making the protocol adaptable to various needs
	- **Performance**: 
		- Routers only need to process the Hop-by-Hop Options header, improving forwarding speed for most traffic
###### How the Header Chain works:
- the next header field in each header acts as a pointer to the next item in the chain, forming a linked list.
- Structure:
  `IPv6 Base header -> Extension Header 1 -> Extension Header 2 -> ... `
  `... -> Extension Header N -> Transport Layer Data`
- Each header's `Next Header` field identifies the type of the header that follows
- Headers must be processed in the strict order they appear in the packet
- Figures:
  ![[extension_headers.png]]
  ![[example_header_chain.png]]
###### Types
| Header Type                    | Code | Purpose/Function                                                                                                                          |
| ------------------------------ | ---- | ----------------------------------------------------------------------------------------------------------------------------------------- |
| Hop-by-Hop Options             | 0    | - carries information that every router along the path must examine                                                                       |
| Routing                        | 43   | - used for source routing, where the sender specifies the path<br>- similar to IPv4's loose/strict source routing                         |
| Fragment                       | 44   | - used for fragmentation<br>- difference from IPv4: only original source can fragment a packet                                            |
| Authentication Header          | 51   | - provides data integrity and origin authentication<br>- ensures the packet is from who it claims and wasn't altered                      |
| Encapsulating Security Payload | 50   | - provides confidentiality through encryption, preventing eavesdropping on the packet's payload                                           |
| Destination Options            | 60   | - carries information that needs to be processed only by the final destination of the packet<br>- no one else has the access to read this |
# 7.4 Transition from IPv4 to IPv6
- the transition from IPv4 to IPv6 is gradual, long-term process because the internet is too vast
- difficult to switch over all at once
- core challenge is ensuring backward compatibility and seamless interoperability between IPv4 and IPv6 systems during this extended period
- 3 strategies have been devised to help the transition:
  Dual Stack, Tunneling and Header translation
## A. Dual stack
- Concept:
	- fundamental transition strategy where a network node (a host or a router) is equipped with complete implementations of both IPv4 and IPv6
- Working:
	- The Dual-Stack Node has two separate protocol stacks, allowing it to understand, process and generate both IPv4 and IPv6 traffic
	- When communicating with an IPv4 node, it uses IPv4 packets
	- When communicating with an IPv6 node, it uses IPv6 packets
- Role of DNS:
	- The decision of which IP version to use is made by querying the DNS
	- if DNS returns an IPv4 address (A record), the source host sends an IPv4 packet
	- If DNS returns an IPv6 address (AAAA record), the source host sends an IPv6 packet
- Significance:
	- This approach allows for a gradual upgrade of systems without breaking existing IPv4 connectivity.
	- it is the prerequisite for other transition techniques like tunneling.
- Figure:
  ![[dual_stack.png]]
## B. Tunneling
- Concept:
	- used to connect isolated IPv6 "islands" over an existing infrastructure
	- an IPv6 packet is encapsulated with an IPv4 packet's payload to be carried across an IPv4 network
- Working:
	- The source IPv6 node sends an IPv6 packet to a Dual-Stack Router at the edge of its network
	- This router encapsulates the entire IPv6 packet inside an IPv4 packet (it becomes the payload)
	- The IPv4 packet is routed through the IPv4 internet to the Dual-Stack Router at the destination IPv6 network
	- The receiving router decapsulates the packet, extracting the original IPv6 packet
	- The IPv6 packet is then delivered to the destination host
- Analogy:
	- like writing a letter in English, but sending it via an envelope addressed in French to get it through French Postal System
- Figure:
  ![[tunneling.png]]
## C. Header Translation
- Concept:
	- this technique is necessary when the majority of the internet has transitioned to IPv6 but a system needs to communicate with remaining IPv4-only server
	- a dual stack router translates an IPv6 packet into an IPv4 packet and vice-versa
- Working:
	- An IPv6 host sends a packet destined for an IPv4 address
	- A header translation router converts the IPv6 header into a functionally equivalent IPv4 header
	- resulting IPv4 packet is then sent to the IPv4-only destination
- Translation Procedure:
	- Change the IPv6 mapped address to an IPv4 address by extracting the rightmost 32 bits
	- Discard the value of IPv6 priority field
	- Set the type of service field in IPv4 to be zero
	- Calculate the checksum for IPv4 and insert in corresponding field
	- Ignore the IPv6 flow label
	- Convert the compatible extension headers to options and insert them in the IPv4 header
	- Calculate the length of IPv4 header and insert it into the corresponding field
	- Eventually, compute the total length of the IPv4 packet and insert it into the corresponding field
- Limitation:
	- not a perfect solution
	- some features are IPv6 exclusive (like flow label or extensive security)
	- these feature have no direct equivalent in IPv4 and maybe lost in translation
	- this technique is used as a last resort
- Figure:
  ![[header_translation.png]]
# 7.5 Multicasting
- in IPv6, multicast traffic operates in the same way that does in IPv4
- Arbitrary located IPv6 nodes can listen for multicast traffic on an arbitrary IPv6 multicast address
- Nodes can join or leave a multicast group at any time
- IPv6 multicast addresses have the first 8 bits set to `1111 1111`
- therefore an IPv6 multicast address always begins with FF.
- IP multicast address has a prefix FF00:/8.
- The second octet defines the lifetime and scope of the multicast address
- Multicast address cannot be used as source address or as intermediate destination in a Routing Extension Header
- Some examples of IPv6 Multicast are for different purposes are: RIPng, OSPv3, EIGRP

[[Chapter 8 Network Security]]