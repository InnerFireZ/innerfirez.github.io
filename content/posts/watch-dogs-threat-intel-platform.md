---
title: "Watch Dogs: Torrent Peer Threat Intel for Bulgaria"
date: 2026-02-03
author: "Zachary Mitev"
draft: false
tags: ["threat-intel", "osint", "python", "flask", "maps", "security"]
summary: "Monitor torrent peers, enrich IPs with multiple intel sources, and visualize risk on a live map with Part of analytics."
showToc: true
TocOpen: true
---

## Overview
This post documents Watch Dogs - Torrent Peer Threat Intel (named after one of my favorite games). It is a Python-based system that monitors torrent peers (focused on Bulgarian IP addresses), enriches them with multiple threat-intelligence sources, and visualizes the results on a live map and analytics dashboards.

The idea came to me because I wanted to see—at least roughly—how many people in Bulgaria (where I’m from) are interested in cybersecurity. It’s one of those topics that not many people like to talk about, and some even prefer to keep it secret. My goal was simply to count how many of them are downloading specialized operating systems built for the cybersecurity field. These torrents are obviously not something your grandma would download (unless she’s an old hacker 😄); they are mostly downloaded by people working or learning in this field.

However, I quickly ran into a problem. There are a lot of bots, proxies, mobile devices, and shared public IPs everywhere. Because of this, I needed a way to verify what types of devices were actually behind the IP addresses(but using only open source data).

At the same time, I also wanted to see how many of these devices were malicious. Many beginners in this field don’t understand the importance of using a VPN, for example, and they sometimes attack other systems directly from their home IP address. This project helped me test whether that assumption is true. Also, many of them are downloaded by using VPS to perform attacks too.

To achieve this, I searched for the best free API providers that could help with IP and threat-intelligence data. With the additional help of AI to write fast and almost perfect Python code, the idea became reality.

In the screenshots below, I will show how much data I collected in just one month and some of the interesting things I discovered from this activity.

It is built to run continuously, store historical context, and generate practical signals you can act on.

## What This Project Does
- Monitors torrent (Kali,Parrot and other custom ones) peers and extracts IPs from specific geolocation in this case Bulgaria.
- Enriches IPs via multiple threat intel APIs.
- Correlates signals into risk levels and attacker classification.
- Visualizes results on a Folium map with filters and HUD controls.
- Provides stats, analytics, and reports for deeper analysis.
- Abstract IP Intelligence integration with full response storage and security flag stats.
- C2 feed sync from C2-Tracker and C2IntelFeeds with daily matching against DB IPs.
- **Correlation-based risk scoring** across AbuseIPDB, IPQS, OTX, GreyNoise, Shodan, and C2 hits.

## Screenshots

![map view](/images/wd/bg-map.png)
*Main Map View*
![Heat map](/images/wd/heatmap-1.png)
*Heat map of the Attackers*

![Part of Statistics View](/images/wd/stats-2.png)
*Part of Statistics View*

![Part of Statistics View](/images/wd/stats-1.png)
*Part of Statistics View*

![Part of Statistics View](/images/wd/stats-3.png)
*Part of Statistics View*

![Part of Statistics View](/images/wd/stats-4.png)
*Part of Statistics View*

![Part of Statistics View](/images/wd/stats-5.png)
*Part of Statistics View*

![Part of Statistics View](/images/wd/stats-6.png)
*Part of Statistics View*

![Part of Statistics View](/images/wd/stats-7.png)
*Part of Statistics View*

![Part of Statistics View](/images/wd/stats-8.png)
*Part of Statistics View*

![Part of Statistics View](/images/wd/stats-9.png)
*Part of Statistics View*

![Part of Statistics View](/images/wd/custom-torrents.png)
*I recently added a custom torrent watch, and these are the results from a single day.*



## APIs Data Sources Used
- AbuseIPDB
- IP-API
- IPInfo.io
- AlienVault OTX
- Shodan
- GreyNoise
- IPQualityScore
- Abstract IP Intelligence
- C2-Tracker feeds (github)
- C2IntelFeeds (github)

## Core Concepts
**Correlation scoring**
- Signals are combined to avoid over-reliance on a single source.
- C2 matches and multi-source consensus raise confidence.
- VPN/Proxy/Tor and mobile signals reduce false positives.

**Attackers Definition**
- Not VPN/Proxy/Tor
- Has AbuseIPDB reports or IPQS score > 0


## Analytics Notes
- **Hourly Activity** shows today's activity, with fallback to last 24 hours if today is empty.
- The analytics dashboard is computed on page load, not as a background job.



## Disclaimer
This project is for research and monitoring purposes. Handle API keys and IP data responsibly.
Project link to build your own: https://github.com/InnerFireZ/watch-dogs-threat-intel/
