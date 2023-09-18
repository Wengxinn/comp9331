# Useful commands for computer 

## ping
- Check connectivity to a host.
- A small packet (8/56/64 bytes) is sent through the network to a particular IP address. 
- The host that sends the packet then waits (listens) for a return packet. 
- If the connections are good, and the target host is up, a valid return packet will be received. 

`ping host`
- `host`: name/IP address of a host.

```
$ ping google.com
PING google.com (142.250.66.206) 56(84) bytes of data.
64 bytes from syd09s23-in-f14.1e100.net (142.250.66.206): icmp_seq=1 ttl=118 time=15.2 ms
64 bytes from syd09s23-in-f14.1e100.net (142.250.66.206): icmp_seq=2 ttl=118 time=14.8 ms
^C
--- google.com ping statistics ---
2 packets transmitted, 2 received, 0% packet loss, time 999ms
rtt min/avg/max/mdev = 14.773/14.997/15.222/0.224 ms
```

- `64 bytes`: Number of data bytes, default = 56, which translates into 64 ICMP data bytes.
- `from syd09s23-in-f14.1e100.net (142.250.66.206)`: IP address of the destination.
- `icmp_seq=1`: ICMP sequence number for each packet.
- `ttl=118`: Time to Live
- `time=15.2 ms`: Ping time, which is the round trip time for the packet to reach the host, and the response to return the sender.

` ping -s packetsize host`
- `-s packet size`: number of data bytes to be sent (default = 56 bytes).

`ping -i interval host`
- `-i interval`: interval between sending ping requests (default = 1s).

`ping -c n host`
- `-c n`: number of packets to be sent.

## traceroute
- Trace an IP packet's route from your host to another Internet host. 
- Measure the round trip time between your host and the intermediate routers along the path. 

`traceroute host`

## telnet (obsolete)
- Connect one host to another (remote login) via the Internet.
- Allow to log onto machines worldwide that you have accounts on or that allow public access

`telnet host [port]`
- `port`: port number (default telnet port is used if isn't specified).

## ssh
- A set of standards and an associated network protocol that allows for establishing a secure channel between a local and a remote computer. 
- Alternative to telnet.

`ssh -l username hostname` or `ssh username@hostname`

## ifconfig
- Interface configuration - view and change the configuration of the network interfaces on your system. 
- Assign an address to a network interface.
- Configure or display the current network interface configuration information. 

`ifconfig`
- Displays information about all network interfaces currently in operation.

```
$ ifconfig
eth0: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet 172.20.1.1  netmask 255.255.240.0  broadcast 172.20.15.255
        inet6 fe80::215:5dff:fed3:1fd5  prefixlen 64  scopeid 0x20<link>
        ether 00:15:5d:d3:1f:d5  txqueuelen 1000  (Ethernet)
        RX packets 3679  bytes 892204 (892.2 KB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 1751  bytes 236119 (236.1 KB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

lo: flags=73<UP,LOOPBACK,RUNNING>  mtu 65536
        inet 127.0.0.1  netmask 255.0.0.0
        inet6 ::1  prefixlen 128  scopeid 0x10<host>
        loop  txqueuelen 1000  (Local Loopback)
        RX packets 0  bytes 0 (0.0 B)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 0  bytes 0 (0.0 B)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0
```

- `eth0`: first Ethernet interface 
- `lo`: loopback interface 

## netstat
- Allow printing the various data related to the network configuration of a station. 

`netstat -i`
- Print the state of the network interfaces. 

```
$ netstat -i
Kernel Interface table
Iface      MTU    RX-OK RX-ERR RX-DRP RX-OVR    TX-OK TX-ERR TX-DRP TX-OVR Flg
eth0      1500     3797      0      0 0          1751      0      0      0 BMRU
lo       65536        0      0      0 0             0      0      0      0 LRU
```

- `MTU` and `Met`: Interface's current MTU and metric values/ 
- `RX` and `TX`: How many packets have been received or transmitted error-free (`RX-OK`/`TX-OK`), or damaged (`RX-ERR`/`TX-ERR`); How many were dropped (`RX-DRP`/`TX-DRP`); How many were lost because of an overrun (`RX-OVR`/`TX-OVR`).
- `Flg`: Flags that have been set for thsi interface.
  - `B`: A broadcast address has been set.
  - `L`: This interface is a loopback device.
  - `M`: All packets are received (promiscuous mode).
  - `O`: ARP is turned off for this interface
  - `P`: This is a point-to-point connection.
  - `R`: Interface is running.
  - `U`: Interface is up.

`netstat -r`
- Displays the kernel rounting table. 

```
$ netstat -r
Kernel IP routing table
Destination     Gateway         Genmask         Flags   MSS Window  irtt Iface
default         WX13.mshome.net 0.0.0.0         UG        0 0          0 eth0
172.20.0.0      0.0.0.0         255.255.240.0   U         0 0          0 eth0
```

- `Gateway`: Gateway to which the routing entry points. `*` will be printed if no gateway is used. 
- `Genmask`: Generality of the route.
- `Flags`:
  - `G`: The route uses a gateway. 
  - `U`: The interface to be used is up. 
  - `H`: Only a single host can be reached through the route.
  - `D`: This route is dynamically created. It is set if the table entry has been generated by a routing daemon like gated or by an ICMP redirect message.
  - `M`: This route is set if the table entry was modified by an ICMP redirect message.
  - `!`: The route is a reject route, and datagrams will be dropped.


