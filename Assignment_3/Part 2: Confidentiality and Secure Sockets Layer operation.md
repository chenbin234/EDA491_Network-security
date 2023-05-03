# Part 2: Confidentiality using TLS

You will now investigate how TLS ensures confidentiality by studying the handshake procedure. There is a tool for debugging SSL/TLS connections which has many useful options: s_client, a sub-command of openssl. By using the appropriate options and flags, you will be able to answer the questions.

### Q5: What is the reason the verification failed?

```shell
openssl s_client -connect localhost:443 -tls1_2
```

**Reason: unable to verify the first certificate**

![Q5_1](images/Q5_1.png)

### Q6: Once theoden’s identity is correctly verified, the printout should differ slightly: What did you do, and why did this solve the problem?

```shell
# using the right root certificate to verify the server's certificate

openssl s_client -CAfile /home/eda491/netsec-lab3/netsec-ca.pem -connect 127.0.0.1:443 -tls1_2
```

![Q6_1](images/Q6_1.png)

![Q6_2](images/Q6_2.png)

![Q6_3](images/Q6_3.png)



### Q7: What algorithms are used for key exchange, authentication of server, application message encryption, MAC calculation?

![Q7_1](images/Q7_1.png)

```shell
TLSv1.2, Cipher is ECDHE-RSA-AES256-GCM-SHA384
```

“Cipher is ECDHE-RSA-AES256-GCM-SHA384" refers to the cipher suite used for the connection. A cipher suite is a set of cryptographic algorithms used to secure the communication. In this case, the cipher suite consists of the following components:

- ECDHE (Elliptic Curve Diffie-Hellman Ephemeral): A key exchange algorithm that allows the client and server to generate a shared secret without revealing their private keys. Ephemeral means that a new key is generated for each connection, which provides perfect forward secrecy, preventing the decryption of previously captured traffic.
- RSA (Rivest–Shamir–Adleman): A widely used public-key encryption algorithm, used in this case for server authentication.
- AES256 (Advanced Encryption Standard with a 256-bit key): A symmetric block cipher that uses a 256-bit key size to provide strong encryption of data.
- GCM (Galois/Counter Mode): A mode of operation for symmetric encryption that provides both confidentiality and authenticity of data.
- SHA384 (Secure Hash Algorithm with a 384-bit hash): A cryptographic hash function used to verify data integrity by generating a fixed-length hash value that can be used to ensure that data has not been altered during transmission.

| key exchange                       | Elliptic Curve Diffie-Hellman Ephemeral  (ECDHE) |
| ---------------------------------- | ------------------------------------------------ |
| **authentication of server**       | **RSA**                                          |
| **application message encryption** | **AES256**                                       |
| **MAC calculation**                | **SHA384**                                       |

###  Q8: RSA with a sufficient keylength is a strong cipher. Why is RSA not used to encrypt application messages?

Because RSA encryption is relatively slow and need more computation resource compared to symmetric encryption algorithms such as AES.

### Q9: At this point you should have an established connection: is there anything strange about the TLS output? (Hint: Do not waste too much time here, ask a TA if you do not find anything after a minute or two.)

```shell
openssl s_server -accept 40123 -cert theoden2015.crt -key theoden2015.key

openssl s_client -tls1_2 -connect localhost:40123 -CAfile /home/eda491/netsec-lab3/cahome/cacert.pem
```

Certificate has expired.

![Q9_1](images/Q9_1.png)

![Q9_2](images/Q9_2.png)

### Q10: Was the string transmitted successfully? Did you expect this to work? Why or why not?

Yes, the string was transmitted successfully.

I didn’t expect this to work, since the certificate has expired, it should not work for the sake of security.

#### sender

​	![Q10_1_send](images/Q10_1_send.png)

#### receiver![Q10_2_receive](images/Q10_2_receive.png)



### Q11: Identify the different TLS messages in Wireshark: which messages are sent? Illustrate your answer with a diagram.





### Q12: Which ciphers are proposed by your client. Where can we find this information?





### Q13: Which cipher is selected by the server? Why is it selected? Where can we find this information?






### Q14: Which TLS message do you think contains the string “TESTMESSAGE”?





