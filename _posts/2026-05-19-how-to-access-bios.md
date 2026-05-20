---
title: "How To Access BIOS or UEFI"
excerpt_separator: "<!--more-->"
categories:
  - How-To
tags:
  - Series Intro
  - Computer Maintenance
  - Beginners
  - BIOS
date: 2026-05-19
is_series: true
series_title: "Computer Maintenance"
series_number: 10 ## Use BASIC-style numbering, where each post's number increments by 10, to allow for insertion of intermediate posts without renumbering.  https://en.wikipedia.org/wiki/Line_number#Line_numbers_and_style
---

[BIOS](https://en.wikipedia.org/wiki/BIOS) stands for **Basic Input/Output System**.  A modern verion is [UEFI](https://en.wikipedia.org/wiki/UEFI), the "Unified Extensible Firmware Interface". In essence, both BIOS and UEFI are software that manage very basic hardware processes of your computer.

<!--more-->

We'll be referring to this firmware as "BIOS" for consistency, even though most computers nowadays use UEFI.[^cmos]



## Scope: Mac vs PC

This guide will be most helpful for **PC users** - people who use Windows, Unix, or Linux machines. However, Mac users should still review the [Boot Order](#boot-order) section.

Most Mac or Apple computers do not have an accessible BIOS. Macs use EFI, but most modern Macs have an entire separate EFI partition[^partition] and do not make it accessible to users.

**The Mac EFI partition is outside the scope of this guide.** Attempting to access and change the data in this partition is performed at the user's risk, and may cause irreparable damage to the device.
{:  .notice--danger}

## Access

The BIOS menu is accessed during startup. There is usually a specific period during startup where you must press a specific key, which will tell the computer that it should load the BIOS menu.

This process is, unfortunately, different for different computer manufacturers.

Usually, you will:

* Turn your computer off
* Turn your computer on
* Press the button during startup.

For some manufacturers, you can press and hold the button.  For some manufacturers, you need to press it at a specific part of startup - the best way to do this is by mashing that button repeatedly.

The most common keys used to access BIOS are [Delete, F2, and F12, or another key shown during the first startup screen](https://www.tomshardware.com/reviews/bios-keys-to-access-your-firmware,5732.html). Apparently HP uses F10, and Lenovo uses F1.

If you can't get access to the BIOS screen, you can search "[Computer Model] BIOS Startup Keys" - if you can find your computer's manual or a reddit thread, it will tell you how to access BIOS.

## Common Usage

Most people will never use the BIOS menu.  We're going to ask you to use it for a few things.

<div markdown="1" class="notice--warning">
### WARNING: The BIOS menu will not stop you from doing something stupid.

It is possible to make changes in BIOS that will permanently brick[^brick] your computer.

Do not make changes in BIOS that you do not completely understand the ramifications of. 
</div>

### Boot Order

Adjusting the boot order is the most common reason we will ask you to access your BIOS menu.

If you have a Windows partition and a Linux partition[^partition], which one will your computer load by default? If you insert a CD that installs an operating system, will it load your existing OS, or will it try to install the new one?

Adjusting the boot order lets you decide the answers to those questions.

For security purposes, you want your computer to boot from the hard drive first, so that a malicious USB or CD won't immediately bork your computer.

But when you're _trying_ to install a new operating system, you want to change your boot order so the installation media is booted first.

#### PC Boot Order Menu
/assets/images/bios-boot-device.png

#### Mac Boot Order Menu

Blah

### Other Uses

The BIOS menu allows you to access a variety of useful information and settings for your computer.



The BIOS menu lets you manage your computer at a very high level, e.g.:

* Enable or disabling components (e.g., your mouse, keyboard, audio chip, network inferface)
* Set the boot order
* Monitor your hardware
* Boot into safe mode (on some computers)

---

[^partition]: A partition is a section of a hard drive or memory system.  Every hard drive has at least one partition - that's what makes it usable.  Adding an extra partition allows you to separate some data and functionality, while keeping it on the same physical disc. <br>
    Mac keeps their BIOS data on a partition you can't easily access.<br>
    You might put a second operating system on a partition of your hard drive, so you can use one computer on Windows some days, and on Linux other days.

[^cmos]: You may also hear people refer to "CMOS" in the context of BIOS - [CMOS](https://en.wikipedia.org/wiki/Nonvolatile_BIOS_memory) is the type of chip that holds the BIOS data. This isn't important in the context of this post, but is good to know about in case you come across it in the wild.

[^brick]: To brick a device is to render it completely inoperable. The device is, functionally, just a brick. It's a hunk of dead weight on your desk, not an actual useful electronic device any more. <br>
    It is impossible to recover a bricked device.