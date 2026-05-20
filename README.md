# Enterprise Branch-to-HQ WAN Lab

Enterprise WAN lab simulating a real-world HQ and Branch network using FortiGate HA, Huawei CE6800 VRRP, OSPF dynamic routing, and dual ISP redundancy.

---

## Topology

![Topology](./images/topology.png)

---

# Project Overview

This lab was built to practice enterprise-grade networking concepts including:

- High Availability (HA)
- Dynamic Routing
- Gateway Redundancy
- WAN Redundancy
- Layer2/Layer3 Redundancy
- Enterprise Routing Design
- Failover Testing

The topology simulates communication between:

- Headquarters (HQ)
- Branch Office (BR)

through redundant WAN links.

---

# Technologies Used

## Firewall
- FortiGate 7.0

## Switching
- Huawei CE6800

## Routing & Redundancy
- OSPF
- VRRP
- STP
- Eth-Trunk (LACP)

---

# Network Design

## HQ Site
- FortiGate HA Cluster
- CE6800 VRRP Pair
- VLAN Segmentation
- OSPF Routing

## Branch Site
- FortiGate HA Cluster
- CE6800 VRRP Pair
- VLAN Segmentation
- OSPF Routing

## WAN
- Dual ISP Links
- Redundant WAN Paths

---

# VLAN Design

## HQ

| VLAN | Purpose | Gateway |
|---|---|---|
| 10 | Users | 10.10.10.1 |
| 20 | Servers | 10.10.20.1 |
| 30 | Management | 10.10.30.1 |
| 999 | Transit / OSPF | 10.255.255.0/29 |

## Branch

| VLAN | Purpose | Gateway |
|---|---|---|
| 10 | Users | 10.20.10.1 |
| 20 | Servers | 10.20.20.1 |
| 30 | Management | 10.20.30.1 |
| 999 | Transit / OSPF | 10.255.255.8/29 |

---

# High Availability Design

## FortiGate HA
Configured in Active-Passive mode for:
- firewall redundancy
- session synchronization
- automatic failover

## VRRP
Implemented on Huawei CE6800 switches for:
- gateway redundancy
- resilient default gateways

---

# OSPF Design

OSPF Area 0 configured between devices for:
- automatic route learning
- dynamic failover
- scalable routing

Router IDs:

| Device | Router ID |
|---|---|
| HQ-CE6800-01 | 1.1.1.1 |
| HQ-CE6800-02 | 1.1.1.2 |
| BR-CE6800-01 | 2.2.2.1 |
| BR-CE6800-02 | 2.2.2.2 |

---

# Layer2 Design

## STP
- Root Primary configured on CE6800-01
- Root Secondary configured on CE6800-02

## Eth-Trunk
Used between CE6800 switches for:
- redundancy
- bandwidth aggregation
- loop prevention

---

# Verification Commands

## Huawei CE6800

### OSPF
```bash
display ospf peer
