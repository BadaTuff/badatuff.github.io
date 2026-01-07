---
layout: default
title: "Week 05 - I Scanned My Home Network and Found More Than I Expected"
parent: Weekly Letters
nav_order: 5
---

# Week 05: I Scanned My Home Network and Found More Than I Expected

This week I took a break from BTL1 modules to do something I've been wanting to do for a while: actually secure my home network. Not just read about network security, but get my hands dirty with it. Scan my own network, find vulnerabilities, and fix them.

Here's the thing. I've been studying all this security stuff for months now. Network+, Security+, BTL1. But there's a difference between knowing what a vulnerability scan is and actually running one on your own network and seeing real results. This week I closed that gap.

**Merry Christmas to everyone reading this!** I hope you all had a great holiday. Let's dive into what I learned securing my home network.

---

## 🔵 What I Did

I ran a full nmap scan on my home network with service detection and vulnerability scripts:

```bash
sudo nmap -sV -sC --script=vuln [network range]
```

I expected maybe 10 to 15 devices. I found over 20.

Smart TVs, printers, phones, tablets, IoT devices, gaming consoles, my lab equipment. All sitting on one flat network where everything could talk to everything. My kids' tablets on the same network as my server. My smart doorbell on the same network as my work PC. Not ideal.

The scan also found actual vulnerabilities on my printers:

**Slowloris DoS (CVE-2007-6750):** This is a denial of service attack that holds many connections open to a web server by sending partial requests. It starves the server of resources until legitimate users can't connect. Low bandwidth, high impact.

**CSRF (Cross-Site Request Forgery):** This means an attacker could trick your browser into making requests to the printer's web interface without your knowledge. You visit a malicious site, and it silently changes your printer settings or resets it to factory defaults. No authentication required.

**JetDirect exposed:** JetDirect is a protocol that sends raw print data directly to the printer on port 9100. No authentication, no encryption. Anyone on the network who can reach it can print, waste resources, or potentially exploit vulnerabilities. It's like a mail slot with no lock. Anyone who can reach it can shove stuff through.

Now, JetDirect isn't exposed to the internet. An attacker outside my network can't reach it. But what if something inside my network gets compromised? A sketchy app on a smart TV, malware on a kid's tablet? That's why I needed to lock it down.

---

## The ASUS Router

I went to Microcenter and picked up an ASUS router. My T-Mobile gateway is limited in what it lets you configure, so I put my own router in front of it to handle security controls. The gateway just provides internet now.

Little did I know how much security functionality is baked into modern ASUS routers. It's like a mini SOC in a box:

- **Router Security Assessment:** Scans for vulnerabilities and tells you what to fix
- **Malicious Sites Blocking:** Blocks malware, phishing, spam, adware, ransomware
- **Two-Way IPS:** Protects against DDoS, blocks attacks like Shellshock and Heartbleed, detects suspicious outgoing traffic from infected devices
- **Infected Device Prevention:** Stops devices from being enslaved by botnets
- **Auto Firmware Upgrades:** Automatically downloads and installs security updates
- **VPN server built in**
- **DNSSEC support**
- **Ad blocking and content filtering**
- **Traffic analyzer with alerting**
- **QoS controls**

All the stuff I learned studying for Network+? QoS, VLANs, firewall rules, DNS? I was actually configuring it for real. Super cool to see that theoretical knowledge translate to something practical.

---

## Network Segmentation

I set up four separate networks:

| Network | Purpose | Access |
|---------|---------|--------|
| Professional | Work PC, server, lab equipment | Internet, isolated from other segments |
| Kids | Their tablets, phones, gaming stuff | Internet only, isolated |
| IoT | Smart TVs, cameras, smart home devices, printers | Internet only, isolated |
| Guest | Visitors | Internet only, isolated |

**What "Internet only, isolated" means:** Devices can reach the internet (browse, stream, download updates), but they cannot see or communicate with devices on other network segments. A smart TV on the IoT network can stream Netflix, but it cannot see my server. A kid's tablet can browse the web, but it cannot access my work PC or files.

The principle is simple: each network segment can only access what it needs. A compromised smart TV can't pivot to my server. A kid downloading a sketchy game can't accidentally infect my work machine. Containment.

---

## Fixing the Printer Vulnerabilities

Both printers had vulnerabilities, but I couldn't just ignore them. People still need to print. Here's the solution I came up with:

### 1. Moved printers to IoT network with static IPs
Static IPs are important because firewall rules and access controls need a consistent address to work.

### 2. Set up an old laptop as a dedicated print station
This laptop sits on the IoT network and has no sensitive data on it. Nothing to steal if it gets compromised.

### 3. Configured ACL on each printer
Access Control List in the printer's web interface. Only the print laptop's IP address can connect. No other device can talk to the printers, even if they're on the same network.

### 4. Configured Windows Firewall on the laptop
Blocked the printers from initiating any inbound connections to the laptop. The laptop can send print jobs out, but the printers can't connect back in.

### 5. Updated firmware where possible
One printer had a firmware update available that patched the Slowloris vulnerability. The other printer is older with no update available, so I accepted the residual risk knowing it's fully isolated.

**When someone needs to print, they walk over to the laptop.**

Less convenient? Yes. Way more secure? Also yes. That's the real-world tradeoff.

### Why this works (defense in depth):

1. Printers isolated on IoT network (can't reach Professional or Kids networks)
2. Only ONE device can communicate with printers (ACL)
3. That device has no sensitive data (nothing to steal)
4. Printers can't initiate connections (can't phone home if compromised)

An attacker would have to compromise something on IoT, then somehow reach the printer (blocked by ACL), then attack the laptop (blocked by firewall), and find nothing valuable anyway. That's layers of defense.

---

## OPSEC Observations

Something interesting from the scan: device hostnames exposed personal information. I could see names of people in my household and even which rooms devices were in through the hostnames.

An attacker who got this scan would learn a lot about my home layout. Renamed devices to generic identifiers. Another reason segmentation matters. A compromised IoT device can't even run this scan against my other networks.

---

## 🚧 The Challenge

**What tripped me up:** The T-Mobile gateway really doesn't play nice with adding your own router. Slow speeds, the mesh extender becomes useless since it wants to pair with the gateway directly, and double NAT issues. It's clearly built to be an all-in-one solution.

**How I'm handling it:** Still figuring out the best setup. The speeds take a hit, though latency is fine. Sometimes the "perfect" security setup isn't practical and you have to adapt. That's a lesson in itself. You work with what you have.

---

## 💡 Quick Wins

1. **Scan your own network.** You probably have more devices than you think. A basic nmap scan will show you what's exposed.
2. **Printers are a problem.** They're often forgotten, running outdated firmware, with web interfaces and services wide open. Check yours.
3. **Segment if you can.** Even basic guest network isolation is better than everything on one flat network.
4. **Static IPs for devices you're managing.** Firewall rules need consistent addresses.
5. **Check for default credentials.** Routers, printers, IoT devices. You'd be surprised how many are still set to factory defaults.
6. **Hostnames leak info.** Rename devices to generic identifiers.

---

## What's Next

This is just the beginning of my home lab.

**Pi-hole:** DNS-level ad and tracker blocking on my Raspberry Pi. All devices use it as their DNS server. It blocks ads and malware domains before they even load, and logs every DNS request so I can see exactly what my devices are trying to reach. Great for catching suspicious activity. Setup is easy, about 30 minutes.

**Network monitoring:** Looking at Wazuh (free, open source SIEM) or simpler tools like ntopng for traffic analysis. Goal is to see traffic patterns, get alerts on anomalies, and have logs to investigate if something goes wrong. Turns my home lab into a mini SOC training environment.

More content coming soon.

---

## Wrap-Up

Week 05 was all about taking the theoretical knowledge from Network+ and Security+ and applying it to real-world network security. Scanning my home network revealed vulnerabilities I didn't expect, and fixing them required actual defense-in-depth strategies: segmentation, ACLs, firewall rules, and accepting practical tradeoffs. This is what security looks like in practice. It's messy, it requires compromises, and it's never truly "done." But that's exactly why I love it. Keep securing, stay vigilant, and never forget to BTuff!

---

<iframe width="560" height="315" src="https://www.youtube.com/embed/snTbIbEJWoI?si=O3_8Nohc7lXcJWYv" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

---

*Published: December 26, 2025*
