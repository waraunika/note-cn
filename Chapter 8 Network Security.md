**Definition**
- Network Security is the practice of protecting a computer network with its data from unauthorised access, misuse, malfunction, modification, destruction or improper disclosure
- It is critically important because networks are fundamental to modern business, government and personal life.
- a breach can lead to financial loss, reputational damage, and the compromise of sensitive information
- A network is considered compromise when an unauthorised individual or program gains access, disrupts operations, or steals data
- this is typically caused by threats like malware, hacking, social engineering or unpatched software vulnerabilities 
**Attacks**:
The internet has helped to open door to vandals all over the world, making any system connected to it vulnerable to attack. possible attacks are:
- **Interruption**: attack on the availability of information by cutting wires, jamming wireless signals, or dropping of packets
- **Interception**: When a message is communicated through network, eavesdroppers can listen and use it for their own benefit and try to tamper it
- **Modification**: Eavesdropper can intercept it and send a modified message in place of the original one
- **Fabrication**: A message may be sent by a stranger by posing as friend
- **Denial of service attacks**: makes a service unusable, usually, by overloading the server or network
- Figure:
  ![[attacks.png]]
# 8.1 Properties of secure communication
1. Confidentiality
	- ensures that data is accessible only to authorised parties
	- protects against eavesdropping
	- achieved via encryption
2. Integrity
	- guarantees that data has not been altered in transit or storage
	- either maliciously or accidentally
	- achieved via hashing and digital signature
3. Non-repudiation
	- prevents a party from denying that they sent a message or performed an action
	- provides legal proof
	- achieved via digital signatures and audit logs
4. Authentication
	- verifies the identity of a user, system, or entity
	- confirms that parties are who they claim to be
	- achieved via passwords, multi-factor authentication, digital certificates
5. Access control
	- restricts what resources a user can access and what actions they can perform after authentication
6. Availability
	- ensures that systems and data are accessible to authorised users when needed
	- protects against Denial of Service (DoS) attacks
	- achieved via redundancy, robust infrastructure and DDoS mitigation
# 8.2 Principles of cryptography
## A. Concept
- Cryptography is the science of securing communication by transforming messages to make them immune to attacks by unauthorised parties (hackers)
- fundamental for ensuring private communication over public networks, like internet
## B. Terminology
- **Plaintext** /clear text: the original, readable message or data
- **Ciphertext** /code text: the scrambled, unreadable output produced by encrypting the plaintext
- **Cipher**: the algorithm (mathematical function) used for encryption and decryption
- **Key**: a secret value (a number or string) that a cipher uses to encrypt or decrypt data. The security relies on the secrecy of the key, not the cipher
## C. Components
- Cryptography uses mathematical algorithms (ciphers) to change text from one form to another
- the foundational principle is Kerchkoff's principle;
	- The encryption and decryption algorithms (ciphers) are public knowledge
	- The security of the system depends entirely on the secrecy of the key
- In other words, even if an attacker knows the exact method used to encrypt a message, they should be unable to read the ciphertext without the specific secret key
- figure:
  ![[components_cryptography.png]]
## D. Encryption Methods
### D.1 Substitution Cipher
This method disguises the message by replacing each letter or group of letters with another
1. **Caesar Cipher**
	- each letter is shifted a  fixed number of positions (k) in the alphabet
	- if k = 2, then "`attack`" would be "`cvvcerm`" in ciphertext
	- Vulnerability: easy to break with only 25 possible keys
2. **Monoalphabetic Cipher**
	- uses a fixed random substitution for each letter throughout the message
	- as long as each letter has a unique substitution
	- Plaintext:    `abcdefghijklmnopqrstuvwxyz`
	- ciphertext: `mnbvcxzasdfghjkipoiuytrewq`
	- for example plaintext: `attack` would be transformed into cipher text `qzzqea`
	- Vulnerability: Breakable by frequency analysis (matching common letters)
3. Polyalphabetic Cipher
	- uses multiple substitution alphabets in a repeating pattern
	- making the same plaintext letter encrypt to different ciphertext letters
	- for example, 
	- if two different caesar cipher (with k = 2 and k = 5) as shown below, one might choose use these ciphers C1 and C2 in repeating patter of C1, C2, C1, i.e. first letter to be encoded using C1 and the second letter encoded using C2 and so on
	- Plaintext  `i`  `a`  `m`  `a`  `s`  `t`  `u`  `d`  `e`  `n`  `t`
	- C1 (k=2)  `k`  `c`  `o`  `c`  `u`  `v`  `w`  `f`  `g`  `p`  `v`
	- C2 (k=5)  `n`  `f`  `r`  `f`  `x`  `y`  `z`  `i`  `j`  `s`  `y`
	- Vulnerability: More secure than monoalphabetic, but patterns can be discovered.
### D.2 Transposition Cipher
reorders the letters of the plaintext without disguising them
- Concept:
	- the letters are rearranged according to a specific scheme (e.g., writing the message in a grid row-by-row and reading it off column-by-column)
- effect: 
	- it destroys the common letter patterns found in the language, making frequency analysis ineffective
	- the ciphertext contains the same letters as the plaintext, but in different order
- Security: while more secure than simple substitution, it can often be broken by anagramming techniques
- Figure:
	![[transposition.png]]
## E. Types of Cryptography Algorithm
### E.1 Symmetric Key Cryptography (Secret-key)
- Concept: Both the sender and receiver use the same single, secret key for both encryption and decryption
- Process:
  `Plaintext + Shared Secret Key -> Ciphertext -> Plaintext + Shared Secret Key`
- figure:
  ![[symmetric_key.png]]
- Characteristics:
	- Fast and efficient, suitable for encrypting large volumes of data
	- Key distribution is a major challenge, how to securely share the secret key with the intended recipient
	- the number of keys grows rapidly with the number of users
- Advantages: speed, efficiency for long message
- Disadv: secure key distribution is difficult, doesn't scale well for large number of users
### E.2 Asymmetric Key Cryptography (Public Key)
- Concept: Uses a mathematically linked pair: a Public Key (shared openly) and a private key (kept secret)
- Process:
	- Encryption: Anyone can encrypt with the recipient's public key
	- Decryption: Only the recipient can decrypt with their private key
- Characteristics:
	- Solves the key distribution problem
	- Computationally intensive and much slower than symmetric encryption
	- primarily used for secure key exchange, digital signatures, and encrypting small amounts of data
- Advantages: No need to pre-share a secret; better scalability
- Disadvantage: slow performance; complex algorithms; requires a way to verify that public key truly belongs to its claimed owner
- Figure
  ![[asymmetric_key.png]]
### E.3 Differences
| Feature          | Symmetric Key System                     | Asymmetric Key System (Public Key)               |
| ---------------- | ---------------------------------------- | ------------------------------------------------ |
| Keys             | Single, shared secret key                | a pair: public key and private key               |
| Speed            | fast. efficient for bulk data encryption | slow. used for small data or key exchange        |
| Key Distribution | major challenge                          | solved: public keys can be freely distributed    |
| Scalability      | poor (requires many keys)                | good (requires fewer keys)                       |
| Primary Use      | confidentiality of data                  | key exchange, digital signatures, authentication |
## F. Block Cipher
- Concept:
	- A method of encryption that processes a fixed-length group of bits (a block) as a single unit
	- complex substitution cipher for very large characters made of bits
- Internal Components: Modern block ciphers like DES combine several operations to create confusion and diffusion:
	- Substitution Boxes (S-boxes): Replace a set of input bits with a different set of output bits, creating confusion to hide the relationship between the key and ciphertext
	- Permutation Boxes (P-boxes): Shuffle or transpose the positions of bits across the block, creating diffusion to spread the influence of one plaintext bit over many ciphertext bits
	- Exclusive-OR (XOR) Operations: Combine data with a round key
## G. Data Encryption Standard (DES)
- DES is a symmetric-key block cipher that encrypts data in 64-bit blocks using a 56-bit key
- foundational encryption standard
- 56 bits are for normal encryption/decryption, remaining 8 bits are for parity check
- Operation of the DES Encryption Algorithm:
	1. The 64-bit plaintext block is fed into the algorithm
	2. it undergoes an Initial Permutation (IP)
	3. The core of the algorithm is 16 identical rounds of complex operation
	4. After the 16 rounds, a 32-bit swap occurs
	5. Finally the data passes through a Final Permutation (IP$^{-1}$), which is the inverse of the initial permutation, to produce the 64-bit ciphertext
- For decryption: the same algorithm, but with the round keys applied in reverse order
- figure:
  ![[encryption_decryption_des.png]]
- structure of DES figure:
  ![[structure_of_des.png]]
- DES uses 16 rounds and each round is a Feistel cipher
- the overall processing at each iteration is shown below figures:
	1. Round operation:
	   ![[round_operation.png]]
	2. Function Operation
	   ![[function_operation.png]]
## H. Deffi Helman Algorithm
- Concept:
	- method that allows two parties to establish a shared secret key over an insecure public channel
	- it is a key agreement protocol, not an encryption algorithm
	- derived key is then used for symmetric encryption
	- two parties exchange public values, derived from their own private secrets
	- an eavesdropper seeing these public values cannot feasibly calculate the shared secret due to the computational difficulty of the discrete logarithm problem
- steps of algorithm:
	- Parameter Agreement: Both parties (Alice and Bob) publicly agree on a large prime number N and a base (or generator) G
	- Private Secrets: Each party chooses their private key:
		- Alice chooses a large random number X 
		- Bob chooses a large random number Y
	- Public Exchange: Each party computes a public key, and sends it to the other
		- Alice computes R1 = G$^X$ mod N, sends R1 to Bob
		- Bob computes R2 = G$^Y$ mod N, sends R2 to Alice
	- Shared Secret Calculation: Each party uses their own private key and the other's public key to compute the same shared secret key, K
		- Alice calculates K = R2$^X$ mod N
		- Bob calculates K = R1$^Y$ mod N
		- Both have same result: K = G$^{XY}$ mod N
- Figure:
  ![[deffi_helman.png]]
# 8.3 RSA Algorithm
- Rivest, Shamir, Adleman Algorithm
- most common public key encryption algorithm used in Network Security 
- uses two numbers 'e' and 'd' as public and private which have a special relationship to each other
- those two keys help to encrypt and decrypt the information 
- it is based upon a fact that it is easy to multiply two prime numbers but it is very difficult to factor that product and them back

**Algorithm**:
1. Key Generation:
	- Choose 2 large primes: p and q
	- Compute modulus: n = p * q
	- Compute z = (p-1) * (q-1)
	- Choose public exponent e : 1 < e < z, and e must be co-prime with z (i.e share no common factors)
	- Compute private exponent d: d is the modular multiplicative inverse of e module z. This means, (d * e ) mod z = 1
	- Public Key: (n, e)
	- Private Key: (n, d)
2. Encryption by sender
	- Convert plaintext message m (as a number) into ciphertext c using recipient's public key:
	- c = m$^e$ mod n
3. Decryption by receiver
	- Recover the original message from the ciphertext using their private key:
	- m = c$^d$ mod n

**Example**: Encrypting "ROSE"
1. Key Generation
	- let p = 11, q = 3
	- n = p * q = 33
	- z = (p-1) * (q-1) = 20
	- choose e = 3 (3 is co-prime with 20)
	- Find d such that (d * 3) mod 20 =1
	- d = 7 works, as 21 mod 20 = 1
	- public key (n, e): (33, 3)
	- private key (n, d): (33, 7)
2. Encryption
	- R = 18, O = 15, S = 19, E = 5
	- Encrypt each number using public key (33, 3)
		- R (18): c = 18^3 mod 33 = 24
		- O (15): c = 15^3 mod 33 = 9
		- S (19): c = 19^3 mod 33 = 28
		- E (5): c = 5^3 mod 33 = 26
	- Cipher text = 24, 9, 28, 26
3. Decryption:
	-  Decryption Key = (33, 7)
	- Decrypt each number:
		- 24: 24^7 mod 33 = 18
		- 9: 24^9 mod 33 = 15
		- 28: 24^9 mod 33 = 19
		- 26: 26^9 mod 33 = 5
	- Decrypted message = ROSE
# 8.4 Digital Signatures
- **Concept**:
	- it is a cryptographic technique that binds a cryptographic technique that binds a person's identity to a digital document
	- provides authentication, integrity and non-repudiation
- **Need**:
	- they are electronic equivalent of a handwritten signature or sealed seal
	- but with much stronger security:
	- they prove:
		- who signed the documentation (authentication)
		- that the document was not altered after signing (integrity)
		- that the signer cannot deny having signed it (non-repudiation)
- **Working**:
	1. Signing (by the sender)
		- the document is passed through a hash function (e.g., SHA-256) to generate a unique, fixed-size message digest
		- this hash is then encrypted with the sender's private key
		- this encrypted hash is the digital signature
		- the signature is attached to the original document and sent to the recipient
	2. Verification (by the recipient)
		- the recipient separates the received package into the original document and digital signature
		- the recipient decrypts the digital signature using the sender's public key
		- this reveals the original hash that sender created
		- the recipient independently takes the received document and runs it through the same hash function to generate a new hash
		- the recipient compares the two hashes
		- if same, signature is valid and document is authentic and unaltered
		- if two hashes do not match, the signature is invalid, and the document was tampered with or not signed by the claimed sender
- Figure:
  ![[digital_signature.png]]
# 8.5 Securing e-mail (PGP)
- **Concept**:
	- Pretty Good Privacy (PGP) is a widely-used encryption program that provides cryptographic privacy and authentication for data communication, primarily used for securing mail
	- combines the best features of both symmetric and asymmetric cryptography to achieve efficiency and strong security.
	- offers confidentiality, authentication, integrity and compression
- **Process of Sending Email**:
	1. Digital Signature
		- The sender's system generates a hash (digest) of the original plaintext email
		- the hash is encrypted with the sender's private key, creating a digital signature
		- the signature is attached to the original message
	2. Compression
		- the combined data (original message + digital signature) is compressed to save space
	3. Encryption for Confidentiality
		- a random, one-time session key is generated
		- the compressed data is encrypted using this session key with a fast symmetric-key algorithm
		- the session key itself is then encrypted with the recipient's public key
	4. Transmission
		- The encrypted session key and the encrypted data are sent to the recipient
- **Process of Receiving Email**:
	1. The recipient decrypts the session key using their own private key
	2. the recipient uses this session key to decrypt the compressed data
	3. the data is decompressed, separating the original message from the digital signature
	4. to verify the signature:
		1. the recipient decrypts the digital signature using the sender's public key to retrieve the original hash
		2. the recipient generates a new hash from the received message
		3. if the two hashes match, the message is authentic and intact
- Figures:
  ![[pgp_1.png]]
  ![[pgp_2.png]]
  ![[pgp_3.png]]
  ![[pgp_4.png]]
# 8.6 Securing TCP connections (SSL)
- **Concept**: 
	- Secure Sockets Layer (SSL) and its successor, Transport Layer Security (TLS), are cryptographic protocols designed to provide secure communication over a computer network, most commonly used to secure connections between web browser and servers
	- it operates between the Application Layer and Transport Layer, creating a secure tunnel over a TCP connection.
	- provides encryption, authentication and data integrity
- **Working**:
	1. The SSL/TLS Handshake:
		- Negotiation: the client and server agree on the SSL/TLS version and cryptographic algorithms (cipher suite)
		- Authentication: the server proves its identity to the client by sending a digital certificate
		- Key Exchange: the client and server securely generate a shared symmetric session key (often using asymmetric encryption like RSA or Diffie-Hellman for key exchange)
		- Secure Channel Established: once the handshake is complete, all subsequent data is encrypted using the fast symmetric session keys
	2. Data Transfer (Record Protocol):
		- Fragmentation: Data is split into manageable blocks
		- Compression: Blocks are compressed (optional)
		- Message Authentication: A Message Authentication Code (MAC) is added to ensure data integrity
		- Encryption: the data and MAC are encrypted for confidentiality
		- Framing: a header is added, and the final block is transmitted over the TCP connection
- Figure:
  ![[SSL.png]]
# 8.7 Network Layer security
## A. IPsec (IP security)
- **Concept**: 
	- A suite of protocols developed by the IETF to provide secure communication at the IP layer. 
	- It can protect data between hosts, routers, or a host and a router, and works with both IPv4 and IPv6.
- **Purpose**: 
	- To add authentication, integrity, and confidentiality to IP packets, securing applications that use the network layer directly (like routing protocols) and enabling secure Virtual Private Networks (VPNs).
#### IPsec Modes
| Mode           | Protection Scope                                                                                                      | Use Case                                                                                     |
| -------------- | --------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------- |
| Transport Mode | Protects the payload (data from the transport layer). <br>The original IP header is not protected.                    | Secure communication between two end hosts (e.g., client and server).                        |
| Tunnel Mode    | Protects the entire original IP packet (header and payload). The secured packet is encapsulated with a new IP header. | Primarily used for site-to-site VPNs where gateways secure all traffic between two networks. |
#### IPsec Security Protocols
IPsec uses two main protocols to achieve security goals, which can be used individually or together.
1. Authentication Header (AH) Protocol
	- Provides: Source authentication and data integrity.
	- Does NOT provide: Confidentiality (no encryption).
	- How it works: Adds an AH header that includes a hash of the packet (and parts of the IP header in transport mode). This hash allows the receiver to verify the packet's sender and that it hasn't been tampered with.
2. Encapsulating Security Payload (ESP) Protocol
	- Provides: Confidentiality (encryption), data integrity, and source authentication.
	- How it works: Encrypts the payload (in transport mode) or the entire original packet (in tunnel mode). It adds an ESP header and an ESP trailer. The trailer includes an Authentication Data field for integrity and authentication, similar to AH.
## B. Virtual Private Network (VPN)
- Concept:
	- VPN creates a secure, encrypted "tunnel" over a public network (like the internet)
	- allows remote users or sites to access a private network as if they were directly connected to it
	- uses tunneling protocols (like IPsec or SSL/TLS) and strong encryption to ensure privacy and security
### B.1 Remote Access VPN
- **Purpose**:
	- Allows an individual user to securely connect to a private organisational network from a remote location via the internet
- **Working**:
	- the user's device runs VPN client software that establishes an encrypted connection to a VPN gateway at the organisation's network perimeter
- **Functions**:
	- Authentication: Verifies the identity of the remote user
	- Access Control: Ensures the user can only access authorised resources on the private network
- Figure
  ![[remote_access_vpn.png]]
### B.2 Site to Site VPN
- **Purpose**: 
	- Connects two or more fixed networks (e.g., a company's main office and its branch offices) over the internet to form a single, cohesive private network
- **Working**: 
	- a VPN gateway (like a router or firewall) at each site establishes a permanent, secure tunnel between the networks.
	- All traffic between the sites is encrypted
- **Types**:
	- Intranet-based: Connects multiple remote locations of the same organisation
	- Extranet-based: Connects the network of different organisations (e.g. a company and its partners or suppliers) to enable secure collaboration
- FIgure:
  ![[site_to_site_vpn.png]]
# 8.8 Wired Equivalent Privacy (WEP) Protocol
- Concept: 
	- WEP was the original data-link layer security protocol for 802.11 (WiFi) networks
	- designed to provide a level of confidentiality equivalent to a wired network
	- **now considered highly insecure and obsolete**
	- uses RC4 stream cipher for encryption
	- a secret key is shared between the wireless client and the access point
	- to encrypt a packet, RC4 uses this key to generate a key-stream, which is then XORed with the plaintext data to produce ciphertext
- **Working**:
	- Key Setup: A static Secret Key (40-bit or 104-bit) is manually configured on the access point and all clients
	- Encryption (Sender):
		- A 24-bit initialisation vector (IV) is generated for each packet
		- the IV is concatenated with the Secret Key to form the full RC4 cipher key
		- This key is used by RC4 to generate a keystream
		- the keystream is XORed with the plaintext data and a checksum (CRC-32) to produce the cipher text
		- The IV is sent in the clear (unencrpyted) with the packet
	- Decryption (Receiver):
		- The receiver uses the received IV and its own stored Secret Key to generate the identical keystream
		- XORing the keystream with the cipher text recovers the original paintext and checksum
		- the checksum is verified to ensure data integrity
# 8.9 Firewalls: Application Gateway and Packet Filtering and IDS
## A. Firewall
- **Concept**:
	- A firewall is a 
		- security system (a combination of hardware and software) that 
		- acts as a barrier between a trusted internal network (e.g., a company's network) and an untrusted external network (e.g., internet)
	- it enforces a security policy by controlling incoming and outgoing network traffic
	- it partitions the network into "inside" (trusted) and "outside" (untrusted) zones
	- it inspects all traffic that cross this boundary and deciding whether to allow or block it based on a predefined set of rules
- **Functions & Benefits**:
	- Access Control: Allows only authorised traffic to pass through and blocking all other connections by default
	- Preventing Unauthorised Access: Stopping external attackers (hackers) from gaining access to the internal network
	- Protecting data integrity: helping to prevent intruders from modifying or deleting internal data
	- safeguarding confidential information: blocking attempts to steal secret or sensitive data
	- mitigating network attacks: helping to protect against denial-of-service (DoS) and other malicious attacks
- FIgure:
  ![[firewall.png]]
### A.1 Packet-Filter Firewall
- **Concept**:
	- A packet-filter firewall is a network security device that operates at the Network Layer and Transport Layer
	- acts as a router that makes forwarding decisions based on predefined rules applied to the headers of individual data packets
	- it statically examines each packet in isolation, comparing information in its header against an Access Control List (ACL) to decide whether to allow or drop it
- **Working**:
	- It inspects some criteria:
		- Source IP address: Where packet is coming from
		- Destination IP address: Where packet is going to
		- Protocol: type of traffic, e.g., tcp, udp, icmp
		- port numbers: the application or service (e.g., port 80 for http, port 25 for smtp)
	- Process:
		1. Packet arrives at the firewall
		2. firewall extracts the header information
		3. it compares this information sequentially against its list of rules
		4. one the first rule match, it takes specified action (allow or deny)
		5. if no rules match, a default action (usually deny) is applied
	- example of rule: DENY ALL traffic FROM IP 192.168.1.199 TO PORT 80
- FIgure:
  ![[packet_filter.png]]
### A.2 Application-Level Gateway (Proxy Firewall)
- **Concept**:
	- is a security system that operates at the application layer
	- acts as an intermediary for specific applications, where all traffic for that service must pass through the proxy
	- the proxy inspects the entire contents of the traffic before deciding to forward it
	- instead of just looking at packet headers, it deeply inspects the actual data and commands within the packet to enforce security policies for a specific application (e.g., HTTP, FTP)
- **Working**:
	1. An internal client sends a connection request to the proxy gateway, not the real external server
	2. the proxy acting as a server for the client, receives and fully inspects the application data
	3. it makes an allow/deny decision based on the content and security policy
	4. if allowed, the proxy then acts as a client and establishes a new, separate connection to the real external server on behalf of the internal user
- Figure:
  ![[application_gateway.png]]
## B. Instrusion Detection System (IDS)
- **Concept**:
	- is a security tool that monitors a network or computer system for suspicious activity, policy violations or known attack patterns
	- acts as a security alarm, detecting and reporting threats, but not automatically blocking them
	- analyses traffic and system activity, compares it against a set of rules or a baseline of normal behaviour, and generates alerts when it identifies potential security incidents
- **Types**:
	- Network IDS
		- Monitors traffic
		- deployed at strategic points to analyse all passing traffic for malicious activity
	- Host-based IDS
		- single host/computer
		- installed on individual devices to monitor system files, logs, and application activity for signs of compromise
- **Methods of Detection**:
	- Signature-Based Detection:
		- compares network traffic or system activity against a database of known attack patterns
	- Anomaly-based Detection
		- Establishes a baseline of "normal" system or network behavior
		- flags any activity that significantly deviates from this baseline as potentially malicious
[[Chapter 1 Introduction to Computer Network]]