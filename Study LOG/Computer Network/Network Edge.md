## Network Edge
- Hosts : clients and servers
	- host sending function
		- takes application message
		- breaks into smaller chunks, known as packets, of length `L` bits
		- transmits packet into access network at transmission rate `R`
			- link transmission rate, aka link capacity, aka link bandwidth
			- $$ packet\ transmission\ delay = time\ needed\ to\ transmit\ L-bit\ packet\ into\ link = \frac{L\ (bits)}{R\ (bits/sec)} $$
- Links: physical media
	- bit : propagates between transmitter/receiver pairs
	- physical link: what lies between transmitter & receiver
	- guided media: signals propagate in solid media: copper, fiber, coax
	- unguided media: signals propagate freely, (e.g. radio)
	- Twisted pair (TP)
		- two insulated copper wires
			- Category 5 : 100 Mbps, 1 Gbps Ethernet
			- Category 6 : 10 Gbps Ethernet
	- Coaxial cable
		- two concentric copper conductors
		- bidirectional
		- broadband
			- multiple frequency channels on cable
			- 100's Mbps per channel
	- Fiber optic cable
		- glass fiber carrying light pulses, each pulses a bit
		- high-speed operation:
			- high-speed point-to-point transmission (10's-100's Gbps)
		- low error rate:
			- repeaters spaced far apart
			- immune to electromagnetic noise
	- Wireless radio
		- signal carried in various "bands" in electromagnetic spectrum
		- no physical "wire"
		- broadcast, "half-duplex"(sender to receiver)
		- propagation environment effects:
			- reflection
			- obstruction by objects
			- interference/noise
	- Radio link types:
		- Wireless LAN (WiFi)
			- 10-100's Mbps; 10's of meters
		- wide-area (e.g. 4G/5G cellular)
			- 10's Mbps (4G) over ~10km
		- Bluetooth: cable replacement
			- short distances, limited rates
		- terrestrial microwave
			- point-to-point; 45 Mbps channels
		- satellite
			- up to < 100 Mbps (Starlink) downlink
			- 270 msec end-end delay (geostaionary)
- servers often in data centers

### Access Networks, Physical Media
- wired, wireless communication links

- How to connect end systems to edge router?
	- residential access nets
	- institutional access networks (school, company)
	- mobile access networks (WiFi, 4G/5G)
- What to look for
	- transmission rate (bits per second) of access network?
	- shared or dedicated access among users?
#### Access Network: Cable-Based Access
- Frequency division multiplexing (FDM) : different channels transmitted in different frequency bands
- Hybrid Fiber Coax (HFC) : asymmetric: up to 40 Mbps - 1.2 Gbps downstream transmission rate, 30-100 Mbps upstream transmission rate
- network of cable, fiber attaches homes to ISP router
	- homes share access network to cable headend
#### Access Network: Digital Subscriber Line(DSL)
- use existing telephone line to central office DSLAM
	- data over DSL phone line goes to Internet
	- voice over DSL phone lines goes to telephone net
- 24-52 Mbps dedicated downstream transmission rate
- 3.5-16 Mbps dedicated upstream transmission rate
#### Access Network: Home Networks
#### Wireless Access Networks
- shared wireless access network connects end system to router
	- via base station aka "access point"
###### Wireless local area networks (WLANs)
- typically within or around building (~100ft)
- 802.11b/g/n (WiFi): 11, 54, 450Mbps transmission rate
###### Wide-area cellular access networks
- provided by mobile, cellular network operator (10's km)
- 10's Mpbs
- 4G/5G cellular networks

#### Access Network: Enterprise Networks
- companies, universities, etc.
- mix of wired, wireless link technologies, connecting a mix of switches and routers
	- Ethernet: wired access at 100Mbps, 1Gbps, 10Gbps
	- WiFi: wireless access points at 11, 54, 450 Mbps

#### Access Network: Data Center Networks
- high-bandwidth links (10s to 100s Gbps) connect hundreds to thousands of servers together, and to Internet
#### Network Core
- mesh of interconnected routers
- network of networks
- packet-switching: hosts break application-layer messages into packets
	- network forwards packets from one router to the next, across links on path from source to destination
- Two key network-core functions
	- Forwarding
		- aka "switching"
		- local action: move arriving packets from router's input link to appropriate router output link
	- Routing
		- global action: determine source-destination paths taken by packets
		- routing algorithms
- Packet-switching: store-and-forward
	- packet transmission delay: takes L/R seconds to transmit (push out) L-bit packet into link at R bps
	- store and forward: entire packet must arrive at router before it can be transmitted on next link
- Packet-switching: queueing
	- Queueing occurs when work arrives faster than it can be serviced:
	- Packet queueing and loss: if arrival rate (in bps) to link exceeds transmission rate (bps) of link for some period of time:
		- packets will queue, waiting to be transmitted on output link
		- packets can be dropped (lost) if memory (buffer) in router fills up
- Alternative to packet switching: circuit switching
	- end-end resources allocated to, reserved for "call" between source and destination
		- in diagram, each link has four circuits.
			- call gets 2nd circuit in top link and 1st circuit in right link
		- dedicated resources: no sharing
			- circuit-like (guaranteed) performance
		- circuit segment idle if not used by call (no sharing)
		- commonly used in traditional telephone networks
- Circuit switching: FDM and TDM
	- Frequency Division Multiplexing (FDM)
		- optical, electromagnetic frequencies divided into (narrow) frequency bands
		- each call allocated its own band, can transmit at max rate of that narrow band
	- Time Division Multiplexing (TDM)
		- time divided into slots
		- each call allocated periodic slot(s), can transmit at maximum rate of (wider) frequency band (only) during its time slot(s)
- Packet switching versus circuit switching
	- How many users can use this network under circuit-switching and pack switching?
		- circuit-switching : 10 users
		- packet switching : with 35 users, probability > 10 active at same time is less than .0004 *
	- Is packet switching a "slam dunk winner"
		- great for "bursty" data - sometimes has data to send, but at other times not
			- resource sharing
			- simpler, no call setup
		- excessive congestion possible: packet delay and loss due to buffer overflow
			- protocols needed for reliable data transfer, congestion control
		- How to provide circuit-like behavior with packet-switching?
			- "It's complicated." There are techniques that try to make packet switching as "circuit-like" as possible such as virtual circuit, packet prioritization
		- Human analogies of reserved resources (circuit switching) versus on-demand allocation (packet switching)?
