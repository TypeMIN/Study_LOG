## Link layer
- Terminology
	- nodes
		- hosts, routers
	- links
		- communication channels that connect adjacent nodes along communication path
			- wired, wireless
			- LANs
	- frame
		- layer-2 packet
		- encapsulates datagram

## Transportation analogy
- trip from Princeton to Lausanne
	- tourist : datagram
	- transportsegment : communication link
	- transportation mode : link layer protocol
	- travel agent : routing algorithm

## Link layer services
- framing, link access
	- encapsulate datagram into frame, adding header and trailer
	- channel access if shared medium
	- "MAC" addresses in frame headers identify source, destination
- reliable delivery between adjacent nodes
	- we already know how to do this
	- seldom used on low bit-error links
	- wireless link
		- high error rates
- flow control
	- pacing between adjacent sending and receiving nodes
- ero