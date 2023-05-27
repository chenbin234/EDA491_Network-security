#### 1. Link-layer attack

**ARP spoofing: **ARP is used to get a system’s MAC address given its IP address and no security is present in the protocol. An attack can easily listen to an ARP request and send a reply to the requesting host before the real receiver responds. Normally the first reply will be used by hosts. 



#### 2. Network-layer attack

**The LAND attack:** The attackers spoofs the source IP address of the packets to match the destination IP address. The attacker also sets the source and destination port numbers to be the same, causing the target system to believe that it is receiving packets from itself. As a result, some systems used to crash when they tried to respond to themselves.

**Teardrop attack:** When data is transmitted over the Internet, it is diveded into smaller units called IP packets. These packets can be fragmented into smaller pieces for efficient transmission. The receiving device reassembles these fragments to reconstruct the original data. However, in a teardrop attack, the attacker sends specially crafted IP fragments that overlap or have invalid offsets, causing the victim’s system to crash.

**Boink attack:** Boink extends fragment outside expected length.

**Ping-of-Death attack:** In a typical scenario, when a system receives a ping request (ICMP echo request), it responds with a ICMP echo reply packet. However, in a ping-of-death attack, the attacker crafts an ICMP echo request packets that exceeds the maximum allowed size specified in the IP standard. This oversized packet can cause buffer overflows or other memory handling errors in the target system.

**How to send such oversized datagram?**

- An oversized IP datagram can be created that exceeds 65,535 bytes by IP fragmentation.
- Where a large IP datagram is divided into several smaller fragments to fit the MTU of the network, and the fragments are reassembled at the destination.

#### 3. Transport-layer attack

A possibility is to try to exhaust the connection table of a receiving host’s TCP stack by never finishing the TCP three way handshake process. By sending a SYN packet only and never response to the SYN-ACK, the receiver waits. By sending lots of such requests, a DOS attack is possible since the table is full and no one else can open new connections.

#### 3.1 DUMB/Idle scanning (why it is useful and how this attack can be done?)

- An attacker who is not allowed to connect with a server due to firewall rules, may find a system that is allowed to access to the server.
- This system can then be the first target in the attack against the server. The way to find such a trusted system is to use fragment numbers in the search for it.
- The attacker first send a SYN to the zombie and record the fragment ID in the reply.
- Then the attacker send a SYN to the target system with the zombie’s address as source
  - if the firewall allowed the traffic from zombie and the target port is open, it will reply a [SYN, ACK] to the zombie, and the zombie will reply with a [RST] and increase the fragment number by one.
- Now, the attacker send another SYN to zombie, and the fragment number will tell whether the target port’s status is open or not.

#### 3.2 SYN cookies / SYN flooding

**What is the problem with a SYN flooding attack?**

- The attacker sends a large number of SYN packets to the target server, but never finishes the TCP three way handshake
- The target server allocates some resources (memory and state table) and return a [SYN, ACK] message for each SYN message, It may exhaust the server’s internal resources to handle legitimate connection requests

**Mention three different ways to, at least to some extent, protect a system against these attacks.**

1. SYN-cookies where the server does not have to keep state.
2. Variable time-out: decrease waiting time when needed.
3. Allocate micro-records and do most of the work when connection completed.
4. Firewalls can be configured to limit the number of incoming SYN packets per second from a single source IP address 
5. IDS/IPS solutions can detect and block suspicious traffic patterns indicative of SYN flooding attacks.

**Why SYN cookies offer protection to the system?**

- By using SYN cookies, the server does not need to maintain a state table or allocate resources for each request before the handshake is completed.
- This allows the target server can handle a large number of connection requests, even in the presence of SYN flooding attack.

**It also makes it harder for the attacker to complete the attack, why?**

The attacker must be using a valid IP address to receive the [SYN, ACk] with the ISN to be able to respond with a valid ACK. Only if the ACK is valid, resources are allocated in the server. 

#### 3.3 Diffie-Hellman key negotiation is computationally expensive which means that an attacker can trigger such computations in order to cause excessive load on a server. Some protocols have protection against this. Mention one such method.

1. IPsec is one example where the server sends a cookie to the client requesting on an IPsec session (using IKE)

2. The cookie contains a hash of the source and destination IP addresses, port numbers and a secret.
3. This must be returned by the client and guarantee that the sender has received the packet.





#### 4. Different scan

- **SYN scan:** send a SYN flag set packet as if you are going to open a real connection and wait for a response.
  - A [SYN, ACK] indicates the port is open
  - A RST indicates the port is closed
- **ACK scan:** send a ACK flag set packet, the purpose of ACK scan is to identify whether a port is filtered or unfiltered.
  - A RST response the host is there, open or closed is undetermined.
  - No response indicates the port is filtered by a stateful firewall or there is no host at all.
- **Null scan:** send a packet with no flags set and wait for a response
  - A RST indicates the port is closed
  - No response indicates the port is open or filtered
- **Xmas scan:** send a packet with FIN, URG, PUSH flags set and wait for a response
  - A RST indicates the port is closed
  - No response indicates the port is open or filtered
- **Fin scan:** send a packet with FIN flag set and wait for a response. The FIN flag is used to indicate the termination of a connection.
  - A RST indicates the port is closed
  - No response indicates the port is open or filtered

**User-case:**

- **SYN** scan is the most common and versatile 
- **ACK** scan is used for identifying firewall rules
- **FIN, NULL, and Xmas** scans are used to evade intrusion detection system and identify host with weak TCP/IP stacks



#### 5. UDP scanning is often harder to do than TCP scanning. Why?

TCP responds with a SYN/ACK to a connection request but UDP just delivers the data to the application and we don’t know how it will react.



#### 6.  Another possibility for an attacker to perform a DoS attack is to try to trigger implementation bugs in protocols. How can this be done? Give two practical examples!

- Abuse header fields, form example send TCP segments with invalid lengths that differ from the real length.
- send IP packets with the source address equal to the address of the receiver.



#### 7. What can be a possible reason for an attacker to send TCP segments with both the SYN and FIN flag set at the same time?

1. To test the stability of the IP stack by sending illegal and malformed packets.

2. Smaller devices with optimized network stacks may crash or system resources may be allocated without ever being freed.



#### 8. What is required for an attacker to be able to insert data into another user’s ongoing TCP session to a web server if the attacker cannot see the traffic between the parties (i.e. the attacker is not a MITM)? Assume the connection is not encrypted and that the attacker is able to guess the IP addresses of the two parties, how easy or complicated is it to perform such an attack and succeed in inserting own data to their session?

- The attacker must guess the TCP sequence numbers.
- In addition, the source port number must be guessed, and since it is a web server, the destination port number is known (80).
- so what the attacker must guess is a 16-bit source port number and 32-bit sequence number.



#### 9. Is it easier or harder to do this attack if the communing parties are located on different continents than very close to each other? Assume that the connection speed is more or less equal. Explain your reasoning!

- It will be easier. A connection with longer delays must allow for more packets to be in transit to optimize performance. 

- It also means that such a connection has a larger receive window, thus maybe only 8 bits of the TCP sequence number has to be guessed.



#### 10. The SMURF attack uses ICMP echo packets and is a magnification attack. Explain how it works and how firewalls connected to the Internet should be configured to prevent such attacks.

- The attacker sends ICMP echo request messages to a broadcast address with a victim as the sender.
- All hosts on the network will send an ICMP echo reply message to the victim, thus one package generates a storm of packets to the victim.
- To prevent this, Firewall should block all external traffic to broadcast addresses.



#### 11. What is required by an attacker to do a blind insertion of a packet into an ongoing TCP session? 

In general, an attacker must guess the TCP sequence number since he is ‘blind’ and cannot see the network traffic. It is enough to guess a number that lies within the current window size.

In addition, IP addresses and port numbers must be guessed.

**Assume you are the attacker and you can see that a person in the room connects to a web server which is well-known to you. What do you have to guess to be able to insert a RST packet into the communication and tear down the connection?** 

- In this case, since you know the web server, both the destination IP address and port number are known.

- So the source port number and some bits of the local IP address plus the TCP sequence numbers must be guessed.



#### 12. The goal of some DoS attacks is to try to exhaust the resources of the target, for example memory, internal tables, network, or the CPU. Briefly describe two possible DoS attacks targeting different resources and what weaknesses they make use of!

- SYN attack, exhausts connection table
- repested requests for encrypted TLS connection (CPU exhausted)































