#### Q: The TTL field in an IP datagram canbe useful when a attacker wants to create a network map, explain how this can be done.

1. The TTL field in an IP datagram is a value that indicates the maximum number of hops that the packet can traverse before being discarded.

2. Each router that handles the packet decreases the TTL value by one. If the TTL reaches zero, the router discards the packet and sends an ICMP message back to the source telling it what router discarded the message.

3. Therefore, an attacker sending a packet with increasing values of TTL (1,2,3) to a host will provide info about what routers exist in the path. 

**How to address this TTL problems in a border firewall?** 

- Drop outgoing ICMP Time Exceeded messages.
- Normalize TTL values for incoming datagrams in the firewall(e.g. set TTL to 255)

**Fingerprints:** Different systems have different defalut values for many header fields such as TTL, window size, DF, SYN message size, MSS, window scaling, etc. These info can be used to tell what system has generated the datagrams.

