---
layout: default
title: "Week 02 - Cybersecurity Skills Transfer to the Real World"
parent: Weekly Letters
nav_order: 2
---

# Week 02: Cybersecurity Skills Transfer to the Real World!

This week I went through more review for the Blue Team Level 1 cert and finally made it out of the Security Foundations phase. Next week I'll be getting into the juicy stuff I've been waiting for: phishing analysis! I'm super excited to start that section. I will say though, we covered a lot of terms I already knew from my current certs and school, but reinforcing them never hurts. I do have an amazing story I'd like to share about how I avoided IRL phishing based on my security training! I hope everyone's week has been going great. Let's go ahead and start this week's blog post!

---

## Story Time: The Phishy Man

<img src="/assets/images/realphishy.png" alt="The Phishy Man" style="width: 100%; max-width: 800px; display: block; margin: 20px auto;">

I was working like any other day and I saw a guy (let's call him Mr. Phish). I'd seen this guy before, and I noticed every time I see him, he has some nice new clothes on: a beautiful suit, sharp tie, dazzling glasses, and a glistening watch! A different beautiful outfit every week I see him. This week I asked him, "Hey, I noticed you always have nice clothes on and I always compliment you for it every week. I was curious, if you don't mind me asking, what do you do for a living?"

As I checked him out, the man looks at me in the eyes and smirks. He goes, "I help people just like you become financially successful."

Interestingly enough, I look at him and say, "What do you mean?"

He goes, "Let's just say I'm a financial strategist." He then pulls me closer and says, "There are other buckets to put your money in that the wealthy don't talk about. Let me get your number and I can tell you more."

He hooked me. I was interested in where he was going with this, so I gave him my number and he tells me we'll talk.

Days later, I forget the man ever got my number and that we were supposed to talk. It was early in the morning when it happened and I get pretty busy. All of a sudden in the afternoon I get a call. I look at my phone and to my surprise it's Mr. Phish. I didn't have his number saved at the time because I hadn't gotten a call from him yet. He was the one who took my number. Then I see he left a voicemail saying who he was and saying we NEEDED to talk so he could tell me about his business and how he could possibly get me in to be financially free.

I call him back. Now that I'm in a cleaner state of mind, I get this gut feeling, a feeling I got from being a cybersecurity professional. Is this guy really who he claims to be? Why does he INSIST on me talking to him? It's not like he's getting anything from speaking to me, right?

I call him back. This time when I speak to him, I'm speaking to him in investigation mode. I'm now looking for signs of phishing, and he leads with saying, "Do you know how the Rothschilds grew to own most of New York..." Using the authority persuasion technique attackers use. And I connect it with his nice clothes. That's also part of his authority persuasion technique. I may have fallen into his trap from the start when I validated his clothes and gave him that sense of authority, making me see him as a person with more money, therefore an authority figure. My mind instantly chimed in on it.

We begin speaking and he continues to insist on me coming to his office so we can begin the process, and he promises I'll be financially free in about a year by just simply getting a license. We can talk more about the details when I schedule a meeting with him. I ask more questions to get more info, but he doesn't give more than that. He then begins to say, "If you don't want to, I can help other people. You're lucky to be one of the FEW people that I let in on this because only so many people can get in."

My mind chimes in again. Scarcity, another tactic used by attackers to get a hook on their phishing rod. Little does he know, he's only making me more and more suspicious and confirming that he's an attacker trying to get me into something malicious.

He lastly puts the nail in the coffin when he makes his last few remarks that allowed me to believe beyond a shadow of a doubt he's a threat. He told me he's helped many across North America, specifically Black Americans, and his persistent insistence on me coming showed me he was leveraging more phishing techniques: social proof (he's referencing his large operation with him and his team helping people across North America), liking (he's in a hurry to establish rapport by saying he's helping people LIKE me), and lastly, his persistence trying to get me to commit to a schedule so I'd feel obligated to fulfill my promise even though I feel skeptical. With me being there on his turf, he can use more tactics to get me into something I don't want to do or that won't be good for me. Commitment and consistency is a technique as well. At some point, it didn't feel like he wanted to help me. It was as if he NEEDED me, like I was a client he was trying to persuade.

After confirming all these things, I was 90% sure he was a phish. I tell him I need to think about it and hang up. He proceeds to text his address and website. After some OSINT work, I find people complaining the guy is part of a large pyramid scheme. With just a few simple Google searches of the man's name and his place of work, I was able to find this public data about him that fully confirmed he was a phish. I finished documenting my interaction with him on the same review site about his location and website, putting out there that he tried to get me into the scam operation as well, and to watch out for him. Don't let his fancy clothes fool you.

Isn't it crazy how being a cybersecurity professional can keep you safe? These techniques that I learned studying cybersecurity, specifically phishing analysis, can assist in the real world. They were able to show up and rescue me when I made a bad decision giving the man my number and taking his word at the start about his work life. This really reminds me how much cybersecurity really is just an abstraction of the real world. Be safe out there and watch out for signs of potential real-life phishing attempts like the one Mr. Phish tried to pull on me. When your gut feeling tells you something is off, a lot of the time it is in situations like these.

---

## Technical Terms I Reinforced This Week!

Like I said above, I knew all of these terms already, but reinforcing them and teaching them doesn't hurt. Check out the YouTube video where I'm gonna be doing a pop quiz on these terms to help my mastery by teaching and giving you, the viewer, maybe a different view on the term or some new knowledge!

### 1. SIEM (Security Information & Event Management)

This is where SOC analysts spend most of their time. This is where most, if not all, assets inside the org send their logs. These can range from application layer logs sent from WAF (Web Application Firewalls, which are basically a wall in front of a web application that chooses what's allowed in and out. The goal is to not allow malicious stuff in or out) or EDR agents (which are agents that basically spy on endpoints and report if they're doing potentially malicious activity). Anything that generates logs can most often be hooked up to a SIEM. This gives security analysts full visibility on what their endpoints are doing and allows for investigation in the case of potential security incidents, which the SIEM flags for analysts to review based on how it's configured.

**Simple terms:** A SIEM is what all the endpoints in a network report to so it can write it down, organize it, review it, and flag it if it's malicious so the cybersecurity pros can investigate.

---

### 2. HIDS/HIPS (Host Intrusion Detection/Prevention Systems)

Host Intrusion Detection Systems (HIDS) are software installed on endpoints checking to see if there's anything malicious going on. If so, it flags it for analysts to review. It does this by using simple rules like "if a user is encrypting files, flag it!"

Host Intrusion Prevention Systems (HIPS) do the same thing as HIDS but actually detect AND prevent whatever is flagged based on the simple rules laid out!

**Simple terms:** Host intrusion detection and prevention systems are spies installed on computers that detect and prevent bad activity from being done on endpoints based on simple rules. Like "if this computer is trying to send stuff outside of our network, flag it" (what HIDS does) or "flag and prevent it" (what HIPS does).

---

### 3. EDR (Endpoint Detection & Response)

Endpoint Detection and Response (EDR) is a solution that centralizes and collects very deep, detailed information about endpoints and what they're doing via EDR agents installed on each endpoint. These agents send as much data about what the endpoint is doing as possible. It completely spies on the endpoint it's installed on. Each endpoint gets its own local agent that sends every bit of information it collects to the centralized EDR console, which takes the information, saves it all in case it needs to be investigated later, and correlates all the security data across every endpoint in a network, searching for anything that could be malicious. In the case that things are flagged as malicious, it will flag that process and can isolate all the infected machines and prevent the spread of malicious activity, as well as proactively block things that are suspicious and out of the ordinary of the endpoint's normal behavior. It uses machine learning to understand normal behavior from suspicious behavior.

**Simple terms:** Endpoint Detection and Response (EDR) is a cybersecurity solution that has detectives on every machine spying on them and reporting what they're doing to a central brain that takes the information, saves it in case they need to investigate it later, and reviews it, checking for weird behavior on the computers. In the case that it does find something, it can flag and potentially block all the associated computers exhibiting weird behavior.

**I had these questions, so in case you do, I want to share what I found:**

**What's the difference between EDR and a SIEM?** I was wondering this because it seems they both collect data, organize it, and correlate it, so how do you know when to use one or the other?

I found that EDR has much deeper analysis for endpoints as it saves very specific actions endpoints are doing at a granular level, and EDR can take action when it comes to endpoints. Then I thought, so why would people use SIEMs? Well, I found that:

1. Not every device can have an EDR agent, like network devices
2. Not all devices support EDR. SIEMs are a lot more adaptable and can take logs from most IT assets, and they're easy to set up
3. It's actually best to have EDR hooked up to the SIEM so the SIEM can get high-level info about the endpoints from another vector. In case the computer goes down, there's not a single point of failure. If the direct connection from the endpoint to the SIEM goes down, we can look at EDR and still see what happened on the endpoint.

There are even more benefits to having EDR hooked up to the SIEM.

**What are the key differences between HIDS/HIPS and EDR?**

- EDR has a memory of what ALL the endpoints are doing, while HIDS/HIPS doesn't have much of a memory at all. It will only have a memory of the few events related to what was flagged
- HIPS/HIDS blocks based on simple rules and has no correlation, unlike EDR, which can take information from a bunch of different endpoints and correlate it to one attack
- EDR has access to all endpoints with agents on them. HIPS/HIDS only uses and acts on information from the one endpoint it's installed on locally
- Overall, EDR is just way more sophisticated and has a lot more visibility and power than HIPS/HIDS. Think of EDR as HIPS/HIDS on steroids.

---

### 4. Risk Management Framework

This is where you prioritize risk that causes the most impact. You can figure out if something is risky by checking if there are ANY vulnerabilities attached to it, and if so, are there threats that correspond to that vulnerability? It can be anything. All humans and hardware have vulnerabilities to nature. A human will typically have a low chance of defeating a hurricane and fighting it off by themselves. Using this analogy, I'm just trying to say everything typically has some form of risk, even if it's very low.

To figure out what to prioritize, use a risk calculation: **Impact x Likelihood**. Once you determine there's risk by checking if there's a vulnerability and a threat worth noting, check the impact and likelihood, and that will tell you what to prioritize when managing risk. What's most important to address and what proactive and reactive measures to make.

For example, if you have an old computer that's internet-facing with a vulnerable operating system and vulnerable services running on it, the likelihood of that getting compromised over time is probably 5 out of 5 because attackers scan the internet all the time looking for ways in. The impact can be catastrophic if that computer has or has access to important business operations, so that's also a 5 out of 5. The likelihood is 5 and the impact is 5, giving a risk score of 25 (the highest possible on a standard 1-5 scale). That should be one of the first things prioritized and addressed.

Once you determine you want to address risk, you can do one of four things to manage it:

- **Risk Acceptance:** Accepting the risk and not doing anything about it, maybe because it's not that impactful or worth the money to the organization to fix it
- **Risk Avoidance:** Getting rid of everything so you don't have to worry about the risk. This is the best for completely eliminating risk, but then you probably have to replace the asset
- **Risk Mitigation:** The most common type of risk management, where you find ways to make the risk level lower by making the likelihood lower or the impact lower
- **Risk Transference:** This is where you transfer risk to another entity by using things like cybersecurity insurance

**Simple terms:** You can check how much of a risk something poses by looking at if there are weaknesses in an asset and if there are threats that can take advantage of this weakness. If you find there's a risk to an asset worth noting, you can determine how risky it is by looking at how likely it is to be taken advantage of and how big of an impact it can leave on the organization.

---

### 5. Vulnerability Scanning (External vs. Internal)

Vulnerability scanning is basically automated security testing that looks for known weaknesses in your systems. Here's the thing, there are two main types, and understanding the difference is important for blue team work.

**External vulnerability scanning** is when you scan your network from the outside, like an attacker would. You're checking what a hacker on the internet can see and potentially exploit. This includes things like open ports, outdated web applications, misconfigured services, anything exposed to the public internet.

**Internal vulnerability scanning** happens from inside the network. This shows you what an attacker could access if they already got a foothold inside, or what a malicious insider could exploit.

Both are critical for a complete security posture. External scans show your attack surface from the internet, while internal scans show your lateral movement risks if someone gets inside.

**Simple terms:** Vulnerability scanning is like running a security checklist on your computers to find weaknesses. External scanning checks what hackers on the internet can see and attack from the outside. Internal scanning checks what threats exist inside your network if someone already got in or if an employee went rogue.

---

### 6. NIDS/NIPS (Network Intrusion Detection/Prevention Systems)

Network Intrusion Detection Systems (NIDS) monitor network traffic looking for suspicious activity or known attack patterns. They sit on your network and analyze packets flowing through, basically watching all the conversations happening between devices.

Network Intrusion Prevention Systems (NIPS) do everything NIDS does but can also actively block threats. When they detect malicious traffic, they can drop those packets, block that IP address, or reset the connection.

The key difference from HIDS/HIPS? Those monitor individual computers. NIDS/NIPS monitor the entire network, watching traffic between systems.

**Simple terms:** NIDS watches all the traffic flowing through your network looking for attacks, like a security camera system for network data. NIPS does the same thing but can also block the bad traffic it finds.

---

### 7. Data Loss Prevention (DLP)

Data Loss Prevention (DLP) is basically a security control that prevents sensitive data from leaving your organization, whether accidentally or maliciously. It monitors data in three states: data at rest (stored files), data in motion (being transferred over networks), and data in use (being accessed or modified by users).

DLP solutions use rules and patterns to identify sensitive information like credit card numbers, Social Security numbers, medical records, intellectual property, or confidential business documents.

**Simple terms:** DLP is like a security guard for your data that makes sure sensitive information doesn't leave the company. It watches when people try to email confidential files, copy them to USB drives, or upload them anywhere outside the network.

---

### 8. Security Awareness Training

Security Awareness Training is honestly one of the most underrated security controls. It's basically teaching employees how to recognize and respond to security threats. Users are often the weakest link in security.

Good security awareness training covers things like:

- Recognizing phishing emails (literally what saved me from Mr. Phish!)
- Creating strong passwords and using password managers
- Identifying social engineering attempts
- Reporting suspicious activity
- Understanding why security policies exist
- Safe browsing habits and avoiding malicious downloads

Little did I know how much this would apply to real-world situations outside of work until I encountered Mr. Phish. The same red flags I learned to spot in email phishing showed up in his in-person pitch.

**Simple terms:** Security Awareness Training teaches employees how to spot and avoid cyber threats like phishing emails, scams, and social engineering tricks. It turns users from the weakest link into an extra layer of defense.

---

### 9. AAA Controls (Authentication, Authorization, Accountability)

AAA is basically the foundation of access control in cybersecurity. It's three core principles that work together to secure systems and track what users are doing.

**Authentication** is proving you are who you say you are. The question it answers is "Who are you?"

**Authorization** is determining what you're allowed to access after you've been authenticated. The question it answers is "What are you allowed to do?"

**Accountability** is logging and tracking what users actually do with their access. The question it answers is "What did you do and when?"

**Simple terms:** AAA Controls are three security principles working together. Authentication proves you are who you say you are, Authorization determines what you're allowed to access, and Accountability tracks what you actually did.

---

### 10. Patch Management (WSUS/SCCM)

Patch Management is the process of keeping all your systems updated with the latest security patches and software updates. Vulnerabilities get discovered all the time, and vendors release patches to fix them.

**WSUS (Windows Server Update Services)** is Microsoft's free tool that lets you centrally manage Windows updates across your organization.

**SCCM (System Center Configuration Manager)**, now called Microsoft Endpoint Configuration Manager, is a much more powerful enterprise tool that handles not just Windows updates but also third-party application patching, OS deployments, and more.

**Simple terms:** Patch Management is keeping all your computers and systems updated with security fixes. WSUS and SCCM are tools that help you control when and how computers in your organization get updates.

---

## Wrap-Up

I hope you enjoyed week 2 of the weekly letters documenting my journey breaking into cybersecurity! I appreciate you reading, have a great Thanksgiving, and never forget to BTuff!

<iframe width="560" height="315" src="https://www.youtube.com/embed/6m0EiJ5yPzk?si=Z5PSVszRPq_EoG4z" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>
