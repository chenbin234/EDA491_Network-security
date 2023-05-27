### 1. Static packet filter

- SYN-scans should not reveal the hidden services.
- Invalid IP packets with expiring TTLS should not be forward.



### 2. Dynamic packet filter

- Protect server against SYN flood attacks coming from one and the same IP address.



### 3. Deep-packet inspection firewall

- Replayed TCP segments should not reach the server.
- DNS requests from the web server and only corresponding replies should be allowed
- ACK and FIN scans should not reveal the hidden services



### 4. Circuit-level gateway

- Hides the real IP address of the sever and protects the server against scanning attacks



### 5. Air-gap firewall





### 6. None of the firewalls

- Inspect web page requests sent to the server.







(A) is the most secure placement, The firewall can have very detailed rules about communication with the web and mail server and can isolate them completely from each other.

(B) is the least secure solution. A cracked server makes it possible for an attacker to listen to all traffic in and out from the corporate network.

(C) is better than (B) but a cracked Web server allows the attacker to listen to all email traffic since they share the network. Link-layer level attack also work between these two servers. 



### 7. Ingress and egress of firewall

**Ingress: filter incoming messages**

- Drop incoming datagrams with internal addresses as source
- Drop incoming datagrams with invalid flags (e.g. SYN and FIN)

**Egress: filter outgoing messages**

- Drop outgoing ICMP echo reply messages
- Drop outgoing datagram containing reserved addresses (e.g. 10.0.0.0/8)



### 8. NAT gateway

**8.1 What level of protection do they offer?**

A NAT gateway hide and isolate internal systems from outside networks. A service not present in its translation table is not accessible from the outside.

**8.2 What do they lack which normal stateful inspection firewalls have?**

It does not inspect traffic that is allowed to traverse.

**8.3 Give an example where a NAT gateway can or should be used.**

- NAT gateways are often used at home where only one official IP address is available and more devices are present.

- It is also popular by companies since NAT hide internal structure of the network and the system’s real IP address inside.



### 9. Circuit-level gateways/proxies remove all headers and replace them with new fresh headers to make sure packet modification attacks do not work.

False, circuit-level gateways work on transport layer, application level header are not touched.



### 10. A stateful firewall must maintain a list of filter rules and also a state table. Give an example of what the state table should contain for TCP and UDP traffic!

1. TCP: port numbers of communicating parties, TCP sequence numbers, TCP state.

2. UDP: port numbers, a timer for when to terminate the connection.



### 11. a stateless screening router as a firewall vs. a NAT gateway to secure your home network

- The stateless firewall can inspect contents of packets, including some application-layer protocol but will not see the relation between packets and can not check TCP sequence numbers, for example. It will not be very secure and it may cause some security problems.
- The NAT gateway on the other hand will only give access to the systems listed in the translation table. However, it does not inspect allowed traffic at all.



#### 12. Stateful firewalls maintain both a state table (connection table) and a table of rules. What is the difference between these tables, why are two needed? Which table is consulted first when an incoming packet is received? Show with an example what happens when some packets go through the firewall and how these two tables are used and what they may contain.

1. **State table** maintains information about established connections, such as source and destination IP addresses, port numbers, protocol, connection status. The state table dynamic updates as new connections are established and existing connections evolve.
2. **Table of rules** defines the criteria and conditions for permitting or blocking network traffic. If a packet matches a rul, the associated actions are implemented.

The reason for having both a state table and a table of rules is to enable stateful inspection, which enhances the firewall’s security.

When an incoming packet is received, the table of rules is consulted first.

Example:

1. **State table:** 

| Source IP     | Source port | Destination IP | Destination port | State       |
| :------------ | ----------- | -------------- | ---------------- | ----------- |
| 192.168.1.100 | 1234        | 10.0.0.1       | 80               | Established |
| 192.168.1.200 | 5678        | 10.0.0.2       | 22               | SYN-sent    |

2. **Table of rules:**

|        |                                                             |
| :----- | ----------------------------------------------------------- |
| Rule 1 | Allow packets from 192.168.1.0/24 to 10.0.0.0/24 on port 80 |
| Rule 2 | Deny packets from any source to destination port 22         |
| Rule 3 | Allow established connections                               |

Packet 1:

- source IP: 192.168.1.100
- Destination IP: 10.0.0.1
- Source port: 1234
- Destination port: 80

Step1: The packet1 is received at the firewall

Step2: The firewall consults the table of rules.

Step3: Rule 1 matches the packet’s criteria, the firewall allows the packet to pass





When an incoming SYN packet is received from the host 22.33.44.55 to port 80 on 1.2.3.4, the ACL list is consulted and a state table entry is created:

22.33.44.55 999 1.2.3.4 80 SYN-recvd

When an SYN/ACK is seen (from 1.2.3.4), the state table is directly consulted and since it contains an entry for this connection, the packet is passed on. It is now updated to:

22.33.44.55 999 1.2.3.4 80 SYN/ACK-sent



#### 13. Give some examples of rules that a screening router likely would have to filter traffic.

- block inout 127.0.0.1
- block incoming packets which have a broadcast address (e.g. 1.2.3.255)
- block outgoing ICMP echo reply message
- block illegal incoming packets (SYN=1, FIN = 1)
- block outgoing packets not belonging to our IP adddress range



#### 14. TTL can sometimes be used to fool firewalls and intrusion detection (IDS) systems. How? Mention a possible protection mechanism against this attack.

- TTL field in a IP packet is used to limit the life time of a packet in the network. It indicates the maximum number of hops that the packet can traverse before being discarded.

- An attacker may increase the TTL value to make the packet as if it was originated from a trusted internal network rather than a external network. By doing that, the packet may bypass certain firewall rules.
- To address this, a possible mechanism is to implement strict TTL checking.



#### 15. What is port knocking? How can it be used to hide a service offered by a system?

- port knocking is a technology used to enhance the security of a service by hiding it from potential attacks.

- The desired service port is closed by default and not publicly accessible.
- Only the correct sequence of port knocks is performed, the system recognizes the pattern and allows the access of the service.



#### 16. (202108 Q4) Now they want to add another access point for visitors coming to the office and consider placing it at one of the positions (a), (b) or (c). The visitors should only be offered Internet access. Where would you place it?

1. (a) is the most secure location since the firewall can inspect the traffic and also make sure all traffic goes to the Internet.
2. (b) is not good since it allows visitors to listen to the in- and outgoing traffic to the company.
3. (c) may allow visitors to monitor all traffic to the web server.



#### 17. Some port scans can be used to get information about the firewall that protects a system. Give an example and explain!

If a ACK or a FIN scan works through a firewall, it has to be stateless since it does not know whether the ACk or FIN packet belongs to a valid session or not.

A stateful firewall would drop it unless the message is valid.



#### 18. Randomizing TCP sequence numbers is good from a security perspective. Why? What problem does it address?

It makes blind TCP guessing attacks much harder. 

If the numbers are predictable, it is much easier for attackers to insert valid data packets into the existing TCP stream.



#### 19. If you are given the task to test whether a firewall is stateful or not, how would you do this? Describe what test you would perform and the expected result! Explain clearly why this test would work!

We could do an ACk or FIN scan. All normal systems respond with a RST packet to the non-matching ACKs.

A reply from a system behind the firewall means that the firewall did not keep state and had to forward the ACK to the inside. A stateful firewall would silently drop the packet.



#### 20. Describe briefly how a stateful firewall works! What information does the firewall (at least) need to save for TCP connections?

Source and destination IP address, source and destination ports.

The firewall must also keep track the TCP state and TCP sequence numbers.

(Real firewall store more info but these info is at least needed for a firewall to be called stateful)



#### 21. What is a DMZ and what purpose does it have?

It is a dedicated network outside the internal network which hosts external services, such as web servers, mail servers and other systems offering services to the outside world.

Purpose is to avoid forwarding traffic to public servers to the internal network.



#### 22. Firewalls must be able to handle UDP traffic, but there is a fundamental problem with it that does not exist for TCP traffic. 

1. Unlike TCP, there are no sessions to keep track of and no sequence numbers.
2. One outgoing datagram may result in one or more replies from the outside.

**How can a firewall handle UDP connections from the “inside” to the “outside”? Is this a good (secure) solution? Assume that the firewall does not understand the application level, thus cannot inspect these datagrams and the replies.**

When a request packet is sent out from the trusted side, it can allows replies from the outside, but only from the same host and port number that received the first packet and only for a limited time period.

