# Network

## What is Networking?

Networking in Linux refers to the process of connecting multiple computers or devices to each other through a network. This allows for communication and sharing of resources, such as files and printers.

The Linux system distinguishes two types of network interfaces – the physical network interface and the virtual network interface. A physical network interface represents a network hardware device such as NIC (Network Interface Card), WNIC (Wireless Network Interface Card), or a modem.

Simply, a network interface is the point of connection between a computer and a network. In other words, how the Linux system links up the software side of networking to the hardware side.

## Network Achitecture

Linux network architecture is made up of layers that work together to allow communication between devices.

What we know is that the `OSI (Open Systems Interconnection)` model has been based on [OSI Basic Reference Model (1984)](https://www.iso.org/standard/14252.html). Created by ISO (International Organisation for Standarisation), it consists on seven layers:

### Layer 1: Physical layer

The physical layer is the lowest layer in the Linux network architecture. It is responsible for the physical transmission of data over the network. This layer deals with the physical components of the network such as cables, connectors, and network interface cards (NICs).

Usage:

Real infrastructure: LAN (Local Area Network), WAN (Wide Area Network), BAN (Building Area Network) etc.

Converts binary data into physical signal

> [!NOTE]
> Information or bits are transmitted either by wires, cables, or without them, for example via Bluetooth, Wi-Fi.
>
> When a network problem occurs, specialists immediately turn to the physical layer to check, for example, whether the network cable is disconnected from the device.

### Layer 2: Data Link Layer

The data link layer is responsible for providing reliable communication between two devices on the same network segment. It deals with protocols such as Ethernet and Wi-Fi and is responsible for ensuring that data is transmitted without errors.

In other words, data link layer provides encapsulation of network layer data packets into frames and its synchronization.

Usage:

Switches operate at the data link layer and use MAC (Media Access Control) addresses to identify devices on the network. When a device sends data to another device on the network, the switch reads the MAC address of the data packet and determines the best route for the packet to take to reach its destination. This process is called packet switching, and it allows multiple devices on a network to communicate simultaneously without interfering with each other.

### Layer 3: Network Layer

The network layer is responsible for providing logical addressing and routing of data between different networks. This layer is where the IP protocol resides, and it is responsible for determining the best path for data to travel across the network.

### Layer 4: Transport Layer

The transport layer is responsible for providing reliable data transfer between applications running on different devices. This layer deals with protocols such as TCP and UDP, and it is responsible for ensuring that data is transmitted without errors and in the correct order.

### Layer 5: Session Layer

The session layer is responsible for establishing, maintaining, and terminating sessions between applications on different devices. This layer deals with protocols such as SSH and Telnet, and it is responsible for managing communication between applications.

### Layer 6: Presentation Layer

The presentation layer is responsible for the formatting and representation of data. It deals with protocols such as ASCII and JPEG, and it is responsible for ensuring that data is presented in a format that can be understood by the receiving device.

### Layer 7: Application Layer

The application layer is the highest layer in the Linux network architecture. It deals with protocols such as HTTP, FTP, and SMTP, and it is responsible for providing services to applications running on different devices.

## Network Interface Names

List the available network interfaces with sys FS:

```bash
$ ls /sys/class/net
docker0  eth0   lo   wlan0    ib0
```

The `ip` command is used to show / manipulate routing, network devices, interfaces and tunnels.

To get more details about the network interfaces:

```bash
ip link
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN mode DEFAULT group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
2: wlan0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP mode DORMANT group default qlen 1000
    link/ether 01:23:45:67:89:ab brd ff:ff:ff:ff:ff:ff
3: docker0: <NO-CARRIER,BROADCAST,MULTICAST,UP> mtu 1500 qdisc noqueue state DOWN mode DEFAULT group default 
    link/ether 01:02:03:04:05:06 brd ff:ff:ff:ff:ff:ff
22: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP mode DEFAULT group default qlen 1000
    link/ether ab:cd:ef:fe:cd:ba brd ff:ff:ff:ff:ff:ff
...
```

## What is IP address?

An IP (Internet Protocol) address is a unique IP address or codename assigned to your Linux computer on either a local or public network. The IP address is used to identify your computer to send and receive data. It serves as an identifier for communication to send network traffic to the correct address.
An IP address is a numeric string, such as 192.168.002.003, which also contains location information to enable two-way communication on your Linux computer.

### How to get the IP address

The `ip addr` command shows all network interfaces and their associated IP addresses:

```bash
$ ip addr
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host noprefixroute 
       valid_lft forever preferred_lft forever
2: wlan0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP group default qlen 1000
    link/ether 01:23:45:67:89:ab brd ff:ff:ff:ff:ff:ff
    inet 192.168.0.2/24 brd 192.168.0.255 scope global dynamic noprefixroute wlan0
       valid_lft 42936sec preferred_lft 42936sec
    inet6 fe80::ba6f:5284:8ffc:e951/64 scope link noprefixroute 
       valid_lft forever preferred_lft forever
...
```

### How to check host availability?

The `ping` command sends ICMP (Internet Control Message Protocol) echo request to a specified host.

```bash
$ ping google.com
PING google.com (2a00:1450:4010:c0e::65) 56 data bytes
64 bytes from lu-in-f101.1e100.net (2a00:1450:4010:c0e::65): icmp_seq=1 ttl=106 time=47.7 ms
64 bytes from lu-in-f101.1e100.net (2a00:1450:4010:c0e::65): icmp_seq=2 ttl=106 time=56.3 ms
64 bytes from lu-in-f101.1e100.net (2a00:1450:4010:c0e::65): icmp_seq=3 ttl=106 time=55.7 ms

$ ping 8.8.8.8
# sends ICMP packets to 8.8.8.8
```

## What is Subnet (Network Mask)?

A network mask is a dotted-decimal number that identifies a node or network. It is used in networks to separate a single network into multiple logical networks. It is necessary for communication between computers in a network to be secure. If you have a network that has multiple subnets, you need to define the subnet’s netmask.

Classless Inter-Domain Routing (CIDR) is a method for allocating IP addresses and for IP routing. The Internet Engineering Task Force introduced CIDR in 1993 to replace the previous classful network addressing architecture on the Internet. Its goal was to slow the growth of routing tables on routers across the Internet, and to help slow the rapid exhaustion of IPv4 addresses.

|    CIDR    | Last IP address |     Subnet      | Addresses count | Hosts count | Subnet class |
|------------|-----------------|-----------------|-----------------|-------------|--------------|
| a.b.c.d/32 |   0.0.0.0       | 255.255.255.255 |        1        |       1*    |    1/256 C   |
| a.b.c.d/31 |   0.0.0.1       | 255.255.255.254 |        2        |       2*    |    1/128 C   |
| a.b.c.d/30 |   0.0.0.3       | 255.255.255.252 |        4        |       2     |    1/64 C    |
| a.b.c.d/29 |   0.0.0.7       | 255.255.255.248 |        8        |       6     |    1/32 C    |
| a.b.c.d/28 |   0.0.0.15      | 255.255.255.240 |        16       |       14    |    1/16 C    |
| a.b.c.d/27 |   0.0.0.31      | 255.255.255.224 |        32       |       30    |    1/8 C     |
| a.b.c.d/26 |   0.0.0.63      | 255.255.255.192 |        64       |       62    |    1/4 C     |
| a.b.c.d/25 |   0.0.0.127     | 255.255.255.128 |        128      |       128   |    1/2 C     |
| a.b.c.0/24 |   0.0.0.255     | 255.255.255.000 |        256      |       254   |    1 C       |
| a.b.c.0/23 |   0.0.1.255     | 255.255.254.000 |        512      |       510   |    2 C       |
| a.b.c.0/22 |   0.0.3.255     | 255.255.252.000 |        1024     |       1022  |    4 C       |
| a.b.c.0/21 |   0.0.7.255     | 255.255.248.000 |        2048     |       2046  |    8 C       |
| a.b.c.0/20 |   0.0.15.255    | 255.255.240.000 |        4096     |       4094  |    16 C      |
| a.b.c.0/19 |   0.0.31.255    | 255.255.224.000 |        8192     |       8190  |    32 C      |
| a.b.c.0/18 |   0.0.63.255    | 255.255.192.000 |      16 384     |     16 382  |    64 C      |
| a.b.c.0/17 |   0.0.127.255   | 255.255.128.000 |      32 768     |     32 766  |    128 C     |
| a.b.0.0/16 |   0.0.255.255   | 255.255.000.000 |      65 536     |     65 534  | 256 C = 1 B  |
| a.b.0.0/15 |   0.1.255.255   | 255.254.000.000 |     131 072     |    131 070  |    2 B       |
| a.b.0.0/14 |   0.3.255.255   | 255.252.000.000 |     262 144     |    262 142  |    4 B       |
| a.b.0.0/13 |   0.7.255.255   | 255.248.000.000 |     524 288     |    524 286  |    8 B       |
| a.b.0.0/12 |   0.15.255.255  | 255.240.000.000 |   1 048 576     |  1 048 574  |    16 B      |
| a.b.0.0/11 |   0.31.255.255  | 255.224.000.000 |   2 097 152     |  2 097 150  |    32 B      |
| a.b.0.0/10 |   0.63.255.255  | 255.192.000.000 |   4 194 304     |  4 192 302  |    64 B      |
| a.b.0.0/9  |   0.127.255.255 | 255.128.000.000 |   8 388 608     |  8 388 606  |   128 B      |
| a.0.0.0/8  |   0.255.255.255 | 255.000.000.000 |  16 777 216     | 16 777 214  | 256 B = 1 A  |
| a.0.0.0/7  |   1.255.255.255 | 254.000.000.000 |  33 554 432     | 33 554 430  |    2 A       |
| a.0.0.0/6  |   3.255.255.255 | 252.000.000.000 |  67 108 864     | 67 108 862  |    4 A       |
| a.0.0.0/5  |   7.255.255.255 | 248.000.000.000 | 134 217 728     | 134 217 726 |    8 A       |
| a.0.0.0/4  |  15.255.255.255 | 240.000.000.000 | 268 435 456     | 268 435 454 |   16 A       |
| a.0.0.0/3  |  31.255.255.255 | 224.000.000.000 | 536 870 912     | 536 870 910 |   32 A       |
| a.0.0.0/2  |  63.255.255.255 | 192.000.000.000 | 1 073 741 824   |1 073 741 822|   64 A       |
| a.0.0.0/1  |  127.255.255.255| 128.000.000.000 | 2 147 483 648   |2 147 483 646|  128 A       |
| 0.0.0.0/0  |  255.255.255.255| 000.000.000.000 | 4 294 967 296   |4 294 967 294|  256 A       |

\* To make it possible to place hosts in networks with this mask dimension, we deviate from the rules adopted for working in other networks.

## How to display network connections and statistics?

The `netstat` command prints network connections, routing tables, interface statistics, masquerade connections, and multicast memberships.

```bash
$ netstat -tuln 
# shows all listening TCP and UDP connections
```

## Hot to show network socket information?

The `ss` command displays network connections and statistics.

```bash
$ ss -tuln 
# shows all listening TCP and UDP connections like netstat 
```
