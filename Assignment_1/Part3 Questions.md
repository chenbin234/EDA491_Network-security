### Q6: How is UDP scanning done by Nmap? Why is this type of scan more problematic than TCP scans?

UDP is a connectionless protocol, which means that there is no handshake process to establish a connection between the client and server before data is sent. Instead, the client simply sends a datagram to the server and waits for a response.

Nmap uses different UDP probes for different protocols, such as DNS, SNMP, DHCP, TFTP, to detect open UDP ports. For example, to scan for open DNS servers, Nmap sends a DNS query to the target machine and checks for a response. If a response is received, it means that the port is open and a DNS server is running on that port.



Problem:

- UDP scanning can **take longer** than TCP scanning because there is no reliable way to determine if a UDP packet has been received by the target machine. This means that Nmap may need to send multiple probes to each port to ensure that a response is not missed.
- **Many network firewalls and intrusion detection systems (IDS) are designed to block UDP traffic.** This can make it difficult for Nmap to scan for open UDP ports, as the probes may be dropped by these security devices.
- UDP scanning can be more difficult to interpret than TCP scanning because **UDP packets can be lost or dropped without any notification.** This means that Nmap may report a port as closed or filtered when it is actually open, or vice versa.

### Q7: How much time does it take to perform a UDP scan on the systems? Is there a difference between the systems in their responses? Explain!

- UDP scanning-target without firewall - 2409s

- UDP scanning-target with firewall - 9.99s

- UDP host virtual interface 10.0.2.2 - 15.92s

- UDP host physical interface 10.0.23.85 - 201s

  

