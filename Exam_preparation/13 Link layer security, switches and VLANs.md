#### 1. How can an attacker see private traffic between two other communicating parties in a switch? 

The attacker may overflow switch memory and make it broadcast all packets to all ports. 

An attacker may spoof other host’s MAC addresses to disturb the functionality of a self-learning switch and force it into a broadcast mode of all packets

**what could an administrator do to decrease this problem?**

- Limit number of MAC addresses per port
- lock some MAC addresses to certain ports

#### 2. DHCP spoofing

An attacker may answer to DHCP requests in order to become a man in the middle.

**How it can be dealt with by a switch?**

Identify and configure the switch port that are connected to the DHCP server as trusted ports, configure the switch only allows these ports to answer DHCP.

#### 3. ARP cache spoofing, Why would the attacker do so?

Goal can be to become a man in the middle.

**Possible solutions to this problem?**

- create smaller subnets
- accept only the first reply
- Secure ARP (S-ARP)

#### 4. There are two main ways VLAN can be used in: with or without tags. What is VLAN and a tag? Explain the difference between with and without tags.

1. VLAN stands for Virtual Local Area Network. It is a technology used to logically segment a single physical network into multiple virtual networks, allowing different group of devices to be isolated as if they were on seperate physical networks.
2. A tag is an additional identifier inserted into the header of an ethernet frame to indicate to which the frame belongs.
3. **VLAN with Tags** allows switches to identify and route the frame to the correct VLANs accross switches.
4. **VLAN without Tags** assigns ports directly to specific VLANs, devices are unaware of VLAN membership, communication between devices within the same untagged VLAN is transparent.

#### 5. Is VLAN a good and secure technology? Mention one attack that it cannot protest against!

1. VLAN is a valuable technology for networking segmentation and traffic management, but it is not inherently secure against all types of attacks.
2. It is vulnerable against MITM attacks
3. Layer 2 MAC flooding attack - The attacker floods the switch with a large number of fake MAC address, overwhelming the switch’s MAC address table and causing it to behave like a hub, broadcasting frames to all ports.

#### 6. On a local network, it may be possible for an attacker to pretend having lots of MAC addresses to confuse more intelligent switches. Why? What could be the reason an attacker performs this action?

1. More intelligent switches can learn where hosts (MAC addresses) are located and will not normally forward private traffic between two ports to any other ports.

2. The attacker’s goal is to overflow the switch memory with garbage MAC address to make it forget the real MAC address and force it to broadcast all traffic to all ports.
3. This enables the attacker the listen to all ongoing conversations.



#### 7. An attacker on a local network may be able to redirect traffic from other hosts to his/her own computer. Give two examples of how such attacks can be done!

- It is possible to fake ARP packets with other hosts IP addresses.
- Another possibility is to send false replies to DHCP requests to become the default route for systems.



#### 8. What is the main difference between using VLAN technology and IPsec to secure a network? Would you use VLAN to create a virtual course lab at Chalmers with lab computers at different locations in the EDIT building? 

- VLAN does not encrypt nor protect the message against modification. But it may be a good solution to seperate the course lab traffic from other types of traffic.
- VLAN can be used to make sure that the traffic from the lab will not be forwarded to other office computers and servers but still sharing the same physical network.



#### 9. Describe 3 different security mechanisms which maybe found in switches, and what they protect against?

1. **MAC address flooding protection:** limit number of addresses per port
2. **DHCP spoofing** : trusted ports
3. **Block traffic between clients:**  
4. **802.1x port-based access control:**
5. **lock MAC addresses to ports:**
6. **functionality to detect IP address spoofing (MAC-IP address monitoring)**



#### 10. Some more advanced switches may have more “intelligent” functionality than a plain dumb €10 switch and can prevent some link layer attacks. VLAN technology can be one such functionality, but describe two other possible functions they can have and explain what attacks they protect against!

1. Limit number of MAC addresses per port - protects against MAC address flooding which may force a switch to broadcast all packets to all ports.
2. Trusted port - limit what ports are allowed to answer, for example, DHCP requests.
3. Lock MAC addresses to ports
4. Functionality to detect IP address spoofing (MAC-IP monitoring)



