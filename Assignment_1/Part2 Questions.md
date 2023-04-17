### Q5: What are the similarities and differences between the five scan types, i.e., syn, ack, fin, null, and Xmas? What are their use-cases, i.e., in which situation can each scan be useful?

**NULL** Scan: The NULL scan sends a packet with no flags set to the target port and waits for a response. 

**Xmas** Scan: The Xmas scan sends a packet with the FIN, URG, and PUSH flags set to the target port and waits for a response.

When scanning systems compliant with this RFC text, any packet not containing SYN, RST, or ACK bits will result in a returned RST if the port is closed and no response at all if the port is open.

**Use-cases:**

**SYN** scans are the most common and versatile.

**ACK** scans are useful for identifying firewall rules. 

**FIN, NULL, and Xmas** scans are used to evade intrusion detection systems and identify hosts with weak TCP/IP stacks.