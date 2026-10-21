# homelab
Home network lab with VLANs, OPNsense, and Proxmox, documented like a real sysadmin would.

# Home Lab: Segmented Network, Firewall, and Virtualization

A documented home lab built to practice how network and systems administrators plan, build, and record their work. This is a work in progress, started October 2026. Last updated: 10/20/2026.

## Goals

- Learn VLAN segmentation, inter-VLAN routing, and firewall policy using OPNsense
- Run self-hosted services on Proxmox, separated into security zones
- Build an isolated pentest lab that cannot reach the rest of the network
- Document the work the way professionals do: physical layout, logical design, IP management, asset inventory, and change records

## Status

| Session | Focus | Status |
|---|---|---|
| 1 | Foundations and design (repo, addressing plan, diagrams) | In progress |
| 2 | OPNsense base install | Not started |
| 3 | Switch and VLANs | Not started |
| 4 | Firewall rules and testing | Not started |
| 5 | Proxmox and Pi-hole | Not started |
| 6 | VPN and Wi-Fi | Not started |
| 7 | Pentest lab | Not started |
| 8 | DMZ, website, monitoring, and review | Not started |

## Network design (planned)

| VLAN | Name | Subnet | Purpose |
|---|---|---|---|
| 10 | Upstairs | 10.0.10.0/24 | Primary workstation and trusted devices |
| 20 | Basement | 10.0.20.0/24 | Basement devices |
| 30 | IoT | 10.0.30.0/24 | Smart-home devices |
| 40 | Services | 10.0.40.0/24 | Internal services (DNS filtering, storage, monitoring) |
| 50 | Pentest | 10.0.50.0/24 | Isolated security lab |
| 90 | Management | 10.0.90.0/24 | Network and hypervisor management |

VPN clients use a separate tunnel network (10.0.100.0/24), terminated on the firewall.

**Design principles**
- Default deny between zones, with specific exceptions documented and justified
- Management is the hardest zone to reach, not the easiest
- Anything exposed to the internet lives in its own zone, away from internal services
- The pentest zone has no route to other networks

## Firewall policy summary (planned)

| Zone | Intended access |
|---|---|
| Upstairs (10) | Broad access, with narrow exceptions to the pentest and management zones |
| Basement (20) | DNS and internet only |
| IoT (30) | DNS, NTP, and web traffic to the internet only |
| Services (40) | Internet only |
| Pentest (50) | No access beyond its own zone |
| Management (90) | Reachable only from the admin workstation |

The full rule matrix, with the reasoning for each rule, is in [`docs/firewall`](docs/firewall).

## Hardware

Core components: a managed switch, a dedicated firewall box, a Proxmox host, and a VLAN-capable access point. The full list with purchase details is in [`docs/assets`](docs/assets).

## Documentation

```
docs/
  physical/    Hardware layout, cabling, and port maps
  logical/     VLAN design, routing, and data flows
  ipam/        Subnets, DHCP ranges, and static assignments
  assets/      Hardware inventory
  firewall/    Rule matrix and rationale
  changes/     One record per change (what, why, risk, rollback, verification)
  runbooks/    Step-by-step procedures for backup, restore, and recovery
  decisions/   Why each design choice was made
```

Each change is recorded before and after it is made, with a rollback plan and a verification result.

## What is published here, and what is not

This repository contains the design, reasoning, and results. It deliberately leaves out serial numbers, MAC addresses, firmware versions, public IP details, credentials, and raw device configuration exports. Those are kept in a separate private repository.

## Tools and technologies

OPNsense, Proxmox VE, Netgear managed switching (802.1Q VLANs), Pi-hole, WireGuard, Git and GitHub, draw.io, Claude AI

## Lessons learned



## About

Christian Killpack. Aspiring red team penetration tester, phsyical and virtual. Home lab enthusiast. www.linkedin.com/in/christian-killpack/

## License

MIT License - Ckillpack97, October 2026