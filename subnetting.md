# Subnetting in 10 Minutes

Subnetting is famously over-taught. Here's the version that covers
95% of real life: **the `/24` and what it tells you.**

## The notation

```text
192.168.1.50/24
```

The `/24` is the **prefix length**: the first 24 bits are the
**network** part, the remaining 8 bits identify the **host**. Same
network part = same local network = devices talk directly. Different
network part = traffic goes through the router.

## What /24 means in practice

An IPv4 address is 32 bits. `/24` fixes the first three numbers:

```text
192.168.1.50/24  →  network is 192.168.1.x, host is .50
```

So on a typical home network (`192.168.1.0/24`):

- Your devices: `192.168.1.2` through `192.168.1.254`
- Your router: usually `192.168.1.1`
- Another home using `192.168.2.0/24` is a *different* network —
  your laptop can't reach `192.168.2.50` without a router in between

That's it. That's the 95%.

## The other prefix lengths you'll see

| Prefix | Network size | Where you see it |
|--------|--------------|------------------|
| `/32` | Exactly one address | Firewall rules ("only this IP") |
| `/24` | 256 addresses | Home and small office networks |
| `/16` | 65,536 addresses | Bigger orgs (`10.1.0.0/16`) |
| `/8` | 16.7 million | `10.0.0.0/8` — the whole private range |
| `/31` | 2 addresses | Point-to-point links (routers talking to each other) |

Each bit you add halves the network. You don't need to do binary
math by hand — but know that `/25` is half a `/24`, because someone
will say it in a meeting.

## Netmasks: the old notation

Before `/24` notation, the same idea was written as a **netmask**:

```text
192.168.1.50  netmask 255.255.255.0   (= /24)
```

`255.255.255.0` in binary is twenty-four 1s followed by eight 0s —
same information, clunkier format. You'll still see netmasks in old
docs and some router UIs. When in doubt: 255s = network part, 0 =
host part.

## Why you can stop here

For home networks and small offices, everything is `/24` and the
router handles the rest. Learn the deeper binary math if you ever
need to carve one network into smaller pieces (VLANs, cloud VPCs) —
until then, "first three numbers match = same network" will serve
you correctly every day.

**Next:** [DNS](dns.md)
