## Authentication
- the process by which the identity of someone or something

### Authentication methods
- typical methods
	- knowledge : something you know
		- password, PIN, ...
	- token : something you have
		- ID card, key, passport, certificate
	- biometrics : something you are
		- a physiological characteristic
			- fingerprint, iris pattern, form of hand
		- a behavioral characteristic
			- the way you sign, the way you speak

### Password-based Authentication
- clear text passwordddd
	- Problem
		- SSL/TLS Encryption
			- Problem
			- Attackers
				- online attackers
					- tries to login to a service by iteratively trying passwords and looking whether he was successful
					- how do we detect an online attacker?
						- too many wrong tries
						- tries multiple accounts instead of just one
					- what can we do?
						- CATCHAs to differentiate between bots and humans
						- temporarily block the IP address or rate-limit the number of requests
						- Temporarily lock the account that is being attacked
				- offline attackers
					- stole password database and tries to recover the passwords
					- attacker somehow obtains the list of our passwords
						- break-in to server
							- Credential guessing
							- SQL injection
							- Remote-command execution
					- 
			- Credential stuffing
				- attackers try these credentials against other services
			- Password hashing
				- server consults database which contains Hash(pw) and validates user response
				- Problems
					- attacker can precompute hashes of popular words and try them against all accounts
					- Salted Hash
						- same password -> different hash value
						- hash the user's password concatenated with a per-user random value(salt)
						- still has a problem
							- offline attackers can still brute-force their way into users with weak passwords
			- Defense: password requirements
				- not a dictionary word
				- must be at least X characters long
				- must contain special characters
				- is not part of a recently compromised database
			- limitations of password requirements
				- overly restrictive password policies result in frustrated users and less security
				- typically, strength of a password and memorability are working against each other
### Token-based Authentication
- things one can have
	- access to your smartphone
	- a bank card
	- a secret token
		- hardware : OTP
		- software : JWT, OAuth
	- a encryption/decryption keys
	- a badge
- Problems
	- stolen, forgotten, lost, duplicated
	- cost of user education and support
- types
	- challenge-response authentication
		- key-idea : avoid sending password-related information
		- why is this better than the password over a network?
			- secrecy : difficult to recover secret from response
			- freshness : if the challenge is fresh, attacker on the network cannot replay an old response
		- use case
			- symmetric key encryption
			- cryptographic hashing
		- zero-knowledge proof
			- a method by which the prover can prove to verifier that they know a secret, without revealing anything about the secret
	- time-based authentication
		- client and server use (shared seed + current time) to generate a passcode
		- various methods are available for users to receive time-based one-time passwords
### Certificate-based Authentication

### Biometric Authentication
- bio + metric
	- fingerprints
	- palms
	- face
	- iris/retina scanning
	- voice
- Pros
	- nothing to remember
	- passive
	- can't share
	- can be fairly unique
- Cons
	- revocability
	- are still spoofable
	- cost
	- error rates

### Multi-factor Authentication (MFA)
- a combination of criteria that need to be met
- 