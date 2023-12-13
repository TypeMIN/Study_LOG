# Concepts in Security
## CIA Properties
- Confidentiality (기밀성)
	- Information is not made available to unauthorized parties
	- 정보나 데이터가 오직 인가된 사용자나 엔터티에게만 엑세스가 허용되어야 함
- Integrity (무결성)
	- Information is not modified in an unauthorized manner
	- 정보나 데이터가 변조되거나 손상되지 않아야 함
- Availability (가용성)
	- Information is readily available when it is need
	- 시스템이 필요한 시간에 사용 가능해야 함
# Cryptography
## Symmetric-key Cryptography
- symmetric : the encryption and decryption keys are the same
- 특징
	- encryption과 decryption key가 동일함
	- 빠른 처리속도
### Block cipher
- block cipher
	- encrypt fixed-length groups of bits, called blocks, at a time, applying the algorithm to the each block
- 대칭키 암호화의 한 유형
- 고정 크기의 블록 단위로 데이터를 암호화/복호화
### Components of a Modern Block cipher
- Transposition cipher (P-box : permutation box)
	- P-box parallels the traditional transposition cipher
	- Three types of P-box
		- Straight P-box
			- n (input) = m (output)
			- invertible
		- Compression P-box
			- n (input) > m (output)
			- non-invertible
		- Expansion P-box
			- n (input) < m (output)
			- non-invertible
- Substitution cipher (S-box : substitution box)
	- invertible
		- only input bits = output bits
- Some other units
	- XOR
		- invertible
	- circular shift
		- invertible
	- swap
		- invertible
	- split
		- invertible
	- combine
### Design Principles for Block cipher
- Diffusion
	- The influence of one plain text bits is spread over many ciphertext bits
	- 입력 데이터의 작은 변화가 출력 데이터에 큰 영향을 미치도록 보장
- Confusion
	- The influence of one key bit is spread over many ciphertext bits
	- 암호문과 키 관계를 복잡하게 만듦
- Rounds
	- Diffusion and confusion can be achieved using iterated block ciphers
	- 추가 라운드는 보안을 강화하지만 암호화/복호화 속도를 늦춤
### Block cipher Modes of Operation
- ECB (Electronic Code Book)![[스크린샷 2023-12-12 13.54.49.png]]
- CBC (Cipher Block Chaining)![[스크린샷 2023-12-12 13.55.03.png]]
- CFB (Cipher FeedBack)![[스크린샷 2023-12-12 13.55.54.png]]
- OFB (Output FeedBack)![[스크린샷 2023-12-12 13.56.44.png]]
- CTR (CounTeR mode)![[스크린샷 2023-12-12 13.57.29.png]]
## Asymmetric-key Cryptography
- each party has two distinct keys
	- public key (공개키)
	- private key (개인키)
### (Extended) Euclidean Algorithm (computation)
- Euclidean Algorithm
	- Finding GCD
		- gcd(a, 0) = a
		- gcd(a, b) = gcd(b, r), where r = a % b
- Extended Euclidean Algorithm
	- computing integers x, y
		- ax + by = gcd(a, b)
### RSA Algorithm
- Key Generation
- Encryption and Decryption
- Correctness of RSA Algorithm
- Security of RSA Algorithm
## Public-key Infrastructure
### Certificate
- Certificate Authority (CA)
	- a trusted party
	- responsible for verifying the identity of users, and then bind the verified identity to a public keys
- Digital certificate
	- a document certifying that the public key included inside does belong to the identity described in the document
### Chain of Trust
- Root CA's Digital Certificate
	- self sign
	- Root CA's public key
- Sub CA's Digital Certificate
	- Root CA's sign
	- Sub CA's public key
- Bob's Digital Certificate
	- Sub CA's sign
	- Bob's public key
## Hash & MAC
### Hash vs MAC vs Digital Signature
- Hash
- MAC (Message Authentication Codes)
	- "Cryptographic checksum" to ensure the integrity of the message and the data origin authentication
### Hash Function Requirements
- Preimage resistant
	- Given y, computationally infeasible to find x such that H(x) = y
	- So-called one-way property
	- Salted Hash
		- use a randomly generated number(salt) to make a hash
- Second preimage resistant
	- Given x, computationally infeasible to find z such that x != z and H(x) = H(z)
- Collision resistant
	- Computationally infeasible to find any pair (x, z) such  that x != z and H(x) = H(z)
- Efficiency
# Software security
## Reverse Engineering
## Control Flow 
- 주로 보안 취약점을 이용하여 프로그램의 실행 흐름을 악의적으로 조작하려는 시도를 가리키는 보안 공격 기술
## Canary & DEP
- Canary
	- Early warnings of buffer overflows
		- not necessarily used for stack, but can also be used for heap
		- insert a checking value(Canary value) before the return address
	- use
		- StackGuard
			- use constant canary value "0x000aff0d"
		- Random canaries
			- pick a random value
- DEP (Data Execution Prevention, a.k.a. NX (No eXecute))
	- doesn't prevent buffer overflow
	- prevent return-to-stack exploits
## ROP (exploit step important)
- ROP (Return-Oriented Programming)
- ROP Workflow
	- Disassemble binary
	- Identify useful instruction sequence
	- Assemble gadgets to perform some computation
## Secure Coding (find, fix the vulnerability)
- Defensive Programming
	- making the software behave in a predictable manner despite unexpected inputs or user actions
- Offensive Programming
	- a category of defensive programming
	- make defensive checks to b e unnecessary by failing fast
# Web security
## SQL injection Attacks
## Same Origin Policy
- SOP (Same Origin Policy)
	- one of the browser sandboxing mechanism
	- the basic security model enforced in the browser
- restricts scripts on one origin from accessing data from another origin
- basic access control mechanism for web browsers
	- all resources such as DOM, cookies, JavaScript has their own origin
	- SOP allows a subject to access only the objects from the same origin
- Origin = Protocol + Domain Name + Port
## Cross-Site Scripting(XSS)
- malicious scripts are injected into benign and trusted websites
- injected codes are executed at the attacker's target origin
- Types
	- Reflected XSS (server-side)
		- exploits a server-side web application vulnerability
	- Stored XSS
		- attacker stores the JS code in the server-side component
	- DOM-based XSS (client-side)
		- attacker payload is executed by modifying the "DOM environment" used by the original client-side script
	- Universal XSS
		- exploits a browser bug to inject malicious payload to any webpage origin
## Content Security Policy
- CSP (Content-Security Policy)
	- Level 1 : Controlling Scripting Resources
	- Level 2 : Nonces and Hashes
	- Level 3 : Strict-dynamic
- Problems
	- User inputs
	- Developer's Mistake/Misconfiguration
	- Browser bugs
# Network security
## TCP SYN Flooding Attack & Defense
- TCP SYN Flooding Attack
	- floods the server with SYN Packets
- how to mitigate
	- set the queue size for TCP Backlog
	- set the firewalls
	- SYN Cookie
## Spoofing
- a situation in which a person or program is successfully identified as another by modifying data
	- IP spoofing
		- 자신의 IP 주소를 다른 사용자나 시스템의 IP 주소로 위조하여 네트워크 트래픽을 속이는 행위
	- ARP spoofing
		- ARP (Address Resolution Protocol)
		- 공격자가 네트워크에서 다른 장치의 ARP 테이블을 위조하여 트래픽을 리다이렉션하거나 감시하는 것
	- DNS spoofing
		- 공격자가 DNS 서버의 응답을 위조하여 사용자를 악의적인 웹 사이트로 리다이렉션하거나 사용자의 DNS 요청을 감시하는 공격
# Protocol Security
## How SSL/TLS Provides Security Properties?
- SSL (Secure Sockets Layer)
- TLS (Transport Layer Security)
- HTTPS = HTTP + SSL/TLS
- SSL/TLS Handshake Protocol
	- Phase 1 : Establishing security capabilities
	- Phase 2 : Sever authentication and key exchange
	- Phase 3 : Client authentication and key exchange
	- Phase 4 : Finalizing the handshake protocol
# Access Control
## DAC
- DAC (Discretionary Access Control)
	- all objects have owners
	- owners can decide permission
## MAC
- MAC (Mandatory Access Control)
	- only the admin can decide permission
	- users cannot change policy
# Authentication
## Password-based authentication
- user has a secret password
- system checks i to authenticate the user
- Cleartext password
- Password Hashing
# Program Analysis
## Soundness vs Completeness
- sound
	- What I say < Truth
- complete
	- What I say > Truth
- perfect (sound & complete)
	- What I say = Truth
## True Positive and False Positive
- Positive
	- The analyzer says bug
- Negative
	- The analyzer says NOT bug

- True Positive
	- 분석은 버그 + 실제도 버그
- False Positive
	- 분석은 버그 + 실제는 아님
- True Negative
	- 분석은 아님 + 실제도 아님
- False Negative
	- 분석은 아님 + 실제는 버그
## Precision, Recall, Accuracy, FP Rate, FN Rate
- Precision
	- TP / (TP + FP)
	- 버그라고 판별한 것중 실제 버그인 확률
- Recall
	- TP / (FN + TP)
	- 실제 버그 중 버그라고 판별한 확률
- Accuracy
	- (TP + TN) / (TP + FP + FN + TN)
	- 전체 데이터에 대한 정답률
- FP Rate
	- FP / (TP + FP)
	- 버그라고 반별한 것 중 실제 버그가 아닌 확률
- FN Rate
	- FN / (FN + TN)
	- 버그라고 반별하지 않은 것 중 실제 버그인 확률
## Symbolic Execution
- A program analysis technique that executes a program with symbolic
## Fuzzing
- simple and popular way to find security bugs
- used by security practitioners
# AI Security
## Adversarial Attacks
- a cyber-attack that aims to misguide a model with malicious input