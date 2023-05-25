#### 1. IPsec

- support perfect forward secrecy
- Transparent to ICMP and transport layer protocols
- Protect application from duplicated messages



#### 2. TLS

- support perfect forward secrecy

- Protect application from dropped messages
- Suitable to build into own application
- Use TCP for transport
- Protects applications from duplicated messages



#### 3. SSH

- support perfect forward secrecy
- Protect application from dropped messages
- Use TCP for transport
- Protects applications from duplicated messages



#### 4. What is SSH, what functionality does it offer that TLS does not have?

SSH is a network protocol that provides a secure remote terminal access, allowing users to log in to a remote system and execute commands over a insecure channel.

This feature is not directly available in TLS, which primarily focuses on secure data transport.

SSH supports port forwarding, which enables secure tunneling of network connections over SSH connections, TLS does not support built-in port forwarding.

- SSH is primarily used for secure remote administration and file transfer, while TLS is commonly used for securing web browsing, email communication, and other client-server interaction.



#### 5. What is the similarity between SSH and TLS?

1. SSH and TLS share similaries in terms of encryption (AES) , authentication (RSA), data integrity (MAC)

2. Both include secure key exchange mechanism to establish a secure shared key between communicating parties (Diffie-Hellman)

3. They both introduce sequence numbers to protect against reply attack



#### 6. Mention one advantage with using TLS instead of SSH in an application

- the use of certificates that allows for example web browser to verify a server’s identity without prior sharing of a host key as in SSH.
- TLS is built-in to the applications whereas SSH is a standalone program.
