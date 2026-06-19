# VLAN Layout

## Recommended VLAN structure for home/small office UniFi deployments

### Subnets

| VLAN | Name | Subnet | Gateway |
|---|---|---|---|
| 1 | Default | 192.168.1.0/24 | 192.168.1.1 |
| 10 | IoT | 192.168.10.0/24 | 192.168.10.1 |
| 20 | Guest | 192.168.20.0/24 | 192.168.20.1 |
| 30 | AV | 192.168.30.0/24 | 192.168.30.1 |
| 40 | Servers | 192.168.40.0/24 | 192.168.40.1 |
| 50 | Security | 192.168.50.0/24 | 192.168.50.1 |

### DHCP Ranges

| VLAN | DHCP Start | DHCP End | Reserved Range |
|---|---|---|---|
| Default | 192.168.1.100 | 192.168.1.200 | .1–.99 (static assignments) |
| IoT | 192.168.10.100 | 192.168.10.200 | .1–.99 |
| Guest | 192.168.20.100 | 192.168.20.200 | — |
| AV | 192.168.30.100 | 192.168.30.200 | .1–.99 |
| Servers | 192.168.40.100 | 192.168.40.150 | .1–.99 (mostly static) |
| Security | 192.168.50.100 | 192.168.50.200 | .1–.99 |

### Notes

- Keep management interfaces (switches, APs, gateway) on VLAN 1 or a dedicated mgmt VLAN
- AV VLAN needs to reach control processors — allow specific ports in firewall rules
- Guest VLAN should have client isolation enabled
- IoT VLAN: enable multicast DNS (mDNS) gateway if you need AirPlay/Chromecast cross-VLAN
