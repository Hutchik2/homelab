# Services Overview

Everything running in the lab and why it's set up that way. General rules: keep things
separated by how much I trust them, don't open inbound ports, and use containers unless
something really needs a full VM.

## What's running

| Service | Type | Where | Reachable from |
|---|---|---|---|
| Proxmox VE | Host | 192.168.6.x | LAN + Tailscale |
| OPNsense | VM | WAN / LAN / VLAN 60 | LAN only |
| Jellyfin | LXC | LAN | LAN + Tailscale |
| Nextcloud | LXC | LAN | Public, via Cloudflare Tunnel |
| Radarr · Sonarr · Prowlarr | LXC | LAN | LAN only |
| Pinchflat | LXC | LAN | LAN only |
| Vaultwarden | LXC | LAN | LAN + Tailscale |
| Tailscale | Subnet router | LAN | Outbound only |
| Minecraft (DiscoPanel) | LXC | 192.168.60.x | Public, via playit.gg |

## Platform

**Proxmox VE** — Dell R430 with an IBM JBOD hanging off it. Runs everything. Most services
are LXC containers rather than VMs because containers are way lighter on RAM and there's only
one box to go around.

**OPNsense** — the firewall and router, running as a VM since it needs its own network stack.
Details in the [network overview](../network/overview.md).

## Media

**Jellyfin** — media server for stuff ripped from discs I own. Picked it over Plex because
it's fully self-hosted, no account with anyone else in the loop.

**Radarr · Sonarr · Prowlarr** — keep the library organized and the metadata sane. Prowlarr
handles indexers for both so I'm not configuring the same thing twice. LAN only.

**Pinchflat** — archives YouTube channels on a schedule into the same storage Jellyfin reads,
so it just shows up in the library.

## Cloud

**Nextcloud** — file sync, and the only thing that's actually public. It goes out through a
Cloudflare Tunnel instead of a port forward, so nothing is open inbound and my home IP isn't
sitting in a DNS record.

**Vaultwarden** — password manager. Opposite call from Nextcloud: it's the most valuable
thing here, so it stays on Tailscale only and never touches the public tunnel.

## Access

**Tailscale** — subnet router, so I can hit LAN services at their normal addresses from
anywhere without opening a VPN port.

## Game server

**Minecraft (DiscoPanel)** — LXC on VLAN 60. It's the one thing strangers connect to, so it
gets its own subnet and firewall rules keep it from reaching the LAN. If it ever gets popped
it lands in an empty subnet instead of next to Vaultwarden. Public access is a playit.gg
tunnel — same idea as Nextcloud, outbound only, no port forward.

## Ground rules

- LXC by default, VM only if it needs its own kernel.
- Static addresses for anything other services depend on.
- LAN-only unless there's a reason not to be. Tailscale before public.
- Tunnels, never port forwards.
- Config gets written down here, not just left on the box.

## Todo

- [ ] Monitoring and alerting (Grafana or Uptime Kuma)
- [ ] Off-site backups, actually tested
- [ ] Reverse proxy + internal TLS so I stop typing IP:port
- [ ] Infrastructure-as-code for spinning up containers
