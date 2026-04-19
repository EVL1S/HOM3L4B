# AdGuard Home

DNS filtering and ad blocking for the homelab network.

## Deployment

- **Host:** node02 (192.168.10.3)
- **Stack:** Docker Compose (`~/docker/adguard/`)
- **DNS port:** 53 (TCP/UDP)
- **Web UI:** http://192.168.10.3:3000

## Network integration

Turris DHCP pushes AdGuard Home as the DNS server to all clients:

    uci set dhcp.lan.dhcp_option='6,192.168.10.3'

node01 and node02 use AdGuard Home as primary DNS (192.168.10.3) with 1.1.1.1 as fallback, configured via Netplan.

## Notes

- systemd-resolved stub listener disabled on node02 (DNSStubListener=no) to free port 53
- Turris AdBlock disabled (replaced by AdGuard Home)
