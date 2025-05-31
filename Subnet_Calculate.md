# Subnet Calculating
Okay, let's tackle the subnetting for your IT Startup network. You have one private network address space and need to divide it among your 5 departments and 1 server room (total of 6 logical network segments).

First, we need to choose a private IP address range. A common choice is the Class C private range: `192.168.1.0` to `192.168.1.255` with a default subnet mask of `255.255.255.0` (/24).



## 1. Determine the Number of Subnets Needed:**

You have 6 logical segments (5 departments + 1 server room), so you need at least 6 subnets.



## 2. Determine the Number of Hosts per Subnet:

Each department has 4-5 devices. The server room has 4 servers. So, the maximum number of hosts in any single subnet is around 5. We need to ensure each subnet can accommodate at least 5 usable host addresses.



## 3. Calculate the Number of Bits Needed for Subnetting:

To get at least 6 subnets, we need to borrow bits from the host portion of the IP address. The formula is $2^n \ge \text{number of subnets}$, where 'n' is the number of bits borrowed.

* $2^2 = 4$ (Not enough)
* $2^3 = 8$ (Sufficient)

So, we need to borrow 3 bits from the host portion of the default /24 subnet mask.



## 4. Determine the New Subnet Mask:

The default subnet mask is `255.255.255.0`, which in binary is `11111111.11111111.11111111.00000000`.

By borrowing 3 bits from the host portion, our new subnet mask in binary becomes: `11111111.11111111.11111111.11100000`.

Converting this back to dotted decimal notation:

$11100000_2 = 1 \times 2^7 + 1 \times 2^6 + 1 \times 2^5 + 0 \times 2^4 + 0 \times 2^3 + 0 \times 2^2 + 0 \times 2^1 + 0 \times 2^0 = 128 + 64 + 32 = 224$

Therefore, your new subnet mask will be **`255.255.255.224`** or **/27** in CIDR notation.



## 5. Calculate the Number of Usable Hosts per Subnet:

With 3 bits borrowed for subnetting, we have $8 - 3 = 5$ bits remaining for the host portion. The number of possible host addresses per subnet is $2^5 = 32$.

The number of *usable* host addresses per subnet is $2^5 - 2 = 30$ (we subtract 2 because the first address in each subnet is the network address, and the last address is the broadcast address).

30 usable host addresses per subnet are more than enough to accommodate the 4-5 devices in each department and the 4 servers in the server room.

## 6. Determine the Subnet Addresses and Ranges:

Now, let's determine the network address for each of your 6 segments. The subnet block size is $256 - 224 = 32$. This means each subnet starts 32 addresses after the previous one.

Assuming our base network is `192.168.1.0`:

* **Subnet 1 (e.g., Software Development):**
    * Network Address: `192.168.1.0`
    * Usable Host Range: `192.168.1.1` - `192.168.1.30`
    * Broadcast Address: `192.168.1.31`

* **Subnet 2 (e.g., Marketing & Sales):**
    * Network Address: `192.168.1.32`
    * Usable Host Range: `192.168.1.33` - `192.168.1.62`
    * Broadcast Address: `192.168.1.63`

* **Subnet 3 (e.g., Customer Support):**
    * Network Address: `192.168.1.64`
    * Usable Host Range: `192.168.1.65` - `192.168.1.94`
    * Broadcast Address: `192.168.1.95`

* **Subnet 4 (e.g., Finance & Administration):**
    * Network Address: `192.168.1.96`
    * Usable Host Range: `192.168.1.97` - `192.168.1.126`
    * Broadcast Address: `192.168.1.127`

* **Subnet 5 (e.g., Human Resources):**
    * Network Address: `192.168.1.128`
    * Usable Host Range: `192.168.1.129` - `192.168.1.158`
    * Broadcast Address: `192.168.1.159`

* **Subnet 6 (Server Room):**
    * Network Address: `192.168.1.160`
    * Usable Host Range: `192.168.1.161` - `192.168.1.190`
    * Broadcast Address: `192.168.1.191`

## Summary:
You can use the private network `192.168.1.0` with a subnet mask of **`255.255.255.224`** to create 8 subnets (we only need 6). Each subnet will have 30 usable host addresses, which is sufficient for your needs. The table above shows the network address, usable host range, and broadcast address for each of your departments and the server room.

Now you can assign IP addresses within these ranges to the devices in each department and the servers in the server room within Cisco Packet Tracer. Remember to configure the subnet mask (`255.255.255.224`) on all devices.

Let me know if you have any questions about this subnetting plan or if you'd like to proceed with setting up the topology in Packet Tracer!
`_(Generate by Gemini)`