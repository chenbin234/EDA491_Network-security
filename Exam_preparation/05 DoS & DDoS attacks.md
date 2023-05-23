**ARP spoofing: **ARP is used to get a system’s MAC address given its IP address and no security is present in the protocol. An attack can easily listen to an ARP request and send a reply to the requesting host before the real receiver responds. Normally the first reply will be used by hosts. 





**The LAND attack:** The attackers spoofs the source IP address of the packets to match the destination IP address. The attacker also sets the source and destination port numbers to be the same, causing the target system to believe that it is receiving packets from itself. As a result, some systems used to crash when they tried to respond to themselves.

**Teardrop attack:** When data is transmitted over the Internet, it is diveded into smaller units called IP packets. These packets can be fragmented into smaller pieces for efficient transmission. The receiving device reassembles these fragments to reconstruct the original data. However, in a teardrop attack, the attacker sends specially crafted IP fragments that overlap or have invalid offsets, causing the victim’s system to crash.



