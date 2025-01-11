### subnet
192.168.x.x represents a network range. A smaller block of IP addresses within this range is called a subnet."

ex:So, 192.168.1.0/24 is a subnet that contains IPs like 192.168.1.1, 192.168.1.2, etc.
### subnet mask
"The subnet mask determines how many IP addresses can exist within a subnet and how the network is divided into smaller blocks.

ex: Subnet Mask: 255.255.255.0 (or /24 in CIDR notation)
This creates a subnet with 256 IPs (e.g., 192.168.1.0 to 192.168.1.255).
Usable IPs: 192.168.1.1 to 192.168.1.254 (excluding the network 192.168.1.0 and broadcast 192.168.1.255).