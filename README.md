# fortinet-FGT-_Enterprise-Branch-to-HQ-WAN-Lab

1. Project Overview
Enterprise Branch-to-HQ WAN Lab
This lab simulates a real enterprise WAN environment between Headquarters and Branch offices using:
FortiGate firewalls in HA mode
Huawei CE6800 switches with VRRP
OSPF dynamic routing
Dual ISP WAN connectivity
VLAN segmentation
Redundant Layer2 and Layer3 design
The objective of this lab is to practice:
enterprise redundancy
gateway failover
WAN resiliency
routing convergence
firewall high availability
Layer2/Layer3 integration

2. Topology Overview
You can insert your topology image here.
Main components:
HQ Site
HQ_FGT_01 / HQ_FGT_02 (FortiGate HA)
HQ_CE6800_01 / HQ_CE6800_02 (VRRP Pair)
Branch Site
BR_FGT_01 / BR_FGT_02 (FortiGate HA)
BR_CE6800_01 / BR_CE6800_02 (VRRP Pair)
WAN
ISP1
ISP2

3. Key Technologies Used
FortiGate HA
Active-passive firewall redundancy
Dedicated HA heartbeat interfaces
Automatic failover
VRRP
Used on Huawei CE6800 switches for:
default gateway redundancy
high availability for VLAN gateways
Example:
VLAN10 gateway: 10.10.10.1
VLAN20 gateway: 10.10.20.1
VLAN30 gateway: 10.10.30.1
Configured using VRRP virtual IPs.

OSPF Dynamic Routing
OSPF Area 0 configured between routing devices.
HQ Router IDs:
1.1.1.1
1.1.1.2
Branch Router IDs:
2.2.2.1
2.2.2.2
Example configuration:
Features:
automatic route learning
dynamic failover
scalable routing design

STP Design
Spanning Tree configured with:
root primary
root secondary
Example:
 HQ_CE6800_01 configured as STP root primary.
HQ_CE6800_02 configured as STP root secondary.

4. VLAN Design
HQ VLANs
VLAN
Purpose
Gateway
10
Users
10.10.10.1
20
Servers
10.10.20.1
30
Management
10.10.30.1
999
Transit/OSPF
10.255.255.0/29


Branch VLANs
VLAN
Purpose
Gateway
10
Users
10.20.10.1
20
Servers
10.20.20.1
30
Management
10.20.30.1
999
Transit/OSPF
10.255.255.8/29


5. Redundancy Design
Firewall Redundancy
FortiGate firewalls operate in HA mode to ensure:
session continuity
firewall failover
minimal downtime
Gateway Redundancy
VRRP provides:
virtual default gateway
automatic gateway failover
WAN Redundancy
Dual ISP links provide:
path redundancy
failover capability
routing resiliency
Layer2 Redundancy
Eth-Trunk used between CE6800 switches:
bandwidth aggregation
redundancy
loop prevention with STP
Example Eth-Trunk config:

6. OSPF Design Decision
Initially, OSPF was enabled between VRRP pairs using VLAN999 transit networks.
Later analysis concluded:
VRRP should handle gateway redundancy
OSPF should primarily exchange routes toward WAN/firewall paths
unnecessary OSPF adjacencies between VRRP peers can increase complexity
This reflects real enterprise design principles:
“Enable only the protocols required for the design.”

7. Validation & Testing
Failover Tests
Tested:
FortiGate HA failover
VRRP master failover
OSPF neighbor recovery
ISP link failure scenarios
Verification Commands
Huawei CE6800
display ospf peer
display vrrp
display stp brief
display ip routing-table
FortiGate
get system ha status
get router info routing-table all
diagnose sys ha status

8. Skills Demonstrated
This lab demonstrates practical experience with:
Enterprise WAN design
High Availability
Dynamic Routing
Huawei CE6800
FortiGate Firewall
VRRP
OSPF
STP
VLAN segmentation
Dual ISP architecture
Troubleshooting
Network failover testing

