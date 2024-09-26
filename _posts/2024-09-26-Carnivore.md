---
title: "Carnivore and Galloway's Email"
date: 2024-09-26
layout: post
category: blog
tags: [Technology, Philosophy]
---

[Carnivore](https://r-s-g.org/carnivore/) is a library of Processing developed by Radical Software Group (led by Alexander Galloway). It was originally designed for local traffic monitoring based on a server-client architecture, and soon abandoned this structure and moved to a distributed model, where every client monitors and stores its own data packet switching information. This project is named after FBI's Carnivore project, the latter aims to collect all the online avtivities by us users, in the guise of national security, after 9/11. Galloway argues that the data collection and monitoring are inevitable in such a networked society, and that is really important is to empower every individual user and small-scaled group with the ability to understand and process data. That is where Carnivore stepped in.

Unfortunately, RSG's Carnivore cannot run in Windows system today (it runs well in MacOS devices), because it is dependent on an external technology named Winpcap, and Winpcap hasn't been updated since 10 years ago. If you Google this problem, several years ago there were some posts reporting this issue, however no valuable answer or solution proposed.  

I report this to RSG through email, and here's Galloway's reply:

![alt text](/images/GallowaysEmail.png)

He need to find another underlying library to use, which means that he has nothing else to do without another library to use. Such a small team cannot make a robust and complex software or system itself, that is why Carnivore is highly denpendent on external library. While Carnivore's vision is partly to empower small teams distributed in this networked society, it brings itself into a dilemma.

Single distributed practice is not enough, for it cannot sustain itself for too long. More networked distributed practices are needed.
