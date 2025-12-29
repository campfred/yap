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
I've seen a lot of DJays panick on stage because their USB key didn't work or, especially, the players behaviour was not like what they use at home. 🫠

So, this page aims at helping not ending up in a similar situation and that gives me the occasion to point out a few things that are easily overlooked.
Hopefully something will be helpful in there. ❤️‍🩹

This guide is structured in two main parts:

1. [USB keys](#usb-drives)
2. [Rekordbox app and settings](#rekordbox-app-and-settings)

Of course, feel free to check the table of contents to jump at any spot! 🔍

{{<alert icon="castopod">}}
**Looking for mixes to listen to?**<br>
I publish my mixtapes in [a podcast](https://music.jackle.ca/@listen/episodes "Listen with Camp on Camp's Castopod instance") and I also have [some demos available to listen](https://music.jackle.ca/@promo/episodes "Camp's demos on Camp's Castopod instance") if interested! 🎶
{{</alert>}}

## USB drives

### Device performance

I noticed there's a few things that can happen with underperforming USB keys and I had to handle DJays that were panicked because of those.
Most of them aren't really show stoppers but they definitely negatively affected the DJays' (or my own) performances.

- <mark>📩 Slow export / transfer speeds with Rekordbox</mark><br>
  Frustrating when adding "that new track that just came out" right before leaving for a set.
- <mark>🔍 Slow library searching / browsing speeds on decks</mark><br>
  Also anxiety inducing when needing to find the track really quickly during a set for a last minute idea.
- <mark>📤 Slow track loading speeds on decks</mark><br>
  Especially relevant when loading and scrubbing in the next track pretty late before the next transition.
- <mark>🥶 Playback freezes on decks</mark> _(vibe killer)_<br>
  Less common but it can happen when the USB key can't keep up with the decks playing through the song.
- <mark>☠️ Corrupted / incomplete recordings on standalone systems</mark><br>
  While the recording feature is reserved to all-in-one units, it's still heart wrenching when a sick set's recording is unusable.

{{<lead>}}In short, please get a good one. A badly performing USB key is anxiety inducing and frustrating.{{</lead>}}

### Shopping for a USB key

It's actually pretty easy as it turns out!
Here's the few specs to keep in check that will take care of the issues.

- <mark>✏️ 4K random write speeds</mark> _(most important)_<br>
  This has an impact on exporting a library from Rekordbox on desktop to the USB drive and even recording a set to some extent.
- <mark>🔍 4K random read speeds</mark><br>
  This helps when searching and browsing for tracks on players as it's a lot of random small data reads in device libraries databases.
- <mark>🎞️ Sequential read speeds</mark><br>
  While this one is usually fine, it does improve the tracks' loading speeds as seen by the waveforms gradually appearing on screen _in sequence_.
- <mark>🏬 Local shops</mark><br>
  It doesn't affect performance, but the ability to get a new drive from a local shop in emergency hours before playing is heavily underestimated. It also helps against counterfeits sold online.

{{<lead>}}Basically, get a USB flash drive that is tested for >=100 MB/s of random 4K read and write speeds.{{</lead>}}

{{<alert cardColor="indianred" iconColor="light">}}
**Portable SSDs are discouraged!**<br>
Players and mixers are likely not providing enough power for running external / portable SSDs with them.[^2]
Please, do not consider using these without providing additional / external power to the storage device.
{{</alert>}}<br>

#### What do _I_ use?

To date, I'm using a [Kingston's DataTraveler Max][kingston-datatravelermax] and that's what I have purchased to DJays during emergencies.

It has good specs for relieving my own and my friends' anxiety during Rekordbox exports with [its ~200 MB/s random 4K speeds][techpowerup-kingston-datatravelermax].
It's also available at the most present computer stores in my area ([Canada Computers][kingston-datatravelermax-canadacomputers], [Best Buy][kingston-datatravelermax-bestbuy] and [Addision Électronique][kingston-datatravelermax-addison]), which has been handy a few times already. ❤️‍🩹

### Disk partitioning schemes

This one's pretty simple as there's only two. Here's a small breakdown of them.

- <mark>MBR _(Master Boot Record)_</mark>
  {{<keyword icon="star">}}Preferred{{</keyword>}}
  Oldest of the two but widely supported with devices other than DJ equipment. Its limitations won't be relevant anytime soon for external storage.
  - ✔ Compatible with all Pioneer DJ / AlphaTheta equipment (and also many other non-DJ stuff)
  - ✔ Supported for equipment firmware upgrades
  - ❕ New disks often don't ship with it nowadays
- <mark>GPT _(GUID Partition Table)_</mark><br>
  Newer of the two with limitations much higher than MBR.
  - ❕ Only compatible starting with the XDJ-XZ and often needs a firmware upgrade to play from it
  - ❌ Unsupported for equipment firmware upgrades
  - ✔ Most disks are shipped with this scheme these days

{{<lead>}}Please use the <mark>MBR</mark> partitioning scheme for external storage.{{</lead>}}

{{<alert icon="circle-info" iconColor="light">}}
**Switching between partitioning schemes**<br>
A disk utility on a computer is required to switch between partitioning schemes.
All operating systems include one and searching for "disk" will bring it up.
Note that, depending on the specific utility, it may be needed to delete all partitions first before attempting to switch.
{{</alert>}}

### Disk partition formats

This one has a little bit more possibilities and has led to some confusion from a few friends of mine. So, here's another breakdown for these.

- <mark>FAT16</mark><br>
  Oldest of the bunch and likely not accessible depending on the disk formatting utility.
  - ✔ Compatible with all Pioneer DJ / AlphaTheta equipment
  - ✔ Supported for equipment firmware upgrades
  - ❌ 4 GB maximum partition size _(Not very useful nowadays!)_
  - ❌ Least resistent to data corruption
- <mark>FAT32</mark>
  {{<keyword icon="star">}}Preferred{{</keyword>}}
  Most common partition format but may not be accessible via Windows' disk formatting utility without an update.
  - ✔ Compatible with all Pioneer DJ / AlphaTheta equipment
  - ✔ Supported for equipment firmware upgrades
  - ✔ 2 TB maximum partition size
  - ❕ Not very resistent to data corruption but still better than FAT16
- <mark>exFAT</mark> _(aka FAT64)_<br>
  Newer partition format that is better suited for flash memory[^1]. Most flash drives ship with it today.
  - ❕ Only compatible with "recent" hardware (XDJ-XZ and later) and may require a firmware update to support it
  - ❕ Only supported for firmware upgrades on recent devices[^3]
  - ✔ 256 TB maximum partition size _(Not gonna hit that anytime soon!)_
  - ✔ Most resistent to data corruption of the FAT family (lol) but please eject your drive before disconnecting still[^0]
- <mark>HFS+</mark> _(aka HFS Extended or Mac OS Extended)_<br>
  Old format reserved to Apple computers that was replaced by APFS later on but is still referred to as supported for playback in Pioneer DJ's support documents[^4].<br>
  It is noted by Pioneer DJ that some characters of some languages can render tracks unusable on some devices like the XDJ-RX3[^5].
  - ✔ Compatible with all Pioneer DJ / AlphaTheta equipment
  - ❌ Unsupported for firmware upgrades
  - ✔ 8 EB maximum partition size
  - ✔ High data corruption resiliency

{{<lead>}}Prefer using <mark>FAT32</mark> as the partition format unless more tech savvy or really need to.{{</lead>}}

#### How _I_ go about this?

Since I'm also an AV / stage tech, I actually have two different USB keys for different purposes.

1. <mark>🛠️ AV tech drive</mark>
   {{<keywordList>}}{{<keyword>}}MBR{{</keyword>}}{{<keyword>}}FAT32{{</keyword>}}{{</keywordList>}}
   I carry this one as part of my AV tech kit I bring to events I am supporting (especially DJ backline).<br>
   It contains the latest firmware of all of the players I usually support in events (hence the FAT32 format) and there's also a basic but still good selection of my library for testing purposes and some light DJing.<br>
   It also contains other stuff like showfile templates and whatnot but these are out of scope for this guide.
2. <mark>💽 DJ drive</mark>
   {{<keywordList>}}{{<keyword>}}MBR{{</keyword>}}{{<keyword>}}exFAT{{</keyword>}}{{</keywordList>}}
   I carry this one at events I am performing or backing up as part of my DJ kit.<br>
   It has my actual performing DJ libraries and serves as my recording target (when possible).<br>
   It could be FAT32 but exFAT has been useful for recording extended sessions and its enhanced corruption resiliency seem to have worked well for me so far.<br>
   And since I only perform on "recent" hardware (OPUS-QUAD, XDJ-AZ, CDJ-3000/X…), exFAT has always been supported for playing anyway.

## Rekordbox app and settings

### In-Rekordbox disk identification

First, I really want to point this out since this is very often overlooked.
USB keys can be labeled on Rekordbox and that label shows up on players and Rekordbox itself!
And it's really easy to set up too! ✨

1. Open the _Devices_ panel
2. Select the storage drive in the list
3. Set the _device name_, _OneLibrary background colour_ and _Device Library background color_
4. Yay! 🎉

![Screenshot of Rekordbox' device (USB key) view showing how I accessed it and that I named my USB "Camp" and I set its colour for both library types as "yellow"](attachments/rekordbox-usb-id.png "The elements may appear slightly differntly in Performance Mode but the features are still all available in that mode too.")

I set mine with my show name and I set it as yellow but there's height colours to choose from. 🌈

{{<alert icon="lightbulb" cardColor="purple" iconColor="light">}}
**Be creative with the _device name_ property!**<br>
I've seen some DJays put their social media username or email address as their _device name_.
My AV tech drive I mentionned earlier has <mark>Camp (backline)</mark> as the name.
So, really, anything useful can be put there!
{{</alert>}}

{{<lead>}}Please take the time to properly ID USB keys. It's very useful during B2Bs and when somone forgets their disk on a player.{{</lead>}}

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

[^0]: "[…] operating systems don’t always finish their behind-the-scenes work the moment your progress bar disappears." — [CORSAIR, the PC components manufacturer][corsair-drive-ejection]
[^1]: "ExFAT was made to be very portable and optimized for flash drives. It’s lightweight like FAT32, but without the same file size restrictions." — [John Bogna @ PCMag Labo][pcmag-storage-formats]
[^2]: "The following may also be the cause of the problem; If you're using HDDs that consume more power than the USB port can provide; […]" — [AlphaTheta @ OMNIS-DUO support document][alphatheta-support-omnisduo-partitionformats-powerconsumption]
[^3]: "When updating the unit's firmware, use a USB storage device formatted in FAT, FAT32 or exFAT." — [AlphaTheta @ CDJ-3000X support document][alphatheta-support-cdj3000x-partitionformats]
[^4]: The support documents about partition formats support on [the CDJ-3000X player][alphatheta-support-cdj3000x-partitionformats], [the XDJ-AZ all-in-one console][alphatheta-support-xdjaz-partitionformats] and [the OneLibrary device library (formerly Device Library Plus)][alphatheta-support-onelibrary-partitionformats], released over a month ago, mentions HFS+ today.
[^5]: "When using an HFS+ format USB storage device, music files that use Hangul characters in the file name, artist name, or album name can't be loaded. In this case, use FAT32 formatted USB storage devices." — [AlphaTheta @ XDJ-RX3 support document][pioneerdj-support-xdjrx3-partitionformats]

[kingston-datatravelermax]: https://www.kingston.com/en/usb-flash-drives/datatraveler-max "Kingston DataTraveler Max USB 3.2 Gen 2 flash drive on Kingston's official website"
[kingston-datatravelermax-canadacomputers]: https://www.canadacomputers.com/en/flash-drives/244849/kingston-datatraveler-max-256gb-usb-a-3-2-gen-2-flash-drive-dtmaxa-256gb.html "Kingston DataTraveler Max in 256 GB USB-A variant on Canada Computers"
[kingston-datatravelermax-addison]: https://addison-electronique.com/fr/cle-usb-type-a-kingston-datatraveler-max-256-go.html "Kingston DataTraveler Max in 256 GB USB-A variant on Addison Électronique"
[kingston-datatravelermax-bestbuy]: https://www.bestbuy.ca/en-ca/product/17039346 "Kingston DataTraveler Max in 256 GB USB-A variant on Best Buy Canada"
[techpowerup-kingston-datatravelermax]: https://www.techpowerup.com/review/quick-look-kingston-datatraveler-max-usb-3-2-gen-2-flash-drive/ "TechPowerUp Labo Quick Look: Kingston DataTraveler Max USB 3.2 Gen 2 Flash Drive"
[pcmag-storage-formats]: https://www.pcmag.com/how-to/fat32-vs-exfat-vs-ntfs-which-format-is-best-for-your-storage-drive#exfat-lightweight-compatible-high-capacity:~:text=ExFAT%20was%20made%20to%20be%20very%20portable%20and%20optimized%20for%20flash%20drives%2E%20It%E2%80%99s%20lightweight%20like%20FAT32%2C%20but%20without%20the%20same%20file%20size%20restrictions%2E "PCMag Labo: FAT32 vs. ExFAT vs. NTFS: Which Format Is Best for Your Storage Drive?"
[corsair-drive-ejection]: https://www.corsair.com/us/en/explorer/diy-builder/storage/do-you-really-need-to-eject-a-usb-drive/ "CORSAIR Labo: Do You Really Need to Eject a USB Drive?"
[pioneerdj-support-xdjxz-partitionformats]: https://support.pioneerdj.com/hc/en-us/articles/4408364513817 "Pioneer DJ Help Center > All-In-One DJ Systems > XDJ-XZ > Connecting Devices & DJ Software > Storage device connection (SD, USB): The unit doesn't recognize some USB storage devices such as USB flash drives and HDDs. Why not?"
[pioneerdj-support-xdjrx3-partitionformats]: https://support.pioneerdj.com/hc/en-us/articles/4409211963289 "Pioneer DJ Help Center > All-In-One DJ Systems > XDJ-RX3 > Using my XDJ-RX3 > Browsing / Loading: I can't load music files in an HFS+ format USB storage device. Why not?"
[alphatheta-support-omnisduo-partitionformats-powerconsumption]: https://support.pioneerdj.com/hc/en-us/articles/27722453642649#:~:text=FAT32.-,The,provide "AlphaTheta Help Center > All-In-One DJ Systems > OMNIS-DUO > Connecting Devices and DJ Software > Storage device connection (SD, USB): The unit doesn't recognize some USB storage devices such as USB storage devices and HDDs. Why not?"
[alphatheta-support-xdjaz-partitionformats]: https://support.pioneerdj.com/hc/en-us/articles/38064747422745 "AlphaTheta DJ Help Center > All-In-One DJ Systems > XDJ-AZ > Connecting Devices and DJ Software > Storage device connection (SD, USB): The XDJ-AZ doesn't recognize some USB storage devices such as USB flash drives and HDDs. Why not?"
[alphatheta-support-cdj3000x-partitionformats]: https://support.pioneerdj.com/hc/en-us/articles/48479834944025 "AlphaTheta Help Center > DJ Players > CDJ-3000X > Ports and Connections > Storage device connection (USB): The unit doesn't recognize some USB storage devices such as USB flash drives and HDDs. Why not?"
[alphatheta-support-onelibrary-partitionformats]: https://support.pioneerdj.com/hc/en-us/articles/51301392931097 "AlphaTheta Help Center > OneLibrary > OneLibrary > Using my OneLibrary: What file formats are supported for USB storage devices when exporting with OneLibrary?"
