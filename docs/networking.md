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