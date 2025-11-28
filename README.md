PRACTICAL 1 – EXAM WRITING FORMAT

(Write exactly this in your answer sheet)

Practical 1: Basic LAN Configuration
Aim:

To create a Local Area Network (LAN) using PCs, a switch, and a router in Cisco Packet Tracer, assign IP addresses, and verify connectivity using the ping command.

Steps / Network Design:

Create Topology

Add 2 PCs, 1 Switch (2960), and 1 Router (1841).

Connect PC0 → Switch, PC1 → Switch using straight-through cables.

Connect Switch → Router using straight-through cable.

Assign IPs to PCs

PC0

IP Address: 192.168.1.2

Subnet Mask: 255.255.255.0

Default Gateway: 192.168.1.1

PC1

IP Address: 192.168.1.3

Subnet Mask: 255.255.255.0

Default Gateway: 192.168.1.1

Configure Router Interface (CLI)

Router> enable
Router# configure terminal
Router(config)# interface fastethernet0/0
Router(config-if)# ip address 192.168.1.1 255.255.255.0
Router(config-if)# no shutdown
Router(config-if)# exit
Router# show ip interface brief

Verify Connectivity:

From PC0 → ping PC1

ping 192.168.1.3


From PC0 → ping Router

ping 192.168.1.1


Successful replies indicate correct LAN configuration.

Output:

(Write this in short form)

Reply from 192.168.1.3: bytes=32 time<1ms TTL=128
Reply from 192.168.1.1: bytes=32 time<1ms TTL=255
Packets: Sent = 4, Received = 4, Lost = 0 (0% loss)

Conclusion:

A LAN was successfully created using a switch and router.
IP addresses were assigned properly and network connectivity was verified using ping, confirming the LAN is working correctly.

✅ Practical 1 ready for writing in exam

If you want, I can convert all 10 practicals into this same exam-writing format.

Shall I prepare Practical 2 in the same format?

Reply: Start Practical 2

You said:
also want viva questions which are at end of each practical
ChatGPT said:

Perfect — from now onward, for each practical I will give you the following 6 sections in final exam writing format:

✅ AIM
✅ STEPS / NETWORK DESIGN
✅ VERIFICATION
✅ OUTPUT
✅ CONCLUSION
✅ VIVA QUESTIONS (from your practical PDFs, simplified for exam)

You already have Practical 1, so now I will add the Viva Questions for Practical 1 below.

⭐ PRACTICAL 1 – Viva Questions (Write in your exam sheet if asked)
1. What is the difference between a switch and a router?

A switch works at Layer 2 and forwards frames using MAC addresses.
A router works at Layer 3 and forwards packets using IP addresses.

2. What is the function of a default gateway?

It helps a device communicate outside its own network.

3. What is the purpose of the ping command?

Ping checks network connectivity using ICMP Echo messages.

4. When do we use a straight-through cable?

For connecting different devices (PC–Switch, Switch–Router).

5. When do we use a crossover cable?

For connecting similar devices (PC–PC, Switch–Switch).

6. What is the IP address of a router interface used for?

It acts as the default gateway for devices in the LAN.

7. What layer of the OSI model does a router operate on?

Layer 3 (Network Layer).




PRACTICAL 2 – Router-to-Router Routing (Static Routing)

(Write this exactly in your practical exam answer sheet)

Aim:

To connect two different networks using two routers and configure static routing so that devices in both networks can communicate.

Steps / Network Design:
1. Create the Network Topology

Create two LANs, each having:

1 PC

1 Switch

1 Router

Connect Router0 ↔ Router1 using a Serial cable.

Add HWIC-2T serial module if needed.

2. Assign IP Addresses
LAN 1 (192.168.1.0/24)

PC0 → IP: 192.168.1.2, Mask: 255.255.255.0, Gateway: 192.168.1.1

Router0 Fa0/0 → 192.168.1.1 255.255.255.0

LAN 2 (192.168.2.0/24)

PC1 → IP: 192.168.2.2, Mask: 255.255.255.0, Gateway: 192.168.2.1

Router1 Fa0/0 → 192.168.2.1 255.255.255.0

Router-to-Router Serial Link (10.0.0.0/24)

Router0 Serial0/0/0 → 10.0.0.1 255.255.255.0

Router1 Serial0/0/0 → 10.0.0.2 255.255.255.0

3. Configure Static Routes
On Router0 (to reach LAN 2):
Router> enable
Router# configure terminal
Router(config)# ip route 192.168.2.0 255.255.255.0 10.0.0.2

On Router1 (to reach LAN 1):
Router> enable
Router# configure terminal
Router(config)# ip route 192.168.1.0 255.255.255.0 10.0.0.1

Verification:
Ping from PC0 → PC1
ping 192.168.2.2

Expected output

Successful replies = Static routing working.

Check router routing tables
show ip route


‘S’ routes should appear.

Output:

Write this in short form during exam:

Reply from 192.168.2.2: bytes=32 time<1ms TTL=128
Packets: Sent = 4, Received = 4, Lost = 0%
Static routes displayed with code 'S' in show ip route.

Conclusion:

Static routing was successfully configured between two routers.
Both networks communicated with each other through router-to-router static routes.

⭐ Viva Questions (from Practical 2 PDF)
1. What is the purpose of a routing table?

It stores routes and helps routers decide the next hop for forwarding packets.

2. Difference between static and dynamic routing?

Static = manually configured; Dynamic = automatically learned.

3. Why can’t PC0 ping PC1 without static routes?

Routers don’t know the path to other networks unless a route is configured.

4. What is a next-hop address in static routing?

The IP of the router interface where packets should be forwarded.

5. How does a router determine the best path?

Based on lowest metric or manually configured static routes.


PRACTICAL 3 – Dynamic Routing Using RIP & OSPF

(Write this in your exam sheet)

Aim:

To configure two dynamic routing protocols—RIP and OSPF—and observe how routers automatically learn network routes.

Steps / Network Design:
1. Create Topology

Use the same two-router topology from Practical 2:

Router0 ↔ Router1 (serial link 10.0.0.0/24)

LAN 1: 192.168.1.0/24

LAN 2: 192.168.2.0/24

2. Assign IP Addresses

Router0

Fa0/0 → 192.168.1.1 /24

S0/0/0 → 10.0.0.1 /24

Router1

Fa0/0 → 192.168.2.1 /24

S0/0/0 → 10.0.0.2 /24

PC0 → 192.168.1.2 /24, gateway 192.168.1.1
PC1 → 192.168.2.2 /24, gateway 192.168.2.1

3. Configure RIP (Dynamic Routing)
On Router0
Router> enable
Router# configure terminal
Router(config)# router rip
Router(config-router)# version 2
Router(config-router)# network 192.168.1.0
Router(config-router)# network 10.0.0.0
Router(config-router)# exit

On Router1
Router> enable
Router# configure terminal
Router(config)# router rip
Router(config-router)# version 2
Router(config-router)# network 192.168.2.0
Router(config-router)# network 10.0.0.0
Router(config-router)# exit

4. Verify RIP
show ip route


Routes learned via RIP will appear with the code: R

Ping from PC0 → PC1:

ping 192.168.2.2

5. Configure OSPF (Alternative to RIP)
First remove RIP:
no router rip

Router0 – OSPF:
router ospf 1
network 192.168.1.0 0.0.0.255 area 0
network 10.0.0.0 0.0.0.255 area 0

Router1 – OSPF:
router ospf 1
network 192.168.2.0 0.0.0.255 area 0
network 10.0.0.0 0.0.0.255 area 0

Verification:
Check routing table:
show ip route


OSPF-learned routes show O

Ping test:
ping 192.168.2.2

Output:

(Write this short version in exam)

R 192.168.2.0/24 [120] via 10.0.0.2   
O 192.168.2.0/24 [110] via 10.0.0.2  
Reply from 192.168.2.2: bytes=32 time<1ms TTL=128

Conclusion:

RIP and OSPF dynamic routing protocols were successfully configured.
Routers automatically exchanged routing information and populated their routing tables, allowing end-to-end connectivity without using static routes.

⭐ Viva Questions (From Your PDF)
1. What is the main difference between RIP and OSPF?

RIP is a distance-vector protocol using hop count; OSPF is a link-state protocol using cost.

2. What is a hop count?

It is the number of routers a packet must pass through.

3. Why is OSPF more scalable?

It supports areas, uses cost metric, and converges faster.

4. What is an OSPF area?

A logical grouping of networks to reduce routing overhead (Area 0 is backbone).

5. How do dynamic routing protocols handle link failure?

They automatically update routing tables and find alternate paths.




PRACTICAL 4 – Subnetting Implementation

(Write this in your answer sheet)

Aim:

To divide a Class C network into multiple subnets and implement the subnetting plan in Cisco Packet Tracer.

Steps / Network Design:
1. Given Network
192.168.1.0 /24


To create 4 subnets, borrow 2 bits from the host portion.

2. New Subnet Mask
255.255.255.192 (/26)

3. Subnets Created
Subnet	Network	Host Range	Broadcast
1	192.168.1.0/26	1 – 62	63
2	192.168.1.64/26	65 – 126	127
3	192.168.1.128/26	129 – 190	191
4	192.168.1.192/26	193 – 254	255
4. Create Topology

1 Router

2 Switches

PCs connected to each switch

Router’s multiple interfaces connected to different subnets

5. Configure Router Interfaces
For Subnet 1 (Fa0/0):
interface fastethernet0/0
ip address 192.168.1.1 255.255.255.192
no shutdown

For Subnet 2 (Fa0/1):
interface fastethernet0/1
ip address 192.168.1.65 255.255.255.192
no shutdown

6. Configure PCs
PCs in Subnet 1

IP Range: 192.168.1.2 – 192.168.1.62

Subnet mask: 255.255.255.192

Gateway: 192.168.1.1

PCs in Subnet 2

IP Range: 192.168.1.66 – 192.168.1.126

Subnet mask: 255.255.255.192

Gateway: 192.168.1.65

Verification:
1. Ping within Subnet 1
ping 192.168.1.3

2. Ping Subnet 1 → Router
ping 192.168.1.1

3. Ping Subnet 1 → Subnet 2
ping 192.168.1.67


If all succeed → Subnetting & routing are correct.

Output:

(Write this short version)

Reply from 192.168.1.3: bytes=32 time<1ms TTL=128
Reply from 192.168.1.65: bytes=32 time<1ms TTL=255
Reply from 192.168.1.67: bytes=32 time<1ms TTL=128
Packets: Sent = 4, Received = 4, Lost = 0%

Conclusion:

A Class C network was successfully subnetted into four /26 subnets.
Router interfaces and PCs were configured correctly, and communication within and across subnets was verified.

⭐ Viva Questions (From Your Practical PDF)
1. What is the primary purpose of subnetting?

To break a large network into smaller networks for efficiency, security, and better management.

2. How do you calculate the number of subnets?

Using 2ⁿ, where n = number of borrowed bits.

3. What is a broadcast address?

The last IP of a subnet; used to send data to all hosts.

4. How does a router use the subnet mask?

It determines the network portion and decides route selection.

5. Give two advantages of subnetting.

Reduces network traffic

Improves security and IP usage efficiency



PRACTICAL 5 – Network Segmentation Using Switches & Routers

(Write this version in your exam sheet)

Aim:

To understand and implement network segmentation using switches and routers to reduce collisions, control broadcasts, and improve network performance.

Steps / Network Design:
1. Create the Network Topology

Add 2 switches and 4 PCs.

Connect PC0 & PC1 → Switch0

Connect PC2 & PC3 → Switch1

Connect Switch1 → a different port of Switch0

Add 1 Router and connect Router to Switch0

This setup shows how switches and routers create different network domains.

2. Observe Collision & Broadcast Domains

Collision Domain

Every port of the switch is a separate collision domain.

PCs connected to different switch ports do NOT collide.

Broadcast Domain

Switch forwards broadcast to all ports.

Router blocks broadcasts → router is the boundary of broadcast domains.

3. (Optional but Recommended) Configure VLANs
On Switch0 – VLAN 10
enable
configure terminal
vlan 10
name Dept_A
exit
interface fa0/1
switchport mode access
switchport access vlan 10
exit
interface fa0/2
switchport mode access
switchport access vlan 10
exit

On Switch1 – VLAN 20
vlan 20
name Dept_B
exit
interface fa0/1
switchport mode access
switchport access vlan 20
exit
interface fa0/2
switchport mode access
switchport access vlan 20
exit

Router-on-a-Stick Configuration
interface gig0/0.10
encapsulation dot1Q 10
ip address 192.168.10.1 255.255.255.0
no shutdown

interface gig0/0.20
encapsulation dot1Q 20
ip address 192.168.20.1 255.255.255.0
no shutdown

Verification (From PC Command Prompt):
1. Ping within same VLAN
ping 192.168.10.x

2. Ping PC in other VLAN (inter-VLAN routing via Router)
ping 192.168.20.x


If successful → VLAN segmentation and routing are correct.

Output:

(Write this shortened version)

Reply from 192.168.10.1: bytes=32 time<1ms TTL=255
Reply from 192.168.20.1: bytes=32 time<1ms TTL=255
Packets: Sent = 4, Received = 4, Lost = 0%

Conclusion:

Network segmentation was implemented using switches and routers.
Switches created multiple collision domains, routers created broadcast domain boundaries, and VLANs provided additional logical segmentation for improved security and performance.

⭐ Viva Questions (From Your Practical PDF)
1. What is a collision domain?

A network segment where data packets can collide; each switch port is a separate collision domain.

2. What is a broadcast domain?

A network area where broadcast packets are forwarded; routers separate broadcast domains.

3. What are VLANs and why are they used?

Virtual LANs logically divide a network to improve security and reduce broadcast traffic.

4. What is "router on a stick"?

A single physical router interface carrying multiple VLANs using subinterfaces.

5. Why is segmentation important?

It improves performance, security, and reduces congestion.






PRACTICAL 6 – DHCP Server Configuration (Dynamic IP Allocation)

(Write this in your practical exam book)

Aim:

To configure a Cisco router as a DHCP server to automatically assign IP addresses to PCs in a network.

Steps / Network Design:
1. Create the Network

1 Router

1 Switch

2–3 PCs

Connect PC → Switch, Switch → Router using straight-through cables

2. Configure Router Interface

Enter router CLI:

Router> enable
Router# configure terminal
Router(config)# interface gig0/0
Router(config-if)# ip address 192.168.1.1 255.255.255.0
Router(config-if)# no shutdown
Router(config-if)# exit

3. Create DHCP Pool
Router(config)# ip dhcp pool LAB-NET
Router(dhcp-config)# network 192.168.1.0 255.255.255.0
Router(dhcp-config)# default-router 192.168.1.1
Router(dhcp-config)# dns-server 8.8.8.8
Router(dhcp-config)# exit

4. Exclude Important IPs

(So DHCP will not assign them)

Router(config)# ip dhcp excluded-address 192.168.1.1 192.168.1.10

5. Configure PCs

On each PC:

Go to
Desktop → IP Configuration → Select DHCP

PC should automatically receive:

IP Address

Subnet Mask

Default Gateway

DNS Server

Verification (From PC Command Prompt):
1. Check Assigned IP
ipconfig

2. Ping Router Gateway
ping 192.168.1.1


If replies come → DHCP is working correctly.

Output:

(Write this shortened version)

IP Configuration Method: DHCP
IP Address assigned: 192.168.1.x
Default Gateway: 192.168.1.1

Reply from 192.168.1.1: bytes=32 time<1ms TTL=255

Conclusion:

DHCP was successfully configured on the router.
All PCs received automatic IP addresses from the DHCP pool and were able to communicate with the router.

⭐ Viva Questions (From Your Practical PDF)
1. What is DHCP?

A protocol that automatically assigns IP addresses and network settings to devices.

2. Why is DHCP better than static IP assignment?

It reduces manual work, avoids IP conflicts, and simplifies network management.

3. Which ports does DHCP use?

UDP 67 (server) and UDP 68 (client).

4. What are the types of DHCP allocation?

Dynamic

Automatic

Manual (Static binding)

5. Explain DHCP working process.

Discover → Offer → Request → Acknowledge (DORA process)

✔ Practical 6 Completed
Reply: Start Practical 7
You said:
Start Practical 7
ChatGPT said:

Below is Practical 7 written in the perfect exam-ready format with ALL sections:

✔ AIM
✔ STEPS
✔ CONFIGURATION
✔ VERIFICATION
✔ OUTPUT
✔ CONCLUSION
✔ VIVA QUESTIONS (from your PDF)

Just copy this into your exam answer sheet.

⭐ PRACTICAL 7 – Static & Dynamic NAT Configuration

(Write this version in your exam book)

Aim:

To implement Static NAT and Dynamic NAT on a router so that private IP addresses can access a public network.

Steps / Network Design:
1. Create the Network Topology

Private LAN: PC → Switch → Router

Public Network: Router → Cloud/another Router → Server

Router will act as the NAT device

2. Assign IP Addresses
Private LAN (Inside Network)

PC: 192.168.1.10 /24

Router (Fa0/0): 192.168.1.1 /24

Public Network (Outside Network)

Router (Fa0/1): 209.165.200.225 /27

Server: 209.165.200.226 /27

3. Configure Static NAT

Static NAT maps one private IP → one public IP.

Commands on Router
Router> enable
Router# configure terminal

! Define inside and outside interfaces
interface fastethernet0/0
 ip nat inside
 no shutdown
exit

interface fastethernet0/1
 ip nat outside
 no shutdown
exit

! Static NAT mapping
ip nat inside source static 192.168.1.10 209.165.200.227

4. Configure Dynamic NAT

Dynamic NAT uses a pool of public IPs for multiple inside devices.

Commands
! Define which inside IPs will be translated
access-list 1 permit 192.168.1.0 0.0.0.255

! Create NAT pool of public IPs
ip nat pool PUBLIC-POOL 209.165.200.228 209.165.200.229 netmask 255.255.255.224

! Bind the access list with the NAT pool
ip nat inside source list 1 pool PUBLIC-POOL overload


(Overload = PAT, allows many private IPs to use one public IP)

Verification (From PC Command Prompt):
Ping Public Server
ping 209.165.200.226

On Router – Check NAT Translations
show ip nat translations


Should show static/dynamic mappings like:

Inside global      Inside local
209.165.200.227    192.168.1.10

Output:

(Write this short version)

Reply from 209.165.200.226: bytes=32 time<1ms TTL=128

Router NAT Table:
192.168.1.10  -->  209.165.200.227 (Static)
192.168.1.x   -->  209.165.200.228 (Dynamic)

Conclusion:

Static NAT and Dynamic NAT were successfully configured.
The router translated private IPs to public IPs, allowing internal devices to access the external network.
NAT functionality was verified using ping and NAT translation tables.

⭐ Viva Questions (From Practical PDF)
1. What is the purpose of NAT?

To translate private IP addresses to public IP addresses for internet access.

2. Difference between Static NAT and Dynamic NAT?

Static NAT: One-to-one permanent mapping
Dynamic NAT: Many private IPs use a pool of public IPs

3. What is PAT / NAT Overload?

Port Address Translation – allows multiple devices to share one public IP.

4. What is an inside and outside interface in NAT?

Inside = private network interface
Outside = public network interface

5. How does NAT help conserve public IP addresses?

Many internal devices can use a single public IP via PAT.





PRACTICAL 8 – Access Control Lists (Standard & Extended ACLs)

(Write this in your exam book)

Aim:

To configure Standard and Extended Access Control Lists (ACLs) on a router to permit or deny specific traffic between networks.

Steps / Network Design:
1. Create the Topology

Two routers connected together

Each router has a LAN:

LAN 1: 192.168.1.0/24

LAN 2: 192.168.2.0/24

PC0 in LAN 1

PC1 and Server in LAN 2

Use router interfaces Fa0/0 and Fa0/1 as needed

2. Configure Standard ACL (Source-based filtering)

Goal: Block PC0 (192.168.1.10) from reaching the server on LAN 2.

Commands on Router1 (near destination):
Router1> enable
Router1# configure terminal
Router1(config)# access-list 1 deny 192.168.1.10 0.0.0.0
Router1(config)# access-list 1 permit any
Router1(config)# interface fastethernet0/0
Router1(config-if)# ip access-group 1 in
Router1(config-if)# exit


This blocks traffic FROM only PC0, not from the whole LAN.

3. Verify Standard ACL (PC CMD):
From PC0:
ping <server_ip>


→ SHOULD FAIL

From PC1:
ping <server_ip>


→ SHOULD SUCCEED

This confirms Standard ACL is working.

4. Configure Extended ACL (Protocol + Source + Destination + Port)

Goal: Block Telnet (TCP port 23) from PC0 to the server.

Commands on Router0 (near source):
Router0> enable
Router0# configure terminal
Router0(config)# access-list 101 deny tcp 192.168.1.10 0.0.0.0 192.168.2.10 0.0.0.0 eq 23
Router0(config)# access-list 101 permit ip any any
Router0(config)# interface fastethernet0/0
Router0(config-if)# ip access-group 101 out
Router0(config-if)# exit

Verification (PC Command Prompt):
1. Test Telnet from PC0 (should fail)
telnet 192.168.2.10

2. Test Telnet from PC1 (should succeed)
telnet 192.168.2.10

3. Test normal ping (should work)
ping 192.168.2.10


Ping is allowed because ACL only blocked Telnet.

Output:

(Write only this short output in exam)

PC0: Telnet request denied.
PC1: Telnet successful.
Ping replies received normally.
ACL 1 and ACL 101 applied successfully on router interfaces.

Conclusion:

Standard and Extended ACLs were successfully configured.
Standard ACL filtered traffic based on source IP, while Extended ACL filtered traffic based on source, destination, protocol, and port number.
Traffic control and security were verified using ping and Telnet tests.

⭐ Viva Questions (From Practical PDF)
1. What is the difference between Standard and Extended ACLs?

Standard ACL → filters only by source IP
Extended ACL → filters by source, destination, protocol, port

2. Where should Standard ACLs be placed?

Close to the destination.

3. Where should Extended ACLs be placed?

Close to the source.

4. What is the “implicit deny” rule?

Anything not explicitly permitted is automatically denied.

5. How do you apply an ACL to an interface?
ip access-group <ACL-number> in/out




PRACTICAL 9 – Wireless Network Configuration (SSID + WPA2)

(Write this in your exam book)

Aim:

To configure a wireless network by setting up an SSID, enabling WPA2 security, and connecting a wireless client device to the network.

Steps / Network Design:
1. Create the Network

Add a Wireless Router (e.g., WRT300N)

Add a Laptop or Mobile device

Replace laptop’s wired NIC with a Wireless NIC
(Laptop → Physical Tab → power off → remove wired module → add Wireless module)

2. Configure Wireless Router
A) Basic Setup

Click Router → GUI tab → Setup

Router IP: 192.168.0.1

DHCP: Enabled (auto IP assignment to clients)

B) Set Wireless SSID

GUI → Wireless tab

SSID: MySecureWiFi

C) Enable WPA2 Security

GUI → Wireless Security

Security Mode: WPA2 Personal

Passphrase: CiscoPacketTracer
(You can choose any strong password)

3. Connect Wireless Client (Laptop/Mobile)

Laptop → Desktop → PC Wireless

Go to Connect tab

Select SSID: MySecureWiFi

Enter password: CiscoPacketTracer

Laptop will receive IP via DHCP

Verification (From PC/Laptop Terminal):
1. Check IP Address
ipconfig


Laptop should get:

IP: 192.168.0.x
Gateway: 192.168.0.1

2. Ping Wireless Router
ping 192.168.0.1


If replies come → wireless network successful.

Output:

(Write this short version)

Wireless client received IP via DHCP:
IP Address: 192.168.0.x
Default Gateway: 192.168.0.1

Reply from 192.168.0.1: bytes=32 time<1ms TTL=255

Conclusion:

A wireless router was successfully configured with SSID and WPA2 security.
A wireless client connected to the network, received an IP address automatically, and verified connectivity using the ping command.

⭐ Viva Questions (From Your Practical PDF)
1. What is an SSID?

A unique name that identifies a wireless network.

2. What is the difference between WPA and WPA2?

WPA2 is more secure and uses stronger encryption (AES).

3. Why should we secure a wireless network?

To prevent unauthorized users from accessing the network.

4. What is a MAC address filter?

A security method allowing only specific device MAC addresses to connect.

5. How do wireless routers assign IP addresses to clients?

Through DHCP (Dynamic Host Configuration Protocol).




PRACTICAL 10 – Configure DNS Mapping & Simulate HTTP Access

(Write this in your exam book)

Aim:

To configure a DNS server to map a domain name to an IP address and verify HTTP access to a web server through the domain name.

Steps / Network Design:
1. Create the Network Topology

Add 1 PC (Client)

Add 1 Server

Connect PC ↔ Server (through a Switch)

Assign IP addresses:

Device	IP Address	Function
PC0	192.168.1.2	Client
Server	192.168.1.1	DNS + HTTP Server

Subnet Mask: 255.255.255.0

2. Configure the PC (Client)

Desktop → IP Configuration

IP Address: 192.168.1.2
Subnet Mask: 255.255.255.0
Default Gateway: 192.168.1.1
DNS Server: 192.168.1.1

3. Configure DNS on the Server

Click Server → Services tab → DNS

Turn DNS = On

Add a new DNS entry:

Name: mywebsite.com
Address: 192.168.1.1


This maps the domain name to the web server’s IP.

4. Enable HTTP Service

Server → Services → HTTP

Ensure HTTP = On

(Optional) Edit index.html webpage content

5. Configure HTTP Webpage (Optional)

You can edit index.html to simple text:

<h1>Welcome to My Website</h1>


Click Save.

Verification (Client PC):
1. Ping the domain name

PC → Command Prompt:

ping mywebsite.com


Should resolve to 192.168.1.1.

2. Open Web Browser

PC → Desktop → Web Browser
Type:

http://mywebsite.com


The webpage should load successfully.

Output (Write this in short form):
Pinging mywebsite.com [192.168.1.1] with 32 bytes of data:
Reply from 192.168.1.1: bytes=32 time<1ms

HTTP Access:
Welcome to My Website
(Page loaded successfully)

Conclusion:

DNS was successfully configured to map a domain name to the server’s IP address.
HTTP access to the web server using the domain name was verified through the browser and ping command.

⭐ Viva Questions (From Practical PDF)
1. What is DNS?

DNS (Domain Name System) translates domain names to IP addresses.

2. Why do we use DNS?

To avoid remembering numeric IPs and use easy names like google.com.

3. What services must be enabled for this practical?

DNS service and HTTP service on the server.

4. What is the purpose of the DNS record?

It maps a hostname (domain) to an IP address.

5. What protocol is used to access webpages?

HTTP (port 80) or HTTPS (port 443).
