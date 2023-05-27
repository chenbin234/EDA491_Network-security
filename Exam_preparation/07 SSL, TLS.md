**A master key** is derived from key negotiation process during the connection setup. It is then used to create session keys which are used for data encryption, etc, keys that are changed regularly.

### 1. TLS

- $ver_{c}$ is the highest TLS version the client support, $ver$ is what the server decides to use.
- $r_{1}$ and $r_{2}$ are random numbers later used in key generation.
- $sid$ is session id, a number identifying the session.
- $ciphers$ is a list of algorithms the client supports (for encryption, MAC and authentication), $cipher$ is the cipher the server decides to use.
- $comps$ is a list of compression algorithm the client supports, $comp$ is what the server decides to use.

### 2. A pseudo-random function used in TLS

It is used to expand short secrets to longer blocks, for example to generate the master key from the pre_master_secret or to generate crypto-keys from the master secret:

$master\_secret = PRF(pre\_master\_secret,\ 'master\ secret',\ r_{c} || r_{s})$

### 3. Why do we often see nonces in security protocols?

To guarantee freshness and prevent replays of old sessions

### 4. Why do we (sometimes) see time stamps in security protocols?

Also to guarantee freshness and prevent replays of older sessions.



#### 5. How is freshness of data packets guaranteed by the TLS record layer protocol? There are no sequence numbers in the header.

It uses implicit sequence numbers, i.e. both sides counts numbers of packets and this counter is included when calculate MAC. This ensures that replays are not possible.



#### 6. A certificate can be used to identify a web server when using SSL/TLS. Describe what happens if an attacker tries to impersonate the server (for example for mybank.com) by faking the DNS reply, which causes the client to connect to the attacker’s computer/IP address instead of to the correct server?

It can lead to a potential security known as “Man-In-The-Middle” attack.

1. The attacker intercepts the DNS query made by the client, in this case “my bank.com”
2. The attacker response to the DNS query with a fake DNS reply, directing the client to connect to their own computer.
3. The client initiate the TLS handshake with the attacker’s server, the handshake involves exchanging cryptographic keys and verify the server’s identity.
4. The attacker’s server sends a fake certificate, claims to be the legitimate server for ‘my bank.com’.
5. The client will verify if the certificate is signed by a trusted certificate authority (CA) and if the domain name matches the one he intends to connect to.
   - if the attacker managed to obtain a fraudulent certificate signed by a trusted CA, then the certificate may pass the verfication process.
   - If the server authentication fails, the web browser displays a warning message.
6. The client establishes a encrypted connection with the attacker’s server. the attacker can now read and modify the data tramsmitted between the client and server whereas the client may do not know about that.



#### 7. A well-known problem in many security protocols is that an attacker in a short time can request lots of sessions with faked IP addresses and force a server to constantly calculate new session keys that are never used. IKE has protection against this. Explain how it works.

- In IKE, The server stores the IP address and port numbers in a cookie which must be returned by the client before it starts calculating any keys. This makes sure the receiver has not faked the IP address.

- The cookie is calculated by : hash(IP address, port numbers, secret).
- A client that requests lots of sessions from the same IP address can be blocked temporarily.



#### 8. SSL/TLS has a “close session” message which is used when they want to quit. Why is it needed? Why not just tear down the TCP connection instead? TCP already has a mechanism to close connections. 

To prevent truncation attacks. 

We don’t want an attacker (for example a MITM) to be able to prematurely terminate a connection between the client and the server by faking a FIN in each direction. This could result in both sides believing that all data has been sent and received.



#### 9.SSL/TLS has both master and session keys. What is the difference? How are they related? When are they created?

- The master key is derived from key negotiation process during connection setup, it is used to create session keys.
- Session keys are used for data encryption and creating MACs, session keys are changed regularly.



#### 10. IPsec has a field “Next Header” as shown on the last page, which tells what upper layer protocol should receive the datagram. IP has a field called “Protocol” with the same purpose. Why does IPsec not use that field?

When IPsec encrypts a datagram, it replaces the receiving upper layer protocol in IP with its own number and place the original content in its Next Header field.

This means that the receiver in the other end will be IPsec, and when it decrypts the datagram it can restore the original received field in IP datagram.



#### 11. Padding is an option present in many security protocols and can be used to make all datagrams of the same size (or of random size). Is this really needed? Give an example of when the absence of padding could be useful for an attacker!

Padding can help prevent attackers from deducing information about the plaintext message by analyzing the length or patterns in the ciphertext.

1. Access to a web server could reveal what pages the user is accessing by observing the amount of data being transferred.
2. Another example was in WEP where it was possible to identify ARP messages which could be exploited to inject own messages.



#### 12. In the latest version of TLS, session establishment is faster due to the introduction of one- round-trip-time negotiation. Why is this faster? How is this possible?

Each round trip takes time and introduce a delay.

It is achieved by letting the client guess what cipher suites the server accepts and what will be used. If the guess is correct, the negotiation can skip one step.



#### 13. TLS consists of several protocols. Describe the functionality of the record layer, change cipher and handshake protocols (see picture on the last page).

1. Record layer protocol performs fragmentation -> compression -> adding MAC -> encryption
1. Change cipher protocol tell the other side to change to change to the last security parameters negotiated.
1. The alert protocol sends warning s and error messages to the other side.
1. The handshake protocol negotiates ciphers, keys and performs authentication.
