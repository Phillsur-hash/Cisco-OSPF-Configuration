Cisco-OSPF-Configuration

Overview

This project demonstrates the configuration and implementation of Open Shortest Path First (OSPF) dynamic routing between two Cisco routers: New York (NY) and Los Angeles (LA).

OSPF is a link-state routing protocol that allows routers to dynamically exchange routing information and determine the best path to destination networks.

The objective of this lab was to configure OSPF, establish an adjacency between routers, exchange routing information, and verify end-to-end network connectivity using ICMP ping tests.
Network Topology

The lab consists of two Cisco routers connected through a shared transit network.
Device	Interface	IP Address	Network
Router 1 (NY)	G0/0	192.168.20.1	192.168.20.0/24
Router 1 (NY)	G0/1	192.168.10.1	192.168.10.0/24
Router 2 (LA)	G0/0	192.168.20.2	192.168.20.0/24
Router 2 (LA)	G0/1	192.168.30.1	192.168.30.0/24
Network Diagram
text

         New York (NY) Router
              NY
               |
       G0/1    |    G0/0
 192.168.10.1  |  192.168.20.1
               |
          192.168.20.0/24
               |
       G0/0    |    G0/1
 192.168.20.2  |  192.168.30.1
               |
         Los Angeles (LA)
               |
        192.168.30.0/24
               |
          Host: 192.168.30.10

Technologies Used

    Cisco IOS
    Cisco Routers
    Open Shortest Path First (OSPF)
    IPv4 Addressing
    Dynamic Routing
    ICMP (Ping)
    Cisco Command Line Interface (CLI)

OSPF Configuration

Both routers were configured to use OSPF Process ID 1 and Area 1.
1. Router 1 – New York (NY)

Enter privileged EXEC mode and global configuration mode.
cisco

NY> enable
NY# conf t

Enable OSPF Process ID 1.
cisco

NY(config)# router ospf 1

Advertise the connected networks into OSPF Area 1.
cisco

NY(config-router)# network 192.168.20.0 0.0.0.255 area 1
NY(config-router)# network 192.168.10.0 0.0.0.255 area 1

Verify the routing table.
cisco

NY(config-router)# do show ip route

NY Routing Table Results:

    192.168.10.0/24 – Directly connected.
    192.168.20.0/24 – Directly connected.
    192.168.30.0/24 – Learned through OSPF.

OSPF-learned route:
text

O 192.168.30.0/24 [110/2] via 192.168.20.2,
  GigabitEthernet0/0

This confirms that the New York router successfully learned the Los Angeles network through OSPF.
2. Router 2 – Los Angeles (LA)

Enter privileged EXEC mode and global configuration mode.
cisco

LA> enable
LA# conf t

Enable OSPF Process ID 1.
cisco

LA(config)# router ospf 1

Advertise the connected networks into OSPF Area 1.
cisco

LA(config-router)# network 192.168.20.0 0.0.0.255 area 1
LA(config-router)# network 192.168.30.0 0.0.0.255 area 1

OSPF Neighbor Adjacency:

The following message appeared after configuring OSPF:
text

%OSPF-5-ADJCHG: Process 1, Nbr 192.168.20.1
on GigabitEthernet0/0 from LOADING to FULL,
Loading Done

This message confirms that the Los Angeles router successfully established a FULL OSPF adjacency with the New York router.

Verify the routing table.
cisco

LA(config-router)# do show ip route

LA Routing Table Results:

    192.168.20.0/24 – Directly connected.
    192.168.30.0/24 – Directly connected.
    192.168.10.0/24 – Learned through OSPF.

OSPF-learned route:
O 192.168.10.0/24 [110/2] via 192.168.20.1,
  GigabitEthernet0/0

This confirms that the Los Angeles router successfully learned the New York network through OSPF.
Connectivity Testing

After completing the OSPF configuration, an ICMP ping test was performed to verify end-to-end connectivity.

Test Destination: 192.168.30.10

Command:
text

ping 192.168.30.10

Ping Test Results:
text

Pinging 192.168.30.10 with 32 bytes of data:

Reply from 192.168.30.10: bytes=32 time<1ms TTL=126
Reply from 192.168.30.10: bytes=32 time<1ms TTL=126
Reply from 192.168.30.10: bytes=32 time<1ms TTL=126
Reply from 192.168.30.10: bytes=32 time<1ms TTL=126

Ping statistics for 192.168.30.10:
    Packets: Sent = 4,
    Received = 4,
    Lost = 0 (0% loss),

Approximate round trip times in milli-seconds:
    Minimum = 0ms,
    Maximum = 0ms,
    Average = 0ms

Ping Test Summary
Metric	Result
Destination IP	192.168.30.10
Packets Sent	4
Packets Received	4
Packets Lost	0
Packet Loss	0%
Minimum Response Time	0ms
Maximum Response Time	0ms
Average Response Time	0ms

Result: Successful connectivity.

All four ICMP packets received responses, confirming successful communication with the destination host.
OSPF Verification Commands

The following commands can be used to verify OSPF operation and routing information on Cisco routers.
cisco

show ip route
show ip ospf neighbor
show ip protocols
show ip ospf interface brief

Command	Purpose
show ip route	Displays the routing table
show ip ospf neighbor	Displays OSPF neighbor relationships
show ip ospf interface brief	Displays OSPF-enabled interfaces
Project Results

The OSPF configuration was successfully implemented between the New York and Los Angeles routers.

The following objectives were achieved:

    Configured OSPF Process ID 1 on both routers.
    Assigned both routers to OSPF Area 1.
    Advertised local networks into OSPF.
    Established a FULL OSPF neighbor adjacency.
    Successfully exchanged routing information.
    Verified dynamically learned routes using show ip route.
    Completed an end-to-end ping test with 0% packet loss.

Conclusion

This lab demonstrates how OSPF enables dynamic routing between geographically separated networks using Cisco routers.

By configuring OSPF on the New York and Los Angeles routers, both devices successfully exchanged routing information and learned remote network routes.

The FULL OSPF adjacency confirmed successful communication between the routers, while the routing tables verified that remote networks were dynamically learned.

Finally, the successful ping test to 192.168.30.10, with four packets transmitted and zero packets lost, demonstrated end-to-end network connectivity.

This project provided hands-on experience with Cisco IOS, dynamic routing protocols, OSPF neighbor relationships, routing table analysis, and network troubleshooting.

Project Name: Cisco-OSPF-Configuration
Routing Protocol: OSPF
Process ID: 1
OSPF Area: 1
Routers: New York (NY) and Los Angeles (LA)
Connectivity Test: Successful (0% Packet Loss)
