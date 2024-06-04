# Path of a HTTPS request

``` mermaid

sequenceDiagram
    participant Client
    participant DNS Server
    participant Server

    Client->>DNS Server: DNS Request (www.example.com)
    DNS Server-->>Client: DNS Response (IP Address)

    Client->>Server: SYN
    Server-->>Client: SYN-ACK
    Client->>Server: ACK

    Client->>Server: Client Hello
    Server-->>Client: Server Hello
    Server-->>Client: Server Certificate
    opt Optional Step
        Server-->>Client: Server Key Exchange
    end
    Server-->>Client: Server Hello Done
    Client->>Server: Client Key Exchange
    Client->>Server: Change Cipher Spec
    Server-->>Client: Change Cipher Spec
    Client->>Server: Finished
    Server-->>Client: Finished

    Client->>Server: Encrypted HTTP Request
    Server-->>Client: Encrypted HTTP Response

    Client->>Server: FIN
    Server-->>Client: ACK
    Server->>Client: FIN
    Client-->>Server: ACK
```

The path of an HTTPS request involves several steps to ensure secure communication between a client (e.g., a web browser) and a server. Here is a detailed explanation of the process:

### 1. **DNS Resolution**

- **Client Request:** The client wants to access a website, so it sends a DNS (Domain Name System) request to resolve the domain name (e.g., www.example.com) to an IP address.
- **DNS Response:** The DNS server responds with the IP address of the server hosting the website.

### 2. **TCP Connection Establishment**

- **Client Request:** The client initiates a TCP (Transmission Control Protocol) connection with the server using the IP address obtained from the DNS resolution.
- **Three-Way Handshake:** This involves three steps:
  1. **SYN:** The client sends a SYN (synchronise) packet to the server to initiate a connection.
  2. **SYN-ACK:** The server responds with a SYN-ACK (synchronise-acknowledge) packet.
  3. **ACK:** The client sends an ACK (acknowledge) packet, completing the handshake and establishing a TCP connection.

### 3. **TLS Handshake**

- **Client Hello:** The client sends a "Client Hello" message, including the SSL/TLS version, cipher suites, and a random number.
- **Server Hello:** The server responds with a "Server Hello" message, selecting the SSL/TLS version, cipher suite, and providing a random number.
- **Server Certificate:** The server sends its digital certificate, which contains the server's public key and is signed by a trusted Certificate Authority (CA).
- **Server Key Exchange (optional):** If required, the server sends a key exchange message.
- **Server Hello Done:** The server signals the end of the server hello messages.
- **Client Key Exchange:** The client sends a "Client Key Exchange" message, which may include a pre-master secret encrypted with the server's public key.
- **Change Cipher Spec:** Both client and server send a "Change Cipher Spec" message, indicating that subsequent messages will be encrypted.
- **Finished:** Both client and server send a "Finished" message to verify that the handshake was successful.

### 4. **Secure Communication**

- **HTTP Request:** The client sends an encrypted HTTP request over the established TLS connection.
- **Server Response:** The server decrypts the request, processes it, and sends back an encrypted HTTP response.

### 5. **Termination**

- **Client Initiated:** The client can initiate termination by sending a FIN (finish) packet.
- **Server Response:** The server responds with an ACK (acknowledge) and then sends its own FIN packet.
- **Client Final ACK:** The client sends a final ACK packet, completing the termination of the connection.

Throughout this process, the data exchanged between the client and server is encrypted, ensuring confidentiality, integrity, and authenticity of the communication.


