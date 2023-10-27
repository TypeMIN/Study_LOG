## Internet

### The Internet: a "nuts and bolts" view

#### Hosts
> 호스트(Host) : 컴퓨터 네트워크에 연결된 모든 디바이스(devices)

- hosts = end systems
- running network apps at Internet's "edge"
- host connect to Internet via access Internet Service Providers (ISPs)


#### Packet Switches
> 패킷 스위치(Packet switch) : 컴퓨터 네트워크와 통신의 방식 중 하나로, 작은 블록의 패킷으로 데이터를 전송하며 데이터를 전송하는 동안만 네트워크 자원을 사용하는 방법
##### Packet
> 패킷(Packet) : 패킷 방식의 컴퓨터 네트워크가 전달하는 데이터의 형식화된 블럭
##### Routers
> 라우터(Router) : 컴퓨터 네트워크 간에 데이터 패킷을 전송하는 네트워크 장치

- 패킷의 위치를 추출하여, 그 위치에 대한 최적의 경로를 지정하며, 이 경로를 따라 데이터 패킷을 다음 장치로 전달
##### Switches
> 네트워크 스위치(Switch) : 처리 가능한 패킷의 숫자가 큰, 네트워크 단위들을 연결하는 통신 장비
#### Communication links
> 링크(Communication link) : 데이터를 전송하는 물리적인 매체

##### Kind of links
1. 광섬우(fiber)
2. 구리선(copper)
3. 라디오파(radio)
4. 위성 마이크로파(satellite)
##### Transmission rate & Bandwidth
-  전송 속도가 빠르다 -> 대역폭이 넓다

#### Networks
> 네트워크(Network) : 조직에서 관리하는 디바이스, 라우터, 링크들의 집합

#### Internet
> 인터넷(Internet) : "Network of networks"
- access ISPs in turn must be interconnected
	- so that any two hosts (anywhere!) can send packets to each other
- resulting network of networks is very complex
	- evolution driven by economics, national policies
- Question : given million of access ISPs, how to connect them together?
	- connecting each access ISP to each other directly doesn't scale: O(N^2) connections
- Option : connect each access ISP to one global transit ISP?
	- Customer and provider ISPs have economic agreement.
	- But if one global ISP is viable business, there will be competitors
		- Internet exchange point (IXP)
		- Peering Link
	- and regional networks may arise to connect access nets to ISPs
	- and content provider networks (e.g. Google, Microsoft, Akamai) may run their own network, to bring services, content close to end users
	- At "center" : small # of well-connected large networks
		- "tier-1" commercial ISPs(e.g. Level 3, Sprint, AT&T, NTT): national $ international coverage
		- content provider networks(e.g. Google, Facebook): private network that connects its data centers to Internet, often bypassing tier-1, regional ISPs

#### Protocols
> 프로토콜(Protocol) : 컴퓨터나 원거리 통신 장비 사이에서 메세지를 주고 받는양식과 규칙의 체계

##### Example of protocols
1. HTTP (Web)
2. Streaming video
3. Skype
4. TCP
5. IP
6. WiFi
7. 4/5G
8. Ethernet

#### Internet standards
> (Internet standard) : 인터넷에 적용되는 기술이나 방법론을 표준으로 제정한 규격
##### RCF
> 의견 요청서(Request for Comments) 

##### IETF
> 국제 인터넷 표준화 기구(Internet Engineering Task Force)

---

### The Internet: a "services" view

#### Infrastructure
> 인터넷(Internet) : 어플리케이션(Application)에게 서비스를 제공하는 기반 시스템(Infrastructure)

### **Programming Interface**
> 인터넷(Internet) : 어플리케이션(Application)에게 API(Application Programming Interface)를 제공

- "hooks" allowing sending/receiving apps to "connect" to, use Internet transport service
- provides service options, analogous to postal service