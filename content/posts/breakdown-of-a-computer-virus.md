---
title: "Breakdown of a Computer Virus"
date: 2021-05-08T13:58:05-04:00
draft: false
---

# Preface

I spent the last week exploring the idea of a computer virus in to get a grasp of this specific type of Malware. As I dug deeper into the different components of a computer virus it dawned upon me that it was really easy to understand the basics of a computer virus, but as you'd try to explore each individual part of designing the virus into code, the definition would start to break down into pieces that didn't make sense. Throughout this blog post, I hope that I can clear any confusing parts regarding the creation of a computer virus.

# Definition

Before we delve into the differnt components of a computer virus, we need to become familiar with the basic definition of a computer virus:

> [a]n unwanted computer program or other set of instructions inserted into a computer’s memory,
> operating system, or program that is specifically constructed with the ability to replicate itself and to affect
> the other programs or files in the computer by attaching a copy of the unwanted program or other set of
> instructions to one or more computer programs or files.
>
> -- *The IT Law Wiki*

By this definition, we can see that the 3 main components of a computer virus include: **[1]** a payload that's **[2]** attached to a program **[3]** with the ability to replicate itself.

## The Payload

The payload, or the 'unwanted computer program', can really be a snippet of instructions to do whatever you like; it really leaves the technical bits up to you. Some payloads that have been used in the past are corrupt data on a hard drive, clog ram consistently, and even frame someone of a crime; use this information wisely and ehtically. Hopefully you realize that I do this for the enjoyment of learning and not to hurt someone. If you use this knowledge harmfully, you will be responsible. Anyways, on we go.

## The 'Attachment'

### Why?

As I'm sure, you're aware of the fact that 'attaching' refers to integrating your malicous code with another piece of code. Why? Well, the user needs to execute the code; he/she will be much more likely to execute your code if it is combined with an application that they'd trust. It also makes your virus harder to detect as in the process manager, the virus will be running through the supposed trusted application. Viruses need to be executed by the victim; if they're not executed, they wouldn't perform the malicious task (as you'd expect). 

### How?

Okay, now the actual attachment part. You get the 'why' of attaching your payload, now how do you do it? This section gets so complex as there are so many methods to attach a virus with another program that it deserves its own blog post.

To give a surface-level idea, you could merge executeable files to get the desired output, or you could run the virus in the background of a word document as it completes it functions in the background. Of course there are many other methods that you can use to hide your virus, like encrypted viruses, but these are meant to compliment the attachment of your virus to a program, not be standalone.

## Self-Replication

### Why?

Why would you want to self-replicate a virus. I mean, isn't it enough to just execute it once? No, it's not. A virus spreads itself throughout the system, adding the malicious code to multiple files on the computer. Doing so ensures that if one copy of the virus is deleted, other parts will continue to torment the system.

### How?

You would need to store the code somewhere since it was going to be replicated. The replication process can differ from virus to virus as there are multiple methods to complete this step and they adapt to the type of virus you are updating. You could hardcode the whole virus within your virus and then use that to replicate, or you could replicate the virus by calling a TOR server. If your executing other types of viruses, like an encrypted virus or a polymorhpic virus, your replication method would differ.

# Conclusion

When I had taken up the idea of learning how a computer virus functions over the last week, I expected it to be quite simple; I was wrong. The main concept of a computer virus is easy to grasp, but as you start to look deeper into the differnt processes that are undertaken by the virus, that process starts to become gibberish. Hopefully this post cleared up any ambiguity that you were facing while understanding the notion of a comptuer virus. 
