---
title: "The Diffie-Hellman Key Exchange"
date: 2021-09-05T12:00:00-04:00
draft: false
tags:
    - Key Exchange
categories:
    - Cryptography
banner: images/posts/diffie-hellman-key-exchange/keys.jpg
---

# Preface

I thought that this post would be simple to write. I wasn't completely wrong, but it did end up taking more time than I expected. With school starting in the coming days, it's going to get tricky to balance all my tasks. I'll try my best to stick to a consistent posting schedule. Hopefully I can finally get that instagram account up and running--that is one of my top priorities for this blog right now.

For the last week, I've been staring at modular mathematics to understand the Diffie-Hellman Key Exchange. 

## Prerequisites

- Able to understand 8mod5=3
- Knows the difference between [symmetric and asymmetric encryption]()
- [Familiar with Cyclic Numbers]()

# Getting Familiar

## What is it? 

The Diffie-Hellman is a method to exchange keys for symmetric encryption to occur. Without the Diffie-Hellman Key Exchange, symmetric encryption would be obselete.

The Diffie-Hellman Exchange is also how an ETEE (End-To-End Encrypted) connection is established.

## Why do we use it?

The Diffie-Hellman Key Exchange provides a way to exchange the same key without having a middle-man snoop onto the key. This allows two clients of a server to keep their messaged content a secret despite them being connected to the same server.

![Diagram of two clients connecting to central server](ETEEdiagram.jpg)

Although the server is relaying data between the clients, it will be unable to undersrtand any of it. 

---

We also use it to prevent Man-In-The-Middle attacks. It uses the same principle as the server from above.

![identical diagram as above but one client is switched with server and in the center there is a MITM computer](MITMdiagram.jpg)

The attacker can choose to relay the requests to the server, but can't see the keys that are exchanged between the server and the client. This allows the client and server to keep an encrypted connection. The attacker would be unable to read the content of the packets.

That specific process between the client and server is called TLS. The Diffie-Hellman Key Exchange is also used in SSH, SMIME, and IKE.

# How does the Diffie-Hellman Key Exchange Work?

## The Setup

There are four variables when the Diffie-Hellman Key Exchange is performed. Two of these variables are public, and two variables are private. We'll refer to these variables as a, b, g, and n.

For this exchange to work, 'g' has to be a large [cyclic number](https://www.geeksforgeeks.org/cyclic-number/).

Client 1, whom we'll call Bob, has var 'a', and Client 2, whom we'll call Alice, has var 'b'. Both variables 'g' and 'n' are publicly available for anyone to see.

![Image showing variables in a diagram](variableDistributionDiagram.jpg)

The variables 'a' and 'b' are randomly selected co-primes of 'n'.

## The Exchange

Both clients get the public variables and apply their corresponding private key in the following manner:

In our case, Bob will do
<span style="font-size:1.5rem;">$$g^amodn$$</span>

...and Alice will do
<span style="font-size:1.5rem;">$$g^bmodn$$</span>

So now this is what each of them have.
![The mathematics above is shown visually in an image](exchangeOne.jpg)

---

Then, both Alice and Bob share their outcome with each other through the server.
![Arrows of Bob and Alice sharing their outcomes of the expression](exchangeTwo.jpg)

---

Now, Alice, Bob, and the Server have some variables. 

Note that the other variables like 'g' are still there, but I've not included them because they're not as important anymore.
![Showing the essential variables that have been distributed throughout the exchange process](exchangeThree.jpg)

This part above confused me the most. [Cyclic Numbers in the Diffie-Hellman Key Exchange](). How is it that the server has no clue about the key, but Alice and Bob have all the necessary information to complete the Diffie-Hellman Key Exchange.

If you're fluent with Moduluar mathematics and are familiar with cyclic numbers, this is probably obvious to you, but for someone that's forgotten or never seen it, it's difficult to grasp. If you're the latter person, check out the [Cyclic Number supplement post]().

---

To complete the Diffie-Hellman Key Exchange, Bob will do:
<span style="font-size:1.5rem;">$$(g^amodn)^b$$</span>

...and Alice will do:
<span style="font-size:1.5rem;">$$(g^bmodn)^a$$</span>

and in both these cases, the answer is
<span style="font-size:1.5rem;">$$g^{ab}modn$$</span>

Now, both Bob and Alice have the same number while the server is left clueless:
![A visual image of what the server and the clients have.](exchangeFour.jpg).

---

Hopefully this makes sense. The Diffie-Hellman Key Exchange doesn't have a inherent encryption method to it, but it would provide both clients (Alice and Bob) to have the same number. This same number could then be used to generate a key for symmetric encryption without the server knowing what the key is.

# The End

I hope you learnt something new today. If the mathematics sounds interesting, it is. I highly suggest you check out my post on [Cyclic Numbers in the Diffie-Hellman Key Exchange]() because it's really cool to see how the numbers work and why it's difficult to brute-force the key.

If there's a way you think I could improve this post, please message me on [Instagram](https://instagram.com/cyberstudent.blog/). I appreciate all feedback that I get on my posts.




###### References
- Why does ((g^a)modn)^b = ((g^b)modn)^a
    - [Math Stack Exchange](https://math.stackexchange.com/questions/2576283/why-does-ga-bmod-nb-gb-bmod-na-gab-bmod-n)
