**Subnetting** is a fundamental concept in networking that involves dividing a larger IP network into smaller, more manageable subnetworks (or subnets). This process improves network efficiency, enhances security, and reduces congestion. Let’s break it down step by step:

### [1. What is Subnetting?]()
- Subnetting allows you to split a single IP network into multiple smaller networks.
- It is done by borrowing bits from the **host portion** of an IP address to create a **subnet mask**, which defines the boundaries of each subnet.

### [2. Why Use Subnetting?]()
- **Efficient IP Address Allocation:** Prevents wastage of IP addresses by allocating only the required number of addresses to each subnet.
- **Improved Network Performance:** Reduces network congestion by limiting broadcast traffic to smaller subnets.
- **Enhanced Security:** Isolates network segments, making it harder for attackers to move laterally.
- **Simplified Management:** Makes it easier to organize and troubleshoot networks.

### [3. Key Concepts in Subnetting]()
a. **IP Address and Subnet Mask**
- An I**P address** (IPv4) is a 32-bit number divided into two parts:
  - **Network Portion:** Identifies the network.
  - **Host Portion:** Identifies the device within the network.

- A subnet mask is a 32-bit number that distinguishes the network and host portions of the IP address.
  - Example: `255.255.255.0` (or `/24` in CIDR notation) means the first 24 bits are the network portion.

b. **CIDR Notation**
- **Classless Inter-Domain Routing (CIDR)** is a compact way to represent IP addresses and their subnet masks.
- Example: `192.168.1.0/24` means the first 24 bits are the network portion.

c. **Network and Host Bits**
- The subnet mask determines how many bits are used for the network and how many for hosts.
- Example: In `192.168.1.0/24`:
  - Network bits: 24
  - Host bits: 8 (32 - 24 = 8)
  - Number of hosts per subnet: $2^8−2=254$ (subtracting the network and broadcast addresses).

### [4. Steps to Subnet a Network]()

**Step 1: Determine the Requirements**
- How many subnets are needed?
- How many hosts are needed per subnet?

**Step 2: Choose a Subnet Mask**
- Based on the number of subnets and hosts, decide how many bits to borrow from the host portion.
- Example: If you need 4 subnets, you need to borrow 2 bits (since $2^2 =4$).

**Step 3: Calculate Subnet Ranges**
- Use the subnet mask to determine the range of IP addresses for each subnet.
- Example: For `192.168.1.0/26` (subnet mask `255.255.255.192`):
  - Subnet 1: `192.168.1.0` to `192.168.1.63`
  - Subnet 2: `192.168.1.64` to `192.168.1.127`
  - Subnet 3: `192.168.1.128` to `192.168.1.191`
  - Subnet 4: `192.168.1.192` to `192.168.1.255`

**Step 4: Assign Subnets**
- Assign each subnet to a specific network segment (e.g., different departments or floors in a building).

### [5. Subnetting Example]()

**Scenario:**
- You have the IP network `192.168.1.0/24`.
- You need to create 4 subnets, each with at least 50 hosts.

**Solution:**
1. Determine the number of bits to borrow:
- To create 4 subnets, borrow 2 bits (since $2^2 =4$).
- New subnet mask: `/26` (`255.255.255.192`).

2. Calculate the number of hosts per subnet:
- Host bits: $32−26=6$.
- Number of hosts: $2^6 −2=62$ (enough for 50 hosts).

3. Define the subnet ranges:

  - Subnet 1: `192.168.1.0/26` (Hosts: `192.168.1.1` to `192.168.1.62`)
  - Subnet 2: `192.168.1.64/26` (Hosts: `192.168.1.65` to `192.168.1.126`)
  - Subnet 3: `192.168.1.128/26` (Hosts: `192.168.1.129` to `192.168.1.190`)
  - Subnet 4: `192.168.1.192/26` (Hosts: `192.168.1.193` to `192.168.1.254`)

### [6. Subnetting Cheat Sheet]()
| **Subnet Mask (CIDR)** | **Subnet Mask (Decimal)** | **Number of Subnets** | **Number of Hosts per Subnet** |
| --- | --- | --- | --- |
| /24 | 255.255.255.0 | 1 | 254 |
| /25 | 255.255.255.128 | 2 | 126 |
| /26 | 255.255.255.192 | 4 | 62 |
| /27 | 255.255.255.224 | 8 | 30 |
| /28 | 255.255.255.240 | 16 | 14 |
| /29 | 255.255.255.248 | 32 | 6 |
| /30 | 255.255.255.252 | 64 | 2 |

### [7. Tools for Subnetting]()

- **Subnet Calculators:** Online tools that automate subnetting calculations.
- **Binary Conversion:** Understanding binary is key to mastering subnetting.

### [8. Common Mistakes to Avoid]()

- Forgetting to subtract 2 for the network and broadcast addresses.
- Misaligning subnet boundaries.
- Overlapping subnets.