#uni 
Every peer looks more like a powerful client from the [[Client-Server]] paradigm.
But technically every peer is on the same level.
The availability of resources this way is not guaranteed from a powerful server, but from the sheer number of peers -> ***self scalability***.
There isn't an always on server.
End systems arbitrarily communicate with each other.

>Peers request service from other peers, providing service to other peers in return.

**Indexes** are needed for mapping information to the right host locations.
# Example applications
### P2P File sharing
Peers make files they have available, asking other peers for files they need.
### Instant Messaging
Usernames have to be mapped to IP address.
# Indexes
**Indexes** are needed for mapping information to the right host locations.
A content index is a [[Database]] with `(key,value)` **pairs**.
- key is the content type
- value is the IP address
The peers query the database with the key and the database replies with values that match the key.
Peers can also insert pairs.
### Centralized Index
This is a service provided by a server (or a server farm).
When a user becomes active, the application notifies the index with its IP address and a list of available files.

> The files are distributed by peers, but the search is client-server style: **Hybrid Approach**

Drawbacks:
- single point of failure
- performance bottleneck
- copyright problems
### Query Flooding
This is a completely decentralized approach.
When searching for one item, a peers starts querying other peers, which in turn contact other "neighbors" (**flooding**), until one sends the item to the original peer searching for it.
**Limited-scope query flooding**:
- it reduces the query traffic.
- but decreases the probability to locate the content.
- *limited-scope*: the query flooding stop at a certain "level" of subquery (for example each query starts with $x$, the peers receiving it decrement it and sends it over and again, until $x=0$)
### Hierarchical Overlay
This approach is a middle ground between centralized and completely decentralized.
Not all peers are equal, ***Super Nodes*** (***SN***) exist, these are peers with high bandwidth and high availability.
SN have **local indexes**: peers inform their SN about content they have available, and SNs form an **SN overlay net**.
Peers ask their local SN where they can find an item, SN responds with the IP of the peer with the item, or, if the item is not in the local index, the SN asks other SNs, until the item is found.
### Distributed Hash Table (DHT)
This is a distributed P2P database.
> non serve saperlo per l'esame

# How much time does it take to distribute one file to N peers?
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
# BitTorrent
The file that needs to be transferred gets divide into 256Kb chunks, and the peers in the torrent send and receive these chunks.

>**Torrent**: group of peers exchanging chunks of a file.
 **tracker**: tracks peers participating in the torrent.
 **Torrent Server:** server that knows the IPs of the trackers.


Chunks don't even get transferred sequentially, every chunk has an ID so the entire file gets rebuilt by the asking peer once every chunk has arrived.

### Entering a Torrent
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