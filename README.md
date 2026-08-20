# Homelab

Self-hosted infrastructure running on enterprise hardware in a house. Built to learn by
doing — network segmentation, service orchestration, and sysadmin work through real problems
instead of coursework.

## Docs

- [Hardware overview](homelab/hardware.md) — the boxes, photos, and how they're cabled
- [Network overview](homelab/network.md) — subnets, VLANs, OPNsense setup
- [Services overview](homelab/services.md) — what's running and why

## Hardware at a glance

| Component | Details |
|---|---|
| Hypervisor | Dell PowerEdge R430 |
| Storage | IBM 1818-D1A JBOD |
| Firewall / Router | OPNsense (VM) |
| Network | Netgear switch, Eero upstream |

## Short version

OPNsense splits the lab into a LAN for services and an isolated VLAN for the game server.
Tailscale handles remote access, and the one public service (Nextcloud) goes out through a
Cloudflare Tunnel — so there are no inbound ports open on the house connection.

Host addresses in these docs are masked.
