# Ports and Protocols

An IP address finds the *computer*. A **port** finds the *program*
on it. `192.168.1.50:8080` means "the program on .50 that's
listening on port 8080."

## The apartment-building analogy

The IP address is the street address; the port is the apartment
number. One building (computer), many apartments (programs), each
with its own number. Mail (packets) addressed to apartment 80 goes
to the web server; apartment 22 goes to SSH. Two programs can't
occupy the same apartment — "port already allocated" means someone's
already in 8080.

## TCP vs. UDP

The two transport protocols — how packets travel:

| | TCP | UDP |
|---|---|---|
| Delivery | Guaranteed, in order | Best-effort, maybe lost/reordered |
| Setup | Handshake first ("hello, ready?") | Just sends |
| Speed | Slower (acknowledgments) | Faster (no overhead) |
| Used for | Web, email, SSH, files | Video calls, games, DNS, live streams |

**The intuition:** TCP is a phone call — both ends confirm, nothing
is lost. UDP is shouting into a canyon — fast, and if the wind
takes a word, it's gone. Video calls use UDP because a late packet
is worse than a lost one (you'd rather glitch than freeze).

## The ports you'll actually meet

| Port | Service | Notes |
|------|---------|-------|
| 22 | SSH | Remote login |
| 53 | DNS | Name lookups (usually UDP) |
| 80 | HTTP | Unencrypted web |
| 443 | HTTPS | Encrypted web (most traffic today) |
| 25/587 | SMTP | Sending email |
| 3306 | MySQL | Database |
| 5432 | PostgreSQL | Database |
| 8080 | — | The conventional "alternate web" port for dev |

Ports 0–1023 are **privileged** — on Linux/macOS, only root can
listen on them (why dev servers use 8080, not 80).

## Seeing your own ports

```bash
ss -tln
```

**Check (verified shape):**

```text
State  Recv-Q  Send-Q  Local Address:Port  Peer Address:Port  Process
```

`-t` = TCP, `-l` = listening, `-n` = numeric (don't resolve names —
faster and honest). Each line is a program waiting for connections.
If your web server should be on 8080 and it's not listed, the
server isn't running — the network was never the problem.

## Firewalls, in one paragraph

A **firewall** is a bouncer with a list: packets to allowed
port/IP combos get in, the rest don't. Your router has one (that's
why the internet can't reach your laptop's ports uninvited). Your OS
has one too (`ufw` on Ubuntu, Windows Firewall). Opening a port
means adding an allow rule — and every open port is a door, so open
deliberately. More in [Security Basics](security-basics.md).

**Next:** [Your LAN](your-lan.md)
