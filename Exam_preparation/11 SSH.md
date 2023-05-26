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



#### 7. SSH uses a (keyed) MAC which is calculated from the plaintext data to protect against modification. What is the drawback/danger of using with this method?

1. It means that the receiver must decrypt the packet before the MAC can be checked.

2. This is the **“Encrypt-and-MAC”** method which may cause additional work for a receiver if garbage packages are sent to it.
3. It can also be dangerous if the receiver has to process data packets before it knows they are authentic and correct.

**What other two alternatives to the SSH method above exist? What are the pros and cons of these?**

1. “MAC-then-Encrypt”, the same problem as in SSH
2. “Encrypt-then-MAC”, It latter offers ciphertext integrity but no plaintext integrity but should not really be a problem.

