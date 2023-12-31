## Socket API
- What would you expect when learning a new Unix command?
	- Source code => Implementation detail
	- Program options => Interface
- Application Programming Interface (API)
	- Interface to a particular "service"
	- Abstracts away from implementation detail
	- Set of functions, data structures, and constants
- Socket API
	- Network programming interface
	- Application <-> Socket API <-> transport <-> Network
- BSD Socket API
	- From UC Berkeley
	- Most popular network API
	- Ported to various OSs, various languages
		- Windows Winsock, OS X, Linux, Solaris, ...
		- Socket modules in Java, Python, Perl, ...
	- Similar to Unix file I/O API
		- In the form of file desciptor
		- can share the same read()/write()/close() system calls
## Type of Sockets
- Sockets
	- Endpoint of a connection
		- Identified by IP address and Port number
	- Primitive to implement high-level networking interface
		- e.g. Remote procedure call (RPC)
- Stream socket (a.k.a. TCP)
	- Connection-oriented
		- Requires connection establishment & termination
	- Reliable delivery
		- In-order delivery
		- Retransmission
		- No duplicates
	- High variance in latency
		- Cost of the reliable service
	- File-like interface (streaming)
	- e.g. HTTP, SSH, FTP,  ... (no loss)
- Datagram socket (a.k.a. UDP)
	- Connection-less
	- "Best-effort" delivery
		- Possible out-of-order delivery
		- No retransmission
		- Possible duplicates
	- Low variance in latency
	- Packet-like interface
		- Requires packetizing
	- e.g. DNS, VoIP, VOD, AOD, ...
- Type of Sockets
	- sending "Hi!" and "Hope you're well"
		- TCP treats them as a single bytes stream
			- thus, TCP needs application-level messages boundary
				- by carrying length in application-level header
		- UDP treats then as separate messages
## Endianess
- Big Endian
	- 순서대로 읽음
- Little Endian
	- 역순으로 읽음
- Network byte order : Big endian
	- To avoid the endian problem
- We must use network byte order when sending 16bit, 32bit, 64bit numbers
- Utility functions for easy conversion