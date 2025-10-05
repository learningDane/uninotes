#uni 
*Problem*: internet hosts and routers have both
- a IP address ([[IPv4]]), used for addressing datagrams
- a "name", used by humans (like www.google.com)
How do we map between IP address and name, and vice versa?
*solution*: the DNS

The ***Domain Name System*** (DNS) is a distributed database implemented in hierarchy of many *name servers*.
Application-layer protocol: hosts and name servers communicate to *resolve* names (addres-name translation).
Managed by  ***Internet Corporation for Assigned Names and Numbers*** (***ICANN***), which also defines what the **top layer domains*** are.

***Registering*** a subdomain means linking it univocally to a IP address, registering it in the DNS database.
# DNS services
- hostname to IP address **translation**
- host *aliasing*
- mail server aliasing
- *load distribution*
	- replicated web servers: many IP addresses correspond to one name