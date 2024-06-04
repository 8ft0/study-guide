# Path of a HTTP request

``` mermaid
sequenceDiagram
    participant Client
    participant DNS
    participant Server

    Client->>DNS: DNS Resolution (Domain to IP)
    DNS-->>Client: IP Address
    Client->>Server: Establish Connection (TCP/TLS Handshake)
    Client->>Server: Send HTTP Request
    Server->>Server: Route Request
    Server->>Server: Authenticate & Authorise
    Server->>Server: Execute Business Logic
    Server->>Database: Query Database (if needed)
    Database-->>Server: Data Response
    Server->>Server: Generate HTTP Response
    Server->>Client: Send HTTP Response
    Client->>Client: Process Response
    Server->>Client: Close Connection (if applicable)

```

The path of an HTTP request involves several steps, each of which plays a crucial role in ensuring that a request is processed correctly and the appropriate response is returned. Here is a detailed explanation of the path of an HTTP request:

### 1. **Client Initiation**
The process begins with a client, typically a web browser, mobile app, or any HTTP client, initiating an HTTP request. This request is usually triggered by user actions such as clicking a link, submitting a form, or programmatically through an API call.

### 2. **DNS Resolution**
Before the request reaches the server, the client's device must resolve the domain name (e.g., www.example.com) to an IP address. This is done through a DNS (Domain Name System) lookup. The DNS resolver queries a DNS server to obtain the IP address associated with the domain.

### 3. **Establishing a Connection**
With the IP address resolved, the client establishes a connection to the server. For secure connections, this involves a TLS handshake to establish an encrypted connection. For non-secure connections, a simple TCP connection is established.

### 4. **Sending the Request**
Once the connection is established, the client sends an HTTP request to the server. This request consists of:

- **Request Line:** Includes the HTTP method (GET, POST, PUT, DELETE, etc.), the URL, and the HTTP version.
- **Headers:** Key-value pairs providing additional information about the request (e.g., `User-Agent`, `Accept`, `Content-Type`).
- **Body:** Optional data sent with the request, typically used with methods like POST and PUT.

### 5. **Server Processing**
The server receives the request and processes it. This involves several steps:

- **Routing:** The server determines which handler or controller should process the request based on the URL and HTTP method.
- **Authentication & Authorisation:** The server checks if the request is authenticated (is the user who they claim to be?) and authorised (does the user have permission to perform this action?).
- **Logic Execution:** The server executes the necessary business logic, which may involve querying a database, processing data, or calling other services.
- **Generating a Response:** The server constructs a response, which includes a status code (e.g., 200 OK, 404 Not Found), headers, and a body (typically HTML, JSON, or XML).

### 6. **Sending the Response**
The server sends the HTTP response back to the client over the established connection. This response includes the status code, headers, and any body content.

### 7. **Client Handling**
Upon receiving the response, the client processes it:

- **Parsing the Response:** The client reads the status code to determine if the request was successful or if there were errors.
- **Rendering or Processing Data:** If the response body contains HTML, the browser renders it. If it contains data (e.g., JSON), the client may process it accordingly (e.g., updating the UI or storing data).

### 8. **Connection Closure**
After the response is received and processed, the connection may be closed. For HTTP/1.1, persistent connections allow multiple requests/responses over a single connection, which can be kept open for a period. For HTTP/2, multiplexing allows multiple requests/responses simultaneously over a single connection.

### Summary
To summarise, the path of an HTTP request involves the following key steps: client initiation, DNS resolution, establishing a connection, sending the request, server processing, sending the response, client handling, and connection closure. Each step is crucial for the accurate and efficient exchange of information between the client and the server.