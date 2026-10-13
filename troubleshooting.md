# Troubleshooting

## The 60-second diagnosis (memorize this)

Run in order; the first failure is the diagnosis:

1. `ping -c 2 127.0.0.1` — my own stack alive? (verified)
2. `ping -c 2 192.168.1.1` — router reachable?
3. `ping -c 2 8.8.8.8` — internet reachable? (no DNS involved)
4. `getent hosts example.com` — DNS working?
5. `traceroute example.com` — where does the path break?

## Symptom → fix

**Nothing loads, all devices**

Reboot the router (cliché, effective). If it recurs: check the
router's logs/status page for ISP outages, try a different DNS
(1.1.1.1), and call the ISP with traceroute evidence, not "it's
slow."

**One device can't connect, others fine**

Forget the WiFi network and rejoin (clears stale DHCP/auth state).
Check it's not on the guest network by accident. `ip -brief addr` —
does it even have an address?

**Names fail, IPs work**

DNS problem. `getent hosts example.com` vs `ping 8.8.8.8` confirms
it. Check `/etc/resolv.conf` (or OS network settings) for dead
resolvers; check `/etc/hosts` for a bad override.

**"Connection refused" to my own service**

The service isn't listening where you think. `ss -tln` — is the
port listed? No → the service isn't running or bound elsewhere
(check it bound to `0.0.0.0`, not `127.0.0.1`, if others should
reach it). Yes → firewall (`ufw`, router) blocking.

**Port forward works remotely, not from home WiFi**

NAT hairpin — see [Home Networking in Practice](home-networking.md).
Use the LAN address at home.

**Intermittent drops, worse at certain times**

WiFi interference (microwave o'clock) or ISP congestion (everyone
streams at 8pm). Test wired to split the two. WiFi Analyzer apps
show channel crowding.

**SSH: "Connection timed out" vs "Connection refused"**

- **Timed out** — packets vanish: firewall, wrong address, or the
  host is down. Nothing answered at all.
- **Refused** — something answered "nobody here": you reached the
  machine, but nothing listens on port 22 (or its firewall
  rejected you explicitly).

That one-word difference halves the search space. Read errors
literally — they're usually telling the truth.

**Slow, but ping is fine**

Ping measures latency, not bandwidth. Run a speed test (wired, one
device, nothing else streaming). If bandwidth is fine but browsing
feels slow, suspect DNS latency or an overloaded router — not the
ISP.

## When to stop and ask

You've done the 60-second sequence, checked the router page, and
searched the exact error. Now bring: what you ran, the full output,
what changed recently, and whether it's one device or all. "The
internet is broken" gets sympathy; the sequence output gets answers.

**Next:** [Glossary](glossary.md)
