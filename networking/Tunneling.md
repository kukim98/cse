# SSH/TCP Tunneling

## Introduction
Tunneling allows the client machine to connect to another machine that is unreachable. This can be because of firewalls or simply lack of routes to connect to the machine. **The idea is to nest TCP segments within each other.** Suppose machine A wants to talk to machine C, but it is unreachable. Machine B can talk to both A and C. By using tunneling, Machine A can talk with Machine C via Machine B.
1. Machine A prepares packets to be sent to Machine C. **The source is set to Machine A, and the destination is set to Machine C. The packet itself is encapsulated again as a segment with the source set to Machine A and the destination set to Machine B.** The packets first arrive at Machine B, and the packets are interpreted. Machine B notices that the data is actually another TCP packet from Machine A to Machine C. **Machine B changes the source from Machine A to itself and sends the packets to Machine C.** Machine C receives the packets and responds back to Machine B. Machine B then changes the destination from Machine B to Machine A, and it sends the response to Machine A. When it arrives Machine A now has access to the data from Machine C.

## Application
* By passing blocked port - If a client wants to access a server that is protected behind a firewall, it does not have direct access to the machine. When a client is trying to do the above, **local port forwarding** can be used.
1. Client creates and opens up a local service at a random port (9000).
2. The job of the local service will be to encapsulate incoming requests and to make an SSH request (22) to the destination server via an access point. In SSH, the command to open a local forwarding port is as follows:
```ssh -L 9000:192.168.1.3:8080 kim@4.56.7.11```
```ssh -L LOCAL_PORT:FINAL_DEST_ADDR:PORT USER@ACCESS_POINT_ADDR```
3. The client now sends requests to the local service (TCP localhost:9000), and the local service will send the SSH request to the access point.
4. The firewall allows SSH (22) and the request arrives at the SSH server. Then the server will automatically unwrap the content and allow communications with the final destination assuming the access point and the final destination machine have access to each other.

* Accessing internal IP - If the destination machine resides within a private network, then clients outside the network do not have direct access to the machine. To allow clients access to the server, **remote/reverse port forwarding** can be used.
1. Publicly visible machine (access point) opens up a port that it listens to. In SSH, the command to open a reverse forwarding port is as follows:
```ssh -R 9000:192.168.1.3:8080 kim@4.56.7.11```
```ssh -R REVERSE_PORT:FINAL_DEST_ADDR:PORT USER@ACCESS_POINT_ADDR```
2. Now, clients connected to the Internet can connect to the machine in the internal network by sending `4.56.7.11:9000`. This will then be forwarded as an internal request to `192.168.1.3:8080`.

* Accessing blocked websites - Certain websites are inaccessible because the ISP (Internet Service Provider) has blocked them. In this case, **dynamic port forwarding** can be used.
1. In SSH, the command to initiate dynamic port forwarding is as follows:
```ssh -D 9000 kim@4.56.7.11```
```ssh -D DYNAMIC_PORT USER@ACCESS_POINT_ADDR```
2. By doing so, the client will be able to access the blocked website via the local dynamic port through the access point.

## Pros and Cons
Tunneling allows **access to blocked sites**, **provides a layer of security and anonymity**, and **allows exposure of internal traffic**. However, because tunneling is running TCP over TCP, **there's a potential for huge latency**. In addition, TCP tunneling **runs without application context** meaning that the "middleware" is not aware of the context and simply relays the information to the final destination.
