### TCP/IP Model

The TCP/IP model is a 4-layer model that is more practical and widely used in real-world networking. It was developed by the U.S. Department of Defense and is the foundation of the modern internet.

`Layers of the TCP/IP Model` (from top to bottom):
1. **Application Layer:**
   - Combines the functions of the OSI Application, Presentation, and Session layers.
   - Handles high-level protocols and data representation.
   - Protocols: HTTP, FTP, SMTP, DNS.
2. **Transport Layer:**
   - Similar to the OSI Transport Layer.
   - Ensures reliable or unreliable data delivery.
   - Protocols: TCP (connection-oriented) and UDP (connectionless).
3. **Internet Layer:**
   - Corresponds to the OSI Network Layer.
   - Handles logical addressing and routing.
   - Protocols: IP, ICMP, ARP.
4. **Network Access Layer (Link Layer):**
   - Combines the OSI Data Link and Physical layers.
   - Manages hardware addressing and physical transmission.
   - Protocols: Ethernet, Wi-Fi.

How data flows through TCP/IP Model with the help of an example browsing a website.

**1. Application Layer:**

   - The user enters a URL (e.g., https://www.example.com) in a web browser.
 
   - The browser uses the HTTP/HTTPS protocol to request the webpage from the web server.

**2. Transport Layer:**

   - The HTTP request is broken into segments.

   - The TCP protocol adds headers, including source and destination port numbers (e.g., port 443 for HTTPS), and ensures reliable delivery.

**3. Internet Layer:**

   - Each TCP segment is encapsulated into an IP packet.

   - The IP packet includes source and destination IP addresses (e.g., the user's IP and the web server's IP).

**4. Network Access Layer:**

   - The IP packet is encapsulated into a frame with a MAC address for the next hop (e.g., the router).

   - The frame is transmitted over the physical medium (e.g., Ethernet or Wi-Fi) to the web server.
