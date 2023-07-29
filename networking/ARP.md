# ARP
## Address Resolution Protocol
When communicating over the Internet, the OSI model uses the MAC addresses (Data Link - 2), the IP addresses (Network - 3), and the port numbers (Transmission - 4) to help identify the machines and the processes that are talking to each other. **Most times, however, we know the IP addresses of the destination, not the MAC address.** ARP (Address Resolution Protocol) solves this issue and is tasked with **mapping IP addresses to MAC addresses by keeping an ARP table**.

## ARP for Internal Connection
1. Machine A wants to connect to Machine B. It knows its IP address (192.168.24.5) and the port number (9000) but not the MAC address.
2. Machine A sends an ARP request to find the MAC address for a machine with the IP address of 192.168.24.5.
3. Machine B receives the ARP request and responds back with its MAC address. All other machines will simply drop the ARP request since it is not for them.
4. Machine A receives the ARP response and adds a row to its ARP table (192.168.24.5 -> aa:bb:cc:dd:ee:ff). Machine A is now able to send its request to Machine B.

## ARP for External Connection
1. Machine A wants to connect to Machine C. It knows its IP address (44.33.22.11) and the port number (80) but not the MAC address.
2. Machine A knows that the IP address is not within its internal network; thus, it decides to contact the gateway/router (192.168.24.1), but it does not know the MAC address of it.
3. Machine A sends an ARP request to find the MAC address of the machine with the IP address 192.168.24.1.
4. The router receives the ARP request and responds back with its MAC address. All other machines will simply drop the ARP request since it is not for them.
5. Machine A receives the ARP response and adds a row to its ARP table (192.168.24.1 -> aa:aa:aa:aa:aa:aa). Machine A is now able to send its request to the gateway.
6. The router receives Machine A's request. It then changes the source IP address and the MAC address and forwards it to the appropriate party, and the cycle continues until it reaches Machine C.

## Spoofing
**If a machine spoof's its IP address, it can trick other machines to think that it is the router.** When sending out an ARP request, if the malicious machine responds first before the actual machine, the IP address gets mapped to the malicious machine's MAC address. Now the malicious machine receives responses from the clients. If the request is encrypted, then there's no way for the machine to have access to the data inside; however when using no encryption, the data will be exposed.
