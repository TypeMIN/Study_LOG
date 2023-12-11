## Transport services and protocols
- provide logical communication between application processes running on different hosts
- transport protocols actions in end systems
	- sender : breaks application messages into segments, passes to network layer
	- receiver : reassembles segments into messages, passes to application layer
- two transport protocols available to Internet applications
	- TCP
	- UDP

## Transport vs Network layer services and protocols
- Transport layer
	- communication between process
		- relies on, enhances, network layer services
- Network layer
	- communication between hosts

## Transport layer actions
- Sender
	- is passed an application layer message
	- determines segment header fields values
	- creates segment
	- passes segment to IP
- Receiver
	- receives segment from IP
	- checks header values
	- extracts application layer messages
	- demultiplexes message up to application via socket

## Two principal internet transport protocols
- TCP (Transport Control Protocol)
	- reliable, in-order delivery
	- congestion control
	- flow control
	- connection setup
- UDP (User Datagram Protocol)
	- unreliable, unordered delivery
	- no-frills extension of "best-effort" IP
- services not available:
	- delay guarantees
	- bandwidth guarantees

## Multiplexing/De-multiplexing
- Multiplexing as sender
	- handle data from multiple sockets, add transport header (later used for demultiplexing)
- Demultiplexing as reciever
	- use header info to deliver received segment to correct socket
- How demultiplexing works
	- host receives IP datagrams
		- each datagram has source IP address, destination IP address
		- each datagram carries one transport layer segment
		- each segment has source, destination port number
	- host uses IP addresses & port numbers to direct segment to appropriate socket
- Connectionless demultiplexing
	- when creating socket, must specify host-local port #
	- when creating datagram to send into UDP socket, must specify
		- destination IP address
		- destination port #
	- when receiving host receives UDP segment:
		- checks destination port # in segment
		- directs UDP segment to socket with that port #
	- IP/UDP datagrams with same destination port #, but different source IP addresses and/or source port # will be directed to same socket at receiving host

## Connection-oriented demultiplexing
- TCP socket identified by 4-tuple:
	- source IP address
	- source port number
	- destination IP address
	- destination port #
- demultiplexing
	- receiver uses all four values(4-tuple) to direct segment to appropriate socket
- server may support many simultaneous TCP sockets:
	- each socket identified by its own 4-tuple
	- each socket associated with a different connecting client

## UDP (User Datagram Protocol)
- "no frills", "bare bones" Internet transport protocol
- "best effort" service, UDP segments may be:
	- lost
	- delivered out-of-order to app
- connectionless:
	- no handshaking between UDP sender, receiver
	- each UDP segment handled independently of others
- Why is there a UDP?
	- no connection establishment (which can add RTT delay)
	- simple : no connection state at sender, receiver
	- small header size
	- no congestion control
		- UDP can blast away as fast as desired
		- can function in the face of congestion
- UDP use:
	- streaming multimedia apps (loss tolerant, rate sensitive)
	- DNS
	- SNMP
	- HTTP/3
- if reliable transfer needed over UDP (e.g. HTTP/3)
	- add needed reliability at application layer
	- add congestion control at application layer
- UDP : Transport layer actions
	- UDP sender actions:
		- is passes an application layer message
		- determines UDP segment header fields values
		- creates UDP segment
		- passes segment to IP
	- UDP receiver actions:
		- receives segment from IP
		- checks UDP checksum header value
		- extracts application layer message
		- demultiplexes message up to application via socket
- UDP checksum
	- Goal : detect error (i.e. flipped bits) in transmitted segment
- Internet checksum
	- Goal : detect errors (i.e. flipped bits) in transmitted segment
	- sender
		- treat contents of UDP segment (including UDP header fields and IP addresses) as sequence of 16-bits integers
		- checksum : addition (one's complement sum) of segment content
		- checksum value put into UDP checksum field
	- receiver
		- compute checksum of received segment
		- check if computed checksum equals checksum field value:
			- not equal - error detected
			- equal - no error detected

## TCP (Transport Control Protocol)
- point-to-point
	- one sender, one receiver
- reliable, in-order byte steam:
	- no "message boundaries"
- full duplex data:
	- bi-directional data flow in same connection
	- MSS : maximum segment size
- cumulative ACKs
- pipelining:
	- TCP congestion and flow control set window size
- connection-oriented:
	- handshaking (exchange of control messages) initializes sender, receiver state before data exchange
- flow controlled:
	- sender will not overshelm receiver