---
title: "Understanding TOR: [01] The TOR Browser"
date: 2021-05-20T09:58:44-04:00
draft: true
---

# Preface

TOR is absolutely bonkers; keeping its users anonymous regardless of where or who they are. I was personally attracted by the deepweb and darkweb; the technical aspect of it. How does TOR work? How does it make exclusive websites with its network? How are you anonymous? These questions got me interested, and here I am starting a series of posts regarding just TOR. *Just TOR.*

# The Main Events

John wants to be anonymous on the internet. Maybe John is in a situation where he has a really sensitive question that he wouldn't want anyone to know; what does he do? He uses TOR. He then proceeds to start the TOR Browser and go to a forum on the deepweb. What happened there? How did John suddenly become anonymous by launching a browser?

I think that this is best explained by viewing the process from the perspective of the TOR Browser. Here are the tasks that the TOR Browser executes when it's launched: 

1. IP Collection
2. Key Exchanges

## IP Collection

When the TOR Browser was launched, it collected the IP addresses of three TOR servers from a public server called the TOR directory. These three servers are generally referred to as TOR relays or TOR nodes and comprise a guard relay, a middle relay, and an exit relay. After the Key Exchanges in the next section, these three relays will form the TOR circuit that'll keep John anonymous as he surfs the web.

## Key Exchanges

John now has the three IP addresses  
