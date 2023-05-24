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

