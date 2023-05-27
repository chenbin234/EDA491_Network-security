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

#### 6. Many protocols such as WEP, WPA and WPA2 use an IV (initialization vector). Why? Explain how it is used!

- The IV makes sure that two identical packages are encrypted differently.
- This is done with the IV + key as input to the pseudo random generator (each IV creates a different stream which is XOR with the plaintext)

#### 7. The 802.11i framework (WPA2) offers substantially better security than WEP. Mention three improvements in this protocol!

- AES instead of RC4 encryption
- Session key introduced
- When all IVs are used new session keys are negotiated
- Passwords are hashed 4096 times to make it harder to do offline searches
- Secrets not used directly.

#### 8. Support 802.1x authentication with a radius server, what does that mean?

1. 802.1x is port based authentication, where a client does not get access to the network unless authenticated and authorized.
2. Instead of using a shared key, Users can be authenticated through the radius server using individual secret or token cards such as SecureID.

#### 9. WPA3 guarantees that all session keys are unique for the session and that they are not in any way related to other session keys. However, WPA2 does not have this property. What is this property called? Why is this a good property?

1. The property is called perfect forward secrecy. In a perfect forward secrecy, a compromised session key should not affect other sessions in the past or future. 

2. Therefore, all session have a unique session key.

**Explain how this is normally achieved?**

This is normally achieved by using Diffie-Hellman key agreement to make session keys unique and never reused.

**what “mistake” WPA2 does?**

WPA2 calculates session keys from the master key which is derived from SSID+Password/shared secret (and by an attacker some known random values). If the password is revealed, session keys for all other sessions can be recalculated.



#### 10. The use of shared keys in for example WLAN authentication is both good and bad. Give one advantage and one disadvantage with using it.

Advantage: 

- shared keys are easy to implement,
- They involves a pre-shared keys that is known by both access point and the client devices
- It is convenient for small-scale deployment and home networks

Disadvantage: 

- lack of scalability and flexibility
- Since the same shared key is among all authorized devices, it is hard to revoke access for specific users
- If a key is compromised and needs to be changed, it requires updating the key on all devices
- Also, when different level of access is needed, pre shared keys can not support.



#### 10. WEP has at least one problem with its handling of IVs. Explain how an attacker may use this weakness! Is this problem likely to occur?

1. WEP allows an IV to be reused. then we will have two packets encrypted with the same key stream.
2. This means that an XOR operation between the cipher texts will be the same with an XOR between clear texts.
3. $c1 \bigoplus c2 = (p1 \bigoplus b) \bigoplus (p2 \bigoplus b) = p1 \bigoplus p2$

4. Since the IV is only a 24-bit value, a busy AP is very likely to reuse IVs.



#### 11. Both WEP and WPA2 uses IVs when encrypting data packets. Why? What would happen if there were no IVs present in the packets?

1. The IVs guarantees that different key streams are created for each packet.
2. Without IVs, the same key streams would always be used, thus XORing two ciphertext would the same as XORing these two cleartext.
3. Also, identifical dtagrams would always have the same crypto text.



#### 12. The first message in WEP is the 128-byte random challenge that authenticates the client. Why is this mechanism flawed?

1. It uses the same method for encryption as is used later for packet encryption.
2. An attacker listening to the authentication procedure can see both the challenge and the encrypted challenge. By XORing them with each other, the 128-Byte ksy stream is obtained which can be used to transmitted own message through the AP.



#### 13. Explain how encryption of data traffic is done in WEP! A figure together with explaining text is needed. You need to show how encryption is done including input and output to the system.

??



#### 14. WEP is not known for its good security. Describe two vulnerabilities or possible attacks against it!

1. Same key for authentication and encryption
2. All session and devices use the same key
3. CRC, not HMAC, with stream cipher allows modification
4. RC4 with weak keys. After collecting enough traffic, key search is possible.
5. No nonces, no sequence numbers, replay attack is possible
6. Too short IV space, reused IVs can be used to decrypt data
7. one known plaintext/ciphertext reveals key stream for IV which can be used forever to transmitted data.







