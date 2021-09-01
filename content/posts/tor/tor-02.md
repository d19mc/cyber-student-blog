---
title: "How Tor Works: [02] Connecting to Onion Services"
date: 2021-07-18T13:00:00-04:00
draft: false
tags:
    - Tor
    - Onion Services
banner: images/posts/tor-02/onion.jpg
---

# Preface

I wanted to write this post for two main reasons: [1] it's cool to see how onion services work, and [2] there isn't much documentation that makes onion services easy to understand.

I've only recently learned how onion services work, but I can say that it was quite fun learning how they serve their websites. I hope that this post doesn't contain too much jargon and can be read by a person with basic technical knowledge. If you know a way to improve this post, send me a DM on [Instagram](https://www.instagram.com/cyberstudent.blog/).

**TL?; Please Read**: There is a lot of detail in this post; hence, the length. Even though I have tried to simplify and condense as much information as I could, the post is still quite a long read.

## Prerequisites

- Common tor terms (guard relay, middle relay, tor directory, etc.)
- How Tor performs its layered encryption 
- Digital Signatures (Large sections of the process won't make sense without this)
- Diffie-Hellman Key Exchange

# Starting the Onion Service

![Image of an onion cut in half from above](onion.jpg)
*<p style="text-align: center;">Let's start our new onion service.</p>*

## Getting Introduction Points

The first thing a new onion service does is find at least three Introduction Points. These Introduction Points can be any server on the Tor network and will be routing traffic to the hosting server. The potential Introduction Point can accept or deny the request to introduce the service. The potential Introduction Point doesn't know what the server is hosting nor does it know its IP address. That is because the traffic goes through two tor relays before reaching the Introduction Point.

If the Introduction Point agrees to introduce tor traffic to the server, the hosting server shares its public key and digitally signs each of its messages to the Introduction Point from that point onwards. This way the Introduction Point can be sure that it's getting the message from the correct server.

### Common Questions

**Doesn't the Introduction Point need to know the onion service IP to send tor traffic to the server?**

No, it doesn't. The Tor circuit that the server opens to the Introduction Point remains open. The Introduction Point never initiates the connection to the server. If the server wants to change the circuit, it can connect to the point with a new circuit and send a digitally signed message saying "Hey, send your data down this relay from now on."

**What if someone takes over the relay before the Introduction Point?**

(Assuming http and not https) I can see why someone would think that the relay could read the message; since it's the last relay, the message should be decrypted right? Not in this case.

The relay doesn't know that it's talking to an Introduction Point because [1] any server on the tor network can be an Introduction Point, and [2] there'd still be a layer of encryption before it got to the Introduction Point, where it would get fully decrypted. 

In the [previous post](https://www.cyberstudent.blog/posts/tor/tor-01/), the last relay (exit relay) would decrypt the data completely. That's because it was the exit relay; it's responsible for exiting the tor network to the clear internet. Servers on the clear internet are not set up to establish anonymous connections; hence, it wouldn't be able to decrypt the data if the last relay hadn't decrypted it. But in the case of an Introduction Point, it has been set up with the purpose of being anonymous and retains a layer of encryption until it gets to the server itself.

# Advertising the Onion Service

![Image of the the same onion above on a billboard](advertiseOnion.jpg)
*<p style="text-align: center;">If you have a question, feel free to DM me on [Instagram](https://www.instagram.com/cyberstudent.blog/). I'll try my best to answer your question.</p>*

## Generating the .onion URL

The actual process of generating the .onion URL is extremely complex. It requires the understanding of public-private key encryption, distributed hash tables, hash checksums, and more. I couldn't find a way to cover this process within this post without it becoming clutter; I've covered it in a separate post. 

## Adding the .onion URL to Tor directory

The service creates a message with Introduction Point IPs and an expiration time. The onion service signs the message with its public key. After signing it, the message is sent to the Tor directory.

The Tor directory is a distributed hash table; but for simplicity, let's think of it like a dictionary. The .onion URL becomes the key to find this message in the Tor directory.

As the onion service would gain and lose Introudction Points, the signed message would change; hence, the existence of the expiration time. Once the message has expired, the onion service sends out a new message that contains the updated IP addresses of the Introduction Points and a new expiration time.

### Common Questions

**That makes sense, but how has the .onion service been 'advertised'?**

They are not 'advertised' in the traditional sense. They're not trying to get themselves in front of peoples' faces, but instead it is a term to say that now the service is accessbile. From now on, you can find the IP addresses of the Introduction Points by typing the service's .onion URL in the Tor browser and pressing enter.

**Okay but why does the .onion URL have to look so random?**

That is the the nature of how the Tor directory has been set up. It's a distributed hash table. A decentralized way of storing .onion URLs. Again, it's too complex to cover in this post--check out the post on [generating .onion URLs]() if you want to know why.

# Connecting to the Onion Service

![Image of Tor browser with an onion image displayed](connectOnion.jpg)
*<p style="text-align: center;">This post is getting long; I hope the onions don't make you cry.</p>*

## Getting the Introduction Points

When the client enters a .onion link in the browser, it creates a Tor circuit to the Tor directory and asks for the IP addresses of the corrosponding Introduction Points. It's able to get the correct IP addresses for the Introduction Points because the .onion URL is the key for the list of Introdution Points for the service. 

## Establishing a Rendezvous Point

A Rendevous Point is the relay that will be the point at which the server and client will pass encrypted data. After you get Introduction Points from the Tor directory, you choose a random relay on the Tor network. You then choose a random 20-byte rendezvous cookie (a key/message) that you send to the Rendevous Point through a Tor circuit. This keeps you anonymous to Rendevous Point.

## Requesting a Connection

When you have a successful connection with a Rendevous Point, you request a connection from the server through a Tor circuit. Recall that the message with the Introduction Point IP addresses was signed by the .onion server's public key. You encrypt a message that you'll be sending to an Introduction Point with this public key. Doing this would make sure that only the .onion server is able to decrypt the final request with its private key. The encrypted message would include:
1. IP of Rendezvous Point
2. The 20-byte rendezvous cookie
3. The first half of a Diffie-Hellman exchange
4. An optional authorization cookie (Check out the Ref. Links at the bottom)

If the server decides that it wants to make a connection to the client, it'll send a message to the Rendevous Point with:
1. The 20-byte rendezvous cookie
2. The second half of a Diffie-Hellman exchange 

The Rendevous Point sees that two different Tor circuits have given it the same 20-byte rendezvous cookie and it connects both of them together. Now there is an encrypted connection--because of the concurrent Diffie-Hellman Exchange--between you and the onion service.

### Common Questions

**What if the Rendevous Point already has an ongiong connection with the same 20-byte rendezvous cookie?**

In this highly unlikely scenario, the Rendevous Point breaks off the connection and the Tor browser attempts to make a new connection to another Rendevous Point. 

**How doesn't the Rendezvous Point know who is sending data**

The Rendevous Point doesn't know this because both the client and onion service use a Tor circuit to reach the Rendezvous Point. 

# The End

If you liked this post, I think you'd like my Instagram account as well. I post similar content there, but it's usually things that I couldn't fit into the blog post itself.

<br/>

###### Reference Links 

- Tor Stack Exchange
    - [What is the authorization cookie of a .onion address?](https://tor.stackexchange.com/questions/22507/what-is-the-authorization-cookie-of-a-onion-address)
- Tor Project
    - [2004 svn-archive](https://svn-archive.torproject.org/svn/projects/design-paper/tor-design.html#sec:rendezvous)
    - [Current onion service documentation](https://github.com/torproject/torspec/blob/main/rend-spec-v3.txt)
    - [Initial Proposal for v3 addresses](https://lists.torproject.org/pipermail/tor-dev/2017-January/011816.html)
- Computerphile
    - [Video: Connecting to onion services](https://www.youtube.com/watch?v=lVcbq_a5N9I) Check this out if you're very confused. (surface-level explanation of onion services)
