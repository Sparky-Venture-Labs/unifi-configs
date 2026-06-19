# Firewall Rules

## Rule Order (apply top to bottom)

### LAN In Rules (traffic entering the gateway from LAN/VLANs)

| Priority | Action | Protocol | Source | Destination | Notes |
|---|---|---|---|---|---|
| 1 | Accept | All | Any | Any | Established/Related connections |
| 2 | Drop | All | Any | Any | Invalid state |
| 3 | Accept | TCP/UDP | AV (192.168.30.0/24) | Default (192.168.1.0/24) | AV control to main LAN |
| 4 | Drop | All | IoT (192.168.10.0/24) | Default (192.168.1.0/24) | Block IoT → Main |
| 5 | Drop | All | IoT (192.168.10.0/24) | Servers (192.168.40.0/24) | Block IoT → Servers |
| 6 | Drop | All | Guest (192.168.20.0/24) | RFC1918 | Block Guest → all private |
| 7 | Drop | All | Security (192.168.50.0/24) | Default (192.168.1.0/24) | Block cameras → Main |

### Common Ports to Allow (AV VLAN → Default)

| Port | Protocol | Service |
|---|---|---|
| 80 | TCP | HTTP |
| 443 | TCP | HTTPS |
| 23 | TCP | Telnet (legacy AV gear) |
| 22 | TCP | SSH |
| 443 | TCP | Savant |
| 11000-11010 | TCP | Crestron |
| 41794 | TCP/UDP | Control4 |

### Tips

- Always put Established/Related accept rule first — prevents breaking existing connections
- Use "Reject" instead of "Drop" on internal VLANs for faster timeout (devices know immediately)
- Use "Drop" on WAN-facing rules
- Log blocked traffic temporarily when troubleshooting — turn off after
