---
title: "How Tor Works: [01] Becoming Anonymnous"
date: 2021-06-27T12:00:00-04:00
draft: false
tags:
    - Tor
categories:
    - Anonymity
banner: images/posts/tor-01/smallServerImg.jpg
---

# Preface

TOR is absolutely bonkers; keeping its users anonymous regardless of where or who they are. I was personally attracted by the deepweb and darkweb; the technical aspect of it. How does TOR work? How does it make exclusive websites with its network? How are you anonymous? These questions got me interested, and here I am starting a series of posts regarding TOR. *Just TOR.*

# The Setup

Let's say that there's a guy named John. John wants to be anonymous on the internet. Maybe John is in a situation where he has a really sensitive question that he wouldn't want anyone to know; what does he do? He uses TOR. He proceeds to start the TOR Browser and go to a forum on the clearnet. What happened there? How did John suddenly become anonymous by launching a browser?

I think that this is best explained by viewing the process from the perspective of the TOR Browser. Here are the tasks that the TOR Browser executes when it's launched: 

1. IP Collection
2. Key Exchanges

## IP Collection

When the TOR Browser is launched, it collects the IP addresses of three TOR servers from a public server called the TOR directory. The collected servers are called TOR nodes or TOR relays and comprise a guard relay, a middle relay, and an exit relay. 

## Key Exchanges

The TOR Browser does a Diffie-Hellman Key Exchange with each collected TOR relay. After this exchange, John's TOR Browser has three keys. One key to corrospond with each TOR relay. The TOR relays have the corresponding key to encrypt and decrypt data to John's TOR Browser. 

# The Request

Let's say that John wants to send request A to server X.
![Visual representation of request A](tor-01-requestA.jpg)

## The Encryption

**Request A:** The browser will change the source IP to the exit relay's IP. 
![Visual representation of request A after change](tor-01-requestA2.jpg)

**Request B:** It'll then encrypt request A with the exit relay's shared key and place it into another request: request B. Request B is given the source IP of the middle relay and the destination IP of the exit relay. 
![Visual representation of request B](tor-01-requestB.jpg)

**Request C:** It'll encrypt request B with the shared key between the browser and the middle relay and place it into another request: request C. Request C is given the source IP of the guard relay and the destination IP of the middle relay. 
![Visual representation of request C](tor-01-requestC.jpg)

**Reqeust D:** It'll encrypt request C with the shared key between the browser and the guard relay and place it into another request: request D. Request D now has the source IP of John and the destination IP of the guard relay.
![Visual representation of request D](tor-01-requestD.jpg)

### The Onion

I hope that you can see why TOR is associated with an onion. Each request is encrypted and placed into another request; hence, the layers of an onion.

## The Decryption

Now the browser will send request D and have it go through each relay. First the guard relay, then the middle relay, and then the exit relay before going off to the server. As the request goes through the TOR circuit, it will decrypt the request when it reaches the relay with the corrosponding decryption key. When a request is decrypted, it will find another request which it would then send off to the next relay on the circuit until it reaches the server.

When the Request comes back from the server, it will follow the same path in reverse and encrypt the packet at each station until John recieves it. The browser will decrypt each layer off of the packet and present John with the data that he requested from the server.
