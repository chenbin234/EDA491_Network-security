#### 1. WEP, the listener gets access to both the cleartext and the ciphertext. it is possible for the attacker to search for the password, another problem?

The attacker can see both the challenge and the ciphertext encrypted with the secret (password). This makes it possible to extract the keystream using the an XOR operation: $c1 = p1 \bigoplus stream$.

And since the same algorithm is used for data transmission, this 128-byte key stream can be used to transmit arbitrary data.

Unfortunately, WEP uses the same algorithm for authentication and packet encryption and IVs can be reused.

#### 2. WEP uses CRC to check packet integrity. why it is not sufficient?

With a CRC function, it is possible to calculate exactly what bit in the checksum need to be changed when a bit is changed in the input (however, a hash requires a complete recalculation). It doesn’t matter whether the data or CRC is encrypted.

#### 3. WAP2-EAP(i.e. Radius)

1. Raduis is a protocol for user authentication supporting AAA (authentication, authorization and accounting).

2. Three parties are involved: the client, the application server and the Radius server.

3. **Authentication:** Typically, the client attempts to access to the application server, the application server receives the connection request and forwards the authentication info to the Raduis server. It is the Radius server to verify the user’s credentials usually through a database, this may involve checking username, passwords, or other authentication factors.

4. **Authorization:** if the user is successfully authenticated, the Radius servers sends an authorization response to the application, this response contains the necessary permissions and access control information for the user.

5. **Accounting:** During the user’s session, the Radius server can also collect accounting info, such as the duration of the session, the amount of the data transferred or other details.

#### 4.  TKIP

TKIP makes sure encryption keys change over time. It extends the IV (with a new field EIV), It makes sure each station uses a unique key by involving the MAC address in key calculation. It also makes sure each packet has a unique sequence number and that the key is changed every 10,000 packets or normally every hour.

#### 5. Port-based authentication 

1. port-based authentication is a link-level mechanism where a client does not get access to the network  unless authenticated and authorized. 
2. It uses Radius for central authentication and authorization. after user authentication, the port is opened and all traffic is allowed from this port.

