# COMPUTER NETWORKS

## 1. NETWORKS
It is a group or system of interconnected peoples or items.
Computers connected with each other with cables or wireless is called **computer networks**
## 2. Internet
It is a network of computer networks. Complex web of interconnected computer networks.

## 3. Terminologies
- **Network Protocols**: It is a set of rules and regulations setup to communicate and share information over a network.
	- e.g.  HTTP, UDP, TCP, SMTP, etc
- **Packets**: In order to share data, we can send big chunk of data over the network. So, we divide the data into small chunks, these small chunks are called packets. 
- **Address**: Sending a message over the networks requires the destination details. This details uniquely identify the end system is called address.
- **Ports**: Any machine could be running many networks applications. In order to distinguish these apps for receiving messages, we use ports(port number).
	> IP-address + port = socket
	- Range : 0-2^16 = 65535
	- **0-1023** is called **known ports**.
	- port 80 belongs to **http** and port 443 to **https**
	- **1024-49152** is called **registered ports**. Any third-party can use these ports.
		- e.g. SQL Server uses 1433, MongoDB uses 27017
	- **49152-65535** is called dynamic ports. These are for future purpose.
- **Access Networks**: These are media using which end systems connect to the internet.
- **DSL (Digital Subscriber Line)**: It uses the existing telephone groundwork lines for internet connection. Generally, DSL is provided by the same company which supplies telephone service. 
	- ISP (Internet Service Provider)
	- Cable Network
	- Fiber Network
	- Satellite Network

## 4. Network Protocol
