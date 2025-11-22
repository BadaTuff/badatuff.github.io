---
layout: default
title: "Week 01 - Rediscovering Network Tools Through a Security Lens"
parent: Weekly Letters
nav_order: 1
---

# Week 01: Rediscovering Network Tools Through a Security Lens

<img src="/assets/images/Sectools.jpeg" alt="Security Tools" style="width: 100%; max-width: 800px; display: block; margin: 20px auto;">

This first week of studying for these certifications was jam-packed with review. Starting these new certs after already having my Security+ and Network+, I already knew a lot of these concepts, but it's always good to revisit and solidify your understanding. I'm really enjoying both courses, especially the OSCP labs. Getting to actually _do things_ in a Kali Linux environment, probing actual machines, is super fun! The BTL1 cert has me going through the basics, which like I said is lots of review, but I'm happy to spread the knowledge.

I'm currently focusing on getting better at using Kali. I'm still relatively new, so just getting into the groove of moving around in the terminal is exhilarating. I'm learning new commands every day. That's one of the most fun things about working in Linux without a lot of experience: it's not as friendly as Windows when it comes to the UI, but everyone knows you're way more powerful and quick using the terminal. It's what most people move to Linux for: full command and power of their computer. It was frustrating trying to do simple things and continuously finding myself having to look up how to do it (and even then, getting it to work), but with persistence, I keep learning how to figure it out and learn from my mistakes. My main focus this week was just that: getting familiar with the command line and using these commands that will help me protect and ethically attack endpoints.

---

## 🔵 BLUE TEAM

### What I Learned: Netstat, Traceroute, Dig/Nslookup, Nmap

I knew what these commands were before from studying for Network+, but back then I didn't have enough security knowledge to understand why they're so important to security professionals. Now that I have way more understanding of both the blue team and red team sides, I completely get it.

#### Netstat

**What it is:** Netstat is a command-line tool that exists across most operating systems. It allows you to see what ports are open on your device, check routing tables, and view network interface statistics. You can see what executables are using which ports, what TCP and UDP connections are currently open, who they're connected to, and more.

**Why it matters for defense:** When you need to check if your machine is connected to any C2 (Command and Control) servers (meaning malware has established a connection back to an attacker), netstat can save the day. You can verify if all your open ports and connections are legitimate.

You can also use netstat for troubleshooting. For example, if you want to make sure services are running on the correct port, netstat helps you diagnose "connection refused" or "cannot reach" errors.

**Key commands to know:**

- `netstat -a` - Displays all current open ports and their connections
- `netstat -a -b` (Windows) - Shows open ports, connections, AND the executable responsible for each
- `netstat -s -p tcp -f` - Displays all current TCP connections and listening ports with their corresponding executables

**How I'll apply this in a SOC role:** If I see suspicious network traffic corresponding to a specific port on an endpoint, I'll immediately run `netstat -a -b` to identify the executable using that port. From there, I can investigate whether it's legitimate software or malware establishing persistence. For example, if I see an unknown process communicating with an external IP on a non-standard port, that's an immediate red flag for potential C2 communication. I'd pivot to analyzing that executable with tools like VirusTotal or sandboxing it for behavioral analysis.

---

#### Traceroute (Linux) / Tracert (Windows)

**What it is:** These two command-line tools do the same thing. The syntax is just different between Windows and Linux. Traceroute allows you to trace the path a packet takes to reach its destination. It shows you each router hop along the way, which is crucial for troubleshooting network issues.

**Why it matters for defense:** While this command isn't _primarily_ a security tool, it's essential for troubleshooting. Never forget the "A" (Availability) in the CIA triad. You never know when you'll need to get your hands dirty doing network troubleshooting in a professional role.

Let's say whenever you try to access a server, it always comes back slow or sometimes doesn't respond at all. This is where traceroute comes in. You can check where in the route the packet is dropping or getting stalled. Once you identify the problematic hop, you can investigate the root cause and have actionable information on how to fix it.

**How I'll apply this in a SOC role:** If users report slow access to an internal application, I'd run traceroute to identify which hop is causing the latency. If it's an internal router or firewall, I can work with the network team to investigate potential misconfigurations or capacity issues. In a worst-case scenario, if I see traffic routing through unexpected hops (especially external ones for internal-only traffic), that could indicate a routing table poisoning attack or misconfigured BGP routes. Both are serious security issues that need immediate attention.

**Try it yourself:** Run `tracert google.com` and see the route your device takes!

---

#### Dig / Nslookup

**What they are:** Dig and Nslookup are both command-line tools that allow you to query DNS records for domains. These tools are incredibly powerful for gathering information about entities you're not familiar with.

**Why they matter for defense:** There are tons of use cases, but here's a common one: investigating a suspicious domain from a phishing email. With these tools, you can look up the domain's DNS records, like which IP address it points to, what mail servers it uses, and more. This gives you immediate technical indicators of whether an email is legitimate or phishing.

**Key commands to know:**

- `dig [domain name]` - Queries DNS for the A record (IP address)
- `dig [domain name] MX` - Queries for mail (MX) records
- `dig [domain name] ANY +nocomments +noauthority +noadditional +nostats` - Queries for all DNS records without extra clutter

**How I'll apply this in a SOC role:** When investigating a phishing email, I'll use dig to research the sender's domain and any URLs in the email. I can check if the domain's MX records point to free email services (Gmail, Outlook) when the email claims to be from a major corporation. That's a red flag. I'd also look up the IP address the domain resolves to and check its geolocation and reputation. Combined with WHOIS data (see my mistake below), this reconnaissance quickly confirms whether an email campaign is malicious before escalating to deeper analysis.

**The Mistake I Made:** Even though I knew what dig/nslookup were, I honestly thought WHOIS was just a smaller, less useful version of these tools. But while writing this, I asked myself: what's the _actual_ difference between the two? Turns out they give you completely different information! **WHOIS tells you WHO registered the domain, WHEN it was made, and the contact emails for registration.** Dig/nslookup tells you **WHAT the domain points to** (IP addresses, mail servers, DNS records). They answer different questions: WHOIS is "who owns it?" and dig/nslookup is "where does it point?" For some reason, I always thought dig/nslookup gave you the registration info too. Good catch on a weakness in my understanding!

---

#### Nmap

**What it is:** Nmap is one of the most popular cybersecurity tools for both blue teamers and red teamers. This tool is incredibly versatile. It handles host discovery, port scanning, service version detection, and has scriptable automation through NSE (Nmap Scripting Engine) that can check for specific vulnerabilities. I can't cover everything Nmap does in this post, so we'll focus on port scanning and host discovery.

**Why it matters for defense:** Nmap allows you to scan hosts and see what ports they have open. This is typically the _first phase_ of what attackers do when targeting a network. They want to map their attack surface to know what they're working with and how they can get in.

As defenders, we need to run Nmap scans _first_ so we can see what attackers will see and patch up any weaknesses. We should also minimize unnecessary information disclosure through service banners and headers.

**How I'll apply this in a SOC role:** If I'm tasked with hardening our network, I'd run regular Nmap scans to identify security weaknesses. For example, let's say I scan an internal web server and discover it's running an outdated Apache version with known CVEs. I can immediately flag it for patching before an attacker finds it. I'd also look for services that shouldn't be exposed, like Telnet (port 23), SMB with default configs (port 445), or database services directly accessible from the network (MySQL on 3306, PostgreSQL on 5432). All it takes is one hole for an attacker to compromise the entire network.

**Important note:** You can download Nmap at [https://nmap.org/download](https://nmap.org/download) and try running scans on your home network to see what you find. **KEEP IN MIND YOU CAN ONLY SCAN NETWORKS YOU HAVE PERMISSION TO ACCESS.** Scanning without permission is illegal and can land you in serious trouble. **I REPEAT: ONLY SCAN NETWORKS YOU HAVE PERMISSION TO.**

---

#### Feynman Technique (For Those Still New to These Concepts)

- **Netstat:** A tool that allows security professionals to make sure everyone their computer is talking to is safe and legitimate.
- **Traceroute/Tracert:** A tool security professionals use to troubleshoot network problems by tracking how their communication reaches its destination. Think of it like tracking a package. You look at all the stops it takes and figure out which stop causes delays or losses. This lets you choose different routes or contact that location to investigate what's happening.
- **Dig/Nslookup:** A tool that lets security professionals look up where a domain points (IP address, mail servers). Combined with WHOIS (which tells you who owns the domain), you can verify if someone contacting you is legitimate.
- **Nmap:** A tool that shows you what "doors and windows" (ports) are open on computers in a network. Security professionals use it to check their own networks first, so they can close unnecessary entry points before attackers find them.

---

## 🔴 RED TEAM

### What I Learned: Nmap from an Attacker's Perspective

Now let's look at Nmap from a penetration testing point of view. As a blue teamer, Nmap gives you a snapshot of how your network looks to attackers. As a penetration tester, Nmap is your best friend.

**Why the other tools aren't here:** You might notice I didn't cover netstat, traceroute, and dig/nslookup in the red team section. That's because red teamers typically have more specialized tools for those purposes, unless they're doing "living off the land" attacks, where they use built-in system tools to avoid detection. For reconnaissance and post-exploitation, attackers rely on custom scripts, frameworks like Metasploit, or stealthier alternatives. But Nmap? That's essential for every penetration tester.

**The pentester mindset:** Penetration testers are ethical hackers. We think and act just like attackers, but we have permission and do it for the greater good. When we use Nmap, we're looking for misconfigurations or vulnerabilities, searching for the easiest way to break the CIA triad. We want to steal information, modify data, or take down systems to demonstrate impact, except we don't actually go through with it. We stop at proving the attack path is possible, then report it so our clients can fix their problems.

**Real-world scenario:** Let's say I'm penetration testing your company's most important server. My first move is to run Nmap to gather information about what the server does by checking its open ports and identifying the OS. I discover this is a Linux server, and you happen to have port 23 (Telnet) open. Your company is small without a dedicated IT department, so they don't know Telnet has been insecure for years. Just like that, by using Nmap, I've found an easy entry point. Telnet gives me a remote shell, meaning I can send commands to your server remotely as if I were sitting at the keyboard.

This is just a small example of how attackers use Nmap. I'm planning to make a small Nmap demonstration video on my channel showing how to break into a system using Telnet, so stay tuned!

**How I'll apply this in a pentest role:** I'd use Nmap to map out the network I'm attacking, just like a real adversary would, and enumerate the easiest attack vectors first. I'd scan for low-hanging fruit: default credentials, outdated software, unnecessary services, and misconfigured access controls. From there, I'd chain vulnerabilities together to demonstrate maximum impact for my client.

---

#### Feynman Technique (For Those Very New)

**Nmap** is a popular tool attackers use to gather massive amounts of information about a network so they can figure out the easiest way to break in. Security professionals know attackers use this, so they use it on their own networks first. This way, they can reduce the information attackers get back, making it much harder to find vulnerabilities.

---

## 🟣 WHY BOTH PERSPECTIVES MATTER

This week reinforced something important: **the same tools serve different purposes depending on which side of security you're on.**

For blue teamers, these tools help us _defend_. We monitor our own systems, troubleshoot issues, and identify weaknesses before attackers do. For red teamers, tools like Nmap help us _attack_. We map networks, enumerate services, and find vulnerabilities.

The real power comes from understanding both perspectives. When I run Nmap as a defender, I'm not just looking for open ports. I'm thinking like an attacker. What would _I_ target if I were trying to break in? That mindset shift makes me better at defense.

---

## WRAP-UP

This is my first technical blog post, and I'm so excited to share it with the world. I appreciate you reading. I hope you learned a thing or two, or at least enjoyed hearing about my week of learning. Continue to BTuff, and have a great rest of your week!

<iframe width="560" height="315" src="https://www.youtube.com/embed/5XEKw-HNBPM?si=Rw1a6qLYLZLZitWT" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>
