### Q9: Why would you want to use fragmented packets for scanning? How do you think fragmented packets should be handled in modern networks?

####  Try to create fragmented packets (flag -f). Limit the scan to one port.

Fragmentation can split the packets into smaller pieces, which can then be transmitted individually and reassembled by the receiving device.

Using fragmented packets for scanning can be useful in situations where a network or a device is configured to block or filter certain types of traffic, such as large packets or packets with specific payloads. By fragmenting packets, Nmap can avoid triggering the IDS and perform the scan more stealthily.

In modern networks, fragmented packets should be blocked by default for security consideration.

### Q10: When checking the output with Wireshark, do you see fragmented packets as expected? What happens if you add the --send-eth option?

#### Task: Please investigate the difference between these options! You may not experience a different behaviour when doing the scans using Kali Linux, but on other systems you will.



Yes,  fragmented packets being sent and received by the target system.

If add the `--send-eth` option when performing the fragmentation scan, the packets sent by Nmap will now use Ethernet frames instead of raw IP packets.