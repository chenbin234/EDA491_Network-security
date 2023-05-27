#### 1. The TTL field in an IP datagram canbe useful when a attacker wants to create a network map, explain how this can be done.

1. The TTL field in an IP datagram is a value that indicates the maximum number of hops that the packet can traverse before being discarded.

2. Each router that handles the packet decreases the TTL value by one. If the TTL reaches zero, the router discards the packet and sends an ICMP message back to the source telling it what router discarded the message.

3. Therefore, an attacker sending a packet with increasing values of TTL (1,2,3) to a host will provide info about what routers exist in the path. 

**How to address this TTL problems in a border firewall?** 

- Drop outgoing ICMP Time Exceeded messages.
- Normalize TTL values for incoming datagrams in the firewall(e.g. set TTL to 255)

**Fingerprints:** Different systems have different defalut values for many header fields such as TTL, window size, DF, SYN message size, MSS, window scaling, etc. These info can be used to tell what system has generated the datagrams.



#### 2. Fragmentation of IP packets is a well-known problem for firewalls since they may not know how the receiving host will reassemble the datagram. Please give a longer explanation for why this is problematic!

If the firewall does not know how the end host will reassemble overlapping datagrams, it will either be making mistakes or it has to try all possible combinations, but this is resource consuming and probably not realistic to do.

**What could a solution to this problem be?**

1. Either to know what systems it protects and how they reassemble fragments
2. or to drop all fragmented datagrams.



#### 3. The length field of IP is 16 bits long which means that a datagram can have any length between 0 and 65535. It is still possible to send larger IP datagrams, for example a datagram which is 75,000 bytes long. How?

An oversized IP datagram can be created that exceeds this size by sending a fragment with an offset and a length extending the datagram beyond this limit, for example by setting offset to 65,000 and length to 10,000 bytes.



#### 4. Why could it be problematic for a system to deal with a packet that has an incorrect (faked) TCP length field that differs from the link-layer length? Describe two possible scenarios! (2p)

1. Packet < actual length: old contents of buffer can be used and sent to receiver. Example is a router that forward an IP datagram, it may take the old contents in the buffer and forward another packets payload to the receiver. 
2. Packet > actual length: may cause a buffer overrun if the receiver dynamically allocates buffer based on the header length. It may overwrite stack contents and change program behavior.



