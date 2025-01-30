**[CIDR (Classless Inter-Domain Routing)](https://en.wikipedia.org/wiki/Classless_Inter-Domain_Routing)** is a method of representing IP addresses and their associated subnet masks in a compact and flexible format. It is widely used in modern networking to allocate IP addresses efficiently and enable routing.

## Structure of CIDR Notation

CIDR notation combines:

- **IP Address:** Identifies the network or device (e.g., `192.168.1.0`).
- **Prefix Length:** Specifies the number of bits used for the network portion of the address, written as `/n` (e.g., `/24`).
Example:

- `192.168.1.0/24` means:
  - IP Address: `192.168.1.0`.
  - Subnet Mask: 255.255.255.0 (24 bits for the network).
  - Hosts: 256 total IPs (254 usable).

## Subnet Masks and Prefix Length

The subnet mask is a 32-bit number that divides the IP address into:

- **Network Portion:** The first n bits defined by the prefix length.
- **Host Portion:** The remaining bits for individual devices.

**Mapping Prefix Lengths to Subnet Masks**

| CIDR Notation | Subnet Mask | Total IPs | Usable IPs |
| --- | --- | --- | --- |
| /8 | 255.0.0.0 | 16,777,216 | 16,777,214 |
| /16 | 255.255.0.0 | 65,536 | 65,534 |
| /24 | 255.255.255.0 | 256 | 254 |
| /30 | 255.255.255.252 | 4 | 2 |

## Calculating Subnets and Hosts

1. Number of Hosts per Subnet
The number of hosts is calculated as:
$2^(32−𝑛)−2$

- `32` is the total bits in an IPv4 address.
- Subtract `2` for the **network address** and **broadcast address**.
Example:

- For `/24`:
  - Host bits = $32−24=8$.
  - Total hosts = $2^8 −2=254$.
2. Subnet Range
The number of subnets depends on how many bits are borrowed for subnetting.

For example:

- Start with a `/24` (255.255.255.0).
- Borrow 2 bits to create subnets:
  - New mask = `/26` (255.255.255.192).
  - Number of subnets = 22=4

## CIDR Aggregation

CIDR allows grouping multiple IP ranges into a single routing entry, known as **route aggregation** or **supernetting**.

Example:

- Combine `192.168.0.0/24` and `192.168.1.0/24` into a single block:
- Aggregated block: `192.168.0.0/23` (spans 512 IPs).

## CIDR in Action

Instead of using fixed classful IP ranges (Class A, B, C), CIDR enables custom subnet sizes to reduce waste.\
Example:

- A network needs 50 IPs.
  - Assign `/26` (64 IPs) instead of `/24` (256 IPs).
2. Simplifying Routing
CIDR helps ISPs advertise a single route for multiple IP ranges.\
Example:
   - Advertise `172.16.0.0/12` instead of multiple smaller blocks like `/16`.

## CIDR Example Walkthrough

1. **IP Address:** 192.168.1.128/25.
2. **Subnet Mask:**
   - `/25` = 255.255.255.128 (first 25 bits are `1`).
3. **Network Range:**
   - Network Address: `192.168.1.128`.
   - Broadcast Address: `192.168.1.255`.
   - Usable IPs: `192.168.1.129` to `192.168.1.254`.
4. **Hosts:**
   - Host Bits = $32−25=7$.
   - Total Hosts = $2^7 −2=126$.

## IPv6 and CIDR

CIDR is also used in IPv6, where the address space is much larger (128 bits).

- Example: `2001:db8::/48`.
  - Network portion: First 48 bits.
  - Host portion: Remaining 80 bits.
IPv6 simplifies subnetting because each subnet typically gets a `/64` allocation (16 bits for subnets, 64 bits for devices).
