1. Diffie-Hellman key exchange cannot identify the other party, All we know is that we share the secret with someone.

2. It is possible to send IP datagram longer than 65,535 bytes by using fragmentation

3. 



#### 1. Hash function properities

- computationally efficient
- same input always give same output
- Given a hash h, it should be infeasible to find any message m such that h = hash(m)
- collisoion resistance: infeasible to find two different inputs resulting in the same hash
- Any change in the input should result in a new unpredictable hash



#### 2. Many security protocols support sending messages without encryption (encryption=NULL) and still protect packets against modification. 

- The protocols use a cryptographic or keyed checksum (e.g. HMAC, short for hash-based Message Authentication Code) where a secret key is used together with the plaintext: $hash(secret key | plaintext)$.

- It requires the key to be known by both to verify and to create hashes.
- This protects the integrity of the message even if it is not encrypted.



#### 3. What fundamental mathematical property is Diffie-Hellman based on?

factorization of large prime numbers is hard. (the discrete logarithm problem)



#### 4. Encrypting traffic is not enough to guarantee freshness. Explain why not! Also mention two different ways to guarantee freshness!

- Encryption only ensure that the contents of the message remain confidential during the transmission but does not address the issue of freshness or prevent replay attacks.

- Timestamp, sequence numbers, nonces



#### 5. Even if we encrypt network traffic with the best cipher available, it is still possible to change the contents and also to replay the packets. How can this be solved?

1. We should use cryptographic hashes (such as HMAC) to protect the packet from modification

2. And add freshness guarantees, for example by using sequence numbers or timestamps.



#### 6. Some protocols create four or more keys from a Master secret, for example a Server write key, Client write key, Server MAC key and a Client MAC key. What is the purpose of all these keys?Why so many and not just one “encryption key”?

1. Client and Server write keys are used to encrypt messages.
2. Client and Server MAC keys are used to create secure hash (i.e. HMAC) to ensure the message integrity.
3. The use of multiple keys derived from a master key enhances security.



#### 7. What makes hash functions such as MD5, SHA-2, etc. fundamentally different from a CRC when protecting message integrity?

1. A message that is protected by a keyed hash cannot be modified without having access to the full input, i.e. the key and the message.
2. With a CRC, it is possible to change parts of the message and predict what to change in CRC without known the original message, even if the message is encrypted.



