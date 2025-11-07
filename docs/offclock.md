---
layout: default
title: Off the Clock
nav_order: 4
has_children: true
permalink: /offclock/
---

# Off the Clock

## Life, Growth, and Everything Beyond the Terminal

This is where I step away from CVEs and log analysis to share thoughts on life, mental health, personal growth, and whatever else is on my mind.

### What You'll Find Here

Unlike the structured weekly cybersecurity letters, these posts are:
- **Unscheduled** - I write when I have something worth saying
- **Varied in length** - Could be a quick thought or a deep reflection
- **Authentically me** - No technical jargon, just real talk
- **About life** - The human side of the cybersecurity journey

### Topics I Cover

- **Mental Health & Balance** - Dealing with burnout, imposter syndrome, staying motivated
- **Personal Growth** - Habits, productivity, mindset shifts
- **Life Lessons** - What I'm learning while chasing certs and career goals
- **Real Talk** - Unfiltered thoughts on challenges and wins
- **Random Interests** - Fitness, books, whatever I'm exploring

### Why This Exists

Breaking into cybersecurity takes more than technical skills. It requires persistence, resilience, and mental toughness. These posts document the non-technical side of the journey - the mindset and habits that keep me going.

If you're on a similar path, hopefully these reflections remind you that you're not alone in the struggle.

---

## Posts

All posts are listed below from newest to oldest. No schedule, no pressure - just authentic thoughts when they're ready.

{% assign sorted_posts = site.offclock | sort: 'nav_order' | reverse %}
{% for post in sorted_posts %}
  <div style="margin-bottom: 30px; padding-bottom: 20px; border-bottom: 1px solid #444;">
    <h3><a href="{{ post.url | relative_url }}">{{ post.title }}</a></h3>
    <p>{{ post.content | strip_html | truncatewords: 50 }}</p>
    <a href="{{ post.url | relative_url }}">Read more →</a>
  </div>
{% endfor %}

---
