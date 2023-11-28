## Operating system security
- one of the main goal of OS : resource sharing
- important question : how to securely share resources?

## Principle of Least Privilege

## Access control
- rules and policies that limit access to confidential information
- determine what users have permission to do
- permission is determined by identity or role
- defense against attacks in the first place
- access control is every where

### Access control method
- check if a subject(user) can perform an operation on an object(resource)
- three key properties
	- must be always invoked
	- must be tamper-proof
	- must be easy to verify
### Access control policy
- how does one grant the right level of permission to an individual?
	- Discretionary access control(DAC)
		- all objects have owners
		- what permission to grant others? Owners can decide
		- e.g. Unix, windows, etc
	- Mandatory access control(MAC)
		- What permission to grant others? Only the admin can decide
		- users cannot change policy themselves
		- e.g. SELinux, military, etc
#### DAC
- Access control matrix
	- Problems
		- Matrix size
			- as the number of subjects and objects increases, a large size of memory is required
			- memory space is wasted
		- Object-oriented approach : Access control list(ACL)
			- widely used in many operating systems as a basic access control method
			- approve requests if the subject has privilege to perform the operation on the object
			- Limitation
				- Confused deputy problem
		- Subject-oriented approach : Capability
			- capability : a pair of an object and a set of privileges
			- Trojan Horse
		- Exploitation
			- malware or buggy SW
			- attacker's intention with the user's privileges
			- no way to tell the difference between the legitimate software and a trojan
#### MAC
- the system assigns both subjects and objects special security attributes
- privileges cannot be changes by users but by system administrators
- more restrictive and secure than discretionary access control
- mostly used in security-critical systems

- Multilevel Security(MLS)
	- most common form of mandatory access control
	- all information(objects) possesses a classification
	- every person(subjects) posses a classification
	- access is allowed if the person's class is higher than the information's class

- Security Classification
	- security level(sensitivity)
		- a total ordered set
			- access is allowed if the subject's level is higher than the objects' level
	- compartment
		- a set of categories
			- access allowed if subject's compartments includes object's compartments
- Classification lattice
	- the combination of security level and compartment forms a lattice
	- lattice : a partially ordered set that satisfies the followings

### The Bell-LaPadula Model(BLP)
- the first mathematical model of the multilevel secure system in 1973
- main concern : prevent information leak
- idea
	- lower class subjects cannot read higher class objects (NO READ UP)
	- higher class subjects cannot write lower class objects (NO WRITE DOWN)
- Pros
	- confidentiality
	- Reporting system
- Cons
	- Integrity
	- fake announcement
### The Biba Model
- dual of BLP
- NO WRITE UP
- NO READ DOWN
- Pros
	- integrity
	- Notification system
- Cons
	- confidentiality