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

