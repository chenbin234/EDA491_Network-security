## 1. Link-layer attack 

**ARP spoofing: **ARP is used to get a system’s MAC address given its IP address and no security is present in the protocol. An attack can easily listen to an ARP request and send a reply to the requesting host before the real receiver responds. Normally the first reply will be used by hosts. 



## 2. Network-layer attack 

**The LAND attack:** The attackers spoofs the source IP address of the packets to match the destination IP address. The attacker also sets the source and destination port numbers to be the same, causing the target system to believe that it is receiving packets from itself. As a result, some systems used to crash when they tried to respond to themselves.

**Teardrop attack:** When data is transmitted over the Internet, it is diveded into smaller units called IP packets. These packets can be fragmented into smaller pieces for efficient transmission. The receiving device reassembles these fragments to reconstruct the original data. However, in a teardrop attack, the attacker sends specially crafted IP fragments that overlap or have invalid offsets, causing the victim’s system to crash.

**Boink attack:** Boink extends fragment outside expected length.

**Ping-of-Death attack:** In a typical scenario, when a system receives a ping request (ICMP echo request), it responds with a ICMP echo reply packet. However, in a ping-of-death attack, the attacker crafts an ICMP echo request packets that exceeds the maximum allowed size specified in the IP standard. This oversized packet can cause buffer overflows or other memory handling errors in the target system.



## 3. Transport-layer attack

A possibility is to try to exhaust the connection table of a receiving host’s TCP stack by never finishing the TCP three way handshake process. By sending a SYN packet only and never response to the SYN-ACK, the receiver waits. By sending lots of such requests, a DOS attack is possible since the table is full and no one else can open new connections.

