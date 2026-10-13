# Networking for Mere Mortals

Every time a web page loads, a video streams, or your phone finds
your printer, a small miracle of coordination happens — and it all
rests on a handful of ideas: addresses, names, ports, and routes.
This guide teaches those ideas plainly, then shows you your own home
network through them.

No CS degree required. Ideas first, then commands you can run.

## What this guide covers

- **What networking is** — packets and the postal analogy
- **IP addresses** — the numbers every device needs, IPv4 and IPv6
- **Subnetting** — the 10-minute version: what `/24` means and why
  you can stop there
- **DNS** — how names become numbers
- **Ports and protocols** — TCP vs. UDP, and what a port really is
- **Your LAN** — routers, DHCP, and finding your own devices
- **WiFi** — SSIDs, bands, and why the microwave matters
- **The path to the internet** — traceroute and what happens when
  you visit a site
- **Diagnostic tools** — ping, traceroute, ss, curl, dig
- **Home networking in practice** — port forwarding, static IPs, and
  the NAT hairpin gotcha
- **Security basics** — firewalls, what not to expose, VPNs in two
  minutes
- **Troubleshooting** — symptom → fix

## What it doesn't cover

Enterprise routing protocols (BGP, OSPF), writing network drivers,
or the math of cryptography. This guide is about *understanding*
networks and running your own — especially your home network.

## How to use this guide

Commands are meant to be typed on Linux or macOS (Windows notes
where it matters). **Check:** blocks show what success looks like.
Outputs from a home network are shown as typical — your addresses
will differ, but the shape matches.

## A note on verification

Local commands (`ip`, `ping` to localhost, `ss`, `getent`) were
verified live. Walkthroughs of DNS resolution, traceroute hops, and
home-router behavior show typical output from a standard home
network — labeled as such — because this sandbox's network is
heavily virtualized.

## Chapters

1. [What Networking Is](what-networking-is.md)
2. [IP Addresses](ip-addresses.md)
3. [Subnetting in 10 Minutes](subnetting.md)
4. [DNS](dns.md)
5. [Ports and Protocols](ports-and-protocols.md)
6. [Your LAN](your-lan.md)
7. [WiFi](wifi.md)
8. [The Path to the Internet](internet-path.md)
9. [Diagnostic Tools](diagnostic-tools.md)
10. [Home Networking in Practice](home-networking.md)
11. [Security Basics](security-basics.md)
12. [Troubleshooting](troubleshooting.md)
13. [Glossary](glossary.md)

*Written to the [nine-point writing standard](criteria.md) shared by
every guide in this series.*
