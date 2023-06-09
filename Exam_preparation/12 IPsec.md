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



#### 5. IPsec uses packet numbering, see the picture. For what purpose?

It protects against replay attacks by discarding duplicates, but unlike TCP, it allows packets to be missing.



#### 6. The ESP header differs depending on what mode is used (see header on last page). Why is it possible to keep the original header in transport mode but not in tunnel mode?

In tunnel mode, it is not the final receiver of the datagram that should receive the encrypted datagram but a IPsec gateway that decrypts it and forwards it to its final destination.

Tunnel mode is often used for site-to-site encryption. it is to create a secure tunnel between two IPsec gateways.



#### 7. On the last page, there is a picture of an IPsec header. Explain what the next header, SPI and padding fields are used for and what purposes they have!

**The SPI** is an index that tells what SA (security association) should be used, i.e. a pointer to a data structure containing info about the type of connection, keys used, etc.

**Next header** tells what upper layer protocol should receive this data.

**Padding**: to disguise to an attacker the actual amount of data being transmitted.



#### 8. In the course, we discussed three different ways to add MACs: MAC-then-encrypt, Encrypt-and-MAC and Encrypt-then-MAC, see the picture below. There are some pros and cons with each solution. IPsec uses the last method (Encrypt-then- MAC). Give an argument for or against Encrypt-then-MAC when compared to the other. Motivate clearly why this is (or is not) advantageous!

- Encrypt-then-MAc makes it possible to check the integrity of the datagram before sending it for decryption.

- It both saves processing time but also prevents attacks against the crypto-engine with specially crafted datagram.

