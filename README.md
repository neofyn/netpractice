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
To install the software, download net_practice.1.8.tgz from intra and extract the archive into a folder on your local host:
```cpp
tar -xvzf filename.tar.gz
```
Run `bash run.sh` to start program, which will open in your preferred browser. Select either the Training or Evaluation tab depending on what is needed. Input your intra name as your login, and click Start!

For each Level, the user needs to input the correct IP addresses and subnet masks to make the network configuration work. Pressing "Check again" on the top left checks if the goals on the top have been met. On the bottom right, a log will be processed that shows errors that can be helpful in creating the network.
If all goals have been met, click "Get my config" dow download the .json file for that level, which will be put into the root directory of your project folder (in the same directory as this readme file).

Clicking "Next level" will move on to the next level until all 10 levels have been completed.

## Resources
### Humans
Danny Flynn (dflynn),Christopher Santos (chsantos)

### Videos
Subnet Mask - Explained by PowerCert Animated Videos
https://www.youtube.com/watch?v=s_Ntt6eTn94

NetPractice: An Intro to IP Addresses and Subnets
https://www.youtube.com/watch?v=HQUw0CfQWAM

You Suck at Subnetting (Playlist) by NetworkChuck
https://www.youtube.com/watch?v=5WfiTHiU4x8&list=PLIhvC56v63IKrRHh3gvZZBAGvsvOhwrRF

### Websites
https://en.wikipedia.org/wiki/Internet_protocol_suite
https://en.wikipedia.org/wiki/Transmission_Control_Protocol
https://en.wikipedia.org/wiki/Internet_Protocol


### TCP/IP
The Internet Protocol suite refers to **TCP/IP**, and is a framework for organizing communication protocols used in the internet and computer networks.
The suite includes:
 - TCP (Transmission Control Protocol).
 - IP (Internet Protocol).
 - UDP (User Datagram Protocol)

### TCP (Transmission Control Protocol)
TCP is a communication protocol used to ensure data is sent and received accurately between devices.

It provides reliable, ordered, and error-checked delivery of a stream of bytes between applications running on hosts communicating via an IP network.

It is a list of rules/standards which are devided into layers:
|    |  | |
| ------- | -------     | -------- |
| Layer 4 | APPLICATION |End-user software, e.g.: web browsers, email clients, etc.|
| Layer 3 | TRANSPORT   | End-to-End communication/Ports: TCP (e.g. 80 (HTTP), 433 (HTTPS), 25 (SMTP), UDP (e.g. 53 (DNS), 67 (DHCP)) |
| Layer 2 | INTERNET    | IP Addressing and routing of packages|
| Layer 1 | PHYSICAL    | Physial transmission of data over a network, e.g. Ethernet cables|

### LAN
LAN (Local Area Network) is a network of devices talking to each other within limited physical area, e.g. a home, office building.

### IP
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

For netPractice we only use iPv4.

An IP Address has 4 Octets separated by a dot. The first 3 Octets are called `Network Portion`. And the last one is `Host Portion` (a device, e.g. a computer, phone, etc.).
```c
Octet		Octet		Octet		Octet
192.			168.			1.			1.
```
- A host (device) will be always assigned a usable IP Address.
- There are always two IP Addresses reserved in a network and we cannot touch them:
  1. **Network Address** (First IP of the network)
  ```c
  192.168.1.0
  ```
  2. **Broadcast Address** (Last IP of the network. A special networking address used to transmit data to all devices connected to a specific network or subnet simultaneously. When a message is sent to this address, every single active device on that network segment receives and processes it).
	```c
  192.168.1.255
  ```
- So usable IP Address *for this network*:
  ```c
  192.168.1.1 - 192.168.1.254
  ```

**But how can we tell if a device belong to a specific network?**
This is where **Subnet** comes in.

### Subnet

Subnet is Network Address, which is basically the first IP Address in the range for that subnet.

So when we see the subnet:
```cpp
192.168.1.0
```
We know that the usable range of that IP Address usable in that network is:
```cpp
192.168.1.1 - 192.168.1.254

// remember, 192.168.1.255 is the host portion & also not usable
```
A subnet is also typically represented with a **CIDR (Classless Inter-Domain Routing)** notation, which is a compact way to write an IP address and its associated submask.
- It indicates how many bits are used for the **network portion**.

In this case we have:
```cpp
SUBNET		:	192.168.1.0 /24 
SUBNET MASK	:	/24
		
		Octet		Octet		Octet		Octet
BINARY	11111111.	11111111.	11111111.	00000000
DECIMAL	255.			255.			255.			0
					Network Portion			Host Portion
```
- All the `1`s indicates how many bits are taken for the network portion of the subnate, making it `fixed`.
- All the `0`s indicate how many host addresses are available, which is a **varible**.

##### Recap: What is a subnet?
- A sub network of a larger network
- It defines a range of IP addresses of a network
  - Helps identifies whether a host/device belongs to a network
- It is essentially the network address with CIDR notation of a subnet mask
  - e.g. `192.163.1.0 /24`
- A subnet maks indicates which part of an IP is fixed (network portion) and variable (host portion)
  - e.g. `/24` or `255.255.255.0`

Changing the subnet mask to suit the need is subnetting.

### Switch Device
A network switch is a hardware device that connects multiple devices (e.g. computers, printers) together within a single LAN.
- Acts as a central hub, receiving incoming data packets and intelligently forwarding them only to their specific inteded destination.
- Allow computers to communicate to each other within the same network.
- Switch can be connected to a router, which connects the LAN (local area network) with the external network (WAN - wider area network).
- Switch connects to a **router**.


> For our device to be able to talk to each other, they have to have the **same subnet mask**.

**Example:**
Suppose we have:
```cpp
SWITCH
- IP:	192.168.42.42
- MASK:	255.255.255 128
```
This means that all devices connected to this switch has the **same subnet mask**.  Here we can extract these information:
```c
SUBNET MASK	:	255.255.255.128
SUBNET		:	192.168.42.0 /25
NETWORK ADR.	:	192.168.42.0
BROADCAST ADR.:	192.168.42.127

USABLE IP RANGE: 192.168.42.1 - 192.168.42.126
```

### How do we know the first and last addresses? What's the range / CIDR notation for a network?
1. Convert the subnet mask to binary
   - Each octet has 8 bits
		```cpp
		2^7	2^6	2^5	2^4	2^3	2^2	2^1	2^0
		128	64	32	16	8	4	2	1
		1	1	1	1	1	1	1	1

		128 + 64 + 32 + 16 + 8 + 4 + 2 + 1
		= 255 
		```
	- Suppose we have:
		```cpp
		SUBNET MASK: 255.255.255.240
		```
		Looking at the 4th octet (`240`):
		```cpp
		2^7	2^6	2^5	2^4	2^3	2^2	2^1	2^0
		128	64	32	16	8	4	2	1
		1	1	1	1	0	0	0	0

		128 + 64 + 32 + 16 + 0 + 0 + 0 + 0
		= 240 
		```
	- Another example:
		```cpp
		SUBNET MASK: 255.255.255.128
		```
		Looking at the 4th octet (`240`):
		```cpp
		2^7	2^6	2^5	2^4	2^3	2^2	2^1	2^0
		128	64	32	16	8	4	2	1
		1	0	0	0	0	0	0	0

		128 + 0 + 0 + 0 + 0 + 0 + 0 + 0
		= 128 
		```
2. Find the CIDR Notation
	- Count the `network bits`
	- Here we have 25 bits out of 32 bits total
	- Therefore we have `CIDR: /25`
	```cpp
	BINARY	11111111.	1111111.	11111111.	1000000
	DECIMAL	255.			255.		255.			128
			NETWORK PORTION					HOST PORTION	
	```

**So what if we want to have more than 1 network?**
With a subnet mask of `255.25.255.128`, we can have two networks:
1. SUBNET MASK : `255.255.255.128`
USABELE IP: `192.168.42.1 - 192.168.42.126`
2. SUBNET MASK : `255.255.255.128`
USABELE IP: `192.168.42.129 - 192.168.42.254`

Be careful of overlapping.

**What if we want to have more networks?**
We use subnetting

### Subnetting

#### Subnetting based on how many networks you need / We need more networks(NetworkChuck method)
1. use the `x2` chart to calculate how many host bits we need to HACK.
When we need more networks, we need more bits. So we take (hack) bits from the host bits and put them into the network portion.

	So for example, if we need 4 networks, we check th `x2` table and see that we need to take `2` bits from the host.
	```c
		128	| 64  | 32 | 16 | 8  | 4 | 2 | 1
	x2	256	| 128 | 64 | 32 | 16 | 8 | 4 | 2 ---> This is how many networks you'll get when you change your submask by a certain number of bits.
	```
	So if we need 17 networks, we need `5` bits for at least 17.

2. HACK the host bits
	```c
	NEW SUBNET MASK: 11111111.11111111.11111111.11000000 
	//This subnet mask will give 4 networks
	```
3. Convert back to decimals
	```cpp
	255.255.255.192 /26
	```
4. Find the increment to determine the size of our networks and what the range
	Now we need to find the range by using **increment**. To find the increment, find the last network bit (the last `1`).
	From the last section:
	```cpp
		NEW SUBNET MASK: 11111111.11111111.11111111.11000000 
												^
											this one
	```
	This is our increment, which is `64`.
5. Create the network
Our range of IP addresses for each network therefore becomes:
```c
NETWORK 1:	192.168.1.0 - 192.168.1.63 // 0 is included
NETWORK 2:	192.168.1.64 - 192.168.1.127
NETWORK 3:	192.168.1.128 - 192.168.1.191
NETWORK 4:	192.168.1.192 - 192.168.1.255
```
Each with the subnet mask of `255.255.255.192`.
1. How many host are available?
To find number of addresses, it is `2^(number of host bits)`.
Therefore the amount of hosts, is 64 minus the subnet address and broadcast address **62 number of hosts**.

#### Router
- A router operates between LAN and WAN (wider area network) and basically connects us to the internet.
- Can have multiple IP addresses for different networks
- Use Routing Table to forward data packets between the mulple networks

##### Routing Table
A routing table is a simple data table stored in a router or network host that lists all the routes to a particular network destination.
In Net Practice, a routing table consists of only two simple informations:

- **Destination** (on the left): it's the `IP address` that you want to send a package to, combined with the `CIDR` of that network, e.g.: `190.3.2.252/30`. If you don't want to specify a destination, or you want to make it a**vailable for the entire network**, you can just set it to `default` or `0.0.0.0/0`.
	- It is the first address of that subnet blck

- **Next Hop** (on the right): it's the IP address of the next router that you need to send the packages to in order to reach the destination-network.



#### Gateway
- A gateway and router are often the same device, though function differently:
  - Router sends packets between different networks based on IP addresses
  - Gateway acts as a "gate" between two networks, allowing them to communicate
    - Can also connects networks that use different communication protocols
    - Has single IP Address (that of a router) as an entry and exit point of a network

### Netpractice Tips
1. Take out the noise and start clean to reduce confusion
2. Work backwards with the provided default values
3. Solve one goal at a time when there's multiple
4. Refer to a subnet chart

### Subnetting


### Quick Notes

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
| CIDR(Host 3rd)   |  /17 |  /18 |  /19 |  /20 |  /21 |  /22 |  /23 | /24 |
| CIDR (Host 4th)   |  /25 |  /26 |  /27 |  /28 |  /29 |  /30 |  /31 | /32 |
| Incr. + Bit   |  128 |   64 |   32 |   16 |    8 |    4 |    2 |   1 |
| Subnet Mask (desc host) | .128 | .192 | .224 | .240 | .248 | .252 | .254 |  .0 |
| Usable Hosts|  126 |   62 |   30 |   14 |    6 |    2 |    2 |   0 |


## Submission Details
10 exported config files are located in the root directory corresponding to the 10 levels completed in Net Practice.
