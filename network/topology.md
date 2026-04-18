# Network Topology

## Overview

Home lab network with VLAN segmentation, managed via Cisco C3560CX switch and Turris 1.x router.

---

## VLANs

| VLAN | Name       | Subnet           | Purpose                        |
|------|------------|------------------|-------------------------------|
| 10   | servers    | 192.168.10.0/24  | Production servers (node01, node02) |
| 20   | lan        | 192.168.20.0/24  | Home LAN devices              |
| 30   | iot        | 192.168.30.0/24  | IoT devices                   |
| 99   | mgmt       | 192.168.99.0/24  | Network management            |

---

## Devices

| Device            | Role             | IP               | VLAN |
|-------------------|------------------|------------------|------|
| Turris 1.x        | Router / Firewall | 192.168.99.1    | 99 (gw) |
| Cisco C3560CX     | L2 Switch        | 192.168.99.2     | 99   |
| node01 (HP ProDesk 405 G4 Mini) | Server | 192.168.10.2 | 10 |
| node02 (Dell OptiPlex 3070)     | Server | 192.168.10.3 | 10 |
| TP-Link Archer AX53 | AP (pending)  | TBD              | TBD  |

---

## Cisco C3560CX — Port Assignment

| Port  | Connected To | Mode   | VLAN(s)       |
|-------|-------------|--------|---------------|
| Gi0/1 | Turris lan1 | Trunk  | 10, 20, 30, 99 |
| Gi0/2 | node01 eno1 | Access | 10            |
| Gi0/6 | node02 enp1s0 | Access | 10          |

---

## Turris 1.x — Subinterfaces

| Interface  | VLAN | IP              |
|------------|------|-----------------|
| lan1.10    | 10   | 192.168.10.1    |
| lan1.20    | 20   | 192.168.20.1    |
| lan1.30    | 30   | 192.168.30.1    |
| lan1.99    | 99   | 192.168.99.1    |

---

## Remote Access

- **Tailscale** — permanent remote access solution, runs on node01 and node02
- Access path: notebook → Tailscale → node01/node02 → SSH jump → Turris → Cisco

---

## Notes

- Turris 1.x (PowerPC) does not support Tailscale — runs on nodes only
- TP-Link AX53 not yet connected
- SSH: ed25519 keys only, password auth disabled on all Linux hosts
