# Networking Questions

<details>
<summary>What is the OSI model? Explain each layer?</summary>

**OSI(Open Systems Interconnection) model** is a conceptual framework used to understand and implement network protocols in seven layers:
1. **Physical Layer**: Deals with the physical connection between devices, including cables, switches, and the transmission of raw binary data over a medium.
2. **Data Link Layer**: Responsible for node-to-node data transfer, error detection and correction, and framing. It includes protocols like Ethernet and MAC addressing.
3. **Network Layer**: Manages data routing, forwarding, and addressing. It determines the best path for data to travel across networks. Protocols include IP (Internet Protocol).
4. **Transport Layer**: Ensures reliable data transfer between end systems, providing error recovery and flow control. Key protocols are TCP (Transmission Control Protocol) and UDP (User Datagram Protocol).
5. **Session Layer**: Manages sessions or connections between applications. It establishes, maintains, and terminates communication sessions.
6. **Presentation Layer**: Translates data between the application layer and the network. It handles data encryption, compression, and formatting.
7. **Application Layer**: The topmost layer that provides network services directly to end-user applications. It includes protocols like HTTP, FTP, SMTP, and DNS.

</details>

<details>
<summary>What is TCP/IP model? Explain each layer?</summary>

The TCP/IP model is a practical networking model used on the Internet.
It has four layers instead of seven, combining some OSI layers together:
1. **Link Layer**
2. **Internet Layer**
3. **Transport Layer**
4. **Application Layer**

OSI is mainly theoretical, while TCP/IP is implementation-oriented and widely used in real systems.
</details>

<details>
<summary>Difference between TCP and UDP?</summary>

**TCP (Transmission Control Protocol)**:
- Connection-oriented protocol
- Reliable data transfer with error checking and retransmission
- Flow control and congestion control
- Slower due to overhead
- Used for applications requiring reliability (e.g., web browsing, email)
- Example: HTTP, FTP, SMTP
  
**UDP (User Datagram Protocol)**:
- Connectionless protocol
- Unreliable data transfer, no error checking or retransmission
- No flow control or congestion control
- Faster due to lower overhead
- Used for applications where speed is critical and some data loss is acceptable (e.g., video streaming, online gaming)
- Example: DNS, VoIP, TFTP

**Use Cases**:
- TCP: Web browsing, file transfers, email
- UDP: Video streaming, online gaming, VoIP
</details>

<details>
<summary>How does TCP ensure reliability?</summary>

TCP ensures reliability through several mechanisms:
1. **Three-Way Handshake**: Establishes a connection between sender and receiver before data transfer.
2. **Sequence Numbers**: Each byte of data is assigned a sequence number, allowing the receiver to reorder segments and detect missing data.
3. **Acknowledgments (ACKs)**: The receiver sends ACKs to the sender to confirm receipt of data. If an ACK is not received within a certain time, the sender retransmits the data.
4. **Flow Control**: TCP uses a sliding window mechanism to control the amount of data sent before receiving an ACK, preventing overwhelming the receiver.
5. **Error Detection**: TCP includes a checksum in each segment to detect errors in transmitted data. If an error is detected, the segment is discarded and retransmitted.
6. **Congestion Control**: TCP adjusts the rate of data transmission based on network congestion, using algorithms like Slow Start and Congestion Avoidance to prevent packet loss.
</details>

<details>
<summary>What is a three-way handshake in TCP?</summary>

The three-way handshake is a process used by TCP to establish a reliable connection between a client and server before data transmission begins. It involves three steps:
1. **SYN (Synchronize)**: The client sends a SYN packet to the server to initiate a connection and synchronize sequence numbers (ISN).
2. **SYN-ACK (Synchronize-Acknowledge)**: The server responds with a SYN-ACK packet, acknowledging the client's SYN and sending its own SYN to the client.
3. **ACK (Acknowledge)**: The client sends an ACK packet back to the server, acknowledging the server's SYN-ACK.

Once this three-step process is complete, a reliable TCP connection is established, and data can be transmitted between the client and server.
</details>


<details>
<summary>Why there are 3 way handshakes but not 2 way?</summary>

3-way handshake ensures mutual agreement and synchronized state between two endpoints, which cannot be guaranteed with only two messages.

</details>

<details>
<summary>What happens during TCP connection termination? </summary>

TCP connection termination involves a four-step process to gracefully close a connection between a client and server:
1. **FIN from Client**: The client sends a FIN (Finish) packet to the server, indicating that it has finished sending data.
2. **ACK from Server**: The server acknowledges the client's FIN by sending an ACK (Acknowledge) packet back to the client.
3. **FIN from Server**: The server then sends its own FIN packet to the client, indicating that it has also finished sending data.
4. **ACK from Client**: Finally, the client acknowledges the server's FIN by sending an ACK packet back to the server.

After these four steps, the TCP connection is fully terminated. Both sides enter a TIME_WAIT state to ensure that any delayed packets are properly handled before completely closing the connection.
</details>

<details>
<summary>   Explain TCP congestion control. </summary>

TCP congestion control is a set of algorithms and mechanisms used to prevent network congestion by controlling the rate of data transmission between a sender and receiver. The main components of TCP congestion control include:
1. **Slow Start**: TCP begins with a small congestion window (cwnd) and increases it exponentially with each acknowledgment received, doubling the cwnd for each round-trip time (RTT) until a threshold (ssthresh) is reached.
2. **Congestion Avoidance**: Once the cwnd reaches the ssthresh, TCP switches to a linear increase, adding one segment to the cwnd for each RTT, to avoid overwhelming the network.
3. **Fast Retransmit**: If a sender receives three duplicate ACKs, it assumes a segment was lost and retransmits it immediately without waiting for a timeout.
4. **Fast Recovery**: After a fast retransmit, TCP reduces the cwnd to half of its current size (ssthresh) and enters congestion avoidance mode, allowing for a quicker recovery from packet loss.
5. **Timeouts**: If a timeout occurs (no ACK received), TCP assumes severe congestion and reduces the cwnd to one segment, re-entering slow start.

**TCP congestion control** dynamically adjusts the sending rate based on network feedback to avoid overwhelming the network.
</details>

<details>
<summary>How TCP handles the connection?</summary>

TCP handles a connection by managing its entire lifecycle, from establishment to termination.

It first establishes the connection using a three-way handshake to synchronize state between both endpoints.
During data transmission, TCP ensures reliability through acknowledgements and retransmissions, applies flow control to protect the receiver, and uses congestion control to adapt to network conditions.

Finally, TCP terminates the connection using a four-way handshake and maintains connection states to ensure a clean and reliable shutdown.

**Summary**: TCP is a stateful protocol that manages connection setup, reliable data transfer, congestion control, and graceful teardown.

</details>

<details>
<summary>What happens if some bits are wrong due to connection errors? How to detect them and fix them?</summary>

If some bits are wrong, the checksum of this packet will not match. In this case, the receiver will discard this packet.
The sender will retransmit the packet after a timeout or upon receiving duplicate ACKs.

</details>

<details>
<summary>How to detect the appropriate number of packets to send (speed of sending packet)?</summary>

TCP determines the appropriate sending rate by dynamically adjusting its congestion window based on network feedback.

It starts with a small sending rate and gradually increases it while monitoring acknowledgements and round-trip time.
If packet loss or timeouts occur, TCP interprets them as signs of congestion and reduces the sending rate.

The effective sending rate is limited by the minimum of the congestion window and the receiver window.
</details>

<details>
<summary>How TCP close the connection?</summary>

TCP closes a connection using a four-step process known as the four-way handshake:
1. **FIN from Client**: The client sends a FIN (Finish) packet to the server, indicating that it has finished sending data.
2. **ACK from Server**: The server acknowledges the client's FIN by sending an ACK (Acknowledge) packet back to the client.
3. **FIN from Server**: The server then sends its own FIN packet to the client, indicating that it has also finished sending data.
4. **ACK from Client**: Finally, the client acknowledges the server's FIN by sending an ACK packet back to the server.
After these four steps, the TCP connection is fully terminated. Both sides enter a TIME_WAIT state to ensure that any delayed packets are properly handled before completely closing the connection.
</details>

<details>
<summary>What is TTL? How does TTL change?</summary>

**TTL (Time to Live)** is a field in the IP header that specifies the maximum number of hops (routers) a packet can traverse before being discarded. It is used to prevent packets from circulating indefinitely in the network.

When a packet is sent, the TTL value is set to a specific number (e.g., 64, 128). Each time the packet passes through a router, the router decrements the TTL value by 1. If the TTL value reaches 0 before reaching its destination, the packet is discarded, and an ICMP "Time Exceeded" message is sent back to the sender.

</details>

<details>
<summary>What is HTTP and how does it work?</summary>

**HTTP (Hypertext Transfer Protocol)** is an application-layer protocol used for transmitting hypermedia documents, such as HTML, over the internet. It is the foundation of data communication for the World Wide Web.
HTTP works on a request-response model:
1. **Client Request**: A client (usually a web browser) sends an HTTP request to a server. The request includes a method (e.g., GET, POST), the URL of the resource, headers, and sometimes a body (for methods like POST).
2. **Server Response**: The server processes the request and sends back an HTTP response.
The response includes a status code (e.g., 200 OK, 404 Not Found), headers, and the requested resource (e.g., HTML content).
HTTP is stateless, meaning each request is independent and does not retain any information about previous requests. To maintain state, mechanisms like cookies and sessions are used.

</details>

<details>
<summary>HTTP/1.1 vs HTTP/2 vs HTTP/3. </summary>

**HTTP/1.1**:
- Text-based protocol
- Uses a single connection per request/response cycle
- Supports persistent connections (keep-alive)
- Limited multiplexing capabilities

**HTTP/2**:
- Binary protocol
- Supports multiplexing multiple requests/responses over a single connection
- Header compression to reduce overhead
- Server push capabilities

**HTTP/3**:
- Based on QUIC protocol (built on UDP)
- Improved performance with reduced latency
- Better handling of packet loss
- Connection migration support
- 
**Summary**: HTTP/2 and HTTP/3 offer significant performance improvements over HTTP/1.1, with HTTP/3 providing the most advanced features for modern web applications.
</details>

<details>
<summary>What is DNS and how it works?</summary>

**DNS (Domain Name System)** is a hierarchical and decentralized naming system used to translate human-readable domain names (e.g., www.example.com) into IP addresses (e.g 142.250.190.14) that computers use to identify each other on the network.
When a user enters a domain name in their web browser, the following steps occur:   
1. **DNS Query**: The browser sends a DNS query to a DNS resolver (usually provided by the ISP) to resolve the domain name.
2. **Recursive Resolution**: The DNS resolver checks its cache for the IP address. If not found, it performs a recursive query, contacting root servers, TLD (Top-Level Domain) servers, and authoritative name servers to find the IP address.
3. **Response**: Once the IP address is found, the DNS resolver sends it back to the browser.
4. **Connection**: The browser uses the IP address to establish a connection to the web server and retrieve the requested web page.
5. **Caching**: DNS responses are often cached by the resolver and the client to speed up future requests for the same domain.

**Summary**: DNS is essential for the functionality of the internet, allowing users to access websites using easy-to-remember domain names instead of numerical IP addresses.
</details>

<details>
<summary>What happens when you type a URL in the browser?</summary>

When you type a URL in the browser, the following steps occur:
1. **URL Parsing**: The browser parses the URL to extract the protocol (e.g http/https), domain name, path, and query parameters.
2. **DNS Resolution**: The browser sends a DNS query to resolve the domain name into an IP address.
3. **Establishing Connection**: The browser establishes a TCP connection to the server using the resolved IP address. If the URL uses HTTPS, a TLS handshake is performed to secure the connection.
4. **Sending HTTP Request**: The browser sends an HTTP request to the server, specifying the desired resource (e.g., a web page).
5. **Server Processing**: The server processes the request, retrieves the requested resource, and generates an HTTP response.
6. **Receiving HTTP Response**: The browser receives the HTTP response, which includes the status code, headers, and the requested content (e.g., HTML, CSS, JavaScript).
7. **Rendering the Page**: The browser renders the web page by parsing the HTML, applying styles from CSS, and executing JavaScript.
8. **Displaying the Page**: The fully rendered web page is displayed to the user.   

**Summary**: Typing a URL in the browser initiates a series of steps involving DNS resolution, connection establishment, HTTP communication, and page rendering to display the requested web content.
</details>

<details>
<summary>Explain latency vs throughput. </summary>

**Latency** refers to the time it takes for a data packet to travel from the source to the destination. It is typically measured in milliseconds (ms) and represents the delay experienced in communication. Lower latency is crucial for real-time applications like online gaming and video conferencing.

**Throughput**, on the other hand, refers to the amount of data that can be transmitted over a network in a given period of time. It is usually measured in bits per second (bps) or bytes per second (Bps). Higher throughput indicates a greater capacity for data transfer, which is important for applications like file downloads and streaming services.
**Use Cases**:
- Low Latency: Online gaming, video conferencing, VoIP
- High Throughput: File downloads, video streaming, cloud storage

**Trade-offs**: Networks with low latency may not always have high throughput, and vice versa. Optimizing for one can sometimes lead to compromises in the other.
**Summary**: Latency measures delay, while throughput measures data transfer capacity. Both are important for network performance but impact different aspects of user experience.
</details>

<details>
<summary>What is a load balancer? </summary>

**A load balancer** is a device or software that distributes network or application traffic across multiple servers to ensure no single server becomes overwhelmed. It helps improve the availability, reliability, and performance of applications by balancing the load, optimizing resource use, and preventing server overloads. Load balancers can operate at different layers of the OSI model, such as Layer 4 (transport layer) or Layer 7 (application layer), and can use various algorithms like round-robin, least connections, or IP hash to determine how to distribute traffic.

A load balancer is often the first building block for scalability and reliability in distributed systems.

</details>

<details>

<summary>Layer 4 vs Layer 7 load balancing. </summary>

**Layer 4 Load Balancing**:
- Operates at the transport layer (OSI Layer 4)
- Makes routing decisions based on IP address and TCP/UDP port information
- Faster and more efficient due to less processing overhead
- Suitable for simple load balancing scenarios where content-based routing is not required 

**Layer 7 Load Balancing**:
- Operates at the application layer (OSI Layer 7)
- Makes routing decisions based on application-level data, such as HTTP headers, cookies, or URL paths
- More flexible and capable of advanced routing, such as content-based routing and SSL termination
- Slightly slower due to increased processing overhead

**Use Cases**:
- Layer 4: Simple TCP/UDP load balancing, gaming servers, VoIP
- Layer 7: Web applications, APIs, content delivery networks (CDNs)

**Summary**: Layer 4 load balancing is faster and simpler, while Layer 7 load balancing offers more advanced features and flexibility for application-level traffic management.

</details>

<details>
<summary>What is NAT and how it works?</summary>

**NAT (Network Address Translation)** is a technique that translates private IP addresses into a public IP address when traffic passes through a router or gateway.

When a device on a private network sends a request to the internet, the NAT-enabled router modifies the source IP address of the outgoing packet to its own public IP address. It also keeps track of the mapping between the private IP address and the public IP address in a NAT table.

When the response comes back from the internet, the router looks up the NAT table to find the corresponding private IP address and modifies the destination IP address of the incoming packet before forwarding it to the appropriate device on the private network.
> NAT is a practical solution for IPv4 scarcity, but it introduces complexity for protocols that require peer-to-peer communication.

</details>


<details>

<summary>What is CDN and how it works? </summary>

**CDN (Content Delivery Network)** is a distributed network of servers strategically located in various geographic locations to deliver web content and services to users more efficiently.

When a user requests content from a website that uses a CDN, the request is routed to the nearest CDN server (also known as an edge server) based on the user's geographic location. The CDN server then delivers the requested content, such as images, videos, or web pages, from its cache rather than fetching it from the origin server. This reduces latency, decreases load on the origin server, and improves overall performance.
CDNs also use techniques like load balancing, caching, and compression to optimize content delivery and ensure high availability.
> A CDN is a distributed network of edge servers that delivers content from locations closer to users to reduce latency and improve performance.

</details>

<details>
<summary>Explain retry and timeout strategies.</summary>

**Retry and timeout strategies** are essential for ensuring reliable communication in networked applications. They help handle transient failures and improve the overall user experience.
1. **Timeouts**: A timeout is a predefined period that a client waits for a response from a server before considering the request failed. If the response is not received within this time frame, the client can take appropriate action, such as retrying the request or notifying the user of a failure. Timeouts should be set based on expected network conditions and application requirements.

2. **Retries**: When a request fails due to a timeout or other transient errors (e.g., network congestion, server overload), the client can retry the request. The retry strategy should include:
   - **Maximum Retry Attempts**: Limit the number of retries to avoid overwhelming the server or causing excessive delays.
   - **Backoff Strategy**: Implement an exponential backoff mechanism, where the wait time between retries increases exponentially with each attempt. This helps reduce the load on the server and allows time for transient issues to resolve.
   - **Jitter**: Introduce randomness to the backoff intervals to prevent synchronized retries from multiple clients, which can lead to a "thundering herd" problem.

**Summary**: Effective retry and timeout strategies involve setting appropriate timeouts, limiting retry attempts, and using backoff and jitter techniques to handle transient failures gracefully.
</details>

<details>
<summary>What is packet loss and how to handle it?</summary>

**Packet loss** occurs when one or more data packets transmitted over a network fail to reach their destination. This can happen due to various reasons, such as network congestion, faulty hardware, signal interference, or software bugs.
To handle packet loss, several strategies can be employed:
1. **Retransmission**: Protocols like TCP automatically detect lost packets through acknowledgments and retransmit them to ensure reliable data delivery.
2. **Forward Error Correction (FEC)**: This technique adds redundant data to the original packets, allowing the receiver to reconstruct lost packets without needing retransmission.
3. **Quality of Service (QoS)**: Implementing QoS policies can prioritize critical traffic, reducing the likelihood of packet loss for important data.
4. **Network Optimization**: Improving network infrastructure, such as upgrading hardware or increasing bandwidth, can help reduce packet loss.
5. **Monitoring and Alerts**: Regularly monitoring network performance and setting up alerts for high packet loss can help identify and address issues promptly.

**Summary**: Packet loss can be managed through retransmission, error correction, QoS, network optimization, and monitoring to ensure reliable communication.

</details>

<details>
<summary>What is a socket?</summary>

A **socket** is an endpoint for communication between two machines over a network. 

It is a combination of an IP address and a port number, allowing applications to send and receive data. They provide a programming interface for network communication, enabling developers to create networked applications.

Types of sockets include:
- **Stream Sockets (TCP)**: Provide reliable, connection-oriented communication.
- **Datagram Sockets (UDP)**: Provide connectionless communication with no guarantee of delivery.
- **Unix Domain Sockets**: Used for inter-process communication on the same host.

Socket lifecycle includes:
1. **Creation**: A socket is created using system calls (e.g., socket()).
2. **Binding**: The socket is bound to a specific IP address and port (e.g., bind()).
3. **Listening**: For server sockets, it listens for incoming connections (e.g., listen()).
4. **Accepting Connections**: Accept incoming connection requests (e.g., accept()).
5. **Data Transmission**: Send and receive data using send() and recv() functions.
6. **Closure**: Close the socket when communication is complete (e.g., close())

**Summary**: A socket is a communication endpoint that enables data exchange between applications over a network using various protocols.

</details>

<details>
<summary>What is head-of-line blocking? </summary>

**Head-of-line (HOL) blocking** is a performance-limiting phenomenon that occurs in networking and computer systems when a line of packets or data units is held up by the first packet in the queue. This means that if the first packet is delayed or lost, all subsequent packets must wait, even if they could be processed independently. HOL blocking can lead to increased latency and reduced throughput, especially in protocols like TCP, where packets must be processed in order.
HOL blocking can be mitigated through techniques such as:
1. **Multiplexing**: Using protocols like HTTP/2 or QUIC that allow multiple streams of data to be sent simultaneously over a single connection.
2. **Out-of-order delivery**: Allowing packets to be processed as they arrive, rather than waiting for earlier packets.
3. **Prioritization**: Implementing Quality of Service (QoS) to prioritize certain types of traffic.
4. **Buffering**: Using larger buffers to accommodate delays and reduce the impact of HOL blocking. 

**Summary**: Head-of-line blocking occurs when the first packet in a queue delays the processing of subsequent packets, leading to performance issues that can be mitigated through various techniques.
</details>

<details>
<summary>Explain REST vs RPC. </summary>

**REST (Representational State Transfer)**:
- Architectural style for designing networked applications
- Uses standard HTTP methods (GET, POST, PUT, DELETE)
- Stateless communication
- Resource-based, with each resource identified by a unique URL
- Data is typically exchanged in JSON or XML format

**RPC (Remote Procedure Call)**:
- Protocol for executing procedures on remote systems
- Can use various transport protocols (e.g., HTTP, TCP)
- Can be stateful or stateless
- Function-based, where clients call functions or methods on the server
- Data can be exchanged in various formats (e.g., JSON, XML, binary)

**Use Cases**:
- REST: Web services, APIs for web applications
- RPC: Microservices, distributed systems, internal service communication

**Summary**: REST is resource-oriented and uses standard HTTP methods, while RPC is function-oriented and can use various transport protocols. Both have their own use cases depending on application requirements.

</details>

<details>
<summary>What is idempotency in network APIs?</summary>

**Idempotency** in network APIs refers to the property of certain operations where performing the same operation multiple times has the same effect as performing it once. In other words, an idempotent operation can be repeated without changing the result beyond the initial application.

Idempotent HTTP methods include: (GET, PUT, DELETE, HEAD, OPTIONS)

Non-idempotent HTTP methods include: (POST, PATCH)

Idempotency is important in network APIs to ensure reliability and consistency, especially in scenarios where network failures or retries may occur. It helps prevent unintended side effects, such as duplicate resource creation or data corruption, when clients resend requests.

**Summary**: Idempotency ensures that repeated operations yield the same result, enhancing reliability and consistency in network APIs.
</details>

<details>
<summary>What is HTTPS and how TLS works? </summary>

**HTTPS (Hypertext Transfer Protocol Secure)** is an extension of HTTP that uses TLS (Transport Layer Security) to encrypt data transmitted between a client (e.g., web browser) and a server. This ensures confidentiality, integrity, and authenticity of the data exchanged.

**How TLS Works**:
1. **Handshake**: The client and server perform a TLS handshake to establish a secure connection. During this process, they agree on encryption algorithms and exchange cryptographic keys.
2. **Certificate Exchange**: The server presents its digital certificate, issued by a trusted Certificate Authority (CA), to the client for authentication.
3. **Session Key Generation**: Both parties generate a shared session key using asymmetric encryption (e.g., RSA, Diffie-Hellman) for secure communication.
4. **Data Encryption**: Once the session key is established, all data transmitted between the client and server is encrypted using symmetric encryption (e.g., AES).
5. **Integrity Check**: TLS also provides data integrity through message authentication codes (MACs) to ensure that data has not been tampered with during transmission.

**Summary**: HTTPS uses TLS to secure data transmission by encrypting communication, authenticating the server, and ensuring data integrity.
</details>

<details>
<summary>What is buffer? why we always need buffer when working with "file"?</summary>

A **buffer** is a temporary storage area in memory that holds data while it is being transferred between two locations, such as between a file and an application or between different components of a system. Buffers help manage differences in data processing speeds and improve overall performance by allowing data to be read or written in larger chunks rather than one byte at a time.

When working with files, buffers are essential for several reasons:
1. **Efficiency**: Reading or writing data in larger blocks reduces the number of I/O operations, which are typically slow and resource-intensive. This leads to better performance and reduced latency.
2. **Smooth Data Flow**: Buffers help accommodate variations in data processing speeds between the application and the file system, preventing bottlenecks and ensuring a steady flow of data.
3. **Reduced System Calls**: By using buffers, the number of system calls to read or write data is minimized, which can significantly improve performance, especially for large files.
4. **Data Integrity**: Buffers can help ensure that data is correctly formatted and complete before being written to a file, reducing the risk of corruption.

**Summary**: Buffers improve file I/O efficiency, smooth data flow, reduce system calls, and help maintain data integrity.
</details>

<details>
<summary>What is unix socket? When to use it?</summary>

A **Unix socket** (also known as a Unix domain socket or IPC socket) is a communication endpoint used for inter-process communication (IPC) on the same host operating system. Unlike network sockets that use IP addresses and ports for communication over a network, Unix sockets use file system paths to identify the communication endpoints.
Unix sockets are typically used in scenarios where high-performance communication between processes on the same machine is required, such as:
1. **Local Inter-Process Communication**: When two or more processes running on the same machine need to exchange data efficiently.
2. **Database Connections**: Many database systems (e.g., PostgreSQL, MySQL) use Unix sockets for local connections to improve performance.
3. **Microservices**: When microservices are deployed on the same host and need to communicate with each other.
4. **System Services**: Operating system services and daemons often use Unix sockets for communication with client applications.
5. **Performance-Critical Applications**: Applications that require low-latency communication can benefit from the reduced overhead of Unix sockets compared to network sockets.
6. **Security**: Unix sockets can provide better security for local communication since they are not exposed to the network.
**Summary**: Unix sockets facilitate efficient inter-process communication on the same host, making them ideal for local IPC, database connections, microservices, system services, and performance-critical applications.

</details>

<details>
<summary>What is TCP proxy? reverse proxy? and VPN?</summary>

**TCP Proxy**: A TCP proxy is an intermediary server that forwards TCP traffic between clients and servers. It listens for incoming TCP connections from clients and relays the data to the appropriate backend server. TCP proxies are often used for load balancing, traffic filtering, and improving security by hiding the backend servers' details.
**Reverse Proxy**: A reverse proxy is a type of proxy server that sits in front of one or more backend servers and forwards client requests to those servers. It acts as an intermediary for requests from clients seeking resources from the backend servers. Reverse proxies are commonly used for load balancing, caching, SSL termination, and enhancing security by hiding the backend infrastructure.
**VPN (Virtual Private Network)**: A VPN is a technology that creates a secure and encrypted connection over a public network, such as the internet. It allows users to send and receive data as if their devices were directly connected to a private network. VPNs are commonly used for secure remote access, protecting sensitive data, and bypassing geo-restrictions.

**Use Cases**:
- TCP Proxy: Load balancing, traffic filtering, security enhancement
- Reverse Proxy: Load balancing, caching, SSL termination, security enhancement
- VPN: Secure remote access, data protection, geo-restriction bypass

**Summary**: A TCP proxy forwards TCP traffic, a reverse proxy forwards client requests to backend servers, and a VPN creates a secure connection over a public network.

</details>

<details>

<summary>How your router at your home works?</summary>

A home router functions as a central hub that connects your local network (LAN) to the internet (WAN). It performs several key functions:
1. **Routing**: The router directs data packets between devices on your local network and the internet, ensuring that data reaches the correct destination.
2. **NAT (Network Address Translation)**: The router translates private IP addresses used within your home network to a single public IP address for internet communication, allowing multiple devices to share one internet connection.
3. **DHCP (Dynamic Host Configuration Protocol)**: The router assigns IP addresses to devices on your local network automatically, simplifying network configuration.
4. **Firewall**: The router provides basic security by filtering incoming and outgoing traffic, protecting your network from unauthorized access.
5. **Wi-Fi Access Point**: Most home routers include a built-in Wi-Fi access point, allowing wireless devices to connect to the network.
6. **Port Forwarding**: The router can be configured to forward specific types of incoming traffic to designated devices on the local network, enabling services like gaming or remote desktop access.

</details>

<details>

<summary>Inside LAN network, it uses IP or MAC address? Why?</summary>

Inside a LAN (Local Area Network), both IP addresses and MAC (Media Access Control) addresses are used, but they serve different purposes.
- **MAC Address**: MAC addresses are used for communication at the data link layer (Layer 2) of the OSI model. They are unique identifiers assigned to network interfaces for physical devices. When devices communicate within a LAN, they use MAC addresses to identify each other on the local network segment.
- **IP Address**: IP addresses are used for communication at the network layer (Layer 3) of the OSI model. They provide logical addressing and are used to route packets between different networks. Within a LAN, devices use IP addresses to identify each other and facilitate communication across the network.
When a device wants to send data to another device within the same LAN, it first uses the IP address to determine the destination. Then, it uses the Address Resolution Protocol (ARP) to map the IP address to the corresponding MAC address for actual data transmission.

**Summary**: Inside a LAN, MAC addresses are used for local communication at the data link layer, while IP addresses are used for logical addressing and routing at the network layer.
</details>
