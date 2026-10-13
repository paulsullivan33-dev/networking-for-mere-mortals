# Home Networking in Practice

The fun stuff: reaching your home server from outside, giving
devices stable addresses, and the gotcha that bites everyone once.

## Port forwarding: letting the internet in

By default, your router's NAT blocks unsolicited inbound traffic —
nothing outside can reach your home server. **Port forwarding** pokes
a deliberate hole: "traffic to my public IP on port 2323 goes to
`192.168.1.118` port 2323."

Router admin → port forwarding → add: external port, internal IP,
internal port, TCP (or UDP). Then it works from anywhere.

**Careful:** Every forwarded port is a door to the internet, knocked
on by bots within minutes. Forward only what you need, keep the
service updated, use strong auth (keys, not passwords, for SSH), and
consider whether a VPN (next section) is safer than exposing the
service directly.

## The NAT hairpin gotcha

You forward port 2323, test from your phone on cellular — works.
Test from your laptop on home WiFi using your *public* address —
fails. The service is fine; you've met **NAT hairpinning** (or its
absence).

What happens: your laptop asks the router for the *public* address.
The router forwards it out... and many consumer routers can't loop
the reply back inside (the "hairpin" turn). From the LAN, use the
*LAN* address (`192.168.1.118:2323`); from outside, use the public
one. Some routers handle hairpins fine; if yours doesn't, this
split-brain addressing is the workaround — or run local DNS
(Pi-hole, router overrides) so the name resolves to the LAN address
at home.

## Static addresses for infrastructure

Anything you connect *to* — NAS, printer, home server, Pi-hole —
wants a stable address. Two ways:

1. **DHCP reservation** (recommended): router admin → DHCP →
   bind the device's MAC address to `192.168.1.50`. The device still
   uses DHCP; it just always gets the same answer. One central
   place to manage.
2. **Static IP on the device**: configure the address, netmask,
   gateway, and DNS manually. Works without router cooperation, but
   now the config lives on the device — document it, because
   future-you won't remember.

Pick a scheme and stick to it: e.g. `.1` router, `.2`–`.49`
infrastructure (reserved), `.50`+ DHCP pool.

## A VPN instead of open ports

Rather than forwarding five ports, forward *one* — a **VPN** server
(WireGuard is the modern pick: fast, simple, ~10 lines of config) —
and join your home network remotely. Your phone/laptop gets a LAN
address and reaches everything as if home, with one encrypted door
instead of five. More setup than port forwarding, much smaller
attack surface.

## Pi-hole (the beloved side project)

A **Pi-hole** is a DNS server for your LAN (runs on a Raspberry Pi)
that blocklists ad and tracker domains network-wide — phones, TVs,
everything, no per-device software. It also gives you local DNS
names (`nas.lan`) and lovely query graphs. It's the classic "my
first home server" project for a reason.

**Next:** [Security Basics](security-basics.md)
