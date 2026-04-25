---
title: LORA Mesh notes
description: Some notes of mine about my experience with some LORA Mesh networks (Meshtastic and MeshCore)
summary: Some personal notes about my experience with some LORA Mesh networks like Meshtastic and MeshCore. 📝🛜
date: 2026-04-13
lastmod: 2026-04-13
draft: true
categories:
  - blog
tags:
  - tech
  - lora
  - mesh
  - meshtastic
  - meshcore
showTableOfContents: true
---

Hi there! 👋🏻

Late last year, my lover bought a pair of Heltec V4 radios for experimenting with LORA Mesh protocols and networks.

Since then, I’ve been a bit obsessed with the tool and have experimented a lot with it to learn about it.
Since then, my view of that tool has shifted significantly but not necessarily for the worse. I’m just wiser and better informed about it.

So, let’s discuss it. I have a lot to share and I want to help new comers work through the issues I had myself with that tech.

This post will be split into two main sections: Meshtastic, since I started on it, and MeshCore.

## Oh so important context

All of my experience comes from using a Heltec V4 radio with the basic small and curly antenna in the Greater Montréal Area in Québec, Canada.
Therefore, all of my starting points for my settings and tests are based on the local community’s setup at that time and, of course, the limitations of my hardware and the software used at that ime.

## Meshtastic

> [!info] Firmware version used at the time of testing
> Version 2.7.15.567b8ea (Stable / Beta) was installed from the [official web flasher](https://flasher.meshtastic.org).

So, first, I began with <abbr title="Meshtastic">MT</abbr> since, at the time, it was the system we would see everywhere online when looking for that tech.
It was also the system with the most publicly showing nodes and repeaters in the area when comparing with [<abbr title="Meshtastic">MT</abbr>'s map](https://meshmap.net) and [<abbr title="MeshCore">MC</abbr>'s map](https://map.meshcore.io).
And so, Meshtastic was picked to begin the journey with LORA Mesh.

### Getting started

Getting it installed was really simple. While the radio shipped with a Heltec-provided Meshtastic firmware on it, it was pretty outdated and, at the time, not considered optimal when asking people online.
So, I flashed the latest official Stable / Beta firmware on it.

> [!tip]- Flashing Meshtastic firmware onto a Heltec V4 radio
> To flash the firmware, the radio needs to be in DFU mode. Here's how to do it on a Heltec V4 radio.
> 1. Press and hold down the BOOT / RESET button
> 2. Connect radio to a computer
> 3. Once connected, wait 1-2 seconds then release the BOOT / RESET button
>
> > [!tip] DFU mode with a battery attached
> > If the radio has a battery attached to it, holding both the USER and the BOOT / RESET button while plugged in to a computer should allow to bring it into DFU mode without having to open the case and pull the battery out.
> {icon="mdi-power-plug-battery"}
>
> 4. Visit the [official web flasher](https://flasher.meshtastic.org) on a Chromium-based browser ([Helium](https://helium.computer) in my case)
> 5. Select the Heltec V4 radio as the <mark>Target device</mark>
> 6. Select the latest Stable / Beta firmware for install if it’s not already selected
> 7. Check on the <mark>Erase device</mark> option
>
> > [!warning] Erasing is only needed for new installs!
> > If you are already running Meshtastic on your device, keep the <mark>Erase device</mark> setting OFF to preserve your settings.
> > Otherwise, you will lose all your settings and have to set up the radio again from scratch if you did not have a backup.
>
> 8. Click <mark>Flash</mark> to start the process
> 9. Select the <mark>USB JAG/serial debug unit</mark> device that shows in the browser’s serial device selection pop up
> 10. Wait for the process to complete
> 11. Open the web client (or the mobile app) and connect to the radio
> 12. Set the appropriate region of use (US in my case)
> 13. Explore and have fun! 🎉
{icon="download"}

From there, it’s pretty easy and mostly a matter of setting up the node’s name (short and long) and maybe a few other settings depending on the use case.

Luckily, my local Meshtastic community is running off the default LORA radio settings (Long Fast), so I was already part of the mesh as soon as I applied the US preset. ✨

And now began my observations on the system. 👀

#### Node roles

I’ve been pleasantly surprised to see that everything is included in the same single firmware. Meaning I can flash the same firmware binaries for a client and for a repeater and only the configuration will determine their role and behaviour.
As someone who is used to cases like RAID cards needing a different firmware to run in an alternative mode, that was really refreshing for me.

From there, I found there’s a lot of different roles that can be used for different use cases. However, I’ll note the most useful ones to me.

- <mark>📱 Client</mark><br>
  This is the most common role for a node on the Meshtastic network and the default one to use when in doubt.<br>
  It allows receiving, sending and forwarding messages on the network and can connect to the mobile and desktop apps.
- <mark>🔇 Client Mute</mark><br>
  This role is like the <mark>📱 Client</mark> role, except it doesn’t forward the messages broadcasted on the mesh (useful for keeping the noise down on the network).
- <mark>🏠 Client Base</mark><br>
  This one is like a client, except it will also always rebroadcast packets from its favourites nodes (usually your own client nodes).<br>
  If you have an extra stationary node at home, this is a good role for it.
- <mark>🛜 Repeater</mark><br>
  Repeaters are pretty self-explanatory.<br>
  They "repeat" (rebroadcast) messages but don’t count in the retransmission hops count of a message and they don’t appear in the discovered nodes list.<br>
  They are very useful for extending the mesh’s network coverage.
- <mark>🛜 Router (Late)</mark>
  Similar to repeaters except they do count in the message hops count and also they do show on the nodes list.<br>
  However, the <mark>🛜 Router Late</mark> variant will only rebroadcast after all other modes have done so.

> [!Info] A complete list of roles is available on the official documentation!
> Meshtastic has a [great list](https://meshtastic.org/docs/configuration/radio/device/#roles) with all of the other modes described in it.
> Don’t hesitate to read through it!
> They even have a [thorough guide on how to choose the node role](https://meshtastic.org/blog/choosing-the-right-device-role/)

If you're unsure or just starting, I'd suggest sticking with the default <mark>📱 Client</mark> role for your own node. It'll work well and have all the interesting features.

Later, if you have some extra nodes, mainly one that stays at home, you could set the stationary one to <mark>🏠 Client Base</mark> and the mobile one to <mark>📱 Client Mute</mark>.

If you have some more extra nodes that can be placed at high altitude in the area, installing <mark>🛜 Repeater</mark> nodes to extend the mesh coverage is very handy to contribute to the network.

#### Private channels

Another thing I was happy about is the existence of private channels that are set up with a private pre-shared encryption key.
Of course, this shouldn't be used for transmitting sensitive information, but I found it was great to use with private communities to prevent polluting the public channel with messages that are more private anyway.
This is also useful if wanting to have the telemetry broadcasted only to specific people since automatic telemetry broadcasts only happen on the primary channel.

For that, you must configure the primary channel to have a private key that's different than the default one. Ideally using the strongest setting (32 bytes / AES-256) for the key length.
Then, the public channel can be set as a secondary channel with the default key to stay connected to the public mesh and have access to the public nodes and repeaters.

However, after doing that, I noticed that the automatic frequency slot selection will switch the radio out from the default one set for the region.
Therefore, kicking me out of the local mesh even while still having the public channel set as a secondary channel.

In order to stay connected with my local community, I needed to use [Meshtastic’s Frequency Slot Calculator](https://meshtastic.org/docs/overview/radio-settings/#frequency-slot-calculator) to obtain the slot number associated with the default frequency with the US preset and join back my local mesh community.

#### Reliability

While this tech was fun to use in testing, I unfortunately wasn't able to reliably transmit or receive messages with friends through hops.
I am still unsure about the source of the issue but I believe the hardware that I was using (Heltec V4 with the small and curly antenna) was not entirely at fault since direct communications were working fine.
Increasing the maximum hop count to 7 didn't seem to help either.

So, I decided to give MeshCore a try to see if it would perform better in that regard considering I am in an urban setting.
Also, at the time I was testing <abbr title="Meshtastic">MT</abbr>, I was seeing a lot of discussion online about trying <abbr title="MeshCore">MC</abbr> instead.
Especially considering its different approach to routing that relies more on repeaters existing in the network and allowing a higher hops count.

> [!info] About using MQTT with Meshtastic
> While setting MQTT allows to reach more nodes and have more reliable communications, using the Internet to transmit messages between nodes that should be off-grid kinds of defeats the purpose I think.
> Therefore, aside experimenting with making my nodes show on the [public map](https://meshmap.net), I have kept MQTT fully disabled to stay true to the off-grid nature of the mesh.

## MeshCore

> [!info] Firmware version used at the time of testing
> Version v1.14.1 (Companion – Bluetooth) was installed from the [official web flasher](https://flasher.meshcore.co.uk).

### Getting started



### Observations



### Configuration suggestions



## How would I approach this now

### Meshtastic use cases



### Meshtastic configuration suggestions



### MeshCore use cases



### MeshCore configuration suggestions
