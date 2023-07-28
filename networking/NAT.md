# NAT (Network Address Translation)

## How it works
NAT is used to map IP endpoints to another endpoints. This can be like forwarding packets received from port 80 to some other port (`127.0.0.1:80 -> 127.0.0.1:9000`). NAT is also used by routers to allow machine communication between the inner network and the outer network. When two machines that are in the same network want to connect to each other (`192.168.24.50` and `192.168.24.10`) because they are in the same network there is no need to perform network address translation; packets are simply forwarded to the appropriate machine via a switch or a router. If two machines are in different networks, NAT is required. Assume machine A wants to talk to machine B in a different network. Machine A sends the packets to its network router, and the router notices that the destination IP address is not something in its network. **The router will change the packet's source IP address to its own public IP address and send out the packets over the Internet. Then, the router creates an IP mapping with the following:**
1. Original Source IP address (Machine A)
2. New Source IP address (Router's public IP address)
3. Destination IP address (Machine B)

The packets arrive at Machine B, and responses are sent back to the router based on the public IP address given. **The router then uses the mapping to translate the network IP address and changes the destination IP address from that of the router's to that of Machine A.**

## Application
**NAT is used to translate private and public IP addresses.** Hence, all machines in the same network have unique IP addresses, but will be accessible using a single IP address. This prevents IPv4 addresses from running out. **NAT can be used for port forwarding** which forwards packets sent for a specific port to some other endpoint. **NAT is also useful for load balancing.** Incoming packets send requests to **virtual IP address** and the servers' gateway router captures these requests. The router then selects a server based on a load balancing algorithm to even out the load and **creates a NAT mapping**. The server's responses are sent back to the user by the router after revisiting the NAT mapping and performing IP address translation.
