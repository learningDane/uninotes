---
number headings: auto, first-level 1, max 3, 1.1
---
#uni 
> Internet Stack Protocol: ![[internetProtocolStack.svg|600]]
# 1 Transport-Layer services
The transport Layer manages the logical communication between application **processes** running on different hosts, whereas the network layer manages the logical communication between **host**.

The fact that there are multiple processes running on the same host calls for the need for multiplexing and demultiplexing.

The Sender in transport protocols breaks application messages into **segments** and passes them to the *network layer* (to the IP).
The Receiver in transport protocols reassembles these segments into messages and demultiplexes them to the *application layer* via a socket.
# 2 Multiplexing and Demultiplexing
## 2.1 Multiplexing
Multiplexing is done at the sender: data from multiple sockets is handled, to which the respective transport header is added, later used for demultiplexing.
## 2.2 Demultiplexing
The transport header info is used to deliver the received segment to the correct socket.

Multiplexing and demultiplexing are done based on segment and datagram header field values.
### 2.2.1 Connectionless demultiplexing
1. the host receives IP datagrams.
	- each datagram has a source IP address and a destination IP address
	- each datagram carries one transport-layer segment
	- each segment has source and destination port numbers
2. the host uses the *IP address and the port number* to direct the segment to the appropriate socket.
### 2.2.2 Connection-Oriented demultiplexing
The TCP socket gets identified by 4 tuples:
- source IP address
- source port number
- destination IP address
- destination port number
The receiver uses *all four* of this values (4-tuple, quadrupla di informazioni) to direct the segment to the appropriate socket.

A server may support many simultaneous TCP sockets:
- each socket is identified by its own 4-tuple
- each socket is associated with a different connecting client

> In TCP a connection is identified by 4 parameters!
# 3 Connectionless transport: UDP
RFC 768:
UDP (**User datagram protocol**) is a "best effort" service, like IP.
Segments may be lost and delivered out of order to the application.
This because UDP is ***connectionless***: there is no handshake between UDP sender and receiver, each UDP segment is handled independently of others.
## 3.1 Benefits and Uses
- no connection
	- connection can add RTT delay
- simplicity
- small header size
- no flow and congestion control
	- UDP can go faster
	- still works under congestion
This leads to UDP being useful in these areas:
- streaming and multimedia applications (loss tolerant, rate sensitive)
- [[DNS]]
- SNMP
- HTTP/3

If a reliable transfer is needed over UDP (for example in HTTP/3) reliability and congestion control are added at the application layer.
## 3.2 UDP segment header
> UDP segment header: ![[Pasted image 20251105161704.png]]
- the payload is a message from the application layer, it is of variable length so we have the length field
- length field: length of the UDP segment (including header) in bytes
## 3.3 UDP checksum
The sender treats the contents of the UDP segment (header and IP address included) as a sequence of 16-bit integers, then the checksum is computed as the sum of these 16-bit integers and the checksum value is put into the UDP checksum field.

The receiver computes the checksum aswell and compares it to the checksum included in the header: if these are not equal and error is detected.
# 4 Connection-Oriented transport: TCP
RFCs: 793,1122, 2018, 5681, 7323
TCP (**transport control protocol**) introduces the **point-to-point** concept: one sender, one receiver.
It achieves a reliable, in-order *byte stream*, from the application standpoint.
The flow is **Full duplex**: the flow is bidirectional in the same connection.

Every segment has an **MSS**: maximum segment size: dimensione frame - dimensione massima dell'ether IP (20 byte) - dimensione massima dell'ether TCP (20 byte)

The TCP congestion and flow control set the window size of the **pipelining** ([[Direct Connection Networks#3.2 Pipelining]]).
## 4.1 TCP segment structure
> TCP segment structure: ![[Pasted image 20251105164940.png]]
- PDLated approach: ACKs are sent inside fragments
	- if A bit is set "Acknowledgement number" is significant (significativo)
- the checksum is the same as in UDP: internet checksum
- R: RST: reset: when connection is having problems and the connection needs a reset
- S: SYN: start: is set in the connection phase
- F: FIN: finish: is set when wanting to close the connection
- receive window: used to repeatedly tell the other end how many bytes are free in the receiving window
- "urgent data pointer": used to tell receiver that in the payload is important data (with priority). Is never used. When this field is significant, bit "U" in the flags is set.
> normally the header is 5 words (5* 32 bits = 20 byte), but it is of variable length, the length is inside the "header length" field
## 4.2 Sequence Numbers and ACKs
In TCP sequence numbers are the *byte stream number* of the first byte in the segment's data.

> TCP Window: ![[Pasted image 20251105170426.png|300]]

TCP uses a go-back-$N$ error recovering approach: it sends cumulative ACKs (see [[Direct Connection Networks#3.2.1.1 Go-back-N]]).

TCP doesn't specify how the receiver must handle out-of-order segments, that is up to the implementor.
## 4.3 TCP connection Management
Before exchanging data, the sender and the receiver handshake: they agree to establish a connection and agree on the connection parameters (for example the starting sequence numbers).
### 4.3.1 the 3-way handshake
> tcp 3-way handshake: ![[Pasted image 20251105171652.png]]

- if the initial sequence number was always the same, we risk mixing segments from two different connections, so we use a random number.
  EG: we have a first connection which is short, every packet is ACKd and the connection is closed, then we open a new connection shortly after, if there are still segments from connection 1 "in flight" the risk is they arrive while we have initiated the second connection, these segments arrive and are mistaken for segments from the new connection.
### 4.3.2 Closing a TCP connection
1. client sends TCP FIN control segment
2. server receives the FIN and replies with an ACK, closes the connection and sends a FIN
3. client receives the FIN, replies with an ACK and starts a **timed wait** (designed to close the connection shortly after the supposed arrival of the ACK to the server)
4. server receives the ACK. The connection is now closed.
   If the server doesn't receive the ACK (it timeouts), it resends the FIN, this is the reason of the timed wait of the client.

What does it mean to "close a connection"?
Deallocating the data needed for the connection.
## 4.4 TCP reliable data transfer
## 4.5 TCP flow control
## 4.6 TCP congestion control
# 5 Evolution of transport-layer functionality