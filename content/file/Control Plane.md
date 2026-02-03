---
number headings: auto, first-level 1, max 3, 1.1
---
- [[#1 Introduction|1 Introduction]]
- [[#2 Routing Protocols|2 Routing Protocols]]
	- [[#2 Routing Protocols#2.1 Link Cost|2.1 Link Cost]]
	- [[#2 Routing Protocols#2.2 Routing protocols classification|2.2 Routing protocols classification]]
	- [[#2 Routing Protocols#2.3 Link state Algorithms|2.3 Link state Algorithms]]
		- [[#2.3 Link state Algorithms#2.3.1 Dijkstra|2.3.1 Dijkstra]]
	- [[#2 Routing Protocols#2.4 Distance Vector Algorithms|2.4 Distance Vector Algorithms]]
		- [[#2.4 Distance Vector Algorithms#2.4.1 Algorithm|2.4.1 Algorithm]]
		- [[#2.4 Distance Vector Algorithms#2.4.2 Cost Update|2.4.2 Cost Update]]
	- [[#2 Routing Protocols#2.5 LS vs DV algorithms|2.5 LS vs DV algorithms]]
- [[#3 Intra-ISP routing: OSPF|3 Intra-ISP routing: OSPF]]
- [[#4 Routing between ISPs: BGP|4 Routing between ISPs: BGP]]

#uni 
# 1 Introduction
There are two approaches for structuring the control plane:
- per-router control (traditional method)
- logically centralized control (SDN: Software Defined Networking)
# 2 Routing Protocols
Routing protocols must determine "good" paths from the sender host to the receiver, through network routers:
- **path**: sequence of routers between sender and receiver
- "**good**": the least expensive, the least congested, the fastest
## 2.1 Link Cost
$c_{a,b}$ cost of the *direct* link between $a$ and $b$.
The cost is defined by the network provider: it can be based on bandwidth, congestion ecc.
Today the most accurate way to determine the link's cost is based on the retransmission needed on said link.
$$
\begin{matrix}
N: \text{router nodes}=\{ u,v,w,x,y,z \}
E: \text{links}=\{ (u,v),(u,x),(v,x), \text{ecc} \}
\end{matrix}
$$
## 2.2 Routing protocols classification
> routing algorithms classification: ![[routingalgorithmsclassification.svg]]
## 2.3 Link state Algorithms
### 2.3.1 Dijkstra
The Dijkstra algorithm is centralized: every node knows the network topology and every link's cost.
This means we need a first phase for synchronizing information, where nodes exchange "link state broadcast" messages.
This algorithm computes the least expensive route between a source node and every other, this means it returns the **forwarding table** for the source node.
This is a iterative algorithm, after $k$ iterations we know the least expensive path from the source node to $k$ destinations.
#### Notation
- $C_{x,y}$: direct link's cost, $=\infty$ if $x,y$ are not directly connected
- $D(v)$: current cost estimate for the path between the source node and the destination $v$ 
- $p(v)$: predecessor node along the path to $v$ 
- $N'$: set of nodes for which the least expensive path is known
#### Complexity
Normally Dijkstra's algorithm has $O(n^2)$ complexity, but with the aid of the *heap* we can get it as low as $O(n\cdot \log n)$.

We also need to take into account the broadcast phase, this has $O(n^2)$ complexity.
#### Considerations
When traffic soares in a network, the costs change and the routes need to get computed again: **routes' oscillation**.
## 2.4 Distance Vector Algorithms
These algorithm are based on the **Bellman-Ford** (**BF**) equation (dynamic programming): 
$$
\begin{matrix}
D_x(y):\text{cost of the least-cost path from } x \text{ to } y. \\
\implies D_x(y)=\min_v \{ c_{x,y}+D_v(y) \} \quad \forall y \in N\\
\min_v: \text{minimum taken between }x\text{'s neighbors } v 
\\
c_{x,y}: \text{direct link cost of }x,y
\\
D_v(y):\text{least-cost path from } v \text{ to } y \text{ estimate}
\end{matrix}
$$
The idea is every once in a while, every node broadcasts the estimate of the distance vector to his neighbors $D_v$.
When a node receives a new $D_v$ from a neighbor, it updates its $D_v$ using the BF equation.
In normal conditions, the $D_x(y)$ estimate converges to the least-cost $d_x(y)$.
### 2.4.1 Algorithm
Every node:
1. *wait* for local links' cost variation or message from neighbors
2. *recompute* $D_v$ estimate
3. if $D_v$ changed for a destination, notify the neighbors

This algorithm is:
- iterative
- asynchronous
- distributed
- self-stopping
### 2.4.2 Cost Update
#### Poisoned inversion
If $z$ passes through $y$ to get to $x$:
1. $z$ notifies $y$ that the cost $z,y$ is $\infty$ 
	1. $D_z(x)=\infty$ even if $z$ knows this is not the case
	2. until $z$ gets to $x$ passing through $y$, it will continue to announce $(z,y)=\infty$ 
2. $y$ will think that $z$ doesn't have a path to $x$, therefore the cycle will not be created, and the costs will be communicated correctly

N.B.: this technique works only for solving cycles creating between adjacent nodes.
## 2.5 LS vs DV algorithms
Complexity:
- LS: for $n$ nodes we have $O(n^2)$ sent messages
- DV: exchanges between neighbors, time varies

Speed of convergence:
- LS: $O(n^2)$, there may be oscillations
- DV: time of convergence varies, also count-to-infinity problem

Robustness:
- LS: routers can notify other routers with incorrect data, every router has its table
- DV: **black-holing**: routers can communicate incorrect path costs ("i have low cost paths to every node"), error gets propagated along the network
# 3 Intra-ISP routing: OSPF
# 4 Routing between ISPs: BGP