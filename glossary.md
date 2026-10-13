# Glossary

| Term | Meaning |
|------|---------|
| bandwidth | How much data per second a link carries (Mbps) |
| baud | Symbols per second (serial); both ends must match |
| broadcast | A packet addressed to everyone on the local network |
| CIDR (`/24`) | Prefix-length notation: how many address bits are the network part |
| DHCP | Hands out IP addresses (and gateway/DNS) automatically |
| DNS | Translates names (`example.com`) to IP addresses |
| gateway | The router your traffic leaves through (usually `192.168.1.1`) |
| hairpinning | Router looping LAN→public-IP→LAN traffic back inside (often unsupported) |
| IPv4 | 32-bit addresses (`192.168.1.50`) — the classic |
| IPv6 | 128-bit addresses (`fe80::...`) — the successor |
| LAN | Local Area Network — your home network |
| latency | Round-trip time (ms) — the "snappy" factor |
| localhost | `127.0.0.1` — "this computer" |
| NAT | Network Address Translation — many private addresses share one public IP |
| netmask | Old notation for the network/host split (`255.255.255.0` = `/24`) |
| packet | A small addressed chunk of data — the unit of network travel |
| port | A number identifying a program on a machine (`:8080`) |
| protocol | Agreed rules for communication (TCP, UDP, HTTP...) |
| router | Forwards packets between networks; your LAN's front desk |
| SSID | A WiFi network's name |
| subnet | A subdivision of a network — same prefix = direct local talk |
| TCP | Reliable, ordered delivery (phone call) |
| TLS | Encryption layer (the S in HTTPS) |
| traceroute | Shows each router hop to a destination |
| TTL (DNS) | How long a DNS answer may be cached |
| UDP | Fast, best-effort delivery (shouting into a canyon) |
| VPN | Encrypted tunnel making a remote device act local |
