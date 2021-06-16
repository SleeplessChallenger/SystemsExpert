**Security And HTTPS**

When client interacts with server over HTTP, we assume that this connection is private, but it’s not correct. Someone can hijack the communication channel and intercept the underlining IP packets that were transferred and either read or alter them. It’s called **MITM (Man-In-The-Middle Attack)**

=> **HTTP** isn’t a secure communication whilst **HTTPS** is (last ’s’ is Secure). 

**Encryption** - process in which message from one party (ex. Client) will be encrypted in a seemingly random characters (or another form of data that is no longer eligible and cannot be tied back to original data) and another party (ex. Server) will decrypt it to read.

<ins><i>Two systems of encryption:</i></ins> Symmetric and Asymmetric

**Symmetric** - type of encryption that relies on symmetric key algorithms. These types of algorithms rely on a single key to both encrypt and decrypt data. Generally, symmetric encryption uses AES. **AES** - advanced encryption standard which is a specification of encryption that uses symmetric key algorithm. Pros of this method: speed.

**Precaution:** this type of encryption uses 1 key which must be shared sometimes to enable both parties to communicate. So, this key must be shared via secured network. Ex: Server must give this key to Client, but if done via unsecured network => vulnerability to attack

**Asymmetric** - type of encryption, aka public key encryption, that relies on two keys to encrypt and decrypt the messages. Those 2 keys are generated together (one of them is called public, another - private) using some cryptographic algorithms in such a way that if you encrypt the message by public key then you can decrypt it only by private key. Everyone can see that public key and even use it to encrypt messages, but the only person who has access to the private key is you (ex. Server). Con: slower compared to symmetric encryption.

```
TLS - transport layer security is a type of protocol over which HTTP runs and becomes HTTPS (HTTP over TLS). So, HTTPS communication is encrypted using TLS.
SSL is a predecessor protocol to TLS (TLS is based on SSL).
SSL - secure socket layer.
TCP - transmission control protocol. Built on top of IP.
```

When client and server establish connection, they at first go through **TLS handshake**. **TLS handshake** is a process that establishes a secure connection between a client and a server.
<br>
Process of the handshake:<br>
1. Client sends so-called `client hello` (random string of bytes) to the server.
2. Server responds with 2 things: a) `server hello` (similar to client one) b) its `SSL certificate`. In this certificate there is a **public key** out of **public/private key pair**. 
3. After client has received the response, 3.1 Client verifies the SSL Certificate using corresponding CA’s public key 3.2 Gets public key from the SSL Certificate which belongs to the server 3.3 Client generates yet another random string of bytes named **premaster secret** which will be encrypted using that public key from SSL certificate in point 3.2.
4. Client sends to the server that encrypted premaster secret.
5. Servers receives it and as Server has private key - it can decrypt the premaster secret. Generally, Server is the only entity that has private key and can decrypt the premaster secret.
6. Using client `hello/server hello/premaster secret`, clients and server will generate **session keys (usually, there are 4 session keys) == symmetric encryption keys (generally 1 symmetric encryption key).** This 1 symmetric encryption key will be used only during this particular session, when session ends they throw away this key. Actually, both of the parties will generate that same symmetric encryption key to interact with each other during one session.

7. In the end of TLS handshake client and server return one final message to each other which is encrypted using those session keys (like ‘finish TLS handshake process’). If everything OK -> secure connection has been established

**Problem of the above process:** if malicious user intercepts first time Server sends its public key and replaces with his own public key -> premaster secret will be encrypted using malicious public key -> malicious user will be able to decrypt the premaster secret => entire communication’s channel has been hijacked.<br>
<ins><i>How can client trust that public key has come from the server?</i></ins> <br>
Here **SSL certificate** comes into play.

<ins><i>SSL certificates</i></ins> - certificates that are granted by trusted third party called a certificate authority (CA). It’s an organization that, let’s say, developers trust to and this organization will give certificates to, let’s say, AlgoExpert’s server. Certificate itself here - digital item that CA signed and client can rely on this certificate and be confident that the server is actually what it’s and not some malicious user. + public/private keys can be given to the server by CA.

<ins><i>SSL Certificate comprises:</i></ins> public key, server entity itself (like AlgoExpert), assurance. And all these things are signed by private key owned by CA. And to verify this digital signature (SSL certificate broadly) client will use public key of the CA.

Generally, browsers have public keys of all the major Certificate authorities so that browsers can verify SSL certificated from various CA.

![Alt text](ImageRepo/Security_first.png?raw=true)

![Alt text](ImageRepo/Security_second.png?raw=true)
