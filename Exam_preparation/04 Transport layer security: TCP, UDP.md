#### 1. UDP traffic is in general harder to protect by a firewall than TCP traffic. Why?

1. TCP is a stateful protocol and it includes sequence numbers and a well-known three handshake for seesion setup. A firewall can check whether this procedure is followed.
2. However, UDP is a stateless and connectionless protocol, it has no setup procedure nor any sequence numbers, so the firewall has no way to know whether a datagram with a faked IP address legitimate or not but to pass it to the receiver unless it understands the application layer protocol.



#### 2. When performing a SYN scan against a system, it may be possible to detect this activity at the target computer by a user or by an administrator. How? 

1. Log monitoring
2. Intrusion Detection Systems (IDS)
3. Network monitoring tools

**And what can an attacker do to make it harder to detect the scan? Explain!**

1. Attackers can deliberately slow down their scanning rate to avoid triggering network monitoring systems.

2. Attackers can attempt to obfuscate their identity by spoofing the source IP address of the SYN packets. 



#### 3. UDP scanning is harder to do than TCP scanning. Why? What is the problem? 

1. UDP is a connectionless and stateless protocol, which means it does not establish a handshake or maintain a stateful connection like TCP.
2. It is hard to know whether a UDP message is accepted or sliently dropped.
3. If a UDP port is closed, the target may respond with a ICMP ‘port unreachable message’, however, this ICMP message is not guaranteed, as it depends on system’s configuration.

**How can operating systems, at least to some degree, protect themselves against leaking information about open UDP ports?**

1. Protection can be to limit the number of transmitted ICMP messages to, for example, one per second
2. 
