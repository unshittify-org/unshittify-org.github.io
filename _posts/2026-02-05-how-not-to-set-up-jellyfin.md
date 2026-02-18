---
title: "How NOT to set up Jellyfin"
excerpt_separator: "<!--more-->"
# excerpt: '"A doddering old fool thinks he knows better than Debian distributors" -Jude'
categories:
  - How-To
tags:
  - Failures
  - Experiments
  - Jellyfin
  - OpenMediaVault
date: 2026-02-09
---
> A doddering old fool thinks he knows better than Debian distributors

> **Jude**

We were really hoping we would get to set up our media server and NAS this week.  That...did not happen.

But every DIY project has the occasional failure.  We may as well share this one, so you don't try to make the same mistakes as us.

<!--more-->

## The Goal

Convert an old laptop to a media server, as a start to replacing our Fire TV Stick.

## Hardware

The hardware we're using is an old laptop from Eluktronics, with the following specs:

* GPU: NVIDIA GeForce GTX 1060
* CPU: Intel Core i7-7700HQ Quad Core
* RAM: 32 GB DDR4
* Boot Drive: 1 TB M.2 SSD
* Secondary Hard Disk: 1 TB 2.5" SATA III

This laptop is from 2017.  Its name is Overkill.

We also have QTY 4 of Western Digital's 4TB Red NAS 3.5" HDDs.  This is what we want to use as storage for our NAS long-term, but we don't have a dock or enclosure for them, so for now, we have to make do with the two 1TB hard drives already housed in Overkill.

## Considerations

We already know we want to use Jellyfin for our media server.

Reddit suggests one of three services/Operating Systems for NAS management for Jellyfin:  UnRAID, TrueNAS, or OpenMediaVault.

### Not using UnRAID or TrueNAS
UnRAID requires a one-time payment, which is better than a subscription, but still isn't something we want to do.

As of February 5, TrueNAS has two software suites, one that's free and Open Source, and one that's a paid enterprise subscription. This would be okay, since the primary difference _was_ premium support initially, but it appears that they're starting to move previously free features and incoming updates behind a paywall. We at Unshittify aren't a huge fan of segregated features in the first place, and we fear this is a sign of further enshittification to come.  So we're not going to suggest or try TrueNAS right now.

### OpenMediaVault

That leaves OpenMediaVault.

It has a lot going for it.  It's an OS based on Debian with the GPLv3 License, so it's FOSS with Copyleft protections. It comes with the easy configuration we need for the media management systems we want to make and use.

But OpenMediaVault (OMV) is _also_ is very opinionated - if it detects that you're using a Graphical User Interface (GUI) (as opposed to a command line interface (CLI)), it will refuse to install.  If you somehow manage to install it, but you have a GUI,[^graphical] it will then refuse to run.

This is annoying, but it has understandable reasons behind it.
- OMV should really run on a dedicated machine.  
    - Requiring a CLI prevents users from running it on their general purpose machine, or their daily driver laptop or PC, since most of those are GUIs.
- Requiring a CLI is a big red flashing sign saying "If you are not comfortable using the command line, you are not ready to install this OS.  You need to learn more before you try to do this."
    - I know: This sounds kind of elitist.  It sounds like gatekeeping.  I promise, it's not just an arbitrary blockade.
    - Maintaining a system that runs on OMV does require some amount of technical literacy.  So you'll either need to learn those skills to use OMV, or find another NAS/Media Server option that you already have skills for.  
    - The CLI requirement doesn't prevent people who are less experienced from figuring it out and running it. But will make someone who is really out of their depth pause for a second before they dive into the cold, black depths.
    - We want people to learn, that's part of why we're documenting our work.  And hopefully these posts will help make this marginally more accessible to folks who otherwise wouldn't have the skills to manage an OMV system.

As for us, we're lucky.  We have a dedicated machine, and Jude has extensive experience with Debian. Tatiana has significantly less experience with CLIs, but is capable.[^averageuser]  But we had other circumstances that made OMV less attractive at the start of this process.

#### OMV Problems

We didn't have all of our equipment ready - specifically, the fact that we were missing the Hard Drive bays for our WD Reds.  If we tried to set up OMV as Overkill's OS, it would only see the internal SSD (which is being used as a boot drive) and the internal HDD (which we are tentatively using as fragile storage).

But without the external hard drives, we don't have enough drives to set up in a RAID array.  And that means we'd be setting up OMV without RAID.  That's less than ideal, and we were worried that it would be tough to reconfigure it with RAID drives later.

We also kind of wanted a GUI.  Tatiana is more comfortable with a GUI, and we suspect some of the readers would be more comfortable with a GUI.

And more importantly, having a GUI would allow us to do _all_ the setup on Overkill.  Yes, OMV is designed to install on a system that uses a CLI, not a GUI.  But the services that OMV packages together have some configuration that is performed via webapp.  So as designed, once we install and do initial setup on Overkill, we'd have to switch to another device, log into the web interface, and finish the configuration there.  That's annoying.

So instead of installing OMV, we decided to. . . install OMV.  Kind of.

Most of what OMV does is install a list of packages.  For the most part[^foreshadowing], you can do that.  It's more tedious, but it gives you more control.  And then we can use the webapps on Overkill.

So that's what we did.  And my god it was tedious.

## Software

We installed the newest stable version of Debian[^setup] (which has a GUI), then started setting up the tools that OMV would normally install.

This was a somewhat recursive process - identify a package we need, try to install.  If it needs dependencies, try to install those.  Repeat until it works, then move on to the next package.

The main ones we knew we needed had decent install instructions, and were:
* [mdadm](https://ruan.dev/blog/2022/06/29/create-a-raid5-array-with-mdadm-on-linux) for RAID[^raid] management
* [SaMBa and NFS](https://www.siberoloji.com/how-to-set-up-network-attached-storage-nas-in-debian-12-bookworm-system/)[^samba] for NAS[^nas] setup
* [Jellyfin](https://linuxcapable.com/how-to-install-jellyfin-on-debian-linux/), for media management

### The NAS Testing Plan

The plan was simple.  We were going to use our Mac upstairs to rip episodes of the *Angelic Layer* anime from our DVDs, then upload it to the media drive on Overkill that we configured with SaMBa and NFS.[^samba]

That didn't happen how we expected.

### The First Hurdle - No Upload

First, Jellyfin doesn't have an upload function.  What?

Frustrating, but possible to overcome and troubleshoot later.  For now, I'm sure we can just manually copy the files onto Overkill, right?

### The Second Hurdle - No NAS

Apparently, we didn't set up SaMBa right.

Theoretically speaking, SaMBa should've turned Overkill into a NAS, and should've made it so that the other computers in our house could access Overkill's storage.

We wanted to mount Overkill's drives as a virtual drive on our Mac (which was on the same wifi network).  Then, on that second computer, we would just drag-and-drop copy our files over to Overkill's storage.

Except, for some reason, the Mac couldn't see Overkill's drives.  We tried to connect to Overkill, but it requested a login that we weren't expecting, blocking our attempt to mount the drive.

Admittedly, this was probably entirely our fault - we think we didn't configure SaMBa correctly.

We have _not_ gathered the energy to try to fix this yet.

### The Third Hurdle - Torrenting Stack Complications

So let's back up. Adding new media should still be possible.  Overkill just has to handle getting it.

We _could_ manually rip disks, or we could use rips that someone else have made.[^ripvspirate].

How hard can it be to make that happen?

Well, over the course of 3 hours, Jude was able to:
* Install qBittorrent to manage the torrent protocol for downloads
    * Easy!  Success!
* Get Sonarr installed, to search for torrents of tv series
    * Hard.  Boo.
    * This package was broken, and we had to install it from a _script_
* Spend 90 minutes fighting to install [nzbget](https://nzbget.net/), to try to search through torrents on UseNet.
    * Awful.  Boooooo.  Ultimately unneccessary.
    * nzbget is _not_ a good Debian citizen.  Installing it was awful.
    * Good news! UseNet still exists!
    * Bad news! UseNet costs $100/year to use!
    * It's installed, but we ain't dealing with this.
* Install Prowlarr, to search through torrents
    * Very difficult.  Still a success.  Meh.  Boo.
    * This did not have a script to download it, but theoretically it shouldn't be too hard to install it _manually_.
    * It was incredibly hard to install it manually.  Installation, setting up a configuration, building an init script - it all took time and effort.
    * It eventually worked.

With this stack - Sonarr, Prowlarr, and qBittorrent - we were successfully able to find _Angelic Layer_!

But before we download it, we want get this set up in a way that will be easy for our users to request media.

### The Stumbling Block - Jellyseerr

[Jellyseerr](https://docs.seerr.dev/) is a service that allows Jellyfin users to request media to be added to the Jellyfin server.  The user can go to the webapp to search and request a show that they don't want to bother ripping, then those services we picked above to manage torrents will find it, download it, and organize it into our Jellyfin server. 

We picked qBittorrent, Sonarr, and Prowlarr because they integrate seamlessly with Jellyseerr.

Perfect.

Except, Jellyseerr is experimental. **There isn't a *good* way to install it on Debian**.

Jellyseerr doesn't have a Debian installer.  It doesn't have a community-made installation script.

There are exactly two ways to install Jellyseer (on Debian).  And we don't like either.

#### 1. A Docker Container

Neither Jude nor Tatiana are particularly familiar with Docker.  We don't want to deal with that.

Besides, if we were going to install Jellyseer with Docker, we should've just installed the entire stack with Docker.[^sunkcost]

#### 2. Build it from source

Building Jellyseerr from source requires Node 22.  Debian only supports up to Node 20.

We could still make it work - we could make our own build environment.  But we'd want redundancy.  And we'd want revision control.  

We'd want all sorts of customization to our build and dev environment that would make this system robust, safe, and unique to our needs - all things that Jude has the knowledge to do because of his decades of work. But it would also make it difficult to explain, difficult to share, difficult to get help with, and difficult to keep up-to-date.

We wouldn't even be able to get support from the Jellyseer community.

Building Jellyseer from source and maintaining it afterwards would be a project in and of itself.  One that would take away from the rest of the media server project - which for us includes the documentation we make for this website (which, again, building from source would make significantly more complicated).

## No.

No.  We're not doing this.  It's been 2 weeks since we started working on Overkill - admittedly in between family emergencies, but still. We've been running face first into wall after wall after wall, and after every broken nose, we're making it harder for other people to help us the next time. We're hitting the Sunk Cost Fallacy, and we're not falling for it.

We _could_ build Jellyfin from source to hit a Minimum Viable Product.  It's possible.  

But there is no good way for us to teach that process here.  Jude has seen first-hand that it takes about 3 months of consistent teaching for a student to become proficient in a build/development environment. We cannot expect to put out a "How to build Jellyseerr from Source" article that will let someone else naiively follow along, and expect to have a successful build at the end.

We can't do y'all justice by doing something too hard for anyone else to duplicate.  And we can't do ourselves justice by making a system that is more hassle to maintain than benefit to use.

## The Plan

We're starting over.

We're going to reimage Overkill, and install OpenMediaVault[^OMV-AI]. We'll deal with using our Macs and other laptops for the Web UI configuration.

We're gonna use the Docker Compose All-in-One to install Jellyfin, and it will include _everything_ we spent 2 weeks setting up the first time around.  We'll have to learn more about Docker, but between Jude and Tatiana we have enough to get started, and Docker is already _extremely_ well-documented, with lots of resources to help us learn.

We will use the systems that everyone has been saying we should use.  We'll follow the guides that already exist.

And we'll be able to document what we've done, what went wrong, and what went well.

There are tools available to help us climb over the walls and sweep away the stumbling blocks.  We're dang well going to use them this time.

---
[^graphical]: A graphical Interface has a screen with icons that you click on.  You usually interact with it primarily with a mouse.  Windows and Mac use graphical interfaces.  This is the type of interface the average person uses on their regular computer. <br><br>
    The alternative is a [Command Line Interface (CLI)](https://en.wikipedia.org/wiki/Command-line_interface). You type instructions for the computer to do.  You may have light experience with this in the form of text adventure games like Zork.  If not, just imagine the cool hacker guy in a spy movie typing fast with the text projecting on his face.  That's a CLI.

[^averageuser]: As always, Tatiana will be your "straight man" for this story, despite the fact that I am neither of those. Any questions I had during this process, I assume the readers will have, too.

[^foreshadowing]: You're not going to get exactly the same thing, and you'll probably have to do some compiling on your own, but you _should_ be able to get a fully working NAS at the end of the work. <br>
    This footnote has absolutely no foreshadowing in it.

[^setup]: For the techy folks: Debian 13 on a USB boot disk.  We used LVM, installing only 80% of the SSD, and saving the other 20% for future expansion and swap usage.  We used server partitioning (`/srv` instead of `/home`, with a small swap).  And we chose to use XFCE over Gnome, added an SSH server, and declined any Debian blend.

[^raid]: For those who don't know, RAID is a way to put data on multiple hard drives, so some of the hard drives can fail without losing any of the data. That being said, [RAID is not a backup](https://www.raidisnotabackup.com/) 

[^nas]: Network Accessible Storage.  

[^samba]: SaMBa is a service that runs on server hardware, that allows the server to share its drives over the network.  A user will install a virtual drive, and can then access the server's drive over the network - like adding a Dropbox folder to your computer (though, Dropbox has additional features not included in SaMBa). SaMBa should theoretically let the NAS running it act like the Dropbox servers - giving users remote access to them.

[^ripvspirate]: I am not a lawyer.  Even if I was a lawyer, I am not _your_ lawyer.  By our understanding, you have a right to create and keep copies of the media you own, for your own personal use.  Downloading a digital copy of that media, for your personal use, is theoretically equivalent to that, but the case law is less settled.  Distribution of that media is pretty firmly disallowed by copyright law.  Be aware of your local laws.

[^sunkcost]: Do I hear the [Sunk Cost Fallacy](https://youtu.be/n4wDmjEn8Vo?si=JZ0Xwubf3cIi1xhq&t=1675) anyone?

[^OMV-AI]: **This disclosure is included on February 9, 2026 per our [AI Usage Policy](about/../../_about/ethics-statement.md#ai-usage-policy)**: The background image of the OpenMediaVault's main login screen is an AI-generated image, generated by the lead dev of the project.  There is a toggle in the settings hide the image. <br>
    This image is the only use of generative AI in OpenMediaVault as far as we can tell, and generative AI is not used in the underlying functional software. We still believe that OpenMediaVault is the best option for us, so we will be changing our login background to remove the AI generated image, **because we do not approve of the use of generative AI to replace human art**. <br>
    If OpenMediaVault is updated to remove the AI generated images, we will remove this disclosure.  If we find that OpenMediaVault uses generative AI in other ways that do not comply with our AI Usage Policy, we will likely switch software.
