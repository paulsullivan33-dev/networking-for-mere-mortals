# Security Basics

You don't need to be a security expert to avoid the common
disasters. You need five habits.

## 1. Know what's exposed

Every listening port is a door. Check yours:

```bash
ss -tln
```

If you don't recognize a listening port, find out what it is before
ignoring it. On the internet-facing side, your router's firewall
blocks unsolicited inbound by default — **don't put devices in the
DMZ or enable UPnP port mapping without understanding it**, or that
protection quietly evaporates. (UPnP lets programs open their own
inbound ports — convenient, and malware's favorite feature.)

## 2. The firewall is on for a reason

- **Router firewall:** leave it on. It's what stands between your
  laptop's ports and the entire internet.
- **Host firewall:** Ubuntu's `ufw`, Windows Firewall — leave them
  on too, and open only what you need:

```bash
sudo ufw allow 22/tcp    # SSH in
sudo ufw enable          # turn it on (careful: do this over console, not SSH, the first time)
```

**Careful:** Enabling a firewall over SSH *before* allowing SSH
locks you out. Allow your access first, enable second. (Everyone
learns this once. Learn it from reading, not doing.)

## 3. SSH: keys, not passwords

Password SSH on a public port gets brute-forced within minutes —
it's background noise on the internet. The fix:

- Key-based auth only (`PasswordAuthentication no` in
  `sshd_config`), non-standard port optional (obscurity, not
  security, but it quiets the logs).
- Or don't expose SSH at all — use a VPN.

## 4. Update the things that face the internet

The service you exposed *will* be probed. "Set and forget" is how
home servers join botnets. If you port-forward something, you own
its updates — check monthly, automate where you can (`unattended-upgrades`
on Debian/Ubuntu for security patches).

## 5. Think in layers, not silver bullets

No single measure saves you: strong passwords *and* firewall *and*
updates *and* minimal exposure. The goal isn't invincibility — it's
being more trouble than the next target. Automated attacks take the
easy wins; don't be one.

## What about antivirus / VPN ads?

- **Antivirus:** Windows Defender (built in) is competent; macOS and
  Linux need less by design. The biggest malware vector is *you*
  running something — no scanner fixes that.
- **Commercial VPNs:** they hide your traffic from your ISP and
  change your apparent location. They don't make you anonymous
  (the VPN provider sees everything instead) and they don't replace
  any habit above. Useful for untrusted WiFi; not a security
  strategy by itself.

**Next:** [Troubleshooting](troubleshooting.md)
