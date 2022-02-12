---
title: "Setting up WeeChat for IRC"
date: 2022-01-16T00:00:00-05:00
draft: false
tags:
    - irc
    - linux
categories:
    - networking
banner: images/posts/setting-up-weechat/weechat.png
---

# Preface

I will be doing the setup process on a CLI Debian Buster distrbution since I'm familiar with Debain more than other distributions. The same process for setting up WeeChat can be used on other linux distributions, but the installation process may differ depending on the package manager that you use. To keep things simple, we'll be using the APT package manager that comes preinstalled on the distribution

If you've only just learning about IRC, you've been missing out. There's a surreal feeling that inhibits you as you chat to someone across a terminal. It's a flood of fascination that words fail to formulate and I believe that WeeChat is one of the best IRC clients to get that rush of a feeling.

## Prerequisities

- A Linux distribution with the APT package manager
- A command-line interface/terminal

# Introduction

## What's IRC?

IRC, internet Relay Chat, is a protocol to communicate with others over the internet in an extremely lightweight manner. It came into existence in 1988 as a means to use the internet for communicating and now serves as the basis for most communication over the internet. Although the use of IRC is rarely used in its purest form, there are people that prefer to use it when running a command-line server, or a small operating system like tinycore for the the protocol's light load.

## WeeChat in the context of IRC

![WeeChat's CLI upon startup](startup.png)

WeeChat is a command-line IRC client that allows a user to use a terminal to communicate with others on IRC servers on a specific IRC server. The people that communicate on the server are typically, in my limited experience, linux geeks, security professionals, server administrators, or college students. Due to the technical nature of an IRC server, most of the general population is filtered through the process of setting up such a client and those that are left in the servers are those that are genuinely interested in the articule world of command-line communication.

## Why use WeeChat and not something else?

If you're looking at WeeChat, you're most likely looking for a feature-rich command-line IRC client. An alternative that I know of and have experience with is irssi, but WeeChat is much better in terms of the features it can provide. If you're looking for convenience, and convenience only, then a GUI web client like KiwiIRC may suit you better. As for irssi and WeeChat, the main benefits seem to be:
- WeeChat is more organized
- WeeChat has a better interface
- WeeChat has better default shortcuts
- WeeChat has many more themes for customization

Irssi seems reserved for more technical users that would be comfortable getting deep into their client and changing fundamental settings to their liking. If you're only starting out, WeeChat seems like the better option.

# Setting Up WeeChat

## Downloading WeeChat

To download the weechat client, you'll need to use the following command:

```light
apt install weechat
```

To start the client, run:

```light
weechat
```

## Connecting to an IRC server

We'll be connecting to libera chat, a well-known IRC server, as an example:

```light
/server add libera irc.libera.chat/6697 -ssl
/connect libera
```

This will add libera chat's irc server address in the keyword libera. Now, whenever you launch weechat, you only have to use the "/connect libera" statement.

## Register an account for liberachat

Now we'll set up an account on liberachat. Note that this process is the same for any IRC server. Also note the word nickname is synonymous with username.

```light
/nick [nickname]
/msg nickserv register [password] [youremail@example.com]
```

## Signing into your account when you connect

Now, you won't have to register a new nick when you join. You'll instead sign in

```light
/nick [your_previously_registered_nickname]
/msg nickserv identify [password]
```

## Connecting to Chat channels.

I typically like to hang out at ##chat and #linux. Libera Chat; however, has a [plethora of channels](https://netsplit.de/channels/?net=libera.chat&num=10) that you could join. 

To join a channel, you first need to sign in. Then you can:

```light
/join #[channel_name]
```

You will see the channel appear on your left side column. 

To leave that channel you may use:

```light
/leave
```

while you are on that channel. 

To switch between channels, you can use Alt + NUM to switch between the windows on the left side column.

# Conclusion

I hope you've got a basic understanding of how you can use WeeChat to communicate with others on an IRC network--specifically Libera Chat.
