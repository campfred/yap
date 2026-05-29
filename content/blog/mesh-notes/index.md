---
title: LORA Mesh notes
description: Some notes of mine about my experience with some LORA Mesh networks (Meshtastic and MeshCore)
summary: Some personal notes about my experience with some LORA Mesh networks like Meshtastic and MeshCore. 📝🛜
date: 2026-05-29
lastmod: 2026-05-29
categories:
  - blog
tags:
  - tech
  - lora
  - mesh
  - networking
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

All of my experience comes from using a Heltec V4 radio with the basic small and curly antenna in the Greater Montréal Area in Québec, Canada, during the month of February 2026.
Therefore, all of my starting points for my settings and tests are based on the local community’s setup at that time and, of course, the limitations of my hardware and the software used at that ime.

## Meshtastic

> [!info] Firmware version used at the time of testing
> Version 2.7.15.567b8ea (Stable / Beta) was installed from the [official web flasher](https://flasher.meshtastic.org).

So, first, I began with <abbr title="Meshtastic">MT</abbr> since, at the time, it was the system we would see everywhere online when looking for that tech.
It was also the system with the most publicly showing nodes and repeaters in the area when comparing with [<abbr title="Meshtastic">MT</abbr>'s map](https://meshmap.net) and [<abbr title="MeshCore">MC</abbr>'s map](https://map.meshcore.io).
And so, Meshtastic was picked to begin the journey with LORA Mesh.

### Getting started

Getting it installed was really simple actually.
So, I flashed the latest official Stable / Beta firmware on it.

> [!tip]- Flashing Meshtastic firmware onto a Heltec V4 radio
> To flash the firmware, the radio needs to be in DFU mode. Here's how to do it on a Heltec V4 radio.
>
> 1. Press and hold down the BOOT / RESET button
> 2. Connect radio to a computer
> 3. Once connected, wait 1-2 seconds then release the BOOT / RESET button
>
> > [!info] DFU mode with a battery attached
> > If the radio has a battery attached to it, holding both the USER and the BOOT / RESET button while plugged in to a computer should allow to bring it into DFU mode without having to open the case and pull the battery out.
> {icon="mdi-power-plug-battery"}
>
> 4. Visit the [official web flasher](https://flasher.meshtastic.org) on a Chromium-based browser ([Helium](https://helium.computer) in my case)
> 5. Select the Heltec V4 radio as the <mark>Target device</mark>
> 6. Select the latest Stable / Beta firmware for install if it’s not already selected
> 7. Check ON the <mark>Full Erase and Install</mark> option
>
> > [!warning] Erasing is only needed for new installs!
> > If you are already running Meshtastic on your device, keep the <mark>Erase device</mark> setting OFF to preserve your settings.
> > Otherwise, you will lose all your settings and have to set up the radio again from scratch if you did not have a backup.
>
> 8. Click <mark>⚡ Flash</mark> to start the process
> 9. Select the <mark>USB JAG/serial debug unit</mark> device that shows in the browser’s serial device selection pop up
> 10. Wait for the process to complete
> 11. Open the [web client](https://client.meshtastic.org) (or the mobile app) and connect to the radio
> 12. Set the appropriate region of use (US in my case)
> 13. Explore and have fun! 🎉
{icon="download"}

> [!info] About the factory-provided firmware
> While the radio shipped with a Heltec-provided Meshtastic firmware on it, it was pretty outdated and, at the time, not considered optimal when asking people online.
> However, some still noted having better power management and even better radio transmittion performance too in some occasions.
> So, it might be worth trying it out if the official firmware doesn't work well for your use case.

From there, it’s pretty easy and mostly a matter of setting up the node’s name (short and long) and maybe a few other settings depending on the use case.

Luckily, my local Meshtastic community is running off the default LORA radio settings (Long Fast), so I was already part of the mesh as soon as I applied the US preset. ✨

And now began my observations on the system. 👀

### Node roles

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

If you're unsure or just starting, I'd suggest sticking with the default <mark>📱 Client</mark> role for your own node.
It'll work well and have all the interesting features to get you going. 👀

Later, if you have some extra nodes, mainly one that stays at home, you could set the stationary one to <mark>🏠 Client Base</mark> and the mobile one to <mark>📱 Client Mute</mark>.

If you have some more extra nodes that can be placed at high altitude in the area, installing <mark>🛜 Repeater</mark> nodes to extend the mesh coverage is very handy to contribute to the network.

### Private channels

Another thing I was happy about is the existence of private channels that are set up with a private pre-shared encryption key.
Of course, this shouldn't be used for transmitting sensitive information, but I found it was great to use with private communities to prevent polluting the public channel with messages that are more private anyway.
This is also useful if wanting to have the telemetry broadcasted only to specific people since automatic telemetry broadcasts only happen on the primary channel.

For that, you must configure the primary channel to have a private key that's different than the default one. Ideally using the strongest setting (32 bytes / AES-256) for the key length.
Then, the public channel can be set as a secondary channel with the default key to stay connected to the public mesh and have access to the public nodes and repeaters.

However, after doing that, I noticed that the automatic frequency slot selection will switch the radio out from the default one set for the region.
Therefore, kicking me out of the local mesh even while still having the public channel set as a secondary channel.

In order to stay connected with my local community, I needed to use [Meshtastic’s Frequency Slot Calculator](https://meshtastic.org/docs/overview/radio-settings/#frequency-slot-calculator) to obtain the slot number associated with the default frequency with the US preset and join back my local mesh community. ✨

If you're familiar with [`meshtastic-cli`](https://meshtastic.org/docs/software/python/cli/) and happen to be in the same situation, here's a configuration code snippet you can re-use to configure your node with the right frequency slot for the US preset while also having a private channel set up.

```yaml
config:
  lora:
    bandwidth: 250
    channelNum: 20
    codingRate: 5
    region: US
    spreadFactor: 11
    sx126xRxBoostedGain: true
    txEnabled: true
    txPower: 30
    usePreset: true
```

### Reliability

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

Now came the time to start using <abbr title="MeshCore">MC</abbr> and see how it performs compared to <abbr title="Meshtastic">MT</abbr>.
Not gonna lie, reading the summaries of differences between these two solutions made me pretty excited to try it out and see how it performs in real life.
It has a lot of potential for addressing the issues I was having with <abbr title="Meshtastic">MT</abbr>.
And so, I took a backup of my Meshtastic settings and private key and flashed the MeshCore firmware on my radio. ⚡

### Getting started

Again, installing it on a node was very simple and pretty much the same as with Meshtastic.

> [!tip]- Flashing MeshCore firmware onto a Heltec V4 radio
> To flash the firmware, the radio needs to be in DFU mode. Here's how to do it on a Heltec V4 radio.
>
> 1. Press and hold down the BOOT / RESET button
> 2. Connect radio to a computer
> 3. Once connected, wait 1-2 seconds then release the BOOT / RESET button
>
> > [!info] DFU mode with a battery attached
> > If the radio has a battery attached to it, holding both the USER and the BOOT / RESET button while plugged in to a computer should allow to bring it into DFU mode without having to open the case and pull the battery out.
> {icon="mdi-power-plug-battery"}
>
> 4. Visit the [official web flasher](https://flasher.meshcore.io) on a Chromium-based browser ([Helium](https://helium.computer) in my case)
> 5. Select the Heltec V4 radio as the <mark>Target device</mark>
> 6. Select the <mark>Companion Bluetooth</mark> role
> 7. Check ON the <mark>Erase device</mark> option
>
> > [!warning] Erasing is only needed for new installs!
> > If you are already running Meshtastic on your device, keep the <mark>Erase device</mark> setting OFF to preserve your settings.
> > Otherwise, you will lose all your settings and have to set up the radio again from scratch if you did not have a backup.
>
> 8. Click <mark>⚡ Flash</mark> to start the process
> 9. Select the <mark>USB JAG/serial debug unit</mark> device that shows in the browser’s serial device selection pop up
> 10. Wait for the process to complete
> 11. Open the the mobile app (or [web app](https://app.meshcore.nz) if flashed the <mark>Companion USB</mark> role) and connect to the radio
> 12. Set the appropriate region of use (US in my case)
> 13. Explore and have fun! 🎉
{icon="download"}

From there, it was again a matter of setting up the node's name, applying the US radio preset and a few other settings for the use case.

Unluckily, my local MeschCore community was not very present in my area. So, I could only test it out on days I would go work on site.
This didn't stop me from trying it out and discovering it! 🔥

### Node roles

MeshCore is pretty simple in comparison when it comes to node roles as there are only three.

- <mark>📱 Companion</mark><br>
  The only role to use unless you want to help building the network.<br>
  It is the only role that can connect to the app for sending and receiving messages.
- <mark>🛜 Repeater</mark><br>
  Pretty self-explanatory. It rebroadcasts messages to extend the mesh coverage but doesn't connect to the app.
- <mark>💬 Room server</mark><br>
  Basically a post office for the mesh.<br/>
  They are a "store-and-forward" bulletin board that holds the last 32 messages of a configured channel and delivers them to you when you come back.<br/>
  Useful if you intend to have a channel with a community and do not want to miss the messages that were broadcasted while you were offline.

And again, if you have extra nodes, setting up repeaters in high places is a good idea to extend the mesh coverage, especially since MeshCore relies more on an existing repeaters network than Meshtastic does.
Another idea is to setup a room server at home with your private community's channel to make sure you don't miss too many messages when you're offline. 🏡

### Private channels and "hashtag" channels

Private channels also exist on <abbr title="MeshCore">MC</abbr> and work pretty much the same way as on <abbr title="Meshtastic">MT</abbr>, except for one thing.
There are also "hashtag" channels which are public channels that anyone can join without needing to know the pre-shared key, but they need to be manually added to be able to see and message on them.

Honestly, I find it pretty neat because it still allowed me to have a private channel for my friends while also have a "hashtag" channel specifically for events (concerts, festivals, etc.) that anyone can join to chat and have fun.

Therefore, the way I configured it is that, outside of the default public channel, I have a private channel with a pre-shared key that I share with my friends, a `#fluffcore` channel for fun of receiving other fluffs on the mesh and finally, when I go to an event, I also add the event's hashtag channel to my node to be able to chat with other attendees. For example, Furnal Equinox's social media hashtag this year was #FE2026, so I added that channel to my node when I went to the event! If I go to Île Soniq this year with a mesh node, I'll add the #ÎLESONIQ2026 channel up for example. 🐺

### Off-grid (client repeat) mode

This feature is very recent and was released in the v1.14 stable firmware version and outside of some tests at home, I didn't have the occasion to use it yet.
However, this solves a pain point I had before with MeshCore's approach.

Basically, it allows a companion node to bet switched into a Meshtastic-like operation mode where it will not only receive and transmit messages, but it will also forward incoming messages not meant for it.
Therefore, breaking the isolation that happens when no repeaters are around.

When that feature got introduced, it allowed MeshCore to cover pretty much the entirity of my own use cases on the mesh.
I'm even considering just leaving that software on my companion permanently from now on. 👀

### Reliability

Reliability was greatly improved for me even though my local mesh community didn't have many repeaters up yet.
In fact, I was bringing my companion node up and back to work for war-walking and discovering repeaters on my way and while I did find one, it was situated far from the office I was working at.
However, while being at the office, I was able to exchange messages with other people on the network via a repeater even though both [MeshMapper](https://meshmapper.net) and [mapme.sh](https://mapme.sh) weren't able to get a successful test out of it.

I think that, aside when I was away from a repeater obviously, I have yet to have a failed message attempt on MeshCore.
Which is pretty refreshing considering I was pretty bummed out with Meshtastic and was considering repurposing the radio for other LORA use cases. ❤️‍🩹

## How I am approaching this now

Now that I'm better informed about that technology and that the novelty wore off a bit, I have a few thoughts on when and where each would be useful that I think would be interesting to know about.

### Meshtastic use cases

Meshtastic still stays relevant for me despite the issues I had of course, but its use case is not a bit strict.

If you want a way to exchange messages at crowded events and your experience has been reliable for direct messaging, I believe this remains a good use case for it.
It's especially useful at places where having a bunch of cellphones tightly packed together will bring down the mobile phone networks to their knees.
Oh! And if you got nodes with GPS installed, this can also allow to share precise location (automatically or manually) with friends to regroup more easily.

Speaking of GPS and telemetry, that's pretty much its strenght for me.
It unlocks a few more use cases for me that MeshCore, right now, don't seem to cover.

One example I've been told about by another user is being able to leave trackers behind alike "breadcrumbs" while hiking.
They'd use them later as checkpoints when backtracking their trip.

It's been also interesting to observe a node in my area that had a few sensors installed and broadcasted onto the mesh.
Essentially acting as a off-grid weather station for the area. 👀

But anything that requires communication over extended distances is probably out of question for me with Meshtastic.
I will miss the reply references, message reactions and priority alerts features that it offers.

### MeshCore use cases

MeshCore doesn't have the same set of features, especially when it comes to telemetry broadcast for example.

However, its focus on messaging makes it really compelling for anything messaging releated.
It's reliable and allows packets to travel far on a network with repeaters present.

Add to that the new client repeat mode and also the "hashtag" channels and it's a really compelling solution for crowded events.

I still wish there was the same kind of telemetry broadcast feature that <abbr title="Meshtastic">MT</abbr> has however.
Like if I am part of a private channel with friends, I'd like us to be able to share our position, battery level and mobile connection status (in case one's phone drop out of their companion) so that we can find eachother at festivals.
The companion connection status would especially be useful to guess what's going on with them no responding after a while. 😌

## My recommendation

Now, with all of that, would I still recommend people to get nodes and try Meshtastic and / or MeshCore?

Yes! Of course!
If you're already interested in this and _especially_ if you're a bit of a tinkerer anyway, you'll likely find something interesting to try out in both solutions.
The radios are cheap and don't need to be fancy with big antennas.
Just get a Heltec V3 or V4 with a battery and a GPS module and "plop" that with its default coily antenna in the plastic box that it came with and you're already set for getting started.

It's just so accessible that even a kid can study it.
They can use it learn and present at school about using LORA on a farm.
Like, explaining how this is used to wirelessly transmit information about the fields' moisture levels and other details back to home base.
And that is useful data to make decisions on harvesting times!

Anyway, I hope these notes have been interesting and maybe even useful for you as much as they've been fun to explore and write.
Even if the novelty of the tech wore off for me, I'm still always excited to bring one and show and try it out with people, especially furries.
We're a big bunch of nerds and the likelyhood of finding someone with the same interest is very high.
So, there's always opportunity to mess around and learn with it. ✨

> [!info]- Useful resources on the matter
> Here's a handful of sites that I found were helpful on the subject to understand and test things out.
>
> **Meshtastic-related**
>
> - [Official website](https://meshtastic.org)
> - [Official documentation](https://meshtastic.org/docs/)
>   - [Frequency slot calculator](https://meshtastic.org/docs/overview/radio-settings/#frequency-slot-calculator)
>   - [Backing up and restoring security keys with `meshtastic-cli`](https://meshtastic.org/docs/configuration/radio/security/#security-keys---backup-and-restore)
> - [Official Meshtastic flasher](https://flasher.meshtastic.org)
> - [Official Meshtastic apps](https://meshtastic.org/docs/software/)
> - [Socialmesh third party app](https://socialmesh.app)
> - [MeshMap's public map](https://meshmap.net)
>
> **MeshCore-related**
>
> - [Official website](https://meshcore.io)
> - [Official documentation](https://docs.meshcore.io)
> - [Official MeshCore flasher](https://flasher.meshcore.io)
> - [Official MeshCore apps](https://meshcore.io#download)
> - [Official MeshCore map](https://map.meshcore.io)
> - [MeshMapper](https://meshmapper.net)
> - [mapme.sh](https://mapme.sh)
> - [samuk's awesome-meshcore document fork](https://github.com/samuk/awesome-meshcore/blob/main/README.md)
>
> **Communities**
>
> - [Canadaverse Mesh](https://wiki.mt.gt)
> - [MIME (Montréal Island Mesh Enthusiasts)](https://www.montrealmesh.ca)
> - [GOME (Greater Ottawa Mesh Enthusiasts)](https://ottawamesh.ca)
> - [NoDak (North Dakota) Mesh](https://nodakmesh.org/)<br/>
>   _(awesome website with instructions and tools linked in it!)_
> - [NHMesh](https://nhmesh.com)
>   - [Channel setup guide](https://nhmesh.com/guides/channel-setup)
>
> **Local, technical and governing resources**
>
> - [ISED (Innovation, Science and Economic Development Canada)](https://ised-isde.canada.ca)
> - [LoRa Alliance](https://lora-alliance.org)
> - [HeyWhat’sThat](https://www.heywhatsthat.com)
