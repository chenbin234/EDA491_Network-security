#### 1. What protocol would you select when building a VPN system between two sites? Motivate your answer!

1. I would select IPsec protocol. tunnel mode.

2. Because IPsec is a robust and widely used protocol designed for secure communication, It provides strong authentication and encryption algorithms to ensure the confidentiality, integrity of data transmission.

3. IPsec tunnel mode is commonly used for site-to-site VPN connections, it offers site-to-site encryption.



#### 2. IPsec has sequence numbers. Why?

To make sure duplicates are not delivered



#### 3. What protocol would you select when building a VPN system for remote users who need to access various services inside an office? TLS, SSH or IPsec? There may be several acceptable solutions to this question.

TLS or SSH, easy to configure, client can run as an application without administrative privileges.



#### 4. IPsec can operate in both Tunnel and Transport mode. In Tunnel mode, a new IP header has to be inserted. Why? Also, the new address is not protected by the MAC. Why is this not needed?

- The purpose of IPsec tunnel is to create a secure tunnel between two sites, the original packet is encrypted to protect its networking address scheme and route info. The new IP header contains the source and destination address of VPN end-points, to make sure intermediate routers can properly route the packet to destination.
- The new address is not protected by MAC, since it is not sensitive info, even if the attacker can modify the IP address, the message inside cannot be read.
