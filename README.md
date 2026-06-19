# unifi-configs

Sanitized UniFi network configurations, VLAN setups, and firewall rules. Built for real deployments — home labs, small offices, and AV/integration installs.

All IP addresses, credentials, and site-specific info have been removed and replaced with placeholders.

---

## Structure

```
unifi-configs/
├── vlans/          — VLAN definitions and naming conventions
├── firewall/       — Firewall rule templates
├── wifi/           — SSID and wireless profiles
├── routing/        — Static routes and inter-VLAN routing
└── scripts/        — UniFi controller API scripts
```

---

## VLAN Layout (recommended)

| VLAN ID | Name | Purpose |
|---|---|---|
| 1 | Default | Management — devices you trust |
| 10 | IoT | Smart home devices, cameras, printers |
| 20 | Guest | Guest WiFi — internet only |
| 30 | AV | AV equipment, control systems |
| 40 | Servers | NAS, home servers, self-hosted services |
| 50 | Security | Cameras, NVR, alarm systems |

---

## Firewall Philosophy

- IoT → LAN: **Block** (IoT devices can't reach your main network)
- Guest → LAN: **Block**
- AV → LAN: **Allow** specific ports only (control system needs)
- All → WAN: **Allow** (outbound)
- Established/Related: **Allow** on all VLANs

---

## Requirements

- UniFi Dream Machine, Dream Router, or any UniFi gateway
- UniFi Network Application 8.x+
- Basic understanding of VLANs and firewall rules

---

## Usage

These are reference configs — not import files. Use them as a guide when building your own network. Adapt VLAN IDs and subnets to your environment.
