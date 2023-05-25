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





