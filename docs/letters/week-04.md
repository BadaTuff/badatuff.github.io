---
layout: default
title: "Week 04 - From Suspicious Email to Verdict: My Phishing Analysis Workflow"
parent: Weekly Letters
nav_order: 4
---

# Week 04: From Suspicious Email to Verdict: My Phishing Analysis Workflow

<img src="/assets/images/Phishing_Analysis_Workflow.png" alt="Phishing Analysis Workflow" style="width: 100%; max-width: 800px; display: block; margin: 20px auto;">

Last week I covered phishing red flags and how to spot a suspicious email. This week I learned what happens next: the actual investigation workflow. How do you go from "this looks phishy" to "this is confirmed malicious, here's the evidence"? Let's dive into the systematic process SOC analysts use to investigate phishing emails from initial triage to final verdict!

---

## 🔵 What I Learned This Week

### The Artifact Collection Process

Artifacts. The pieces that bring together the full story of an email. These are what allow SOC analysts to determine whether or not an email is malicious. There are a few types: email artifacts, web artifacts, and file artifacts. All of these make the email pie whole in determining whether to mark an email malicious or legitimate. They're important because they give the direct reasons why an analyst would classify something as malicious or benign.

**The artifacts:**
- **Email artifacts:** Sending address, subject line, recipient(s), sender IP, reply-to address, date/time
- **Web artifacts:** Full URLs, root domains
- **File artifacts:** Filename, extension, SHA256 hash

I love using Sublime Text, a free text editor, for analyzing emails. It has great extensions you can download to help with manual analysis and it allows you to truly get the big picture of a .eml file (a downloaded version of the email including all the headers needed for analysis). Just by opening Sublime Text, a lot of the time you can collect all the artifacts you need to make a verdict. But if things are trickier, you can move into sandboxing and viewing web and file artifacts, which is even more interesting. Watching how potentially malicious artifacts behave from a distance is key.

**Never run anything that could be malicious on a machine that isn't isolated and dedicated to sandboxing.** You don't want to make any hackers happy. When you run a malicious file like a malDoc, you could be doing exactly what an attacker wants and completely allow them into your network. That's the opposite of why we're analyzing the email in the first place!

I learned how to use many cool tools for analysis: a few PowerShell commands, lots of browser tools, and even automation to make the job super quick and easy. I'm going to be sharing them today, so stick around to the end of the letter!

**How this applies to SOC work:**
I learned exactly how to analyze and triage phishing emails. I created an SOP for how I'd work through investigating a phishing email, and I'll continue to improve it as I learn more. (Check out the SOP below!)

---

### SPF, DKIM, and DMARC (The Email Authentication Trio)

Sender Policy Framework (SPF), DomainKeys Identified Mail (DKIM), and Domain-based Message Authentication, Reporting and Conformance (DMARC). I like to call these the Big 3 email authentication protocols. Together, they thwart most spoofing attempts and phishing campaigns by defining who can send emails for a domain, proving the email actually came from that sender, and specifying what to do with emails that fail authentication. With all three working together, it's way harder for attackers to lie about being a legitimate sender. Though attackers still find ways around this with things like typosquatted domains and Business Email Compromise (BEC).

**Breaking it down:**
- **SPF:** A record people can look up to verify the IDs of senders who claim to be from a certain organization. If you show your ID and you're not on the list of authorized senders, you fail.
- **DKIM:** The magic signature that proves the sending server wrote the contents of the email and it wasn't changed in transit. Think of it like this: the domain owner has a special pen that creates unique signatures. They also publish a key anyone can use to verify those signatures. If the key can verify the signature and the email content matches (using hashing), you know the email hasn't been tampered with and came from the right place.
- **DMARC:** This tells receivers what to do with emails that fail SPF or DKIM checks. Options are: reject them, let them in but keep an eye on them (quarantine), or let them in anyway scot-free.

**How this applies to SOC work:**
One of the first things I'd check when analyzing a phishing email as a SOC analyst is whether the email passed the Big 3 checks. More often than not, if they failed, the email probably wouldn't have even made it to the inbox since it's bad practice to let emails like that through. But if they did find a way in, that's a major red flag and IOC.

---

### Reputation Tools and Sandboxing

I learned lots of new tools for reputation checks on artifacts as well as sandboxing. These tools are amazing for checking whether other people have flagged suspected artifacts as malicious, and for checking yourself if things look out of the ordinary. Sometimes if an attack is targeted or brand new, you won't get flags from reputation checks. That's why I love the "guilty until proven innocent" mentality. You must assume the email and its contents are malicious until you have concrete evidence it's legitimate.

**A few tools I learned (you can find the rest in the SOP):**
- **VirusTotal / URLScan:** These tools let you do reputation checks on URLs, IP addresses, file hashes, and more. Super useful for getting quick indicators on whether an email is malicious. But don't blindly trust the results since sometimes they can flag things as safe even when they're not.
- **Hybrid Analysis:** A free malware sandboxing tool! It does static and dynamic analysis, giving you tons of information about how a file behaved and whether it was acting maliciously. Super useful for quick sandboxed analysis, especially if you haven't gotten much from simple reputation checks.
- **PhishTool:** A powerhouse phishing automation tool. All you need to do is submit an email file and it will auto-collect artifacts, give you functions for quickly analyzing them, estimate whether the email is malicious, and save tons of time. The console is sort of an all-in-one interface. But never rely on just one tool!

**How this applies to SOC work:**
If I were in a SOC analyst role, I would use tools like PhishTool to save time, and depending on the scenario, use other tools to determine whether a phishing email is malicious. Always keep the "guilty until proven innocent" mindset.

---

## 🚧 The Challenge

**What tripped me up:**
Honestly, the concepts this week clicked pretty fast. The hardest part wasn't understanding the workflow. It was keeping track of all the different artifacts and tools. There's a lot to remember: email artifacts, web artifacts, file artifacts, reputation tools, sandboxing tools, authentication checks. It adds up quick.

**How I worked through it:**
This is exactly why I built the SOP. Instead of trying to memorize everything, I documented the entire workflow step by step. Now I have a reference I can follow every time, and I'll keep improving it as I learn more. Building documentation while learning is a habit I want to carry into my SOC career.

---

## 🎯 My Phishing Analysis Playbook

Here's the workflow I'd use on day one as a SOC analyst when a user reports a suspicious email. I'd follow the SOP I created. Here's a high-level overview:

**Step 1: Collect Artifacts**
Round up the important artifacts and look for low-hanging fruit that will tell you if the email is malicious:
- Domain spoofing?
- SPF/DKIM/DMARC failure?
- Body content suspicious? (Bad grammar, generic speech, poor styling, manipulation tactics)
- Reply-To address differ from From address?

**Step 2: Analyze Artifacts Deeper**
- Analyze sender IP address using WHOIS queries and reputation checks
- Submit hashes and URLs to reputation checkers
- Use screenshot tools to view web artifacts safely (check root domain and full paths)
- Sandbox file artifacts for static and dynamic analysis

**Step 3: Make the Call & Document**
- Record all artifacts in your report
- Write down your verdict with justification
- Take preventative and reactive measures if needed
- Document those measures too!

---

## 📋 My Phishing Analysis Investigation SOP

I created a comprehensive Standard Operating Procedure documenting the entire phishing investigation workflow. This is a living document I'll continue to refine as I learn more, but it covers everything from initial triage to report writing.

**What's inside:**
- Safety requirements for analyzing phishing emails
- Phase-by-phase investigation workflow
- Artifact collection checklists
- Analysis techniques for senders, URLs, and files
- Verdict determination criteria
- Defensive actions checklist
- Professional report writing template
- Tool reference guide

<div style="margin: 30px 0; padding: 20px; border: 2px solid #0366d6; border-radius: 8px; background-color: #f6f8fa;">
  <h3 style="margin-top: 0;">📄 View the Full SOP</h3>
  <p>You can view the complete SOP below or download the PDF for offline reference:</p>

  <iframe src="/assets/documents/Phishing_Analysis_Investigation_SOP.pdf"
          width="100%"
          height="800px"
          style="border: 1px solid #ddd; margin: 15px 0;">
    Your browser does not support PDFs.
    <a href="/assets/documents/Phishing_Analysis_Investigation_SOP.pdf">Download the PDF</a> instead.
  </iframe>

  <p style="margin-bottom: 0;">
    <a href="/assets/documents/Phishing_Analysis_Investigation_SOP.pdf" download style="display: inline-block; padding: 10px 20px; background-color: #0366d6; color: white; text-decoration: none; border-radius: 5px; font-weight: bold;">
      📥 Download PDF
    </a>
  </p>
</div>

---

## What's Next

Thanks for reading Week 4 of my journey to becoming a SOC analyst! Watch the YouTube video, I plan to drop it very soon. Next week we're starting threat intelligence. I've been on phishing for about two weeks now, so I'm ready to move on to the new stuff. Happy holidays and I'll see you in the next one!

---

## Wrap-Up

Week 04 solidified my understanding of the phishing investigation workflow. From collecting artifacts to making the final verdict, I now have a systematic approach I can follow. The SOP I created isn't just for show - it's a practical tool I'll use and improve as I continue learning. Documentation is just as important as the technical skills themselves. I hope you enjoyed this week's letter and found the SOP useful. Keep analyzing, stay suspicious, and never forget to BTuff!

---

**Video coming soon!**

---

*Published: December 16, 2025*
