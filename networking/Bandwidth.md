# Bandwidth
## Introduction
Bandwidth is the rate at which data flows. Internet Service Providers offer various plans with differing bandwidth to people who want to use the Internet. If the plan offers 80 mb/s (mega-bits per second) download bandwidth - which is equivalent to 10 MB/s (megabytes per second) - the maximum incoming data flow will be at max 10 MB/s. The same applies for upload bandwidth. Because a machine has high bandwidth rate does not mean that it will be able to download and upload data fast at that particular rate. For instance, if a client has a low download bandwidth but the server has a high upload bandwidth, then the data transfer will throttle due to the low download bandwidth of the client. This is maintained by TCP's congestion control by checking ACKs and NACKs. Once the sender detects that the receiver is not responding with ACKs for the sent packets, the sender will slow down and reduce the upload rate. Otherwise, it will slowly increase the upload rate, and this cycle will continue.