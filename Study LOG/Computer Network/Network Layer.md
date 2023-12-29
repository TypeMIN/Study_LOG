## Network layer services and protocols
- transport segment from sending to receiving host
	- sender
		- encapsulates segments into datagrams, passes to link layer
	- receiver
		- delivers segments to transport layer protocol
- network layer protocols in every Internet devices:
	- hosts
	- routers
		- examines header fields in all IP datagrams passing through it
		- moves datagrams from input ports to output ports to transfer datagrams along end-end path

## Two key network layer function
- network layer functions:
	- forwarding:
		- move packets from a router's input link to appropriate router output link
	- routing:
		- determine route taken by packets from source to destination
			- routing algorithms
- analogy: taking a trip
	- forwarding:
		- process of getting through single interchange
	- routing:
		- process of planning trip from source to destination

## Network layer : Data plane, Control Plane
- Data plane:
	- local, per-router function
	- determines how datagram arriving on router input port is forwarded to router output port
- Control plane:
	- network-wide logic
	- determines how datagram is routed among routers along end-end path from source host to destination host
	- two control plane approaches:
		- traditional routing algorithms:
			- implemented in routers
		- software-defined networking (SDN):
			- implemented in (remote) servers

## Packet Scheduling
- FCFS
	- packets transmitted in order of arrival to output port (a.k.a FIFO)
- Priority scheduling
	- arriving traffic classified, queued by class
		- any header fields can be used for classification
	- send packet from highest priority queue that has buffered packets
		- FCFS within priority class
- Round robin scheduling:
	- arriving traffic classified, queued by class
		- any header fields can be used for classification
	- server cyclically, repeatedly scans class queues, sending one complete packet from each class (if available) in turn
- Weighted Fair Queuing (WFQ):
	- generalized Round Robin
	- each class, i, has weight, wi, and gets weighted amount of service in each cycle:
	- minimum bandwidth guarantee (per-traffic-class)

## IP addressing
- IP address
	- 32-bit identifier associated with each host or router interface
- interface
	- connection between host/router and physical link
		- router's typically have multiple interfaces
		- host typically has one or two interfaces
- how does host get IP address?
	- hard-coded by sysadmin in config file
	- DHCP (Dynamic Host Configuration Protocol)
		- dynamically get address from as server
		- "plug-and-play"
## Subnets
- subnet
	- device interfaces that can physically reach each other without passing through an intervening router
- IP address have structure
	- subnet part
		- devices in same subnet have common high order bits
	- host part
		- remaining low order bits
- recipe for defining subnets
	- detach each interface from its host or router, creating "islands" of isolated networks
	- each isolated network is called a subnet

## CIDR (Classless InterDomain Routing)
- subnet portion of address of arbitrary length
- address format: a.b.c.d/x, where x is # bits in subnet portion of address

## DHCP (Dynamic Host Configuration Protocol)
- Goal : host dynamically obtains IP address from network server when it "joins" network
	- can renew its lease on address in use
	- allows reuse of addresses
	- support for mobile users who join/leave network
- DHCP overview:
	- host broadcasts DHCP discover msg
	- DHCP server responds with DHCP offer msg
	- host requests IP address : DHCP request msg
	- DHCP server sends address : DHCP ack msg

## NAT (Network Address Translation)
- all devices in local network share just one IPv4 address as far as outside world is concerned
- all devices in local network have 32-bit addresses in a "private" IP address space (10/8, 172.16/12, 192.168/16 prefixes) that can only be used in local network
- advantages:
	- just one IP address needed from provider ISP for all devices
	- can change addresses of host in local network without notifying outside world
	- can change ISP without changing addresses of devices in local network
	- security: devices inside local net not directly addressable, visible by outside world
- implementation:
	- outgoing datagrams
		- replace (source IP address, port #) of every outgoing datagram to (NAT IP address, new port #)
			- remote clients/servers will responding using (NAT IP address, new port #) as destination address
	- remember (in NAT translation table) every (source IP address, port #) to (NAT IP address, new port #) translation pair
	- incoming datagrams
		- replace (NAT IP address, new port #) in destination fields of every incoming datagram with corresponding (source IP address, port #) stored in NAT table

## Network layer functions
- forwarding (data plane)
	- move packets from router's input to appropriate router output
- routing (control plane)
	- determine route taken by packets from source to destination

## Graph abstraction
- link costs

## Routing algorithm classification
- global
	- all routers have complete topology, link cost info
	- "link state" algorithm
- static
	- routes change slowly over time
- decentralized
	- iterative process of computation, exchange of info with neighbors
		- routers initially only know link costs to attached neighbors
		- "distance vector" algorithms
- dynamic
	- router change more quickly
		- periodic updates or in response to link cost changes

## Dijkstra's link state routing algorithm
- centralized
	- network topology, link costs known to all nodes
		- accomplished via "link state broadcast"
		- all nodes have same info
	- computes least cost paths from one node ("source") to all other nodes
		- gives forwarding table for that node
	- iterative
		- after k iterations, know least cost path to k destinations
- algorithm complexity
	- each of n iteration : need to check all nodes, w, not in N
	- n(n+1)/2 comparisons : O(n^2) complexity
	- more efficient implementations possible : O(nlogn)
- message complexity
	- each router must broadcast its link state information to other n routers
	- efficient (and interesting) broadcast algorithms : O(n) link crossings to disseminate a broadcast message from one source
	- each router's message crosses O(n) links : overall message complexity : O(n^2)
- oscillations possible
	- when link cost depend on traffic volume, route oscillations possible

## Distance vector algorithm
- Bellman-Ford equation (dynamic programming)

## Making routing scalable
- Internet approach to scalable routing
	- Intra-AS(Autonomous Systems) (a.k.a. intra-domain)
		- routing among routers within same AS
			- all routers in AS must run same intra-domain protocol
			- routers in different AS can run different intra-domain routing protocols
			- gateway router
				- at "edge" of its own AS, has links to routers in other AS'es
	- inter-AS (a.k.a. inter-domain)
		- gateways perform inter-domain routing

## Intra-AS routing
- most common intra-AS routing protocols
	- RIP (Routing Information Protocol
		- classic DV
			- DVs exchanged every 30 secs
		- no longer widely used
	- OSPF (Open Shortest Path First)
		- link-state routing
		- IS-IS protocol essentially same as OSPF
	- EIGRP (Enhanced Interior Gateway Routing Protocol)
		- DV based
		- formerly Cisco-proprietary for decades

## Inter-AS routing
- BGP (Border Gateway Protocol)
	- allows subnet to advertise its existence, and the destinations it can reach, to rest of Internet
	- eBGP (externer)
	- iBGP (interner)
	- BGP protocol messages
		- OPEN
		- UPDATE
		- KEEPALIVE
		- NOTIFICATION (also used to close)
	- BGP advertised route (prefix + attributes)
		- prefix
			- destination being advertised
		- attributes
			- AS-PATH
				- list of ASes through which prefix advertisement
			- NEXT-HOP
				- indicates specific internal-AS router to next-hop AS
	- Hot potato routing
		- choose local gateway that has least intra-domain cost