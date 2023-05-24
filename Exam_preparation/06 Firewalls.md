### 1. Static packet filter

- SYN-scans should not reveal the hidden services.
- Invalid IP packets with expiring TTLS should not be forward.



### 2. Dynamic packet filter

- Protect server against SYN flood attacks coming from one and the same IP address.



### 3. Deep-packet inspection firewall

- Replayed TCP segments should not reach the server.
- DNS requests from the web server and only corresponding replies should be allowed
- ACK and FIN scans should not reveal the hidden services



### 4. Circuit-level gateway

- Hides the real IP address of the sever and protects the server against scanning attacks



### 5. Air-gap firewall





### 6. None of the firewalls

- Inspect web page requests sent to the server.









