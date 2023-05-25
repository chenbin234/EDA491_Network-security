## 1. Radius







**MD5** is a cryptographic hash function that takes the message as input of any length and changed it into a fixed-length message of 16 bytes.





## 2. what are the most important fields in a certificate used for authentication ?

Subject, issuer, subject’s public key, signature of the issuer, validity/expiration date.





## 3. Diffie-Hellman

- Diffie-Hellman provides a secure method for two parties to establish a shared secret key over a insecure channel.
- It is based on that factorization of large numbers is very hard.

**How does it work?**

1. Both parties agree on and publicly share a prime number (p) and a base number (g)
2. Each party generate their own private key, let’s say Party A generates ‘a’, Party B generates ‘b’, the private key are kept secret.
3. Each party calculates their public key and sends to the other party, Party A calculates (g^a) mod p, Party B calculates (g^b) mod p.
4. Since the exponentiation operation is commutative, the shared secret key can now be calculated, Party A calculates (B public key ^ a) mod p, Party B calculates (A public key ^ b) mod p

**Weakness?**

- Diffie-Hellman is valnerable to certain attacks, such as Man-In-The-Middle attack.
- An attacker can intercept and modify the public key exchanged between two parties.
- To address this, additional security methods can be combined such as digital signature and certificate authorities, to ensure the integrity of the exchanged public keys.



