#### 1. Challenge response authentication, How does it work?

- The server generates a random challenge and sends it to the client.
- The client performs a calculation using the received challenge and the user’s password and sends the result back to the server, the calculation can involve cryptographic algorithms.
- Since the server knows the user’s password and performs the same calculation, then the server compares the two results, If the two matches, the authentication is successful.

**What is its main weakness if someone can listen to the communication?**

- since the attacker can see both the challenge and the cleartext, the attacker can do an exhaustive search of the password.
- The server need to store the password in cleartext.

#### 2. what is smart card? what does it contain and how it can be used for user authentication?

Smart card is a pocket-sized card that contains an embedded integrated circuit chip.

**how it can be used for user authentication:**

- When a user wants to authenticate themselves to a system, the system generates a random challenge and sends it to the smart card.
- The smart card performs cryptographic calculations using the challenge and info stored in the card (user credentials, cryptographic keys, certificates, personal information, and application-specific data), and generates a response.
- The response are then sends back to the system, the system verify the response

#### 3. Mention 4 functions or features Kerberos has.

- It provides SSO (Single sign-on) functionality, which means it allows the user to access multiple applications with a single set of credentials, instead of enter seperate username and password for each application.
- It offers both authentication and authorization.
- It is highly scalable 
- Kerberos has two types of tickets: TGT - Ticket Granting Ticket, SGT - Service Granting Tickets
- Cross-realm trust is possible

#### 4. Kerberos is a protocol performing both authentication and authorization. It has some advantages and at least one disadvantage:

 1: it uses symmetric keys;

 2: the tickets handed over to the clients contains its internal state;

 3: however, it requires applications to be Kerberized.

**Explain these concepts and what the advantages and disadvantage mean!**

1. Symmetric keys are easier to work with than asymmetric keys and eliminates complicated calculations.
2. This makes servers stateless and many servers can share the workload without consulting each other or a common database.
3. Application servers must understand the ticket concept and how they should be used.



#### 5. The Kerberos server is stateless which means that it does not keep track of the users it has authenticated. It is still possible for a user to come back to it and request tickets to services without repeating the authentication process. How is this possible?

When a user initially authenticates with the kerberos server, the server generates a TGT (Ticket Granting Ticket) for the user, the TGT is a long-lived ticket that is used to obtain SGT (Service Granting Ticket) without re-authenticating for a certain period of time. 

The TGT contains the user’s indetity,  timestamp, and is encrypted with the user’s long-term key and password, It is encrypted by the server and cannot be decrypted by anyone else.
