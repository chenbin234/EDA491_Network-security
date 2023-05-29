#### 1. Security protocols have some common properties:

- Negotiate algorithms and ciphers to use
- Always derive new key material
- Only use private keys for authentication - enforce perfect forward secrecy
- change keys regularly



#### 2. IPsec

- Transport Mode
  - offers end-to-end encryption
  - Often used for remote access
  - Drawback: End-devices must implement IPsec
- Tunnel Mode
  - offers site-to-site encryption
  - Used to implement VPN

**IPsec protocols**

- Authentication Header (AH)
  - support data integrity
  - Uses HMAC to verify integrity
  - Does not encrypt messages
- Encapsulating Security Payload (**ESP**)
  - support data integrity and message confidentiality
  - ESP in transport mode and tunnel mode
  - The ESP package:
    - SPI tells under what SA (security association) a received packet should be processed
    - SA is an array with connection-related info
    - Selectors determines what SA an outgoing packet belongs to
    - 
- IKE (Internet Key Exchange)
  - two-way authentication of peers
  - negotiates security algorithm 
  - handles exchange of session keys



#### 3. Different Dos attacks

- Bandwidth exhaustion : Reflection, flooding and magnification attacks (Smurf and Fragile)
- Resource exhaustion : SYN flooding
- Trigger implementation bugs: Ping-of-death, Teardrop

**What is Fraggle attack?**

The attacker sends a large number of spoofed UDP packets or ICMP  to the broadcast address of a network to overload a victim’s network resources.

**what is DNS magnification attacks?**

Send DNS request with faked victim addresses, some DNS server can reply lots of info.

**What is memcached attack?**

1. Memcached servers are used to cache database queries and replies

2. The. attacker exploits misconfigured memcached servers that have UDP enabled, then sends a small request spoof with the source IP address of the victim, to overwhelm the victim’s systems.



#### 4. RST attack

1. The attacker sends a spoofed TCP RST packets to one or both endpoints of an established TCP connection

2. These RST packets contain the appropriate sequence and acknowledge numbers, making them appear as legitimate packets.
3. When the receiver check the spoofed packets,  it interprets it as a request to terminate the connection and immediately closes the connection.



#### 5. kerberos

