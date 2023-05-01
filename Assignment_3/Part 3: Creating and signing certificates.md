# Part 3: Creating and signing certificates

### Q15: What are the implications of making the CA’s private key public?





### Q16: Why would you encourage public sharing of the CA’s certificate when the private key must be kept secret?



### Q17: What is verified when using the openssl library when a TLS connection is being established? (Hint: It checks five related things, provide at least three.)



### Q18: Compare the output to the unsigned request you saved earlier. In what ways do the outputs differ?





### Q19: Consider the following scenario: You need to buy something and you search the web for more information. After a while you find a small and unknown (at least to you) web-shop which has the lowest price. What a great price, you think! You also see that they have an https connection, and the little lock in your browser is closed (i.e., the server certificate is validated, with a signature by some CA). When you are about to enter your credit card details, you ask yourself...

1. Does the CA’s signature imply that you can trust the person who holds the server certificate (the web shop)?
2. Can you trust the server that holds the certificate? For instance, do you believe the information you enter will be kept secure?

