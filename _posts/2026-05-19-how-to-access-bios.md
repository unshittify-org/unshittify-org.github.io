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

{% include figure popup=false image_path="/assets/images/Thinkpad-t430-bios-main-cc-by-sa.jpg" alt='A screen titled "ThinkPad Setup" with monospace text. A blue menu bar at the top has tabs for "Main", "Config", "Date/Time", "Security", "Startup" and "Restart". The "Main" tab is selected, and the screen shows information about the UEFI BIOS version and date, the controller version, and a variety of other information about the computer hardware.  The bottom of the screen includes indications for what keys to use for keyboard navigation of the menu.' caption='*Approximately* what your BIOS screen will look like - the menus may be in a different order or different place, but it will be able to access the same stuff. Blue, white, and black are typical colors, but your mileage may vary.' citation='<a href="https://commons.wikimedia.org/wiki/File:Thinkpad-t430-bios-main.jpg">Vitaly Zdanevich</a>, <a href="https://creativecommons.org/licenses/by-sa/4.0">CC BY-SA 4.0</a>, via Wikimedia Commons' %}

## Scope: Mac vs PC

This guide will be most helpful for **PC users** - people who use Windows, Unix, or Linux machines. However, Mac users should still review the [Boot Order](#boot-order) section.

Most Mac or Apple computers do not have an accessible BIOS. Macs use EFI, but most modern Macs have an entire separate EFI partition[^partition] and do not make it accessible to users.

**The Mac EFI partition is outside the scope of this guide.** Attempting to access and change the data in this partition is performed at the user's risk, and may cause irreparable damage to the device.
{:  .notice--danger}

## Access on PC

The BIOS menu is accessed during startup. There is usually a specific period during startup where you must press a specific key, which will tell the computer that it should load the BIOS menu.

This process is, unfortunately, different for different computer manufacturers.

Usually, you will:

* Turn your computer off
* Turn your computer on
* Press the button during startup.

For some manufacturers, you can press and hold the button.  For some manufacturers, you need to press it at a specific part of startup - the best way to do this is by mashing that button repeatedly.

The most common keys used to access BIOS are [Delete, F2, and F12, or another key shown during the first startup screen](https://www.tomshardware.com/reviews/bios-keys-to-access-your-firmware,5732.html). Apparently HP uses F10, and Lenovo uses F1.

If you can't get access to the BIOS screen, you can search "[Computer Model] BIOS Startup Keys" - if you can find your computer's manual or a reddit thread, it will tell you how to access BIOS.

### Special Access on Windows 10 and 11

On Windows 10 and 11, you can access the UEFI Firmware Settings from a special startup mode called a "Recovery Environment".  Windows has [several ways to access the recovery environment](https://support.microsoft.com/en-us/windows/windows-recovery-environment-0eb14733-6301-41cb-8d26-06a12b42770b),[^windows-recovery-archive] including:
* In the Settings Menu, in `System -> Recovery`, under `Recovery options`, the `Restart Now` button
* Pressing and holding the `SHIFT` button while selecting `Power -> Restart` in the Start menu
* A hardware recovery button available on some computers

When it loads into the recovery environment, select the `Troubleshoot` option, then the `UEFI Firmware Settings` option.  Reboot the computer, and the UEFI/BIOS menu will load.

{% include figure class="half" popup=false image_path="assets/images/recovery-environment-c-microsoft.png" alt='A blue screen titled "Choose an Option". Four options with related icons are available in two columns. The first column includes "Continue", "Use a device" and "Troubleshoot".  The second column contains "Turn off your PC"' citation='&copy; Microsoft 2026, Accessed 2026-05-2022 from Microsoft Support page "<a href="https://support.microsoft.com/en-us/windows/windows-recovery-environment-0eb14733-6301-41cb-8d26-06a12b42770b">Windows Recovery Environment</a>"' %}

{% include figure class="half" popup=false image_path="assets/images/recovery-troubleshooting-c-microsoft.png" alt='A blue screen titled "Advanced options". Six options with related itcons are available in two columns. The first of column includes "Startup Repair", "Startup Settings" and "Command Prompt".  The second column includes "Uninstall Updates", "UEFI Firmware Settings", and "System Restore".  There is a text-only option at the bottom of "See more recovery options".' citation='&copy; Microsoft 2026, Accessed 2026-05-2022 from Microsoft Support page "<a href="https://support.microsoft.com/en-us/windows/windows-recovery-environment-0eb14733-6301-41cb-8d26-06a12b42770b">Windows Recovery Environment</a>"' %}

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

The boot order decides the answers to those questions.

For security purposes, you normally want your computer to boot from the **hard drive** first, so that a malicious USB or CD won't immediately bork your computer.

But when you're _trying_ to install a new operating system, you _want_ to change your boot order so the **installation media** is booted first.

So let's get to the boot order menu.

#### PC Boot Order Menu

First, load the BIOS menu.

Then, navigate to a tab or menu that says "Startup" or "Boot Menu" or similar.  It may vary between manufacturers, but there _will_ be a menu for the boot order.

{% include figure popup=false image_path="/assets/images/Lenovo_ThinkPad_T470_UEFI_BIOS_1_75_setup_-_boot_menu_selection-cc-by-sa.JPG" alt='A laptop with a minimal menu using monospace code-style text.  The menu named "Startup" is selected, and "Network Boot" appears to be selected.  A blue box has a list of memory devices, including USB CD, several HDD options, and LAN options, and "PCI LAN" appears to be selected.  The right side of the screen includes the text "Item Specific Help" and "Select top priority of the "Boot Priority Order when waking up from LAN".' caption="What the boot menu looks like on a Lenovo ThinkPad. Your mileage may vary on different devices." citation='<a href="https://commons.wikimedia.org/wiki/File:Lenovo_ThinkPad_T470_UEFI_BIOS_1.75_setup_-_boot_menu_selection-cc-by-sa.JPG">Paowee</a>, <a href="https://creativecommons.org/licenses/by-sa/4.0">CC BY-SA 4.0</a>, via Wikimedia Commons' %}

Find the menu that allows you to change the "Boot Order" or "Boot Priority".

There will be a list of possible boot drives.  Some systems have you reorder them (often by selecting them and then using your up and down keys to move them in the list).  Other systems will just have you select the highest priority drive for it to use.

Read the information on the screen to figure out what your computer wants you to do.  Follow those instructions, and change the boot order so that the boot drive you want to use is first.

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
    It is functionally impossible to recover a bricked device.

[^windows-recovery-archive]: This information comes from the Microsoft Support documentation, and was accessed on May 22, 2026, from https://support.microsoft.com/en-us/windows/windows-recovery-environment-0eb14733-6301-41cb-8d26-06a12b42770b.  If the page is not available at time of viewing, it has been archived with [the Wayback Machine](https://web.archive.org/).