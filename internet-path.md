# The Path to the Internet

A packet from your laptop to a website crosses ~10–20 routers.
`traceroute` shows you the journey — it's the most fun diagnostic
tool there is.

## Watching the hops

```bash
traceroute example.com
```

**Check (typical output):**

```text
1  192.168.1.1      1.2 ms    ← your router
2  10.20.0.1        8.4 ms    ← your ISP, first hop out
3  72.14.0.5       12.1 ms    ← ISP backbone
4  ...
9  93.184.216.34   28.7 ms    ← the destination
```

Each line is a router that handled your packet, with round-trip
times. Read it like a travel itinerary: home → ISP → backbone →
destination network → server.

(Windows: `tracert`. Same idea. Some systems need `traceroute`
installed — `sudo apt install traceroute`.)

## What the times tell you

- **Jump at hop 2** (1ms → 40ms): the slowdown is between you and
  your ISP — your line, not the website.
- **Jump in the middle**: someone's backbone is congested. Nothing
  you can do but wait (or complain with evidence).
- **`* * *` timeouts mid-route**: a router configured not to
  answer traceroute. Common and harmless — the packet still passed
  *through*; it just didn't wave.
- **Everything fine until the last hop fails**: the destination is
  down or firewalled, but the path to it is healthy.

## What happens when you visit a website (the full sequence)

1. **DNS** — `example.com` → `93.184.216.34` (see [DNS](dns.md))
2. **TCP handshake** — your computer and the server agree to talk
   (SYN → SYN-ACK → ACK, ~1 round trip)
3. **TLS handshake** — they negotiate encryption; the server proves
   its identity with a certificate (~1–2 round trips)
4. **HTTP request** — "GET / please," encrypted
5. **Response** — the page, in packets, reassembled by TCP

That's 3–4 round trips before a single byte of *your* page moves —
why latency (ping time) matters more than bandwidth for "snappy"
browsing, and why a 30ms-away server feels instant while a 300ms one
feels sluggish even on gigabit.

## Latency vs. bandwidth

- **Bandwidth** — how *wide* the pipe is (Mbps). Matters for
  downloads, streams, backups.
- **Latency** — how *long* a round trip takes (ms). Matters for
  gaming, video calls, "snappy" feel.

A satellite link can have huge bandwidth and terrible latency —
great for Netflix, awful for Zoom. Most "my internet feels slow"
complaints are latency, not bandwidth.

**Next:** [Diagnostic Tools](diagnostic-tools.md)
