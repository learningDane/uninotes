#uni 
*Problem*: internet hosts and routers have both
- a IP address ([[IPv4]]), used for addressing datagrams
- a "name", used by humans (like www.google.com)
How do we map between IP address and name, and vice versa?
*solution*: the DNS

The ***Domain Name System*** (DNS) is a *distributed database* implemented in hierarchy of many *name servers*.
Application-layer protocol: hosts and name servers communicate to *resolve* names (addres-name translation).

***Registering*** a subdomain means linking it univocally to a IP address, registering it in the DNS database.
# DNS services
- hostname to IP address **translation**
- host *aliasing*
- mail server aliasing
- *load distribution*
	- replicated web servers: many IP addresses correspond to one name
# DNS structure
The DNS is a distributed, hierarchical database:
- **ROOT**: root DNS servers
- **TOP LEVEL DOMAIN**: .com DNS servers, .org DNS servers ecc
- **AUTHORITATIVE**: yahoo.com DNS servers, google.com DNS servers, pbs.org DNS servers ecc
# ICANN
The distributed DNS server is managed by  ***Internet Corporation for Assigned Names and Numbers*** (***ICANN***), which also defines what the **top layer domains*** are.
# Local DNS name servers
Also called *default name server*, these are installed into each ISP and they act as a sort of proxy DNS server, they have a local cache of recent name-to-address translations pairs, BUT it may be out of date!

>Local DNS servers use the user-server paradigm, but use **UDP** connections.
# Name resolution Approaches
### Iterated Query
The contacted server replies with a list of servers to contact
This approach is better.
### Recursive Query
Every contacted server asks the next.
More load on the servers.
# DNS records
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
# DNS protocol messages
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
# Inserting Records into DNS
1. register name (name.topleveldomain) at **DNS registrar*** (e.g. Network Solutions)
	- provide names and IP addresses of authoritative name server (both primary and secondary)
	- registrar inserts NS and A records (RRs) into the TLD (top level domain) server
2. create the authoritative server locally with the IP address inserted into the TLD
# example of DNS resolution
Requesting host (alice.iet.unipi.it) asks the local DNS server what the IP for www.networkutopia.com is.
Local DNS server contacts the root DNS server, which replies with the IP of the .com DNS server.
Local DNS server now contacts the .com DNS servers, which replies with the IP of the authoritative server for networkutopia.com.
Now the local DNS server contacts the authoritative server, which replies with the information needed, which is now rooted back towards the initial client with finally a reply to the requesting host.