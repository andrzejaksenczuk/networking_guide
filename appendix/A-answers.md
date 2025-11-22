
# Answers Appendix

> This appendix collects answers to in-chapter self-checks and quick labs. Lab outputs may vary by your exact topology and device models; where exact values differ, use the **expected outcome** column to verify your work.

---

## Network Fundamentals

### Network Components

**Switch1 (L2)**

Based on outputs from above commands which ports are access/trunk?

   - Trunks: Gi0/1, Po1
   - Fa0/1–Fa0/4 are up/up so can be potentially threated as access ports

Did the switch learn PCs NIC’s MAC?

   - No, need to send some initial message first from PC like ping.

Which VLANs exist (active)?

   - VLANs active: 1, 10, 11, 12, 13, 1002, 1003, 1004, 1005

**Multilayer Switch0 (L3)**

What is the default route?

   - Gateway of last resort is not set

Which interface is the gateway for your subnets?

| VLAN | Gateway (SVI)             | Status |
| ---: | ------------------------- | ------ |
|    1 | **192.168.1.1** (`Vlan1`) | up/up  |
|   10 | **10.0.10.1** (`Vlan10`)  | up/up  |
|   11 | **10.0.11.1** (`Vlan11`)  | up/up  |
|   12 | **10.0.12.1** (`Vlan12`)  | up/up  |
|   13 | **10.0.13.1** (`Vlan13`)  | up/up  |


---

### Addressing — Networks & Netmasks

### Task A — Two variable subnets
Given `192.168.10.0/24`, create:
- **Subnet A** for **40 hosts**
- **Subnet B** for **20 hosts**

Allocate the larger block first (/26 from .0–.63), then place the /27 in the next free block (.64–.95).

| Specification                | Subnet A (40 hosts)       | Subnet B (20 hosts)       |
| ---------------------------- | ------------------------- | ------------------------- |
| Number of bits in the subnet | **6**                     | **5**                     |
| New IP mask (dec)            | `/26` (`255.255.255.192`) | `/27` (`255.255.255.224`) |
| Max usable subnet            | **4**                     | **8**                     |
| Max usable hosts             | `2^26-2 = 62`             | `2^27-2 = 30`             |
| IP Subnet (Network)          | `192.168.10.0/26`         | `192.168.10.64/27`        |
| First IP Host address        | `192.168.10.1`            | `192.168.10.65`           |
| Last IP Host address         | `192.168.10.62`           | `192.168.10.94`           |
| Broadcast                    | `192.168.10.63`           | `192.168.10.95`           |

(Answers: 30; 192.168.10.127; a router/L3 SVI (gateway).)

2) Answers

a) 30 usable hosts

b) 192.168.10.127

c) A router / L3 SVI (default gateway)

---

### Packet Flow & Hands‑On Configuration

[Final Subnet topology](../assets/labs/packet_tracer/finals/subnets_final.pkt)

---

## Switching & VLANs

### Switching & VLANs Basis

[Final vLANs topology](../assets/labs/packet_tracer/finals/vlans_final.pkt)

### Inner-VLAN Routing

[Final inter-vLAN topology](../assets/labs/packet_tracer/finals/inter_vlans_final.pkt)

### EtherChannel

[Final EtherChannel topology](../assets/labs/packet_tracer/finals/etherchannels_final.pkt)

---

## Routing Basics

### Routing Table and Static Routing

[Final Routing topology](../assets/labs/packet_tracer/finals/routing_final.pkt)

### Dynamic Routing Algorithms

[Final OSFP topology](../assets/labs/packet_tracer/finals/routing_ospf.pkt)

### Default Routing & IPv6 Routing

[Final IPv6 Routing topology](../assets/labs/packet_tracer/finals/routing_ipv6_final.pkt)

---

## Wireless LAN with Controllers & Lightweight APs

[Final WLAN topology](../assets/labs/packet_tracer/finals/wlc_min_final.pkt)

---

## IP Services - NAT, DHCP, DNS

1) [Final NAT topology](../assets/labs/packet_tracer/finals/nat_final.pkt)

2) [Final DHCP topology](../assets/labs/packet_tracer/finals/dhcp_final.pkt)

3) [Final DNS topology](../assets/labs/packet_tracer/finals/dns_final.pkt)

### IP Services - continue

1) [Final NAT topology](../assets/labs/packet_tracer/finals/tftp_final.pkt)

---

## Security Fundamentals

### Firewalls and VPN

1) [Final Firewall topology](../assets/labs/packet_tracer/finals/firewall_final.pkt)

2) [Final VPN topology](../assets/labs/packet_tracer/finals/vpn_final.pkt)

---

## Automation

[Ansible server setup](../assets/labs/packet_tracer/lab18/ansible.zip)