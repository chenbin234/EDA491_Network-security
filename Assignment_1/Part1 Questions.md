### Q1: Why are higher port numbers (> 1024) still of interest for, e.g., hackers or penetration testers?

There are a number of common networking ports that are used frequently. Ports 0 through 1023 are defined as well-known ports. Registered ports are from 1024 to 49151. The remainder of the ports from 49152 to 65535 can be used dynamically by applications. A brief description of these are as follows:

-   Port 20 and 21: FTP data and FTP control, respectively
    
-   Port 22: Remote login protocol secure shell (SSH)
    
-   Port 23: Telnet, used for accessing system remotely but is not very secure
    
-   Port 25: Simple Mail Transfer Protocol (SMTP) used by e-mail servers
    
-   Port 53: DNS protocol
    
-   Port 80: Used for accessing Web servers
    
-   Port 110: The POP service or Post Office Protocol used by local e-mail clients to retrieve mail from servers
    
-   Port 123: NTP to synchronize time with remote time servers
    
-   Port 143: E-mail clients can use the Internet Message Access Protocol (IMAP) to retrieve mail from servers
    
-   Port 443: This is the Hypertext Transfer Protocol (HTTP) Secure that combines the HTTP with a cryptographic protocol, which can be used for payment transactions and other secure transmission of data from Web pages.
    
-   Port 631: The Internet Printing Protocol (IPP) used to print to printers located remotely on the network
    
-   Port 3306: The standard port for MySQL
    

These ports are defined in the /etc/services file on Linux systems.

1. While commonly used services like HTTP, SSH, FTP, and DNS often use well-known port numbers, other less common services may use higher port numbers. These services can be vulnerable to various exploits, and attackers can use nmap to identify such services.

2. Misconfigured firewalls or security policies may allow traffic on high port numbers, making them a potential attack vector for hackers. Nmap can be used to identify these open ports and use them to exploit vulnerabilities in the target system.

3. By scanning higher port numbers, attackers can gain a better understanding of the network topology and identify potential targets for further attacks.

### Q2: Look at the resulting packets with Wireshark. What is sent and received? How are the different scans done (what is being sent)? Do the scanned systems behave differently? Why?

1. SYN - This technique is often referred to as half-open scanning, because you don't open a full TCP connection. You send a SYN packet, as if you are going to open a real connection and then wait for a response. 
   - **A SYN/ACK** indicates the port is listening (open), 
   - **A RST (reset)** is indicative of a non-listener.
   - If no response is received after several retransmissions, the port is marked as filtered.
2. ACK - **(decide filtered? not filtered?)** The ACK scan probe packet has only the **ACK flag set,**
   - When scanning unfiltered systems, `open` and `closed` ports will both return a RST packet. Nmap then labels them as `unfiltered`, meaning that they are reachable by the ACK packet, but **whether they are `open` or `closed` is undetermined**. 
   - Ports that don't respond, or send certain ICMP error messages back (type 3, code 0, 1, 2, 3, 9, 10, or 13), are labeled `filtered`.
3. FIN - FIN flag set, 
   - when it is sent to a closed port, the target system should respond with a TCP RST packet indicating that the port is closed.
   - However, if the port is open, the target system may simply ignore the FIN packet and not send any response. Therefore, by analyzing the response (or lack thereof) to a series of FIN packets sent to different ports, a TCP FIN scan can identify which ports are open on a target system.

### Q3: Some scans take a long time to complete. Why?! Look at the responses from the system and try to explain! (The answer has been mentioned during a lecture.)

TCP FIN scanning-target with firewall take 22.2 seconds, 

Nmap scans may trigger security alerts or be blocked altogether. This can cause delays or timeouts in the scan.



### Q4: Nmap can report ports to be in different states. What do the states ”open”, ”closed”, ”filtered” and ”unfiltered” mean? Read the manual page and documentation! Which are the most/least interesting ones? Run a scan against the target systems and try to find examples of all these types of ports. Look at the responses from the system. Can you match the replies with the different states?

1. **Open**: means that an application on the target machine is listening for connections/packets on that port.
2. **Closed**: `Closed` ports have no application listening on them, though they could open up at any time.
3. **Filtered**: means that a firewall, filter, or other network obstacle is blocking the port so that Nmap cannot tell whether it is `open` or `closed`.
4. **unfiltered**: Ports are classified as `unfiltered` when they are responsive to Nmap's probes, but Nmap cannot determine whether they are open or closed.
5. **open|filtered**: cannot determine which of the two states describe a port
   - For example, the port may be protected by a firewall or an intrusion detection system (IDS) that is configured to drop or ignore certain types of packets. Alternatively, the port may be open, but the target system is configured to send no response, making it difficult for Nmap to determine the state with certainty.
6. **closed|filtered**: cannot determine which of the two states describe a port
   - This can happen if the target system is behind a firewall that is configured to block or drop packets sent to closed ports. In this case, Nmap may be able to determine that the port is closed based on the lack of response from the target system, but it cannot determine whether the packets were dropped by a filter or whether the port is truly closed.



**most interesting ones**: open|filtered, closed|filtered

**least interesting one**: closed

