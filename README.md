# Homelab

Self-hosted infrastructure running on enterprise hardware in a house — a Dell PowerEdge R430
running Proxmox, with OPNsense handling routing and VLAN segmentation.

## Why I built it

I built this homelab so I can practice what I learn in class in a real environment that I
control. I use it to run and test new services, and I keep parts of it as a sandbox for
picking up something new.

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

---

_Host addresses in these docs are masked._
