#uni 
It stands for (HyperText Transfer Protocol).
This protocol is based on the [[Client-Server]] paradigm.
Two type of http messages:
- *request*
- *response*
the message format is **ASCII**
After a a timeout the connection is closed automatically
TCP connection consume memory and leave them open leaves the data structures allocated waisting memory
# Status Codes
there are multilple status codes for http responses
- 200 -> Ok
	- request succeeded
- 301 -> Move Permanently
	- requested object is moved, new location is specified later in the message with the tag `Location` 
- 400 -> Bad Request
	- request msg not understood by the server
- 404 -> Not Found 
	- requested document not found on this server
- 505 -> HTTP version not supported
# TELNET
`telnet <host> <port>` cli command open a tcp connection to the specified url and port
	type `GET <url>` HTTP/1.1 to make a get request then press enter
	type  `Host: <host>` and press enter twice so have the response

# Cookies
Used by some browers to maitain some state between transactions
Four Components:
- **Cookie Header Line** of http response message
- **Cookie Header Line** of http request message
- **Cookie File** kept on the user's end system
- **Back-End Database** at the Web site

The client make a simple http request to a server
The server creates and ID for the user and store it in a database

This means that the next time you make a http request the server know who you are
This is how website can keep you logged in even when the website is closed

They have various implementations:
- Authorizations
- Shopping Carts
- Reccomendations
- User session state (web, e-mail)

The question is *How do we keep the state?*
	protocol endpoints: maintain state at sender/reciever over multiple tansactions
	cookies: HTTP messages carry state

The Cookies permits the sistes to learn about you on their site
Third party persistent cookie allow common identity to be tracked across multiple web sites

# Web Caches (proxy servers)
*Goal*: satisfy client request without involving origin server
*Why*: to alleviate the load on origin servers. Caches are closer to clients so it reduces response time. Caches also alleviate the load on internet as a whole.
The user configures the browser to point to a **web cache**.
- if the objects is in the cache: the cache return object to client
- if the object isn't in cache: the cache ask and receives the object from the origin server, caches it and sends it to client

Proxy servers act both as a client and as a server. They are typically installed by ISP.
### Problem of recency of cached objects
What do we do if the object is updated on the remote servers and the proxy server isn't aware?
**Conditional GET**:
goal: don't send object if cache has up-to-date version
- Cache: the cache when sending the GET statement includes the version of the cached copy:
  `if-modified-since:<date>`
- Server: response contains no object if the cached copy is up to date:
  `http/1.0 304 Not Modified`
# Important updates
### HTTP 1.1
In this versione the scheduling algorithm for GET requests is **FCFS**: first come first served.
Issue: small objects may wait for bigger (slower) objects (requests) (==HOL blocking==: **Head of line blocking**). Also loss recovery (retransmitting lost TCP segments) stalls object transmission.
### HTTP 2
RFC 7540, 2015: The key goal for this version was decreasing delay in multi-object HTTP requests.
Increased the flexibility for servers when sending objects to clients:
Objects are divided into frames and the frame transmission is interleaved.
Problems: recovery still stalls transmission, also no extra security over vanilla TCP connections.
### HTTP 3
Adds
- security
- per object error (and congestion) control (more pipelining) over UDP
