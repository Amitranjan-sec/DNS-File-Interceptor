# DNS File Interceptor

A Python-based network traffic interception and file-replacement tool built for isolated ethical hacking and network security lab testing. It uses `NetfilterQueue`, `Scapy`, and `iptables` to intercept queued packets, inspect HTTP/DNS traffic for target file downloads, and redirect or serve a substitute file from a local web server in a controlled lab environment.

> **Disclaimer:** For authorized educational testing and isolated home-lab environments only. Do not run packet-interception or spoofing tools on networks you do not own or have explicit permission to test.

## How It Works

1. **Traffic Redirection (`iptables`):** Routes intercepted packets through a user-space queue (`NFQUEUE`) so a Python script can inspect and modify them before forwarding.
2. **Packet Inspection (`Scapy` & `NetfilterQueue`):** Captures packets from the queue, parses headers/payloads, and matches target domain or file-download requests (such as plain HTTP endpoints like `http://neverssl.com` or local Apache2 test pages).
3. **Response Modification & File Substitution:** Modifies or injects responses so the client retrieves the designated lab file instead of the original payload, updating packet fields and recalculating checksums before releasing the packet.

## Lab Environment & Tech Stack

- **Attacker / Interceptor OS:** Kali Linux (VMware)
- **Target Client OS:** Windows 10 (VMware)
- **Local Web Server:** Apache2 (hosting replacement test files)
- **Language & Libraries:** Python 3, `scapy`, `netfilterqueue`
- **Firewall / Packet Queuing:** `iptables` (`NFQUEUE`)

## Prerequisites

1. Run on a Linux system (such as Kali Linux) with root privileges.
2. Install required Python packages:
   ```bash
   pip install scapy netfilterqueue
