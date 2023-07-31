# HTTP
## Introduction
HTTP (HyperText Transfer Protocol) is the basis on which the Internet communicates; it is the application layer protocol used to communicate between two machines. HTTP can be either a **request** or a **response**. HTTP requests contain **URL**, **method type**, **headers**, and **body**. HTTP responses contain **status code**, **headers**, and **body**. To make an HTTP request, a connection is established between the two machines. The client then prepares the HTTP request and will be sent over the Internet. The server will then send back an HTTP response. Once done, the connection is closed. **With HTTPS, a TLS handshake occurs after a connection is opened up; this is to exchange the symmetric key information between the client and the server to safely encrypt and decrypt the data sent.**

## HTTP 1.0
Back in the 90s, machines had very low memory, and this caused an issue since each open TCP connection took up some memory of the server. **To fix this issue, with HTTP 1.0, TCP connections were closed after a single request.** Although this freed up the machines memory, this   required clients to establish new connections for every single request. This did not work well due to huge latency. In addition HTTP 1.0 used **buffering**. This required the entire data payload to be prepared before sending out the HTTP requests. And this added additional latency to the protocol.

## HTTP 1.1
This introduced the **keep-alive** header to keep the connection alive. This reduced latency from reestablishing TCP connections significantly. Once done, the connections were closed. This is closed **persisted TCP connection**. HTTP 1.1 also introduced caching with **E-tags** and improved the caching mechanism of HTTP 1.0. **Streaming with chunked transfer** was enabled with HTTP 1.1. This allowed big data payloads to be stream-delivered to the other machine as opposed to being buffered. This is the reason why sometimes large images were slowly loaded like in a stream. **Pipelining** was introduced where clients send requests in parallel as opposed in sequences.

## HTTP 2
**Multiplexing** allows multiple HTTP requests to be grouped into a single request. By doing so, we eliminate the need for pipelining and sequence in-order checks. **Compression** was also introduced. **Server push** is when the server pushes data to the client, which is faster than a server's response. It is **secure by default**, and has **protocol negotiation during TLS** that allows the server to pick the protocol.

## HTTP 2 over QUIC (HTTP 3)
HTTP 3 replaces TCP with **QUIC** which is UDP with congestion control. It has all the HTTP 2 features and is currently experimental.

