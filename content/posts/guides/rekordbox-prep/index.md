---
title: "Rekordbox Preparation Guide"
date: 2025-12-13
# publishDate: 2025-12-13
draft: true
description: "Detailed guide on how to prepare for using standalone Rekordbox hardware (CDJs, XDJs a nd whatnot) on stage."
categories: ["guides"]
tags: ["djing", "rekordbox", "tech", "music"]
# series: "Preperation guides"
# series_order: 1
showTableOfContents: true
---

Hiya! 👋

Welcome to my guide on getting prepared to use standalone Rekordbox hardware (CDJs, XDJs and whatnot) on stage. ✨

I'm an IT professionnal by day who did a lot of AV and DJ work over the past 10+ years.
I've seen a lot of DJays panick on stage because their USB key didn't work or the settings applied to the players were not working for them. 🫠

So, this page aims at helping you to not end up in a similar situation and that gives me the occasion to point out a few things you may easily overlook.
Hopefully you'll find something helpful in there. ❤️‍🩹

This guide is structured in two main parts:

1. [USB keys](#usb-drives)
2. [Rekordbox app and settings](#rekordbox-app-and-settings)

Of course, feel free to check the table of contents to jump at the spot you're the most interested in. 🔍

{{<alert icon="castopod">}}
**Looking for mixes to listen to?**<br>
I'm publishing my mixtapes in [a podcast][castopod-listen] and I also have [some demos available to listen][castopod-demos] if you're interested! 🎶
{{</alert>}}

## USB drives

### USB drive performance

I noticed there's a few things that can happen when DJing off an underperforming USB key and these have had real impact on DJays playing on stage at events I was involved in.

- <mark>📩 Slow export / transfer speeds with Rekordbox</mark><br>
  Frustrating when you just wanna add "that new track that just came out" right before leaving for your set.
- <mark>🔍 Slow library searching / browsing speeds on decks</mark><br>
  Also anxiety inducing when you get an idea and need to find the track really quickly.
- <mark>📤 Slow track loading speeds on decks</mark><br>
  Especially relevant when loading and moving in your next track pretty late before your next transition.
- <mark>🥶 Playback freezes on decks</mark><br>
  Less common but it can happen when the USB key can't keep up with the player running through the song.
- <mark>☠️ Corrupted / incomplete recordings on standalone systems</mark><br>
  While the recording feature is reserved to all-in-one units, it's still heart wrenching when your sick set's recording is unusable.

{{<lead>}}In short, a badly performing USB key is anxiety inducing and frustrating. Please get a good one.{{</lead>}}

So...now that you understand the importance of your "cheap" USB keys to run reliably, let's look at what to look for to prevent these issues. 😉

### How to shop for a USB key

It's actually pretty easy as it turns out! Here's the few specs you wanna keep in check for your next purchase.

- <mark>✏️ 4K random write speeds</mark><br>
  This has an impact on exporting your library from Rekordbox on desktop to your USB key and even set recording to some extent.
- <mark>🔍 4K random read speeds</mark><br>
  This helps when searching and browsing your library on players as it's a lot of random small data reads in device libraries.
- <mark>🎞️ Sequential read speeds</mark><br>
  While this one is usually fine, it does improve your tracks' loading speeds as seen by the waveforms gradually appearing on screen _in sequence_.
- <mark>🏬 Local shops</mark><br>
  It doesn't affect performance, but the ability to get a new drive from a local shop in emergency hours before playing is heavily underestimated. It also helps protecting against counterfeits sold online.

{{<lead>}}Basically, get a USB flash drive that is tested for >=100 MB/s of random 4K read and write speeds.{{</lead>}}

{{<alert>}}
**Portable SSDs are discouraged!**<br>
Players and mixers are often not providing enough power for running external / portable SSDs with them.
Please, do not consider using these without additional external power.
{{</alert>}}<br>

{{<alert icon="circle-info">}}
**What I'm using**<br>
To date, I'm using a [Kingston's DataTraveler Max][kingston-datatravelermax].
It has good specs for relieving my own anxiety and my friends' during Rekordbox exports with [its ~200 MB/s random 4K speeds][techpowerup-kingston-datatravelermax].
It's also available at the most present computer stores in my area ([Canada Computers][kingston-datatravelermax-canadacomputers], [Addision Électronique][kingston-datatravelermax-addison] and [Best Buy][kingston-datatravelermax-bestbuy]), which already has been handy in a few occasions. ❤️‍🩹
{{</alert>}}

Assuming you've got a nice USB key now, how about getting it formatted properly? 👀

### USB disk formatting

#### Partitioning schemes

This one's pretty simple. There's only two and here's a small breakdown of them.

- <mark>MBR (Master Boot Record)</mark><br>
  Oldest of the two and widely supported with devices other than DJ equipment. It has limitations but they won't be relevant anytime soon for USB drives.
  - ✔ Compatible with all Pioneer DJ / AlphaTheta equipment (and also many other non-DJ stuff)
  - ✔ Supported for equipment firmware upgrades
  - ❕ New disks often don't ship with it nowadays
- <mark>GPT (GUID Partition Table)</mark><br>
  Newer of the two with limitations much higher than MBR.
  - ❕ Only compatible starting with the XDJ-XZ and needs a firmware upgrade in some cases
  - ❌ Unsupported for equipment firmware upgrades
  - ✔ Most disks are shipped with this scheme these days

{{<lead>}}So, the <mark>MBR</mark> partitioning scheme is preferred for DJ USBs.{{</lead>}}

{{<alert icon="circle-info">}}
**Switching between partitioning schemes**
A disk utility on a computer is required to switch between partitioning schemes.
All operating systems include one and searching for "disk" will bring it up.
Depending on the utility, it may be needed to delete all partitions first before attempting to switch.
{{</alert>}}

#### Partition formats

This one has a little bit more possibilities and has led to some confusion from a few friends of mine. So, here's another breakdown for these.

- <mark>FAT16</mark><br>
  Oldest of the bunch and likely not accessible depending on your disk formatting utility.
  - ✔ Compatible with all Pioneer DJ / AlphaTheta equipment
  - ✔ Supported for equipment firmware upgrades
  - ❌ 4 GB maximum partition size (not very useful nowadays!)
  - ❕ Least resistent to data corruption
- <mark>FAT32</mark><br>
  Most common partition format but may not be accessible via Windows' disk formatting utility without an update.
  - ✔ Compatible with all Pioneer DJ / AlphaTheta equipment
  - ✔ Supported for equipment firmware upgrades
  - ✔ 2 TB maximum partition size
  - ❕ Not very resistent to data corruption but still better than FAT16
- <mark>exFAT (FAT64)</mark><br>
  Newer partition format that is better suited for flash memory[^2]. Most flash drives ship with it.
  - ❕ Only compatible with "recent" hardware (XDJ-XZ and later) and may require a firmware update of said devices to support it
  - ❌ Unsupported for firmware upgrades
  - ✔ 256 TB maximum partition size
  - ✔ Most resistent to data corruption of the FAT family (lol)
- <mark>HFS+</mark><br>
  Old Apple computers only format.
  - ✔ Compatible with all Pioneer DJ / AlphaTheta equipment
  - ❌ Unsupported for firmware upgrades
  - ✔ 8 EB maximum partition size
  - ✔ High data corruption resiliency

{{<lead>}}Prefer using <mark>FAT32</mark> as the partition format unless more tech savvy.{{</lead>}}

If you must know how _I_ go about this, I actually have two USB keys.

1. The first one is basically my AV tech drive I carry at events I am supporting.<br>
   It is formatted in <mark>MBR</mark>+<mark>FAT32</mark> and contains the latest firmware of all of the players I usually support in events and also a basic selection of my library for testing.
2. The second one is my actual DJ drive I carry at events I am performing in.<br>
   It is formatted in <mark>MBR</mark>+<mark>exFAT</mark> and contains my actual performing DJ libraries and is also the recording target on recording-supported devices.

[^1]: "[…] operating systems don’t always finish their behind-the-scenes work the moment your progress bar disappears." — [CORSAIR, the PC components manufacturer][corsair-drive-ejection]
[^2]: "ExFAT was made to be very portable and optimized for flash drives. It’s lightweight like FAT32, but without the same file size restrictions." — [John Bogna @ PCMag Labo][pcmag-storage-formats]


## Rekordbox app and settings

### USB key identification

First, I really want to point this out since this is overlooked very often.
You can label your USB keys on Rekordbox and that label shows up on players and Rekordbox itself! ✨

Just open the properties of your USB key while in Export mode and then you'll see all of it there! 🎉

![Screenshot of Rekordbox' device (USB key) view showing how I accessed it and that I named my USB "Camp" and I set its colour for both library types as "yellow"](attachments/rekordbox-usb-id.png "Click on the very tiny USB key icon on the left sidebar, then click on your USB key's name and it will displayed right front and center.")

As you can see, I set mine with my name and I set it as yellow. But there's height colours to choose from. 💛

Now's the time to turn your attention to your settings because that's another anxiety reliever that a lot of people are missing on.

### USB DJ settings



You likely noticed that there are a few more settings presented to you right under those name and colour settings.
Notably, the waveform colour, position and divisions, the songs' key display format and, probably my favourite, a picture that you can display on your jog wheels.
I very much use this to put some funny memes there. Kind of a easter egg for people hanging out or taking pictures in the booth. 👀

However, please also take a look at the other tabs.
They contain a lot of settings you're likely gonna want to setup also.

- <mark>General</mark><br>
  You probably know that one by heart now but this has all the essentials to at least get started.
- <mark>Category</mark><br>
  That's where you set the "views" you want available on the players. You really need to set this beforehand otherwise you likely won't be able to get them back once on stage. 😅
- <mark>Sort</mark><br>
  Less crucial of a setting to set but, again, getting new ones shown _on device_ is a bit hard. Set this in advance.
- <mark>Column</mark><br>
  This allows you to select the information you want displayed when browsing tracks. I personnally set it to rating as I use that as a way to gauge the energy of tracks.
- <mark>Color</mark><br>
  Just make sure that your Colour tags are set to the same names you have in Rekordbox' application preferences. Otherwise you may not remember what they mean on stage. 😅
- <mark>My Settings</mark><br>
  As you can see, nothing can be changed there. That's because it is reflecting your Rekordbox applications' DJ Settings preferences. And of course they don't give you a button to access them quickly. 🫠

{{< carousel images="{attachments/rekordbox-usb-general.webp,attachments/rekordbox-usb-category.webp,attachments/rekordbox-usb-sort.webp,attachments/rekordbox-usb-column.webp,attachments/rekordbox-usb-color.webp,attachments/rekordbox-usb-mysettings.webp}" >}}

<!-- ![Screenshot of Rekordbox' device (USB key) view showing my "General" settings.](attachments/rekordbox-usb-general.webp "You can see I have selected \"3Band\" as my preferred waveform type and a few other options.")
{style="width:50%;"}
![Screenshot of Rekordbox' device (USB key) view showing my "General" settings.](attachments/rekordbox-usb-general.webp "You can see I have selected \"3Band\" as my preferred waveform type and a few other options.")
{style="width:50%;"} -->

There's also more tabs to click through at the top with even more settings.
These are all of your DJ settings you will be able to recall on the players and mixers when you'll hop on stage for your set.
Please take the time to go through them and configure them to your liking. 😇

A lot of DJays I supported during shows were understandably anxious when they found out that the players were not behaving to their liking because they were running off the previous DJ's settings. 🫠



## Device libraries

[castopod-listen]: https://music.jackle.ca/@listen/episodes "Listen with Camp on Camp's Castopod instance"
[castopod-demos]: https://music.jackle.ca/@promo/episodes "Camp's demos on Camp's Castopod instance"
[kingston-datatravelermax]: https://www.kingston.com/en/usb-flash-drives/datatraveler-max "Kingston DataTraveler Max USB 3.2 Gen 2 flash drive on Kingston's official website"
[kingston-datatravelermax-canadacomputers]: https://www.canadacomputers.com/en/flash-drives/244849/kingston-datatraveler-max-256gb-usb-a-3-2-gen-2-flash-drive-dtmaxa-256gb.html "Kingston DataTraveler Max in 256 GB USB-A variant on Canada Computers"
[kingston-datatravelermax-addison]: https://addison-electronique.com/fr/cle-usb-type-a-kingston-datatraveler-max-256-go.html "Kingston DataTraveler Max in 256 GB USB-A variant on Addison Électronique"
[kingston-datatravelermax-bestbuy]: https://www.bestbuy.ca/en-ca/product/17039346 "Kingston DataTraveler Max in 256 GB USB-A variant on Best Buy Canada"
[techpowerup-kingston-datatravelermax]: https://www.techpowerup.com/review/quick-look-kingston-datatraveler-max-usb-3-2-gen-2-flash-drive/ "TechPowerUp Labo Quick Look: Kingston DataTraveler Max USB 3.2 Gen 2 Flash Drive"
[pcmag-storage-formats]: https://www.pcmag.com/how-to/fat32-vs-exfat-vs-ntfs-which-format-is-best-for-your-storage-drive#exfat-lightweight-compatible-high-capacity:~:text=ExFAT%20was%20made%20to%20be%20very%20portable%20and%20optimized%20for%20flash%20drives%2E%20It%E2%80%99s%20lightweight%20like%20FAT32%2C%20but%20without%20the%20same%20file%20size%20restrictions%2E "PCMag Labo: FAT32 vs. ExFAT vs. NTFS: Which Format Is Best for Your Storage Drive?"
[corsair-drive-ejection]: https://www.corsair.com/us/en/explorer/diy-builder/storage/do-you-really-need-to-eject-a-usb-drive/ "CORSAIR Labo: Do You Really Need to Eject a USB Drive?"
[pioneerdj-support-partitionformats]: https://support.pioneerdj.com/hc/en-us/articles/4406512519193-What-sort-of-formats-are-supported-for-USB-memory-devices-and-USB-hard-disks "AlphaTheta Help Center: What sort of formats are supported for USB memory devices and USB hard disks?"
