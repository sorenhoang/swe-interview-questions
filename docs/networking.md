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