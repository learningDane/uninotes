---
number headings: auto, first-level 1, max 3, 1.1
---
#uni 
Chapter (2)
# 1 Principles of network apps (2.1)
Creating a network app means writing a program that runs on different end systems and communicates over a network.

There is no need to write software for device on the network-core: these devices do not run user applications. Routers don't need to implement the whole [[Internet Protocol Stack]].

Running applications only on systems on the edge of internet allows for a rapid app development and propagation.

Internet is transparent, meaning the two (or more) devices communicating apparently are directly connected.
## 1.1 Client-Server vs P2P
The two most important application paradigms are:
- [[Peer to peer]]
	- bitTorrent
- [[Client-Server]]
	- web, http
	- e-mail, smtp, imap
	- dns
### 1.1.1 Client-Server paradigm
A server is an always-on host with a permanent IP address ([[Internetworking#3 IP the internet protocol]]), often found in data centers, for scaling advantages.

Clients contact and communicate with the server intermittently, the may have dynamic IP addresses and *do not* communicate directly with each other.
### 1.1.2 Peer-to-Peer paradigm
Every peer looks more like a powerful client from the [[Client-Server]] paradigm.
But technically every peer is on the same level.
The availability of resources this way is not guaranteed from a powerful server, but from the sheer number of peers -> ***self scalability***.
There isn't an always on server.
End systems arbitrarily communicate with each other.

>Peers request service from other peers, providing service to other peers in return.

**Indexes** are needed for mapping information to the right host locations.
## 1.2 Process Communicating (2.1.2)
A process is a program running within a host.
Within a host two processes communicate using *inter-process communication*, which is offered and defined by the operating system ([[Sistemi Operativi]]).
Processes in different hosts instead communicate by exchanging **messages** (obviously two processes on the same host can still communicate using messages if needed).

> In the client-server paradigm the ***client process*** (often just called *the client*) is the process that initiates the communication, the ***server process*** (often just called *the server*) is the process that waits to be contacted.
> P2P applications have both a client process and a server process!

### 1.2.1 Socket
A process sends and receives messages to/from its **socket(s)**.
Sending a message means leaving it in the socket, thrusting the transport infrastructure will bring it to the receiving process' socket, there are in fact two sockets involved in every message exchange, one on each side.
### 1.2.2 Addressing Processes
To receive messages a process must have an *identifier*. The host device has a unique 32-bit IP address (or multiple unique IPs), but this is not enough since a single host can run multiple processes concurrently.
A process is identified using both the host's IP address and a **port number** associated with said process on it's host. 

This means different processes on the same host have the same IP address but different ports.
## 1.3 Application-layer protocols (2.1.5)
An application-layer protocol defines:
- the types of messages exchanged
- the message syntax: what fields are in the message and how these fields are delineated
- the message semantics: what the different fields inside a message mean
- rules for when and how processes should send and respond to messages

Protocols can be:
- **open protocols**
	- defined by RFCs (requests for comments)
	- allow for interoperability
- **proprietary protocols** 
## 1.4 Choosing the correct transport service (2.1.3)
When designing a network application we must choose the correct transport-layer service for our needs: some apps require a 100% reliable data transfer, some are loss tolerant, some apps require a minimum amount of throughput to be effective, some don't, some apps need security and the list goes on.

In short:
- TCP service:
	- reliable transport
	- flow control
	- congestion control
	- connection oriented
- UDP service:
	- unreliable data transfer

Here is a quick cheat table:

| application           | data loss tolerancy | minimum throughput                        | time sensitivity |
| --------------------- | ------------------- | ----------------------------------------- | ---------------- |
| file transfer         | no                  | no                                        | no               |
| e-mail                | no                  | no                                        | no               |
| web documents         | no                  | no                                        | no               |
| real-time audio/video | yes                 | audio: 5Kbps-1Mbps<br>video: 10Kbps-5Mbps | 10's msec        |
| interactive games     | yes                 | Kbps+                                     | 10's msec        |
| text messaging        | no                  | no                                        | depends          |

here is a table with different application-layer protocol and its used transport-layer protocol:

| application           | application-layer protocol | transport-layer protocol |
| --------------------- | -------------------------- | ------------------------ |
| file transfer         | FTP                        | TCP                      |
| e-mail                | SMTP                       | TCP                      |
| web documents         | HTTP 1.1                   | TCP                      |
| internet telephony    | SIP, RTP, or proprietary   | TCP or UDP               |
| streaming audio/video | HTTP, DASH                 | TCP                      |
| interactive games     | WOW, FPS (proprietary)     | UDP or TCP               |
### 1.4.1 Securing TCP
Normally TCP and UDP sockets do not offer encryption.

**Transport layer security** (**TLS**) must be implemented in network applications, it provides encrypted TCP connections, data integrity and end-point authentication.
Applications use TSL libraries, that in turn use TCP.
Using a TLS socket API we send cleartext into a socket, but the message then gets encrypted and traverses the internet in security, before getting decrypted at arrival to destination.
# 2 Client-Server Applications
## 2.1 Web and HTTP (2.2)
### 2.1.1 Overview
Web pages consist of **objects**, each of wich can be stored on different web servers. An object can be an [[HTML]] file, an image, a [[Java]] applet eccetera.
A web page consists of a base [[HTML]] file, which includes several referenced objects, each addressable by a URL.
### 2.1.2 HTTP
**HTTP** stands for (HyperText Transfer Protocol).
This protocol is based on the Client-Server paradigm.

HTTP uses TCP:
1. the client initiates a TCP connection to the server, port 80
2. the server accepts the TCP connection from the client
3. now HTTP messages (which are application-layer protocol messages) are exchanged between the client (the browser) and the web server
4. the TCP connection is finally closed

HTTP is *stateless*: the server mantains no information about past client requests. 
*Stateful* protocols are complex: past history must be maintained, if the server or the client crashes their views of the "state" may be inconsistent and must be reconciled.

There are two types of HTTP connections:
- *non persistent HTTP*:
  At most one object is sent over the TCP connection between the client and the server, after which the connection is closed
$$\text{response time for } n \text{ objects} = n \cdot ( 2 \cdot \text{RTT} + \text{file transmission time})$$
- *persistent HTTP*:
  Multiple objects can be sent over a single TCP connection, the connection is arbitrarily closed by either the client or the server
$$\text{response time for } n \text{ objects} = 2 \cdot \text{RTT} + n \cdot \text{file transmission time}$$

Where **RTT** (**round trip time**) is the time it takes for a small packet to travel from the client to the server and back.
Generally speaking RTT is much larger than a sigle file transmission time, thus leading to MUCH longer response times for non-persistent HTTP connections when dealing with multiple objects.
For example when transferring two small objects, *the response time is cut in half* using persistent HTTP.

After a a timeout the connection is closed automatically: TCP connections consume memory and leaving them open leaves the data structures allocated waisting memory.
### 2.1.3 HTTP messages
There are two types of http messages:
- *request*
- *response*
the message format is **ASCII**.
#### HTTP request messages
> HTTP request message general format: ![[Pasted image 20251113191922.png|500]]

There are multiple possible request messages:
- **POST** method: web pages often include form input, the user's input is sent from the client to the server in the body of a HTTP POST request message
- **GET** method: this is used to send data to a server: the user's data is included in the URL field of a HTTP GET request message, following a '?' (`www.site.com/subdomain?userdata`)
- **HEAD** method: this is used to request only the headers, without any objects, it is used during implementation
- **PUT** method: this uploads a new object to the server, completely replacing the file that exists at the specified URL with the content in the body of the POST HTTP request message
#### HTTP response messages
> Structure of a HTTP response message: ![[Pasted image 20251113193352.png|600]]
### 2.1.4 Status Codes
The status code appears in the first line in the server-to-client response message, there are multiple status codes for http responses:
- 200 -> Ok : request succeeded, the requested object is included later in this message
- 301 -> Moved Permanently : the requested object got moved, new location is specified later in the message with the tag `Location` 
- 400 -> Bad Request : request message not understood by the server
- 404 -> Not Found : the requested document was not found on this server
- 505 -> HTTP version not supported
### 2.1.5 TELNET
Telnet is a client-server application protocol that provides access to virtual terminals of remote systems on local area networks (LANs) or the Internet.
It is a protocol for bidirectional 8-bit communications. Its main goal was to connect terminal devices and terminal-oriented processes.

#### Example
`telnet <host> <port>` cli command open a tcp connection to the specified url and port
	type `GET <url>` HTTP/1.1 to make a get request then press enter
	type  `Host: <host>` and press enter twice so have the response

### 2.1.6 Cookies (2.2.4)
**Cookies** are used by some browsers to *maintain some state* between transactions (HTTP is *stateless*).

The Cookies mechanism can be divided in four components:
- **Cookie Header Line** in http *response* message
- **Cookie Header Line** in the next http *request* message
- **Cookie File** kept on the user's end system
- **Back-End Database** at the Web site

1. The client makes a simple http request to a server
2. The server creates and ID for the user and creates an entry in the backend database for that ID
3. The server includes a cookie with this new ID in the response message to the client
4. The client store this cookie in a cookie file, stored and managed by the browser
5. The next time that same client will make a HTTP request to that same server, it will include this cookie in the cookie header line of the request message
6. The server receiving this request message with this cookie will now be able to identify the client and offer extra functionality bounded to this new kind of *statefulness* 

Cookies have various implementations:
- Authorizations
- Shopping Carts
- Recomendations
- User session state (web e-mail)

The question is *How do we keep the state?*
 - protocol endpoints: maintain state at sender/receiver over multiple transactions
 - cookies: HTTP messages carry the state

> - **Cookies** permit the sites to learn (a lot) about you on *their* site.
> - **Third party persistent cookies** allow common identity to be tracked *across multiple web sites*.

### 2.1.7 Web Caches (proxy servers) (2.2.5)
*Goal*: satisfy client request without involving origin server
*Why*: to alleviate the load on origin servers. Caches are closer to clients so it reduces response time. Caches also alleviate the load on internet as a whole.

The user configures the browser to point to a **web cache**.
- if the objects is in the cache: the cache returns the object to th client.
- if the object isn't in cache: the cache asks and receives the object from the origin server, caches it and sends it to client.

Proxy servers act both as a client and as a server. They are typically installed by ISPs.
#### Problem of recency of cached objects
What do we do if the object is updated on the remote servers and the proxy server isn't aware?
**Conditional GET**:
*Goal*: don't send an object if the cache already has an up-to-date version.
- Cache: the cache when sending the GET statement includes the version of the cached copy:
  `if-modified-since:<date>`
- Server: response contains no object if the cached copy is up to date: `http/1.0 304 Not Modified`. 
  Otherwise, if the object has been updated, the new version is included in the HTTP response: `HTTP/1.0 200 OK <data>`.
This way the object is only sent if necessary, keeping the stress on the link low.
### 2.1.8 Important updates
#### HTTP 1.1
This version introduced *multiple pipelined GETs over a single TCP connection*.

In this versione the scheduling algorithm for GET requests is **FCFS**: first come first served.
Issue: small objects may wait for bigger (slower) objects (requests) (==HOL blocking==: **Head of line blocking**).

Also loss recovery (retransmitting lost TCP segments) stalls object transmission.
#### HTTP 2
RFC 7540, 2015: The key goal for this version was decreasing delay in multi-object HTTP requests.
Increased the flexibility for servers when sending objects to clients: objects are divided into frames and the frame transmission is interleaved.
Frames are scheduled to mitigate HOL blocking: smaller frames get sent first.
The order of transmission of requested object is now based on client-specified object priority, not necessarily FCFS.

Problems: recovery from packet loss still stalls transmission, also no extra security over vanilla TCP connections.
#### HTTP 3
The key goal for this version was to decrease delay in multi-object HTTP requests:
Adds:
- security
- per object error (and congestion) control (more pipelining) over UDP
## 2.2 E-mail, SMTP, IMAP (2.3)
The e-mail infrastructure is made of these three major components:
- **user agents**: the user reading, composing and editing mail messages
- **mail servers**: these have a *mailbox* containing incoming messages for the user and a *message queue* of outgoing (to be sent) messages
- **simple mail transfer protocol** (**SMTP**)

The E-Mail protocol is described in RFC(5321).
It uses TCP to reliably transfer email messages from clients (mail server that initiates the connection) to servers, port 25. It essentially is a direct transfer from the sending server (acting as a client) to the receiving server.

The transfer is divide in 3 phases:
1. handshaking (greeting)
2. transfer of messages
3. closure

This is command/response interaction, like http:
- commands: ASCII text
- response: status code and phrase
The messages must be in 7-bit ASCII.
### 2.2.1 Sending Emails
1. User composes email
2. sends email to his email server
3. the client side of SMTP server opens a TCP connection with the destination user's server
4. email is sent over the tcp connection
5. destination user can access the email via his email server
### 2.2.2 Sample SMTP interaction
```pseudocose
S: 220 hamburger.edu
C: HELO crepes.fr
S: 250 Hello crepes.fr, pleased to meet you
C: MAIL FROM: <alice@crepes.fr>
S: 250 alice@crepes.fr... Sender ok
C: RCPT TO: <bob@hamburger.edu>
S: 250 bob@hamburger.edu ... Recipient ok
C: DATA
S: 354 Enter mail, end with "." on a line by itself
C: Do you like ketchup?
C: How about pickles?
C: .
S: 250 Message accepted for delivery
C: QUIT
S: 221 hamburger.edu closing connection
```
### 2.2.3 Comparison SMTP-HTTP
- HTTP: pull
- SMTP: push
- both have ASCII command/response interaction, status codes
- SMTP uses persistent connections
- SMTP requires the message (header and body) to be in 7-bit ASCII
- SMTP server uses CRLF.CRLF to determine end of message
### 2.2.4 Mail message format
The format of e-mail messages is specified in RFC 531 (defines protocol) and RFC 822 (defines syntax).
- header lines:
	- To:
	- From:
	- Subject:
- `blank line`
- body: the message, 7-bit ASCII characters only
### 2.2.5 Mail access protocols (2.3.4)
SMTP defines delivery and storage of e-mail messages to the receiver's server.
We need a way to retrieve e-mails from our mail server: a **mail access protocol** like **IMAP** (Internet mail access protocol, RFC 3501).

IMAP defines how messages are stored on the server and provides retrieval, deletion and folders of stored message on the mail server.

We also use [[#HTTP]] to access web-based interfaces (like gmail, hotmail ecc) that work on top of SMTP (to send e-mails) and IMAP (or [[#POP]]) (to retrieve e-mails).
#### POP: Post Office Protocol
POP3 is an extremely simple MAP (mail access protocol), defined in RFC 1939.

POP3 begins when the user agent begins a TCP connection with the mail server, on port 110.
The server accepts the connection and the protocol now processes through 3 phases: authorization, transaction, and update.

1. **authorization**: the user agent sends a username and a password (in the clear) to authenticate the user. To do this the user uses two commands: `user: <username>` and `pass: <password>` 
2. **transaction**: the user agent retrieves messages and issues commands: mark messages for deletion, remove deletion marks, and obtain mail statistics. Commands: `list`, `retr`, `dele`, `quit`
3. **update**: occurs after the client has issued the _quit_ command, ending the POP3 session. At this time, the mail server deletes the messages that were marked for deletion.

A user agent using POP3 can be configured by the user to adhere to one of two modes: *download-and-keep* and *download-and-delete*.

In a POP3 transaction, the user agent issues commands, and the server responds to each command with a reply.
There are two possible responses: _+OK_ (sometimes followed by server-to-client data), used by the server to indicate that the previous command was fine; and _-ERR_, used by the server to indicate that something was wrong with the previous command.

A POP3 server only holds *some* state in a single session, like the list of marked messages, it does not hold state between sessions, this greatly simplifies the implementation of this protocol.

POP servers also do not offer any kind of message managing functionality, no folders and such.
#### IMAP
To solve this and other problems, the IMAP protocol, defined in RFC 3501, was invented. Like POP3, IMAP is a mail access protocol. It has many more features than POP3, but it is also significantly more
complex.

An IMAP server will associate each message with a folder; when a message first arrives at the server, it is associated with the recipient’s INBOX folder. 
The recipient can then move the message into a new, user-created folder, read the message, delete the message, and so on.
The IMAP protocol provides commands to allow users to create folders and move messages from one folder to another. 
IMAP also provides commands that allow users to search remote folders for messages matching specific criteria.

Another important feature of IMAP is that it has commands that permit a user agent to obtain components of messages. For example, a user agent can obtain just the message header of a message
or just one part of a multipart MIME message. This is useful in low-bandwidth situations.

Note that an IMAP server holds state between sessions.
## 2.3 The Domain Name System (DNS) (2.4)
*Problem*: internet hosts and routers have both
- a IP address ([[IP]]), used for addressing datagrams
- a "name", used by humans (like www.google.com)
How do we map between IP address and name, and vice versa?
*solution*: the DNS

The ***Domain Name System*** (DNS) is a *distributed database* implemented in hierarchy of many *name servers*.
Application-layer protocol: hosts and name servers communicate to *resolve* names (addres-name translation).

***Registering*** a subdomain means linking it univocally to a IP address, registering it in the DNS database.
### 2.3.1 DNS services (2.4.1)
- hostname to IP address **translation**
- host *aliasing*
- mail server aliasing
- *load distribution*
	- replicated web servers: many IP addresses correspond to one name
### 2.3.2 DNS structure
The DNS is a distributed, hierarchical database:
- **ROOT**: root DNS servers
- **TOP LEVEL DOMAIN**: .com DNS servers, .org DNS servers ecc
- **AUTHORITATIVE**: yahoo.com DNS servers, google.com DNS servers, pbs.org DNS servers ecc
### 2.3.3 ICANN
The distributed DNS server is managed by  ***Internet Corporation for Assigned Names and Numbers*** (***ICANN***), which also defines what the **top layer domains*** are.
### 2.3.4 Local DNS name servers
Also called *default name server*, these are installed into each ISP and they act as a sort of proxy DNS server, they have a local cache of recent name-to-address translations pairs, BUT it may be out of date!

>Local DNS servers use the user-server paradigm, but use **UDP** connections.
### 2.3.5 Name resolution Approaches
#### Iterated Query
The contacted server replies with a list of servers to contact
This approach is better.
#### Recursive Query
Every contacted server asks the next.
More load on the servers.
### 2.3.6 DNS records
The DNS is a distributed database storing **resource records** (**RR**):
```
RR format: (name, value, type, ttl)
```
- type=A (address)
	- name is a hostname
	- value is IP addres
- type=NS (name system)
	- name is domain (what you enter in the search bar)
	- value is hostname of authoritative name server for this domain
- type=CNAME ("canonical name")
	- name is alias name for some "canonical" name (the real name)
	- value is canonical name
- type=MX
	- value is name of mailserver associated with `name`
- there are even more types
### 2.3.7 DNS protocol messages
DNS *query* and *reply* messages use the same format:
- message header:
	- identification: 16 bit number (ID) for query, reply uses the same number
	- flags:
		- query or reply
		- recursion desired
		- recursion available
		- reply is authoritative

| identification  | flags            |
| --------------- | ---------------- |
| # questions     | # answer RRs     |
| # authority RRs | # additional RRs |
| questions       |                  |
| answers         |                  |
| authority       |                  |
| additional info |                  |
nolookup command
### 2.3.8 Inserting Records into DNS
1. register name (name.topleveldomain) at **DNS registrar*** (e.g. Network Solutions)
	- provide names and IP addresses of authoritative name server (both primary and secondary)
	- registrar inserts NS and A records (RRs) into the TLD (top level domain) server
2. create the authoritative server locally with the IP address inserted into the TLD
### 2.3.9 example of DNS resolution
Requesting host (alice.iet.unipi.it) asks the local DNS server what the IP for www.networkutopia.com is.
Local DNS server contacts the root DNS server, which replies with the IP of the .com DNS server.
Local DNS server now contacts the .com DNS servers, which replies with the IP of the authoritative server for networkutopia.com.
Now the local DNS server contacts the authoritative server, which replies with the information needed, which is now rooted back towards the initial client with finally a reply to the requesting host.
# 3 P2P applications (2.5)
Every peer looks more like a powerful client from the [[Client-Server]] paradigm.
But technically every peer is on the same level.
The availability of resources this way is not guaranteed from a powerful server, but from the sheer number of peers -> ***self scalability***.
There isn't an always on server.
End systems arbitrarily communicate with each other.

>Peers request service from other peers, providing service to other peers in return.

**Indexes** are needed for mapping information to the right host locations.
## 3.1 Example applications
### 3.1.1 P2P File sharing
Peers make files they have available, asking other peers for files they need.
### 3.1.2 Instant Messaging
Usernames have to be mapped to IP address.
## 3.2 Indexes
**Indexes** are needed for mapping information to the right host locations.
A content index is a [[Database]] with `(key,value)` **pairs**.
- key is the content type
- value is the IP address
The peers query the database with the key and the database replies with values that match the key.
Peers can also insert pairs.
### 3.2.1 Centralized Index
This is a service provided by a server (or a server farm).
When a user becomes active, the application notifies the index with its IP address and a list of available files.

> The files are distributed by peers, but the search is client-server style: **Hybrid Approach**

Drawbacks:
- single point of failure
- performance bottleneck
- copyright problems
### 3.2.2 Query Flooding
This is a completely decentralized approach.
When searching for one item, a peers starts querying other peers, which in turn contact other "neighbors" (**flooding**), until one sends the item to the original peer searching for it.
**Limited-scope query flooding**:
- it reduces the query traffic.
- but decreases the probability to locate the content.
- *limited-scope*: the query flooding stop at a certain "level" of subquery (for example each query starts with $x$, the peers receiving it decrement it and sends it over and again, until $x=0$)
### 3.2.3 Hierarchical Overlay
This approach is a middle ground between centralized and completely decentralized.
Not all peers are equal, ***Super Nodes*** (***SN***) exist, these are peers with high bandwidth and high availability.
SN have **local indexes**: peers inform their SN about content they have available, and SNs form an **SN overlay net**.
Peers ask their local SN where they can find an item, SN responds with the IP of the peer with the item, or, if the item is not in the local index, the SN asks other SNs, until the item is found.
### 3.2.4 Distributed Hash Table (DHT)
This is a distributed P2P database.
> non serve saperlo per l'esame

## 3.3 How much time does it take to distribute one file to N peers?
- Server upload capacity: $u_s$
- Peer upload capacity: $u_i$ 
	- max upload rate (limiting max download rate) is $u_s + \sum u_i$
- Peer download capacity: $d_i$ 
	- minimum client download rate: $d_{min}$ 
- file size: $F$ 

time to distribute in client-server approach: $$D_{c-s} \geq \max \left\{  \frac{N*F}{u_s} , \frac{F}{d_{min}}  \right\}$$
the first component scales linearly with $N$.

time to distribute in peer-to-peer approach:$$D_{P2P} > \max \left\{  \frac{F}{u_s}  \quad ,\quad  F/d_{min} \quad , \quad N*F / (u_s + \sum u_i\right\}$$
if we suppose $\sum u_i = N * \overline u$, we have $\lim{N \to \infty} \quad N*F / (u_s + \sum u_i= \frac{F}{u}$.

So client-server scales linearly with $N$, and instead peer-to-peer tends to a limited number.
## 3.4 BitTorrent
The file that needs to be transferred gets divide into 256Kb chunks, and the peers in the torrent send and receive these chunks.

>**Torrent**: group of peers exchanging chunks of a file.
 **tracker**: tracks peers participating in the torrent.
 **Torrent Server:** server that knows the IPs of the trackers.

Chunks don't even get transferred sequentially, every chunk has an ID so the entire file gets rebuilt by the asking peer once every chunk has arrived.
### 3.4.1 Entering a Torrent
1. Alice contacts the torrent Server and gets the IP of the tracker.
2. Alice contacts the tracker and asks to be included in the torrent.
3. The tracker adds Alice to the list of peers participating to the torrent and then sends the list to Alice.
4. Alice *tries* to open TCP connections with every peer in the list.
5. Alice manages to open TCP connections with only a subset of the torrent list, the peers she manages to connect with are called **neighbors**. Peers are divided in ***leeches*** (ones who don't have a complete copy of the file), ***seeders*** (ones who have every chunk) and ***free-riders*** (who only want to download the file, not seed the file).
6. Alice asks now her neighbors what chunks they have.
7. Alice asks first for the **rarer** chunks, the ones that are scarse in the "neighborhood". This approach is called **rarest first**.
8. Now that Alice has some chunks, other neighbors ask her for chunks, she now has to choose which neighbors to send the chunks to. She now adopts the **tit for tat** approach, she starts with sending the data to the **4** neighbors sending her chunks at the highest rate.
	- Other peers are **choked** by Alice.
	- Alice re-evaluates the top 4 peers every 10 seconds.
9. Every 30 seconds Alice randomly selects another peer for sending to: she "**optimistically unchokes**" this peer. This new peer may also join the top 4.
# 4 Video streaming and content distribution networks (2.6)
The video stream traffic is the major consumer of internet bandwidth.
Content Distribution services are responsible for 80% of residential ISP traffic (data from 2020).

Two challenges:
- how do we scale to ~1 billion users?
- heterogeneity: different users have different capabilities
The solution is **distributed, application-level infrastructure**.
## 4.1 Coding
We can use redundancy within and between frames to decrease the number of bits used to encode the image.
- **spatial coding**: instead of sending $N$ values of the same color, just send the color and the number if times it repeats ($N$).
- **temporal coding**: instead of sending the complete $i+1$ frame, just send the differences from the $i$ frame
## 4.2 Challenges of streaming
- server-to-client bandwidth will vary over time.
- packet loss will also vary over time #ricontrolla

In an ideal world the servers send one frame every 1/30th of a second, the user receives one frame at the same interval, with a fixed network delay, and displays the frames at the correct framerate.
**Network delay though is variable**! Solution: clients stores the received frames and displays them at the correct framerate with a "video reproduction delay".
## 4.3 Compression
An important characteristic of video is that it can be compressed, trading quality with lower file sizes.
Today we have algorithms that can compress videos to any desired bit-rate, the higher the bitrate the higher the quality and the overall user viewing experience.

Compressed video typically ranges between 100 kbps to over 10 Mbps for 4k streaming. This amounts to a huge amount of traffic and storage: a single 2 Mbps video of a duration of 67 minutes will consume 1 GB of storage and traffic ($\text{size}=\text{bitrate}*\text{time([s])}$).
In order to provide continuous playout, the network must provide an avera end-to-end throughput to the streaming application that is at least as large as the desired bitrate for the video.

We can use compression to create and store the same video at different bitrates, so that the streaming application (user) can choose which one to request based on the internet throughput it knows can achieve.
## 4.4 HTTP streaming (2.6.2)
The video is simply stored at an HTTP server as an ordinary file with its URL. When an user wants that video, it establishes a TCP connection with the server and issues an HTTP HGET request for that URL.
The server then sends the video file within an HTTP response message, as quickly as the network allows.
On the client side the bytes are **buffered**, once the number of collected bytes achieve a predetermined threshold, the client application begins playback:
the streaming application gets the bytes from the streaming buffer, decompresses them into frames, and plays them back at the right framerate on the user's screen, all while continuing to receive new information (the video) from the server.
This way of streaming has worked well but it has a shortcoming: every user receives the same video, independently from its network capability.
### 4.4.1 Dynamic Adaptive Streaming over HTTP (DASH)
In DASH the video gets stored on the server at different bitrates (every version is a different file so it has a different URL), the streaming application dynamically chooses chunks of a few seconds of the video in whatever bitrates it deems adequate.
The HTTP server has a **manifest file**, which provides an URL for each version of the video along with its bitrate.
1. The client requests the manifest file
2. the client requests a chunk of the video at a desired bitrate
3. while downloading the chunk the client measures the received bandwidth and runs a rate determination algorithm to select the chunk to request next.
## 4.5 Content Distribution Networks (CDNs) (2.6.3)
For a content provider the simplest approach would be to just build a single capable server, but has many drawbacks (single point of failure, popular media sent many times over the same network, congestion ecc), thereby the applied strategy is to build servers all around the world, that sort of act like proxies, in which they store the most requested files in their area of operation.
The user ask the generale server where it can find the file and the server redirects it to a server near the client which has that piece of media stored. If there is no such server near the client CDNs utilize the *PULL* approach: the main server will quickly send the media to one of the servers accessible by the client, who will then download the file from the latter. When a server is full it removes the less frequently requested files.

There are two different approaches:
- **Enter deep**: building many servers and incorporate them near access ISPs, improving user perceived delay and overall user experience.
- **Bring home**: building many servers but less than the previous approach and employing them near IXPs. This results in lower maintenance needed compared to "enter deep".