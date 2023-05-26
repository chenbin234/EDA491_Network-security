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



#### 4. In the picture above, we can see an attack against a Radius server. What is the purpose of this attack? What is it the attacker tries to do? Explain! (20210531 Q2)

The only unknown in the request to the raduis server is the “shared_secret” and it may be possible to do an exhaustive search to find the shared_secret.

#### 5. Can a rainbow table be of help to the attacker in the example above? 

It is not useful since the hash (MD5) contains random data, it is infeasible to create pre-calculated tables for a random data.



#### 6. Performing password authentication over networks is always problematic. Instead of sending a password in clear-text, challenge response authentication is a better method. How does it work? What is its main weakness?

Passwords can not be sent in cleartext over the network (sniffed, replayed), One solution is to use challenges that the client encrypts and send back to the server which can verify that the client is in possession of the password.

A major weakness is  that an attacker can see both the challenge and the cleartext and may do an exhaustive search of the password.

Another weakness is that the server needs to store the passwords in cleartext.

