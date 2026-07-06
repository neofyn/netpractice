_This project has been created as part of the 42 curriculum by fyudris._

# Net Practice
## Description
This project is for teaching the user about networking. Specifically about IP addresses, subnetting, using routers, switches, and connecting hosts to form a network of computers, including to the internet.

Understanding these concepts will also naturally teach:
 - IPv4 Basics
 - Binary, decimal, and CIDR subnet mask conversion
 - Network and host bits
 - Creating ranges of IPs
 - Broadcast addresses and Network Addresses
 - Address Classes: A-E, Loopback IP (127.0.0.0), Private IP (192.168.0.0)

## Instructions
To install the software, download net_practice.1.8.tgz from intra and extract the archive into a folder on your local host. run "bash run.sh" to start program, which will open in your preferred browser. Select either the Training or Evaluation tab depending on what is needed. Input your intra name as your login, and click Start!

For each Level, the user needs to input the correct IP addresses and subnet masks to make the network configuration work. Pressing "Check again" on the top left checks if the goals on the top have been met. On the bottom right, a log will be processed that shows errors that can be helpful in creating the network.
If all goals have been met, click "Get my config" dow download the .json file for that level, which will be put into the root directory of your project folder (in the same directory as this readme file).

Clicking "Next level" will move on to the next level until all 10 levels have been completed.

## Resources
### Humans
Tania Marcos (tmarcos), Danny Flynn (dflynn)

### Videos
Subnet Mask - Explained by PowerCert Animated Videos
https://www.youtube.com/watch?v=s_Ntt6eTn94

Routing Tables | CCNA - Expalined by PowerCert Animated Videos
https://www.youtube.com/watch?v=CGmTvukObOw

You Suck at Subnetting (Playlist) by NetworkChuck
https://www.youtube.com/watch?v=5WfiTHiU4x8&list=PLIhvC56v63IKrRHh3gvZZBAGvsvOhwrRF

### Websites
https://en.wikipedia.org/wiki/Internet_protocol_suite
https://en.wikipedia.org/wiki/Transmission_Control_Protocol
https://en.wikipedia.org/wiki/Internet_Protocol
https://en.wikipedia.org/wiki/Datagram

### TCP/IP
The Internet Protocol suite refers to **TCP/IP**, and is a framework for organizing communication protocols used in the internet and computer networks.
The suite includes:
 - TCP (Transmission Control Protocol).
 - IP (Internet Protocol).
 - UDP (User Datagram Protocol)

#### TCP (Transmission Control Protocol)
TCP is a communication protocol used to ensure data is sent and received accurately between devices.

It provides reliable, ordered, and error-checked delivery of a stream of bytes between applications running on hosts communicating via an IP network.

It is a list of rules/standards which are devided into layers:
|    |  | |
| ------- | -------     | -------- |
| Layer 4 | APPLICATION |End-user software, e.g.: web browsers, email clients, etc.|
| Layer 3 | TRANSPORT   | End-to-End communication/Ports: TCP (e.g. 80 (HTTP), 433 (HTTPS), 25 (SMTP), UDP (e.g. 53 (DNS), 67 (DHCP)) |
| Layer 2 | INTERNET    | IP Addressing and routing of packages|
| Layer 1 | PHYSICAL    | Physial transmission of data over a network, e.g. Ethernet cables|

#### LAN
LAN (Local Area Network) is a network of devices talking to each other within limited physical area, e.g. a home, office building.

#### IP
- IP (Internet Protocol) is a logical address of a device within a network allocated by a router.

- It helps to identify and locate a machine/device within a LAN.

- It enables devices to communicate with each other.

- Each device will have a unique IP Address.

- **IPv4 (32-bit)**
    ```c
    192.168.1.1
    ```
- **IPv6 (128-bit)**
    ```c
    2001:Odb8:85a3:0000:0000:8a2e:0370:7334
    ```

The network layer communications protocol for relaying datagrams (a basic transfer unit that connectionless, where each unit is self-contained, independently routed, and does not require a pre-established connection) across network boundaries. It uses a routing function that enables internetworking, that makes the internet. Delivers packets from the source host to the destination host based on IP addresses in the packet headers.

### Classes
Class A:
1.0.0.0 - 126.255.255.255
Subnet mask 255.0.0.0

Class B:
128.0.0.0 - 191.255.0.0
Subnet mask 255.255.0.0

Class C:
192.0.0.0 - 223.255.255.0
Subnet mask 255.255.255.0

Class D: (Reserved for Governments):
224.0.0.0 - 239.255.255.255
(classless)

Class E: (Reserved for experimental):
240.0.0.0 - 255.255.255.255
(classless)

Loopback network tests for everyone at:
127.0.0.0 - 127.255.255.255

### Fixing IP Shortage
RFC 1918
In 1996 RFC 1918 decided that Private network addresses existed and were no longer unique.

Class A Private Addresses:
10.0.0.0 - 10.255.255.255
Subnet mask 255.0.0.0

Class B Private Addresses:
172.16.0.0 - 172.31.255.255
Subnet mask 255.255.0.0

Class C Private Addresses:
192.168.0.0 - 192.168.255.255
Subnet mask 255.255.255.0

### NAT (Network Address Translation)
When a device with private IP goes to the internet, NAT translates the private IP to the one assigned IP address that your router uses, then connects.

The router handles where the traffic goes in and out of.

ifconfig finds your private IP
find your public IP by looking it up online

### IPv6
IPv4 has 2^32 addresses to use
IPv6 has 2^128 addresses to use

looks like:
2001:db8:3333:4444:5555:6666:7777:8888

### Converting binary to decimal
Decimal: 192.168.0.1
Binary: 11111111.11111111.11111111.11111111
4 octets
32 bits
(8 bits make 1 byte)
IP addresses are 4 bytes/32 bits

Powers of 2
converting from matrix/binary to decimal
128 | 64 | 16 | 8 | 4 | 2 | 1

11000000.10101000.00000001.00010101
192     .168     .1       .21

### Subnet masks
the 1s show you which one are the network bits.
the 0s show which parts of the address are host bits.

255.255.255.0
11111111.11111111.11111111.00000000

2^8 gives us 256. 2 addresses are reserved (0 and 255), so we have 254 hosts we can have. 0 is reserved for the subnet address, and 255 is reserved for the broadcast address.
there are 8x 0s in that address.

Therefore, if the subnet mask is
255.255.254.0
11111111.11111111.11111110.00000000
2^9 = 512 addresses. 2 addresses are reserved, therefore 510 are possible for devices

Changing the subnet mask to suit the need is subnetting.

### Subnetting
#### Subnetting based on how many networks you need (NetworkChuck method)
When you need more networks, take bits from the host bits.

128 | 64  | 32 | 16 | 8  | 4 | 2 | 1
256 | 128 | 64 | 32 | 16 | 8 | 4 | 2 ---> This is how many networks you'll get when you change your submask by a certain number of bits.
So for example, if you need 4 networks, it takes 2 bits to get there.
If you need 17 networks, you need 5 bits.

11111111.11111111.11111111.11000000 This subnet mask will give 4 subnets
255.255.255.192

This is also called a /26 network, because there are 26x 1s in the subnet mask

To find the increment, find the last network bit.
in the last section:
.. | .. | .. | 11000000
                ^ This is our increment, which is 64.
Our range of IP addresses for each network therefore becomes:
192.168.1.0 - 192.168.1.63
192.168.1.64 - 192.168.1.127
192.168.1.128 - 192.168.1.191
192.168.1.192 - 192.168.1.255
(it works as an index and must include the 0, so there are 64 in total)

To find number of addresses, it is 2^(number of host bits)
Therefore the amount of hosts, is 64 minus the subnet address and broadcast address
62 number of hosts.

#### Subnetting based on how many hosts you need (NetworkChuck method)

use the double chart to find out how many host bits we need to have.
We need 40 hosts on each network, therefore find the number that can hold 40 addresses:
256 | 128 | 64 | 32 | 16 | 8 | 4 | 2
             ^ This one
Then we count how many bits we need to get to 64. We need 6 bits.

So our subnet mask will need to be:
11111111 . 11111111 . 11111111 . 11000000 (6 bits are now 0)
                                  ^ this is our increment, which is 64 in the double octet
255.255.255.192

If our private IP is 10.1.1.0
We will assign each network an admin:
10.1.1.0 /26
10.1.1.64 /26
10.1.1.128 /26

#### Reverse subnetting (NetworkChuck method)

Question:
172.17.16.255 /20
What is the network address?
What is the broadcast address?
What is the range?

First find our subnet mask, which is determined by the /20 and means there are 20 1's
255.255.240.0
11111111.11111111.11110000.00000000
16 is the increment

So we can build the network ranges.
172.17.0.0 - 172.17.15.255
172.17.16.0 - 172.17.31.255 ----> This is where 172.17.16.255 lives
172.17.32.0 - 172.17.65.255

Your default gateway should be in your own network so you can access the internet.

#### Subnetting subnets: VLSM - variable length subnet mask(ing) (NetworkChuck method)
Based on host requirements:

For everything, you'll always use this method:
1. Use the nosferat2 chart to calculate how many host bits you need
2. hack the host bits
3. find the increment
4. create the networks

If our network is:
172.21.42.0 /24
our subnet mask based on /24 is
255.255.255.0

We have the requirements:
Workers -> 117
Servers -> 26
Robots -> 57
Guests -> 10

We always start with the biggest networks we need to create first, then go smaller.

For our workers
We'll need the network addresses 172.21.42.0 - 172.21.42.127
Therefore the subnet for the workers will be 172.21.42.0 /25

For the robots
The subnet mask will need 255.255.255.192
This is /26 and will have an increment of 64
So our network addresses will be 172.21.42.128 - 172.21.42.191 (we start 1 address after the last used one from our workers.
Subnet for the robots will be 172.21.42.128 /26

For the servers:
start with 172.21.42.192 (which is one higher than the above where the robots are
172.21.42.192 - 172.21.42.223
Subnet for the servers will be 172.21.42.192 /27

For the guests:
Range will be 172.21.42.224 - 172.21.42.239
Subnet will be 172.21.42.224 /28

Subnet is the network address, the first address.

/24 is CIDR notation for the subnet mask

Sub network of a larger network, defines a range of IP addresses of a network.

Network address with CIDR notation of the subnet mask:
192.168.0.1 /24

1. convert subnet mask to binary
    - refer to the 2^ chart
2. Find the CIDR notation
    - total number of network bits
3. Find the inrement
    - the last network bit in the 2^ chart
4. Create the networks and find the ranges for each
    - include the network and broadcast addresses which are always reserved (first and last addresses)

### Quick Notes
#### Switches
Connects multiple devices to allow computers to communicate to each other
Switch can be connected to a router, which connects the LAN (local area network) with the external network (WAN - wider area netowrk)

#### Gateway
Gateway and router can be the same thing.
Router: Sends data packets between different networks based on IP addresses
Gateway: is a gate between two networks, allowing them to communicate


#### Subnet Chart

|    SUBNET       | CIDR |   BINARY    | INC | IPs | NETWORK  | BROADCAST   |   HOST RANGE         |
|-----------------|------|-------------|-----|-----|----------|-------------|----------------------|
| 255.255.255.254 | /31  | ...11111110 |   2 |   0 |  x.x.x.0 |   x.x.x.1   |                      |
| 255.255.255.252 | /30  | ...11111100 |   4 |   2 |  x.x.x.0 |   x.x.x.3   |  x.x.x.1 - x.x.x.2   |
| 255.255.255.248 | /29  | ...11111000 |   8 |   6 |  x.x.x.0 |   x.x.x.7   |  x.x.x.1 - x.x.x.6   |
| 255.255.255.240 | /28  | ...11110000 |  16 |  14 |  x.x.x.0 |   x.x.x.15  |  x.x.x.1 - x.x.x.14  |
| 255.255.255.224 | /27  | ...11100000 |  32 |  30 |  x.x.x.0 |   x.x.x.31  |  x.x.x.1 - x.x.x.30  |
| 255.255.255.192 | /26  | ...11000000 |  64 |  62 |  x.x.x.0 |   x.x.x.63  |  x.x.x.1 - x.x.x.62  |
| 255.255.255.128 | /25  | ...10000000 | 128 | 126 |  x.x.x.0 |   x.x.x.127 |  x.x.x.1 - x.x.x.126 |
| 255.255.255.0   | /24  | ...00000000 |   1 | 254 |  x.x.x.0 |   x.x.x.255 |  x.x.x.1 - x.x.x.254 |

#### Quick Subnet Chart
|             |      |      |      |      |      |      |      |     |
|-------------|------|------|------|------|------|------|------|-----|
| CIDR(3rd)   |  /17 |  /18 |  /19 |  /20 |  /21 |  /22 |  /23 | /24 |
| CIDR(4th)   |  /25 |  /26 |  /27 |  /28 |  /29 |  /30 |  /31 | /32 |
| Inc + Bit   |  128 |   64 |   32 |   16 |    8 |    4 |    2 |   1 |
| Binary Mask | .128 | .192 | .224 | .240 | .248 | .252 | .254 |  .0 |
| Usable Hosts|  126 |   62 |   30 |   14 |    6 |    2 |    2 |   0 |

Note: for /31, 2 usable hosts exist, but there are no separate network or broadcast addresses available, and are used for point to point links where broadcast is unnecessary.

#### Conversion

Binary to decimal conversion table:
128 | 64 | 32 | 16 | 8 | 4 | 2 | 1

#### Subnetting based on how many networks needed
if you need 13 more networks, you need 4 bits (seen in the conversion table) to get there.

256 | 128 | 64 | 32 | 16 | 8 | 4 | 2  <--(# of networks you'll get)
                       ^ We need this one, takes 4 bits to get there

255.255.255.0 aka /24
11111111.11111111.11111111.00000000
11111111.11111111.11111111.11110000 <--take 4 network bits
255.255.255.240 will be your new subnet mask. aka /28

#### Counting hosts
The amount of 0's help find how many hosts there will be.
2^(amount of 0's) = (# of addresses)
(# of addresses) - 2 = (# of hosts)

#### Find increment
256 - (subnet mask value) = increment

for 255.255.255.240:

256 - 240 = 16 is our increment
OR
the rightmost network bit = 16

#### Find network ranges

192.168.0.0 /28:
11111111.11111111.11111111.11110000

192.168.0.0 - 192.168.0.15
192.167.0.16 - 192.168.0.31
192.168.0.32 - 192.168.0.47
...63
...79
...95
...111
...127
...143
...159
...175
...191
...207
...223
...239
...255

### Subnetting based on how many hosts needed Example

Use the double chart to find how many host bits we need to have
If we need 30 hosts per network:

256 | 128 | 64 | 32 | 16 | 8 | 4 | 2 <-- Hosts table powers or 2 addresses
                 ^ We need this one, therefore 5 host bits saved.

11111111.11111111.11111111.11100000
255.255.255.224
/27 subnet mask

Increment is 32, the rightmost 1-bit in the subnet mask.
or 256 - 224 = 32

192.168.0.0 - 192.168.0.31
...63
...95
...127
...159
...191
...223
...255

### Reverse Subnetting Example
#### Question
Question: 182.17.16.255 /20
What is the network address?
What is the broadcast address?
what is the range?

#### subnet mask
/20
11111111.11111111.11110000.00000000
255.255.240.0 is the subnet mask

#### increment
rightmost 1-bit is 16
or 256 - (network mask:240) = 16

#### build the network ranges
182.17.0.0 - 182.17.15.255
182.17.16.0 - 182.17.31.255 <-- 182.17.16.255 lives here

#### network address
182.17.16.0

#### broadcast address
last address in 182.17.16.0 is:
182.17.31.255 <-- Broadcast address

#### range
182.17.16.0 - 182.17.31.255

### Tips for Netpractice
1. take out all noise and start clean
remove everything
2. work backwards with default values
3. solve one goal at a time
4. refer to a subnet chart

## Submission Details
10 exported config files are located in the root directory corresponding to the 10 levels completed in Net Practice.
