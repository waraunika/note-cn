IPv6 is the most recent version of the Internet Protocol (IP), the communications protocol that provides an identification and location system for computers on that networks and routes traffic across the Interent
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
7. It aids multicasting by allowing scopes to be specified
# 7.2 Packet Formats
# 7.3 Extension headers
# 7.4 Transition from IPv4 to IPv6
## Dual stack
## Tunneling
## Header Translation
# 7.5 Multicasting
[[Chapter 8 Network Security]]