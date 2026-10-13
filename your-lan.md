# Your LAN

Your **LAN** (Local Area Network) is your home network — the
`192.168.1.x` world behind your router. Understanding its three
moving parts explains most home-network mysteries.

## The router: your network's front desk

Your router does four jobs:

1. **Gateway** — the door between your LAN and the internet
   (usually `192.168.1.1`).
2. **DHCP server** — hands out IP addresses to devices that ask
   ("you're `192.168.1.50` for the next 24 hours").
3. **DNS forwarder** — passes your name lookups upstream.
4. **NAT + firewall** — translates your private addresses to its one
   public address, and blocks unsolicited incoming traffic.

**NAT** (Network Address Translation) is why 50 devices share one
public IP: the router rewrites outgoing packets to look like they're
from *it*, remembers who asked, and routes replies back. It's also
why nobody on the internet can just connect *to* your laptop —
there's no mapping for unsolicited inbound traffic (until you add
one — see [Home Networking in Practice](home-networking.md)).

## DHCP: addresses on loan

**DHCP** (Dynamic Host Configuration Protocol) is how devices get
configured without you typing addresses:

1. New device shouts: "any DHCP server out there?"
2. Router replies: "take `192.168.1.50`, gateway `192.168.1.1`, DNS
   `192.168.1.1`, lease 24 hours."

**The lease gotcha:** DHCP addresses can *change*. Your printer was
`.50` yesterday and `.57` today, and your bookmark broke. Fix: a
**DHCP reservation** (router always gives the printer `.50`) or a
**static IP** configured on the device. Printers, NAS boxes, and
servers want stable addresses — phones and laptops don't care.

## Finding your devices

```bash
ip -brief addr    # YOUR address (verified)
```

**Check (typical):** `eth0  UP  192.168.1.50/24` — you're `.50` on
the `.1.x` network, so your router is probably `.1` and your
devices are `.2`–`.254`.

To see who's on the network: your router's admin page (usually
`http://192.168.1.1`) lists DHCP clients — the friendliest device
inventory. Command-line options (`nmap`, `arp -a`) exist; the
router page needs no installs.

## The two-device test

New device not reachable? Halve the problem:

```bash
ping 192.168.1.1       # can you reach the router?
ping 192.168.1.50      # can you reach the other device?
```

Router answers but device doesn't → the device's own firewall, it's
asleep, or wrong network (is it on the guest WiFi? — separate
network, by design). Neither answers → *your* connection is down;
check WiFi/cable first.

**Next:** [WiFi](wifi.md)
