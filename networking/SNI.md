# SNI (Server Name Indication)
## Introduction
When a machine hosts a web service, contacting the IP address of the machine results in the access of that particular web service. With SNIs, a machine can host multiple web services on the same IP address, and the clients can select the appropriate machine to contact using SNIs. **Server Name Indication** is basically a "tag" that clients send to the server, and the server uses SNIs to deliver the appropriate content/services.

## HTTP with SNI
After establishing the TCP handshake, the client sends HTTP requests with the SNI set to the hostname (this is done by setting the *host* header value in the request); **SNI resides in the application layer**. The destination IP address - let's say - is 14.23.41.8. The packets are sent to the destination machine. The machine looks at the host header and responds back with the appropriate data. **The canonical names will all be mapped to the same IP address in the authoritative name server** so that all requests arrive at the same machine; a software that runs on the machine will reroute the incoming requests by looking at the host header value.

## HTTPS with SNI
Assuming we are using TLS 1.3, after establishing the TCP handshake, the client sends a *client hello* to the server with the hostname. The server machine will look at the hostname and respond back with the appropriate certificates for the webpage. The rest is then identical to what happens in HTTP with SNI but with encryption. And because of the exposure of the SNI during the TLS handshake, ISPs can sniff the data (since the SNI itself is not encrypted) and prevent users from accessing certain websites.

## ESNI
**ENSI (Encrypted SNI)** applies encryption to regular SNIs to prevent ISPs from sniffing the data. When a DNS query is made, the authoritative name server will not only provide the IP address but also the public encryption key for the server. After establishing the TCP connection, the client sends the *client hello* to the server with the SNI encrypted using the public encryption key from the DNS query. The server receives the call and decrypts the SNI with its private key to get the hostname.
