---
title: "Take Down The Stealers For Fun"
date: 2026-02-03
author: "Zachary Mitev"
draft: false
tags: ["threat-intel", "malware", "stealer", "hacking", "security"]
summary: "I want to share one old fun experience of taking down stealers and make quick interview with one of them."
showToc: true
TocOpen: true
---

## Summary
We've all seen them: those sketchy emails with an attachment-usually a RAR archive or a fake PDF-that's actually just malware waiting to steal your data. One day, I decided to finally do some analysis on these files to find out exactly what they do and where they're sending our information.

Over a short stretch of about a month or two, I kept getting the exact same type of phishing emails. They all seemed to point back to the same sender, so I started digging into it. The static analysis turned out to be pretty tough because of how these particular stealers operate. They basically scour your entire Windows system, trying to export every stored credential they can find from browsers, password managers, email clients, you name it.

But when I ran dynamic analysis on them, a really clear pattern emerged: they almost always relied on FTP-or sometimes SMTP servers-to upload the stolen credentials back to the attacker.

In today's post, I'm going to walk you through exactly what I found. I'll also share how this research unexpectedly led to a short interview with one of the people actually running these campaigns, and we'll dive into why they do it in the first place.



## Network Analytics
Here some screenshot from dynamic analytics of network activity of the stealer , when it grab all the data it uploaded on the server via FTP.

![map view](/images/hk/network-activity.png)
*Network Activity*


The password is very strong but one of the problems clearly here is the plain text protocol - FTP. So, sometimes the length and entropy of the password is not really mater.

## Connecting to the Hacker's FTP and Deleting the Logs
I write one simple bash script that connects to the hacker FTP server list the number of logs and delete them.


![map view](/images/hk/ftp-connection.png)
*FTP connection*

I decided to automate the process. I spent some time setting up a script to automatically catch all their new stealers and wipe the victims' data right off their servers. As you can imagine, this really started to piss them off.

![map view](/images/hk/fuck-off-message.png)
*"fuck off"*

Sure enough, I eventually logged in and found a new folder sitting there named "FUCK OFF." Since I still had write permissions on their FTP server, I decided to leave a reply of my own. I created a new folder proposing that the owner and I find a secure place to chat.

![map view](/images/hk/attempt-to-contact.png)
*Wanna be friends?*

After that, he dropped a Skype ID and we started talking. My goal was simple: figure out why and how they run these campaigns. In exchange, I promised to tell him exactly how I breached his server. It was the perfect bait to get him talking, and honestly, my plan was to block him the second I got my answers.

But he actually beat me to the punch and blocked me first.

Thank god I was taking screenshots in real-time. If you've ever dealt with Skype, you know that when someone blocks you, the entire chat history just vanishes. Because he pulled the plug so fast, I am missing the very last part of the conversation, but I managed to capture all the important stuff.

Here is the chat I managed to capture before he cut me off. To get him to open up, I had to play along and make him think I was actually on his side. I'm almost positive he lied to me about his name, and maybe even his age, but honestly, that's just how this game works...


![map view](/images/hk/skype-1.png)
*Skype Screenshots*

![map view](/images/hk/skype-2.png)
*Skype Screenshots*

![map view](/images/hk/skype-3.png)
*Skype Screenshots*

![map view](/images/hk/skype-4.png)
*Skype Screenshots*

![map view](/images/hk/skype-5.png)
*Skype Screenshots*

![map view](/images/hk/skype-6.png)
*Skype Screenshots*

![map view](/images/hk/skype-7.png)
*Skype Screenshots*

![map view](/images/hk/skype-8.png)
*Skype Screenshots*

![map view](/images/hk/skype-9.png)
*Skype Screenshots*

![map view](/images/hk/skype-10.png)
*Skype Screenshots*

![map view](/images/hk/skype-11.png)
*Skype Screenshots*

![map view](/images/hk/skype-12.png)
*Skype Screenshots*



## Conclusion

Keep in mind, that all went down back in 2020. Today, these types of attacks have evolved into something much harder to catch. Attackers are now using platforms like Discord bots and Telegram to exfiltrate data, which makes both static and dynamic analysis a lot tougher than it was back then.

But at the end of the day, if you are truly determined to figure out what an executable is doing under the hood, you can still crack it.

The biggest hurdle nowadays is that the domains they use for C2 (Command and Control) or exfiltration usually only stay alive for 24 hours—sometimes even less. Because they burn through infrastructure so fast, by the time you finally get your hands on the credentials for their server, it's often too late to actually reach them.