### Q8: What packet(s) does Nmap send to figure this out? Also, look at the responses sent by the systems using Wireshark. Do you see any differences that may reveal what type of system is being used? (You may want to limit the number of ports it scans to avoid waiting, and look at protocol parameters. Which ports should you select?!)

To perform OS detection, Nmap sends a series of probes to the target and analyzes the responses to identify patterns that are characteristic of specific operating systems. The probes that Nmap sends during OS detection can vary depending on the version of Nmap being used, as well as the options and settings specified by the user. However, some common probes include:

- TCP/IP stack fingerprinting: This involves sending a series of TCP and UDP packets to the target and analyzing the responses to determine the operating system's network stack characteristics, such as the order in which flags are set and how they respond to certain edge cases.
- ICMP probes: TTL and timestamp values
- TCP sequence prediction: This involves sending a series of TCP packets with various sequence numbers and analyzing the responses to predict the target's TCP/IP stack characteristics.



When limiting the number of ports to scan, it's recommended to choose a set of commonly used ports that are likely to be open on most systems. Some popular ports for OS detection include:

- 22 (SSH)
- 23 (Telnet)
- 80 (HTTP)
- 443 (HTTPS)
- 3389 (Remote Desktop Protocol)

