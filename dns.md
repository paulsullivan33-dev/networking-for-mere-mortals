# DNS

**DNS** (Domain Name System) is the phone book: it translates human
names (`example.com`) into IP addresses (`93.184.216.34`). Almost
nothing you type as a name ever travels the network as a name.

## The lookup, step by step

When you visit `www.example.com`, your computer asks, in order:

1. **Its own cache** — "have I looked this up recently?" (and the
   browser's cache before that)
2. **`/etc/hosts`** — a local file that overrides everything (great
   for testing, dangerous if forgotten)
3. **The configured resolver** — usually your router, which asks
   your ISP's DNS server (or 1.1.1.1 / 8.8.8.8 if you changed it)
4. **Up the chain** — the resolver walks from the root servers down:
   `.` → `com` → `example.com` → `www.example.com`, asking each
   level "who handles the next one?"

The answer comes back with a **TTL** (time to live) — "cache this
for 300 seconds." That's why DNS changes take time to propagate:
the world's caches hold the old answer until its TTL expires.

## Trying it

```bash
getent hosts example.com
```

**Check (typical):** prints the resolved address(es):

```text
93.184.216.34    example.com
```

(`getent hosts` checks the local files *and* DNS, in system order —
it's the honest "what does this machine think this name is.")

For the full story, `dig` (install `dnsutils`/`bind-utils` if
missing):

```bash
dig +short example.com
```

shows just the address. Plain `dig example.com` shows the whole
exchange — query time, which server answered, the TTL. When DNS is
suspect, `dig` is the microscope.

## /etc/hosts: the override file

```text
127.0.0.1       localhost
192.168.1.50    printer.lan
```

Each line maps an address to names. Entries here win over DNS —
useful for giving your home devices stable names (`printer.lan`,
`nas.lan`). **Careful:** a stale or malicious entry here silently
redirects traffic. If a site resolves wrong *only on one machine*,
check this file first.

## DNS failure modes

- **"Can't resolve" but IP works** — DNS is down, network is fine.
  Try `ping 8.8.8.8` (an address needs no DNS): if that works, it's
  DNS. Switch resolvers temporarily to confirm.
- **Wrong answer on one machine** — `/etc/hosts` or a poisoned
  cache. `dig` shows the TTL; suspiciously long TTLs on a fresh
  lookup mean something cached aggressively.
- **Slow lookups** — a dead resolver listed first: every lookup
  waits for it to time out. Check `/etc/resolv.conf` (or your OS's
  network settings) for stale entries.

## A word on DNS privacy

Classic DNS is unencrypted — your ISP (and anyone on the path) sees
every name you look up. **DoH** (DNS over HTTPS) and **DoT** (DNS
over TLS) encrypt it. Browsers increasingly enable DoH by default;
you can also set it at the OS or router level. It hides the *names*
from snoopers, not the *addresses* you then connect to.

**Next:** [Ports and Protocols](ports-and-protocols.md)
