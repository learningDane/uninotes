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