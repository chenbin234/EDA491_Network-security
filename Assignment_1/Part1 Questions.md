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





### Q3: Some scans take a long time to complete. Why?! Look at the responses from the system and try to explain! (The answer has been mentioned during a lecture.)





### Q4: Nmap can report ports to be in different states. What do the states ”open”, ”closed”, ”filtered” and ”unfiltered” mean? Read the manual page and documentation! Which are the most/least interesting ones? Run a scan against the target systems and try to find examples of all these types of ports. Look at the responses from the system. Can you match the replies with the different states?

