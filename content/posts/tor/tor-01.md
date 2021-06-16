---
title: "Understanding TOR: [01] Standard Insight"
date: 2021-05-20T09:58:44-04:00
draft: true
---

# Preface

TOR is absolutely bonkers; keeping its users anonymous regardless of where or who they are. I was personally attracted by the deepweb and darkweb; the technical aspect of it. How does TOR work? How does it make exclusive websites with its network? How are you anonymous? These questions got me interested, and here I am starting a series of posts regarding TOR. *Just TOR.*

# The Setup

Let's say that there's a guy named John. John wants to be anonymous on the internet. Maybe John is in a situation where he has a really sensitive question that he wouldn't want anyone to know; what does he do? He uses TOR. He proceeds to start the TOR Browser and go to a forum on the deepweb. What happened there? How did John suddenly become anonymous by launching a browser?

I think that this is best explained by viewing the process from the perspective of the TOR Browser. Here are the tasks that the TOR Browser executes when it's launched: 

1. IP Collection
2. Key Exchanges

## IP Collection

When the TOR Browser was launched, it collected the IP addresses of three TOR servers from a public server called the TOR directory. These three servers are generally called TOR relays or TOR relays and comprise a guard relay, a middle relay, and an exit relay. 

## Key Exchanges

The TOR Browser does a Diffie-Hellman exchange with each of the three TOR relays that it collected from the TOR directory in the previous step. After this exchange, John's TOR Browser has 3 keys to encrypt and decrypt messages with each of the TOR relays and each of the TOR relays have the corresponding key to encrypt and decrypt data to John's TOR Browser.

# The Request

Let's say that John wants to send request A to server X after his browser has completed the steps above.

## The Encryption

Request A, by default, has the source IP of John and the destination IP of X. The browser will change the source IP of request A to the exit relay's IP and then proceed to encrypt the *entire* request and places it into request B. Request A was encrypted by the shared key between the browser and the exit relay. 

