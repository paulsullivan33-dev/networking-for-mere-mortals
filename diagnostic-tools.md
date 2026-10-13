# Diagnostic Tools

The toolkit, in the order to use them. Every one of these is worth
ten guesses.

## ping — "are you there?"

```bash
ping -c 4 192.168.1.1
ping -c 4 8.8.8.8
```

Sends echo requests, reports replies and round-trip times.
**Check (verified):** `4 packets transmitted, 4 received, 0% packet
loss`.

The two-ping test: `8.8.8.8` needs no DNS (it's a bare address), so
`ping 8.8.8.8` working while names fail = DNS problem, network fine.
Neither working = network problem. One command, total clarity.

## traceroute — "show me the path"

```bash
traceroute example.com
```

Hop-by-hop itinerary (see [The Path to the Internet](internet-path.md)).
Use when ping works but things are slow — it shows *where*.

## ss — "what's listening here?"

```bash
ss -tln
```

**Check (verified shape):** lists listening TCP ports. "My server
won't connect" → is it even listening? This answers in one line.

## curl — "talk to it like a client"

```bash
curl -I http://192.168.1.50:8080   # headers only: is the web server answering?
curl -v http://192.168.1.50:8080   # verbose: DNS, connect, TLS, headers — the full story
```

`curl -v` is a network education in one command: watch it resolve
the name, open the TCP connection, negotiate TLS, and send the
request. When a web service misbehaves, `-v` shows exactly which
stage failed.

## dig — "what does DNS say?"

```bash
dig +short example.com     # just the address
dig example.com            # the full exchange: server, TTL, timing
```

When names misbehave, `dig` shows what the resolver actually
returned — versus what you *assumed* it returned.

## ip — "what's my network config?"

```bash
ip -brief addr    # my addresses (verified)
ip route          # how do I reach things? (shows the default gateway)
```

`ip route` output centers on the `default via 192.168.1.1` line —
that's your router, the door everything leaves through. No default
route = no internet, and now you know the exact sentence to search.

## The 60-second diagnosis order

1. `ping -c 2 127.0.0.1` — is my own network stack alive? (verified)
2. `ping -c 2 192.168.1.1` — can I reach the router?
3. `ping -c 2 8.8.8.8` — can I reach the internet? (no DNS needed)
4. `getent hosts example.com` — does DNS work?
5. `traceroute example.com` — where does the path break?

The first failure in that sequence *is* the diagnosis. Don't skip
steps — each one rules out a layer.

**Next:** [Home Networking in Practice](home-networking.md)
