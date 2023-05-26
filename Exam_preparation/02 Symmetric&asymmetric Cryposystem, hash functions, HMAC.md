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



