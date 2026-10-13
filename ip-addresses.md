# IP Addresses

Every device on a network needs an address — otherwise packets can't
find it. The **IP address** is that address.

## IPv4: the classic

```text
192.168.1.50
```

Four numbers, 0–255, separated by dots. Each number is one **byte**
(8 bits), so the whole address is 32 bits — about 4 billion possible
addresses. That sounded like plenty in 1981. It wasn't, which is why
the rest of this chapter exists.

Your address right now (typical home network):

```bash
ip -brief addr
```

**Check (verified shape, typical addresses):**

```text
lo               UNKNOWN        127.0.0.1/8 ::1/128
eth0             UP             192.168.1.50/24 ...
```

(The `/24` is the subnet — next chapter.)

## Private vs. public

Only some IPv4 addresses route on the internet. Three ranges are
**private** — free for any home/office network, never valid on the
public internet:

| Range | Typical use |
|-------|-------------|
| `10.0.0.0` – `10.255.255.255` | Large networks |
| `172.16.0.0` – `172.31.255.255` | Medium networks |
| `192.168.0.0` – `192.168.255.255` | Home networks (your router uses one) |

Your laptop is probably `192.168.1.x`. Your router has *two*
addresses: a private one facing your home (`192.168.1.1`) and a
public one facing the internet (assigned by your ISP). It translates
between them — that's **NAT**, covered in [Your LAN](your-lan.md).

## Special addresses worth knowing

| Address | Meaning |
|---------|---------|
| `127.0.0.1` | **localhost** — "this computer." Always works, needs no network |
| `0.0.0.0` | "All interfaces" — a server listening here accepts from anywhere |
| `255.255.255.255` | Broadcast — "everyone on my local network" |

**Check (verified):**

```bash
ping -c 2 127.0.0.1
```

```text
2 packets transmitted, 2 received, 0% packet loss
```

localhost always answers — it's the simplest possible network test.

## IPv6: the successor

IPv4's 4 billion addresses ran out (workarounds like NAT delayed the
crisis for decades). IPv6 uses 128 bits — 340 undecillion addresses,
enough for every grain of sand to have a network:

```text
fe80::70dc:7cff:fe34:2ffd
```

Eight groups of hex, with `::` compressing runs of zeros. Your
devices almost certainly have IPv6 addresses already; most home
traffic still uses IPv4, and everything in this guide works for both
unless noted. You don't need to master IPv6 to run a home network —
just recognize the format when you see it.

**Next:** [Subnetting in 10 Minutes](subnetting.md)
