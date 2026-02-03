---
number headings: auto, first-level 1, max 3, 1.1
---
- [[#1 Physical Link|1 Physical Link]]
- [[#2 Data Layer (link layer)|2 Data Layer (link layer)]]
		- [[#2.1.1 Framing|2.1.1 Framing]]
		- [[#2.1.2 Flow control|2.1.2 Flow control]]
	- [[#2 Data Layer (link layer)#2.2 Error Detection|2.2 Error Detection]]
		- [[#2.2 Error Detection#2.2.1 Parity Checking|2.2.1 Parity Checking]]
		- [[#2.2 Error Detection#2.2.2 Internet Checksum (review)|2.2.2 Internet Checksum (review)]]
		- [[#2.2 Error Detection#2.2.3 Cyclic Redundancy Check (CRC)|2.2.3 Cyclic Redundancy Check (CRC)]]
		- [[#2.2 Error Detection#2.2.4 Error Correction|2.2.4 Error Correction]]
- [[#3 Reliable Data transfer (RDT) protocol|3 Reliable Data transfer (RDT) protocol]]
	- [[#3 Reliable Data transfer (RDT) protocol#3.1 RDT3.0|3.1 RDT3.0]]
	- [[#3 Reliable Data transfer (RDT) protocol#3.2 Pipelining|3.2 Pipelining]]
		- [[#3.2 Pipelining#3.2.1 Error recovering strategies|3.2.1 Error recovering strategies]]
- [[#4 Point-to-Point Protocol (PPP)|4 Point-to-Point Protocol (PPP)]]
	- [[#4 Point-to-Point Protocol (PPP)#4.1 Frame|4.1 Frame]]
		- [[#4.1 Frame#4.1.1 Byte stuffing/unstufing|4.1.1 Byte stuffing/unstufing]]
- [[#5 Multiple Access Protocols|5 Multiple Access Protocols]]
	- [[#5 Multiple Access Protocols#5.1 Ideal Protocol|5.1 Ideal Protocol]]
	- [[#5 Multiple Access Protocols#5.2 MAC protocols taxonomy|5.2 MAC protocols taxonomy]]
		- [[#5.2 MAC protocols taxonomy#5.2.1 Channel partitioning|5.2.1 Channel partitioning]]
		- [[#5.2 MAC protocols taxonomy#5.2.2 Random Access Protocols|5.2.2 Random Access Protocols]]
		- [[#5.2 MAC protocols taxonomy#5.2.3 "Taking Turns"|5.2.3 "Taking Turns"]]
- [[#6 LANs|6 LANs]]
	- [[#6 LANs#6.1 MAC and IP addresses|6.1 MAC and IP addresses]]
		- [[#6.1 MAC and IP addresses#6.1.1 Portability|6.1.1 Portability]]
	- [[#6 LANs#6.2 Ethernet|6.2 Ethernet]]
	- [[#6 LANs#6.3 Physical topology|6.3 Physical topology]]
	- [[#6 LANs#6.4 Ethernet frame structure|6.4 Ethernet frame structure]]
	- [[#6 LANs#6.5 Problems|6.5 Problems]]
	- [[#6 LANs#6.6 Ethernet CSMA/CD protocol|6.6 Ethernet CSMA/CD protocol]]
	- [[#6 LANs#6.7 Ethernet Standards|6.7 Ethernet Standards]]

#uni 
Let's now analyze how two connected Nodes transfer data.
The simplest case is having two computers connected by the same network
# 1 Physical Link
Physical links are by nature unreliable and introduce errors in the communication.
The **physical layer** works as follows: bits are *encoded* by the *transmitter* through an electric/electro-magnetic/light signal and sent over the **physical link**, this signal is then *decoded* by the *receiver*.
The physical link is *unreliable*:
- signal attenuation
- noise
	- interferences, fading
- transmitter and receiver must have perfectly synchronized clocks, but also this is impossible
- it is physically impossible to produces prefect square (high voltage=1, low voltage=0) curves
This means the **bit error rate** is never Zero: the received data sequence may be (very) different from the transmitter one.

How we achieve reliable communication over unreliable links?
We need to introduce failsafes on the **data layer**, which exists right over the physical layer.
# 2 Data Layer (link layer)
The data layer is implemented in a **network interface card** (**NIC**), or on a chip, in each-and-every host.
This NIC or chip attaches to the host's system buses.
The data link is a mix of hardware and software.
Ethernet, wifi card or chip implement both the data layer and the physical layer.

The sending side:
- encapsulates datagram in a frame
- adds error checking bits, reliable data transfer, flow control eccetera..
The receiving side:
- looks for errors
- flow control etc
- extracts datagram and passes it to the upper layer
### 2.1.1 Framing
This is a service incorporated in the data link:
- we incapsulate the datagram (trama) into **frames**
- we add **header** and **trailer** to each frame
```
|    header   |     payload     |     trailer   |
```
Obviously we introduce overhead.
### 2.1.2 Flow control
This is another possible service on the data link: receiver decides pacing between transmissions.
## 2.2 Error Detection
The receiver finds corrupted bits, then it can recover automatically the bits or ask the transmitter to re-send the corrupted frames.
- **Half-Duplex**: nodes at both ends of link can transmit, but not at the same time: achieved over a physical link by putting at both end **transceiver**, which is both a transmitter and a receiver.
- **Full-Duplex**: we put two lines of physical link, one is used to transmit by one end, the other line is used to transmit by the other end.

The message includes:
- **R**: error detection bits (redundancy bits), these are included in the **trailer** (because these are calculated while transmitting the message)
- **D**: data protected by error checking, may include header fields

What we do is apply a certain *mathematical operation* to the data, and include the result in the encoded message. 
When the receiver gets the message, it applies the same operation to the D data bits, and then checks if the resulting redundancy bits are the same as the received redundancy bits.

So D and R are the sent bits and D' and R' are the received bits. If the result of the operation on D' is different from the received R' bits, the message changed and we have N errors. This could mean the D' bits are wrong, or the R' bits are wrong.

Here are some of the commonly used operations:
### 2.2.1 Parity Checking
This method detects single bit errors.
Only one bit, the **parity bit**, is added as trailer to the D bits.
- Even parity: set parity bit so there is an even number of 1's
- Odd parity: set parity bit to there is an uneven number of 1's

Used between computers because sent messages usually only go up to 64bits
### 2.2.2 Internet Checksum (review)
The sender:
- treats the package as a sequence of 16-bit integers
- checksum: the sum of the integers
- checksum value put into the **checksum field** 
The receiver:
- calculates the checksum and compares it to the received one in the checksum field
	- if these are not equal an error is detected

Used in the TCP protocol, assuming the lower layers have already checked.
### 2.2.3 Cyclic Redundancy Check (CRC)
This is a more powerful error detecting coding.
- **D**: data bits
- **G**: bit pattern (generator), of r+1 bits (known by both sender and receiver)
Sender:
- calculates the trailing R bits
```
bit pattern:
   |       D        |   R    |

Formula per bit pattern:
<D,R> = D*2^r XOR R
```
The goal is to choose r CRC bits and R, such that <D,R> is exactly divisible by G (mod 2)
Receiver:
- receiver knows G and divided <D,R> by it. If the remainder of the result is not zero and error is detected

This operation can detect all burst errors that are less than r+1 bits

Widely used in practice, in Ethernet, 802.11 Wifi and more.
Used in the data link.
### 2.2.4 Error Correction
We now want to not only detect that an error occurred, but also want to localize the wrong bits.
- **EDC**: error detection and correction bits
- **D**: data
#### Two-Dimension Parity checking
Works the same as [[#Parity Checking]] but we divide the message in a matrix where every line and also every column has its parity bit. This helps us localize the wrong bits.
# 3 Reliable Data transfer (RDT) protocol
Sender utilizes rdt_send(), receiver uses rdt_receive.
We will incrementally develop the sender and the receiver sides of the reliable data transfer (RDT) protocol.
We will use finite state machines (FSM) to descrive the sender and the receiver.
## 3.1 RDT3.0
su Ipad o slide.
#### RDT3.0 "Stop and Go" Performance evaluation
"Stop and Go": sending one packet and waiting for ACK.
$$
\begin{matrix}
D_{trans}= \frac{L}{R} \\
RTT= D_{trans}+ping \\
t=RTT+D_{trans} \\ 
U=\frac{D_{trans}}{t}
\end{matrix}
$$
But since $D_{trans} << ping$ we get that $U$ is extremely low.
## 3.2 Pipelining
The answer to the RDT3.0 Performance problem is sending multiple packets back to back, without waiting for an ACK for every packet.

This leads to:
- needing bigger sequence numbers
- buffering at both receiver and sender side
- how do we recover lost/corrupted packages?
### 3.2.1 Error recovering strategies
#### Go-back-N
The sender sends maximum $N$ unACKed packets in the pipeline, the receiver *only sends cumulative ACKs* and doesn't ACK a packet it there's a gap: all the packets following a corrupted or not received packet are discarded by the receiver and resent.
The sender implements a timer for the oldest unacked packet: if the timer expires it retransmits all unacked packets.

This was needed back in the main-frame era, because there wasn't much memory to buffer potentially useless out of order packets.
##### Sender
The sender has a window of up to $N$ consecutive transmitted, but unacked, packets.
A $k$-bit sequence number is included in the packet header.
##### Receiver
The receiver always sends an ACK for the highest (in sequence number) correctly received packet: this may generate duplicate ACKs; it only needs to remember the `rcv_base`. 
On receipt of out of order packets it re-sends the ACK for the highest corretly received packet, as for the out-of-order arrived packet it may discarded or buffered, this is an implementation detail.
#### Selective repeat
The sender sends maximum $N$ unACKed packets in the pipeline, the receivers *ACKs individual packets*.
The sender implements a timer for every unacked packet: if the timer expires it retransmits all unacked packets.

This is more efficient.
##### Pseudocode
Let's now descrive how sender and receiver should act, using pseudocode instead of finite state machines.

> Steps: for each machine, define what events are possible and define how the machine should act on them.
###### Sender
- data from above:
	- if next available seq # in window, send packet
- timeout(n):
	- resend packet n, restart timer ACK(n) in [sendbase,sendbase+N]:
	- mark packet n as received
	- if n smallest unACKed packet, advance window base to next unACKed sequence number
###### Receiver
- packet n in `[rcvbase, rcvbase+N-1]`
	- send ACK(n)
	- out-of-order: buffer
	- in-order: deliver (also deliver buffered, in-order packets), advance window to next not-yet-received packet
- packet n in `[rcvbase-N,rcvbase-1]`
	- send ACK(n) (maybe sender didn't receive earlier ACK)
- otherwise:
	- ignore
##### Problem
It may happen (for example if sender sends 4 packets and receiver sends 4 acks, all lost in transmission) that the sender sends a duplicate packets and the receiver accepts it.
This happens because the sequence number goes from 0 to windowSize.

> Solution: max sequence number must be at least double of the window size.
# 4 Point-to-Point Protocol (PPP)
This is a protocol at the data link level (data layer) ([[Internet Protocol Stack]]).
This protocol was defined in a period in which the [[TCP/IP stacks]] was only one of the possible internet architectures.
Features:
- packet framing
- error detection ([[#Cyclic Redundancy Check (CRC)]] algorithm)
- no error correction! no retransmission! -> *unreliable service* 
- **bit transparency**: no limitations on what bit patterns can be transmitted
- network layer address negotiation
- no point-to-multipoint communication
- no flow control
## 4.1 Frame
```
| flag | address | control | protocol | info | check | flag |
   1B       1B        1B       1,2B     varL    2,4B     1B
```
- flags are delimiters for the framing, and are set to `01111110`
- address is useless, and always set to $0xFF$. Historically address with every bit set means Broadcast.
- control does nothing, could be used in the future
- protocol specifies to which upper layer protocol to deliver the frame (e.g. IP)
- info is the data carried for the upper layer, and is so obviously of variable lenght
- check is for the [[#Cyclic Redundancy Check (CRC)]] for error detection

### 4.1.1 Byte stuffing/unstufing
How do we ensure bit transparency? How do we make sure that info is not confused with the escape flag
We use an escape sequence:
to transmit `01111110` the transmitter sends `01111101 01111110`.

So the sequence `01111101` followed by either `01111110` or `01111101` tells the receiver to not interpret these last two as escape or flag, just data.
#### Sender (byte stuffing)
- 01111110 -> 01111101 01111110
- 01111101 -> 01111101 01111101
#### Receiver (byte unstuffing)
- 01111101 01111110 -> 01111110
- 01111101 01111101 -> 01111101
# 5 Multiple Access Protocols
There are two types of links:
- point-to-point
	- point-to-point link between ethernet switches or hosts
	- [[#Point-to-Point Protocol (PPP)]] for dial-up access
- **broadcast** on a **multiple access channel** (**MAC**) (shared wire or medium)
	- old fashioned ethernet
	- upstream HFC in cable-based access network
	- 802.11 wireless LAN, 4G, satellite

Using a single shared Broadcast channel leads to **collision**: a node receives two or more signals at the same time.
Also we suppose we do not have access to a second, out-of-band, channel for coordination.
We therefore need a **multiple access protocol**: a *distributed algorithm that determines how nodes share a channel*.
## 5.1 Ideal Protocol
Consider a multiple access channel (**MAC**) of rate $R$ bps.
Criteria:
1. when one node wants to transmit, it can send at rate $R$
2. *fair*: when M nodes want to transmit, each can send at an average rate of $R/M$ 
3. *fully decentralized*
4. *simple* (fissazione degli americani: metodo KISS, keep it stupid simple)
## 5.2 MAC protocols taxonomy
There are 3 broad classes:
### 5.2.1 Channel partitioning
Divide the channel into smaller pieces (time slots, frequency, code), then allocate each piece for exclusive use of a node.
#### TDMA: time division multiple access
The channel is accessed in "rounds": each station gets a fixed lenght slot in each round (lenght = packet transmission time).
Unused slots go idle :( .

This protocol doesn't meet criteria 1,2 and 3 ([[#Ideal Protocol]]).
#### FDMA: frequency division multiple access
NON IMPORTA
### 5.2.2 Random Access Protocols
The channel is not divided and collisions are allowed, but it is needed to "recover" from them.
- When a node wants to send a packet, it sends it a full channel data rate ($R$)
- no coordination among nodes beforehand

A random Access MAC protocol specifies:
1. how to detect collisions
2. how to recover from collisions
#### Slotted ALOHA
Assumptions:
- all frames are of the same size
- time is divided into equal size slots (the time it takes to transmit 1 frame)
- nodes start to transmit only  at the beginning of a slot
- nodes are synchronized
- if 2 or more nodes transmit in the same slot, all nodes detect the collision

Operation:
1. When a node obtains a fresh frame it transmits it in the next available slot
	- if there's no collision (receives ACK) the node can send also the new frame in the next slot
	- it there's a collision (no ACK) the node at every new slot retransmits the frame with probability $p$, until it actually sends it, so hopefully the two colliding nodes "choose" different slots to retransmits.
##### p
Suppose: $N$ nodes with many frames to send, each transmits in a slot with probability $p$.
- probability that a given node has a succesful transmission in a slot: $p(1-p)^{N-1}$ 
- probability that any node has success: $Np(1-p)^{N-1}$
- so to find the $\overline p$ that maximizes ($\to 1$) $Np(1-p)^{N-1}$
	- $\lim_{N \to \infty} N \overline p (1-\overline p)^{N-1}$
	- max efficiency: $\overline p = 1/e=0,37$ 
#### (unslotted) ALOHA
Designed by professor Abrahamson. Aloha means "hello" in Hawaian.
- no synchronization

1. When a node obtains a fresh frame it transmits it immediately
	- the probability of collision increases without synchronization, in the slotted version only a full collision can happen, in the unslotted version only a small part of the frame may collide and invalidate the whole frame:
		- a frame sent at $t_0$ collides with another frame sent in $[t_0 -1 ,t_0+1]$ 
##### p
Redoing the math we find that the optimal $p$ is $\overline p = 0,18$, much worse than [[#Slotted ALOHA]].
#### CSMA
**Carrier sense multiple access**.
The underlying idea is to listen to the channel before transmitting, so as to not interrupt others.

Collision can still occur with carrier sensing: the propagation delay means two nodes may not hear each other's just started transmission.
#### CSMA/CD
This is CSMA with **collision detection**.
The colliding transmissions are aborted.
Collision detection is easy with a wired channel, difficult in wireless.
##### Algorithm
1. NIC receives a datagram from the network layer, and creates a frame
2. if the NIC senses that the channel is:
	- idle: starts frame transmission
	- busy: waits until the channel is idle, then transmits
3. if the NIC transmits the entire frame without collision, the NIC is done with the frame
4. if the NIC detects another transmission while sending, it aborts and sends a **Jam** signal (signal stronger than normal transmissions)
5. after aborting, the NIC enters the ***binary (exponential) backoff***:
	- after the $m$th collision, the NIC chooses a $K$ at random from $\{ 0,1,2,...,2^m-1\}$. The NIC waits $k*512$ bit times, returns to `step 2`.
	- more collisions: longer backoff interval

> in ethernet the maximum dimension of a window is 10
#### CSMA/CS
### 5.2.3 "Taking Turns"
The nodes take turns, but nodes with more to send can take longer turns.
#### Polling
A master node invites other nodes to transmit in turn.
This is typically used with "dumb" devices.

Concerns:
- polling overhead
- latency
- SPF (master)
#### Token Passing
The control **token** is passed from one node to the next sequentially. This resolves a few issues with [[#5.2.1.1 TDMA time division multiple access]]: no idle slots are wasted for example.

Concerns:
- token overhead
- latency
- SPF[^1] (token)
	- when the token fails, the node tasked with emitting the token in the network at some point recognizes the failure and emits another token in the network
# 6 LANs
**Local Area Networks** (**LANs**) are a broadcast medium that utilize **MAC** addressing, where MAC stands for **Medium access control protocol**.
These cover a limited area (home, building, uni campus) and have a high bit rate (100Mbps - 10 Gbps).
## 6.1 MAC and IP addresses
A **MAC address** is a **48 bit** (for most LANs) address burned in the **NIC** ROM (sometimes software settable), it is used "locally" to get a frame from one interface to another physically-connected interface.
The IP address is instead a 32 bit address used in network layer forwarding.

Every interface in a LAN has a unique MAC address and a **locally** unique 32-bit IP address.

The MAC address allocation is administered by the [[IEEE]]: every manufacturer buys a portion of the MAC address space, to assure uniqueness.
### 6.1.1 Portability
An interface can move from one LAN to another, the IP address instead depends of the IP subnet to which the node is attached.
## 6.2 Ethernet
**Ethernet** is the dominant, and first widely used, wired LAN technology.
Benefits:
- fast (10 Mbps - 400 Gbps)
- a single chip can have multiple speeds
## 6.3 Physical topology
There are two possible physical topologies for ethernet:
- Bus: all nodes are in the same collision domain.
- Switched: each host connected to a switch runs a separate ethernet protocol, so no collision is possible.
## 6.4 Ethernet frame structure
The sending interface encapsulates the IP datagram (or other network layer protocol packet) in a **Ethernet Frame**:
```
| preamble | dest.address | src.address | type | data(payload) | CRC |
```
- preamble: used to synchronize the receiver and the sender clock rates. It is made of 7 bytes of 10101010 followed by one byte of 10101011
- addresses: these are 6 byte - 48 bit MAC addresses. If the receiver's adapter receives a frame with it's destination address, or with the broadcast address, it passes the data in the frame to the network layer.
- type: this field indicates the higher layer's protocol, mostly IP, and it is used to demultiplex up at the receiver.
- data: the dimension of the payload must be between 1500 bytes and 48 bytes
- CRC: [[Direct Connection Networks#2.2.3 Cyclic Redundancy Check (CRC)]], if an error is detected the frame is dropped.
## 6.5 Problems
- connectionless: there is no handshaking between the sending and the receiving NICs
- unreliable: because ethernets doesn't use ACKs, dropped frames are lost if the sender uses a higher layer RDT protocol (e.g. TCP)
## 6.6 Ethernet CSMA/CD protocol
Ethernets uses **unslotted CSMA/CD with binary backoff** as it's MAC ([[Direct Connection Networks#5 Multiple Access Protocols]]) protocol.
See [[#5.2.2.4 CSMA/CD]].

1. The NIC receives the data from the network layer and creates a frame
2. if the NIC senses that the channel is idle for **96 bit** it starts the transmission of the frame, otherwise it waits
3. if the NIC transmits the entire frame without collision, the NIC is done with the frame
4. if the NIC detects another transmission while transmitting it aborts and sends a **48 bit** jam signal
5. After aborting, the NIC enters **exponential backoff**:
	   after the $i$-th collision:
	   1. the NIC chooses $K$ at random from $\{ 0,1,2,...,2^{m}-1\}$, where $m=\max(i,10)$.
	   2. the NIC sets a backoff timer at $k\cdot 512 \ \text{bit times}$
	   3. the NIC waits until the backoff timer expires
	   4. NIC returns to step 2
- After 17 trials the frame is dropped.
- $\text{bit time} =  0,1 \mu \text{sec}$ for 10 Mbps ethernet
## 6.7 Ethernet Standards
There are many different ethernet standards, all with the same MAC protocol and frame format.
These different standards have different speeds and use different physical layer media (fiber, cable ...).

[^1]: SPF = single point of failure
