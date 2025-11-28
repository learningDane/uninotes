---
number headings: auto, first-level 1, max 3, 1.1
---
#uni 
# 1 Context
There are much more wireless phone subscribers than wired phone subscribers.
The are much more mobile-broadband-connected devices than fixed-broadband-connected devices.
We need to face two different challenges:
- wireless: communication over wireless link
- mobility: handling the mobile user who changes point of attachment to the network
# 2 Introduction
## 2.1 Elements of a wireless network
- Wireless Hosts
	- laptop, smartphone, IoT
	- these run applications
	- these may be stationary (non-mobile) or mobile
		- wireless does not always mean mobility! (a laptop that never leaves the office but is connected via wifi is wireless but not mobile)
- Base Station / Wifi Access Points
	- these are typically connected to the wired network
	- these are a relay: they are responsible for sending packets between the wired network and the wireless hosts in its "area"
- Wireless Link
	- they are typically used to connect mobile users to the base stations
	- multiple access protocol coordinate the link access
	- various transmission rates, distances and frequency bands
## 2.2 Characteristics of different wireless links
Different wireless Links have different characteristics, link bandwidth and range:![[Pasted image 20251128120618.png]]
- WiFi is the commercial name for the 802.11 technology
- Bluetooth is the commercial name for the 802.15.1 technology: short range, low energy, "high" (lol) bandwidth
	- 802.15.4 is short range, low energy and low bandwidth
## 2.3 Classification of Wireless Networks
There are different classes of wireless networks:
- Infrastructured Mode:
	- the base station connects mobiles into a wired network
	- **handoff**: mobiles when moving change the base station providing connection into the wired network, the change is called handoff
- Ad hoc Mode:
	- no base stations
	- nodes can only transmit to other nodes within link coverage
	- nodes organize themselves into a network and route among themselves
### 2.3.1 Wireless Network Taxonomy
<table>
	<tr> <th></th><th>Single Hop</th><th>Multiple Hops</th>
	</tr> <tr> <td>Infrastructure-based</td>
	<td>Host connects to base station which connects to the larger internet: WiFi, cellular networks</td>
	<td>Host may have to relay through several wireless nodes to connect to the larger internet: <it>sensor networks</it></td> </tr> <tr>
	<td><it>Ad Hoc</it></td>
	<td>No base station, no connection to the larger internet: <it>Bluetooth</it></td>
	<td>No base station, no connection to larger internet. May have torelay each other a given wireless node: <it>MANET,VANET</it></td></tr>
</table>
# 3 Wireless
## 3.1 Wireless Links and network characteristics
## 3.2 Wireless LANs: WiFi
## 3.3 Wireless PANs: Bluetooth
## 3.4 Cellular networks: 4G and 5G
# 4 Mobility
## 4.1 Mobility management: principles
## 4.2 Mobility: impact on higher-layer protocols