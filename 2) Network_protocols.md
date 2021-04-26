**Network protocols**

IP, TCP, HTTP

**IP** - internet protocol. Defines how machine-to-machine communicates with each other. 
Modern internet operates using IP. 

**IP packet** is a unit of data that is sent from one machine to another. It is a building block between machine communication. 

**Note:** all data in IP packet is stored in bytes

IP packet: header & data

Header contains info about the packet: <i>source IP address, destination IP address, total size of the packet, version of the IP</i>

Data (**payload**): the very info. The size is 2^16 bytes. It’s a small amount, hence a couple of IP packets can be used. But there is risk that some of the packets may be lost during transition over the network. TCP comes into play. It allows to send multiple IP packets and ensure that they all got delivered.

**TCP** - transmission control protocol. Built on top of IP.
It ensures that packets: 1. Sent in ordered way 2. Sent in reliable way 3. Error free way

**TCP header** goes after IP header in that same IP packet. 

When machine wants to communicate with another machine over TCP (i.e. browser wants to communicate with website server) it 1. Creates connection with destination server via **TCP handshake** by sending a couple of packets 2. After the connection has been established, data can be sent between them

Note: one machine can end connection via special command; connection can end due to time out  (no response from one of the sides). But it’s difficult for developers to communicate with TCP (no robust framework for developers to establish Client-Server communication), here **HTTP** appears.

**HTTP** - hyper text transfer protocol. Abstraction above IP & TCP
It introduces the idea of machines communicate in Client-Server manner.

HTTP: hyper text transfer protocol.
	Protocol: set of rules how to communicate.
	Transferred: request was transferred by the client and server accepts it.
	After some work server gives response to the client (web browser in this case) to generate 		a new web page.
	In that response above the BODY of the response is HTML. HT are first two letters.

**HTTP verbs are requests from Client**
```
HTTP VERBS | CRUD
	GET       READ
	POST      CREATE
PUT, PATCH    UPDATE
	DELETE    DELETE
```

**Headers** - a collection of key-value pairs which comprises essential metadata about the request<br>
**Body** - data that is sent in the request (key-value pair also)

Response can have status <i>code/ headers/ body</i>

**In a nutshell:** HTTP is the one that allows to create business logic and interact with data

![Alt text](ImageRepo/Network_Protocols_first.png?raw=true)
![Alt text](ImageRepo/Network_Protocols_second.png?raw=true)
![Alt text](ImageRepo/Network_Protocols_third.png?raw=true)
