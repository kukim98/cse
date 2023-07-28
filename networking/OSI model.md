# OSI Model

## Introduction
All machines have a unique 48 bit **MAC (Media Access Control) address**. The OSI model explains how two machines communicate over a network.

## Application Layer
This is the top-level layer of the OSI model. The application layer is what SW engineers deal with regularly; HTTP, FTP, and SMTP are some examples of popular application layer protocols.

## Presentation Layer
This layer is responsible for encryption of the application layer data if necessary. Encryption occurs for HTTPS.

## Session Layer
This layer is responsible for tagging data with a session id.

## Transmission/Transport Layer
This layer is responsible for adding source and destination port numbers. Also, the data is broken down into multiple **segments**. With TCP, sequence numbers are attached to these segments to ensure ordering of data. UDP is also a popular protocol living in this layer.

## Network Layer
This layer is responsible for adding source and destination IP addresses to the segments from the transmission layer and turns them into **packets**. IP (Internet Protocol) is the one that is used the most today.

## Data Link Layer
The layer is responsible for adding source and destination MAC addresses to the packets from the network layer and turns them into **frames**. It also breaks down packets into smaller pieces. **The data link layer upon reception of frames is responsible for dropping packets that are not for the machine.**

## Physical Layer
The layer is responsible for converting the frames into binary format that can be physically relayed using electrical signals, radio waves, and etc. 
