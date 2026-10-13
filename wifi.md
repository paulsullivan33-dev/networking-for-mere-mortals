# WiFi

WiFi is just your LAN over radio instead of cable — same IP
addresses, same protocols, new physical quirks.

## The basics

- **SSID** — the network's name ("HomeNet"). It's a label, not
  security — hiding it (not broadcasting) stops casual browsers but
  not anyone trying.
- **Bands** — 2.4 GHz travels farther and through walls better;
  5 GHz (and 6 GHz / WiFi 6E) is faster but shorter-range. One SSID
  can span both; your device picks.
- **Standards** — WiFi 5 (802.11ac), WiFi 6 (802.11ax), WiFi 7
  (802.11be). Newer = faster and better at crowded airspace, but
  both ends need to support it to benefit.

## Security: the part that matters

| Mode | Verdict |
|------|---------|
| Open (none) | Anyone can join and snoop. Never for home. |
| WEP | Broken since 2001. Only on ancient gear — replace the gear. |
| WPA2 | Fine. The long-standing default. |
| WPA3 | Better (stronger handshake, protects weak passwords). Use if everything supports it. |

Use **WPA2 or WPA3 with a strong password**. The password isn't
just for keeping neighbors off your Netflix — on WiFi, the
encryption key derives from it, so a weak password lets anyone in
radio range decrypt your traffic.

**Guest network:** most routers offer one — isolated from your LAN
by design. Guests (and IoT gadgets you don't quite trust) go there;
they get internet but can't see your computers. Use it.

## Why WiFi is weird (the honest physics)

- **Half-duplex-ish.** WiFi radios generally can't talk and listen
  simultaneously on one channel — devices take turns. More devices =
  more waiting, which is why a crowded café crawls.
- **Interference is real.** Microwaves, baby monitors, Bluetooth,
  and your neighbor's router all share 2.4 GHz. If WiFi dies every
  day at 6pm, look for a pattern (the microwave dinner theory is a
  cliché because it's often true).
- **Speed drops with distance and walls.** The "up to 1200 Mbps" on
  the box is a lab number at close range. Through two walls, expect
  a fraction — that's physics, not a defect.

## WiFi troubleshooting, ranked

1. **Move closer.** If it's fast next to the router, it's range,
   not the internet.
2. **Check the band.** Stuck on 2.4 GHz in a crowded apartment?
   Try forcing 5 GHz (or split the SSIDs so you can choose).
3. **Change the channel.** Router admin → wireless settings →
   pick a less crowded channel (apps like WiFi Analyzer show the
   crowd). Auto-channel usually works; sometimes it doesn't.
4. **Reboot the router.** Cliché because it works — clears stuck
   DHCP leases and wedged radios.
5. **Test wired.** Plug in a cable: fast now? It's the WiFi. Still
   slow? It's the internet connection (or the router itself).

**Next:** [The Path to the Internet](internet-path.md)
