# What Networking Is

**The one-sentence version:** Networking is computers exchanging
**packets** — small, addressed chunks of data — over shared
infrastructure, following agreed rules (**protocols**).

## The postal analogy (it actually holds up)

| Postal system | Network |
|---------------|---------|
| Letter | Packet |
| Envelope address | IP address (who it's for / from) |
| "Fragile / Express" markings | Protocol headers (how to handle it) |
| Post offices sorting mail | Routers forwarding packets |
| ZIP codes | Subnets (which neighborhood) |
| Phone book | DNS (names → addresses) |

A packet, like a letter, carries two things: the **payload** (your
data) and the **headers** (source address, destination address,
handling instructions). Routers read the headers and pass the packet
along, never needing to understand the payload. That's the whole
trick that lets one infrastructure carry web pages, video calls, and
game traffic simultaneously.

## The big ideas, up front

1. **Everything is best-effort.** The network promises to *try* to
   deliver each packet. Packets can be lost, duplicated, or arrive
   out of order — reliability is built *on top* (that's TCP's job),
   not assumed underneath.
2. **Layers.** Networking is described in layers, each handling one
   concern: the physical wire, addressing, reliable delivery, the
   application. You don't need the 7-layer OSI model memorized —
   you need the instinct that "which layer is broken?" narrows every
   problem.
3. **Dumb network, smart ends.** The internet's core just forwards
   packets. The intelligence (encryption, reliability, ordering)
   lives in the computers at the ends. This is why innovation
   happens at the edges — nobody had to upgrade "the internet" to
   invent video calling.

## What a "connection" really is

When your browser "connects" to a website, no wire is dedicated to
you. Your computer and the server just agree to exchange numbered
packets and keep track. Thousands of such "connections" share the
same wires, interleaved packet by packet. It's less like a phone
call, more like two people passing notes in a crowded room and
numbering them so nothing gets lost.

**Next:** [IP Addresses](ip-addresses.md)
