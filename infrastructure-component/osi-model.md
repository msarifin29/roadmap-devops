The **OSI (Open Systems Interconnection) Model** is a set of rules that explains how different computer systems communicate over a network. OSI Model was developed by the International Organization for Standardization (ISO). The OSI Model consists of 7 layers and each layer has specific functions and responsibilities. This layered approach makes it easier for different devices and technologies to work together. OSI Model provides a clear structure for data transmission and managing network issues. The OSI Model is widely used as a reference to understand how network systems function.

The OSI model is a 7-layer conceptual framework that standardizes the functions of a communication system. It was developed by the International Organization for Standardization (ISO) in 1984. Each layer has a specific role and interacts with the layers above and below it.

`Layers of the OSI Model` (from top to bottom):
1. [**Application Layer (Layer 7):**](https://www.geeksforgeeks.org/application-layer-in-osi-model/)
   - Closest to the end user.
   - Provides network services directly to applications (e.g., web browsers, email clients).
   - Protocols: HTTP, FTP, SMTP, DNS.
2. [**Presentation Layer (Layer 6):**](https://www.geeksforgeeks.org/presentation-layer-in-osi-model/)
   - Translates data into a format the application layer can understand.
   - Handles encryption, compression, and data formatting.
   - Example: SSL/TLS for encryption.
3. [**Session Layer (Layer 5):**](https://www.geeksforgeeks.org/session-layer-in-osi-model/)
   - Manages sessions between applications.
   - Establishes, maintains, and terminates connections.
   - Example: NetBIOS, RPC.
4. [**Transport Layer (Layer 4):**](https://www.geeksforgeeks.org/transport-layer-in-osi-model/)
   - Ensures reliable data transfer between devices.
   - Handles error correction, flow control, and segmentation.
   - Protocols: TCP (reliable) and UDP (unreliable).
5. [**Network Layer (Layer 3):**](https://www.geeksforgeeks.org/network-layer-in-osi-model/)
   - Handles logical addressing and routing of data packets.
   - Determines the best path for data to travel.
   - Protocols: IP, ICMP, ARP.
6. [**Data Link Layer (Layer 2):**](https://www.geeksforgeeks.org/data-link-layer/)
   - Manages direct communication between devices on the same network.
   - Handles MAC addressing and error detection.
   - Protocols: Ethernet, PPP.
7. [**Physical Layer (Layer 1):**]((https://www.geeksforgeeks.org/physical-layer-in-osi-model/))
   - Deals with the physical connection between devices.
   - Transmits raw bits over a physical medium (e.g., cables, radio waves).
   - Example: Ethernet cables, Wi-Fi.

How data flows through OSI Model with the help of an example mentioned below.

Let us suppose, Person A sends an e-mail to his friend Person B.

- **Step 1:** Person A interacts with e-mail application like Gmail, outlook, etc. Writes his email to send. (This happens at Application Layer).

- **Step 2:** At Presentation Layer, Mail application prepares for data transmission like encrypting data and formatting it for transmission.

- **Step 3:** At Session Layer, there is a connection established between the sender and receiver on the internet.

- **Step 4:** At Transport Layer, Email data is broken into smaller segments. It adds sequence number and error-checking information to maintain the reliability of the information.

- **Step 5:** At Network Layer, addressing of packets is done in order to find the best route for transfer.

- **Step 6:** At Data Link Layer, data packets are encapsulated into frames, then MAC address is added for local devices and then it checks for error using error detection.

- **Step 7:** At Physical Layer, Frames are transmitted in the form of electrical/ optical signals over a physical network medium like ethernet cable or WiFi.

After the email reaches the receiver i.e. Person B, the process will reverse and decrypt the e-mail content. At last, the email will be shown on Person B email client.