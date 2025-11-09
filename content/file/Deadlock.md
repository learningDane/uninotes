#uni 
# The deadlock problem
# Deadlocks
Prevenzione statica: preemption
Prevenzione dinamica: deadlock avoidance

A deadlock is a set of blocked processes each holding a resource and waiting to acquire a resource held by another process in the set.

An arrow from $P_0$ to $A$ means the process $P_0$ called a `wait(A)`.
An arrow from $B$ to $P_1$ means the process $P_1$ has control of the resource $B$.
If we map like this and we get a cycle, this means we currently have a deadlock.
# System Model
A system has resource types $R_1,R_2,...,R_m$ 
	These can be [[CPU]] cycles, memory space, I/O devices..

Each resource type $R_i$ has $W_i$ instances.

Each process utilizes a resource as follows:
- **request**
- **use**
- **release**

# Deadlock Characterization
A deadlock can occur if these four conditions hold simultaneously:
- **mutual exclusion**
- **hold and wait**: a process holding at least one resource is waiting to acquire additional resources held by other processes
- **no preemption**
- **circular wait** (cycle)
## Resource-Allocation Graph
An arrow from $P_0$ to $A$ means the process $P_0$ called a `wait(A)`.
An arrow from $B$ to $P_1$ means the process $P_1$ has control of the resource $B$.
## Basic Facts
- If a graph contains no cycles $\implies$ no deadlock.
- If a graph contains a cycle:
	- if only there is one instance per resource type $\implies$ deadlock
	- if several instances per resource type $\implies$ possibility of deadlock
# Methods for handling Deadlocks
Methods can be:
- ensuring that the system will **never** enter a deadlock state
- allow the system to ender a deadlock and then recover
- ignore the problem and pretend that deadlock never occur in the system: this is used by most operating systems, including [[Unix]] 
## Deadlock Prevention
Prevention is done by restraining the ways requests can be made:
- **mutual exclusion**: this is not required for sharable resources, but must hold for nonsharable resources
- **hold and wait**: must guarantee that whenever a process request a resource it does not hold any other resource
	- require processes to request and get allocated all the resources it will need, before it begins execution, or only allow processes to request resources when they have none
	- low resource utilization: starvation possible
- **no preemption**: 
	- if a process that is holding some resources request another resource that cannot be immediately allocated to it, then all the resource currently being held are released
	- preempted resources are added to the list of resource for which the process is waiting
	- the process will be restarted only when it can regain its old resources, as well as the new ones that it is requesting
- **circular wait**: impose a total ordering of all resource types, and require that each process reqeust resources in an increasing order of enumeration: "if $P$ already holds $R_k$, it cannot request $R_{k-i}$"
## Deadlock Avoidance
Requires that the system has some additional *a priori* information available:
- the simplest and most useful model requires that each process declares the *maximum number* of resources of each type that it may need
- this avoidance algorithm dynamically examines the resource-allocation state to ensure that there can never be a *circular-wait condition*
- the **resource-allocation *state***  is defined by: 
	- the number of available allocated resources
	- the maximum demands of the processes
### Safe State
The System is in a **safe state** if there exists a sequence of ALL processes in the systems such that for each process, the resource that it can still request can be satisfied by the currently available resource or the resources held by all processes scheduled before it.

When a process requests an available resource, the system must decide if immediate allocation leaves the system in a safe state.

So if a processe's resource needs cannot be immediately met, this process waits for all the processes before it that hold resources it would need. When these processes finish, their resources get returned to the system and the process that was waiting can be executed.

> The *deadlock state* is a **subset** of the *unsafe states set*.
#### Basic Facts
- If a system is in *safe state* $\implies$ no deadlocks
- if a system is in *unsafe state* $\implies$ possibility of deadlocks
- avoidance $\implies$ ensuring that the system will *never* enter an unsafe state
### Avoidance Algorithms
Single instance of a resource type: use a resource-allocation graph.

Multiple instances of a resource type: use the **banker's algorithm**.
#### Resource-Allocation Graph Scheme
- **Claim edge** $P_i \to R_j$ indicated that process $P_j$ may request resource $R_j$; represented by a *dashed* line
- Claim edge converts to **request edge** when a process requests a resource
- Request edge converted to an **assignment edge** when the is allocated to the process resource
- When a resource is released by a process, assignment edge reconverts to a claim edge
- Resources must be claimed *a priori* in the system

If a process has an outgoing request edge, it is *bloccato*.
##### Algorithm
Suppose that process $P_i$ requests a resource $R_j$: the request can be granted only if converting the request edge to an assignment edge does not result in the formation of a cycle in the resource allocation graph.
#### Banker's Algorithm
This algorithm is used when having multiple instances of a resource type.

- Each process must *a priori* claim its maximum resource use
- when a process request a resource it may have to wait
- when a process gets all its resources *it must return them in a finite amount of time* 
##### Data Structures for the Banker's Algorithm
Let `n = number of processes` and `m = number of resources type`.
- **Available**: Vector of length `m`. If `Available[j] = k`, there are $k$
instances of resource type $R_j$ available
- **Max**: $n \times m$ matrix. If `Max[i,j] = k`, then process $P_i$ may request at
most $k$ instances of resource type 
- **Allocation**: $n \times m$ matrix. If `Allocation[i,j] = k` then $P_i$ is currently
allocated $k$ instances of $R_j$
- **Need**: $n \times m$ matrix. If `Need[i,j] = k`, then $P_i$ may need $k$ more
instances of $R_j$ to complete its task
> we have: $$\text{Need}[i.j] = \text{Max}[i,j] - \text{Allocation}[i,j]$$

##### Safety Algorithm
1. Let `Work` and `Finish` be vectors of length $m$ and $n$, respectively. Initialize:
	- `Work = Available`
	- `Finish[i] = false for i = 0, 1, …, n- 1`
2. Find an $i$ such that both:
	- (a) $\text{Finish}[i]=\text{false}$
	- (b) $\text{Need}_i \leq \text{Work}$
	If no such $i$ exists, go to step `4`
3. $\text{Work} = \text{Work} + \text{Allocation}_i$
	$\text{Finish}[i]=\text{true}$
	go to step `2`
4. If $\text{Finish}[i]==\text{true} \quad \forall i$, then the system is in a safe state
##### Resource-Request Algorithm for Process $P_i$
Request = request vector for process Pi.

If $\text{Request}_i[j] = k$ then process $P_i$ wants $k$ instances of
resource type $R_j$

1. If $\text{Request}_i \leq \text{Need}_i$ go to step `2`.
   Otherwise, raise error condition, since process has exceeded its maximum claim
2. If $\text{Request}_i \leq \text{Available}$, go to step `3`. Otherwise $P_i$ must wait, since resources are not available
3. Assume to allocate requested resources to $P_i$ by modifying the state as follows:
		- $\text{Available} = \text{Available} – \text{Request}_i$;
		- $\text{Allocation}_i = \text{Allocation}_i + \text{Request}_i$;
		- $\text{Need}_i = \text{Need}_i – \text{Request}_i$;
	- If safe $\implies$ the resources are allocated to $P_i$
	- If unsafe $\implies$ $P_i$ must wait, and the old resource-allocation state is restored
## Deadlock Detection
# Recovery from Deadlock