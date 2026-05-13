---
title: "The First USB Raid Problems"
author: "Tatiana"
excerpt_separator: "<!--more-->"
categories:
  - Blog
tags:
  - troubleshooting
  - plans
  - raid
  - power
date: 2026-05-12
---

A short blog post today, because we have had an odd issue, with a simple solution.

This morning[^at-time-of-writing], Sonarr and Radarr could not access our hard drives.  The hard drives were still there, still running, and still available, but for some reason our Docker containers couldn't access them.

Luckily, we _think_ this won't be too hard to fix.

<!--more-->

## The Background {#test-id}

For anyone new here[^coming-soon], we're running a NAS[^nas] on Overkill - my old, off-brand laptop from 2017.  It has an internal hard drive, but most of our storage is a set of external hard drives, configured for RAID[^raid], connected via two USB HDD bays.

That USB data transfer is the weird part of our system.  Most consumer hard drives connect via SATA - a data transfer standard - but Overkill doesn't have any available SATA ports to connect to.

Overkill _does_ have plenty of USB ports.  So we bought a pair of USB two-bay hard-drive docks, and are using them.  It does decrease the maximum read-write speed, and most folks online suggest *against* using RAID over USB for a variety of reasons, but this was a cheap, reasonable option, and Jude has the expertise to mitigate problems.

And problems we have found.

## The Symptoms

We have a very limited list of symptoms.

1. This morning, Docker containers running on the internal hard drive (namely, the ones running Radarr and Sonarr) could not access the hard drives in our RAID array.
2. From the command line, Jude could verify that the hard drives were still present and reachable.
3. All drives in the RAID array passed their [SMART testing](https://en.wikipedia.org/wiki/Self-Monitoring,_Analysis_and_Reporting_Technology) (the internal monitoring system on the hard drives), indicating that the drives were undamaged.

## The Theory

We think that a power fluctuation caused this problem.

Unfortunately, one of the reasons you shouldn't use RAID over USB is because the USB docks are sensitive to power fluctuations.  Power over USB isn't enough for the docks to run the hard drives, and that often causes damage to the drives.

We had mitigated this problem by powering these docks with their own power cables, plugged into the power strip that we ran for Overkill.

But we did _not_ include a UPS[^ups] between the computer, the hard drives, and the wall.

Our theory is that last night, our house experienced a brownout, power dip, or other power flicker, which momentarily underpowered the dock, momentarily closing its data connection to Overkill.
{:.notice}

Our house is in an area prone to power outages, and we get power dips and power flickers fairly regularly.  Our UPS downstairs was giving some weird beeps yesterday evening.  Even though we didn't visibly see a brownout happen, we suspect that means there was a power fluctuation.

If Overkill lost connection to the RAID array, then the Docker containers running on Overkill's local drive would have lost access to them too - and likely didn't have a way to reconnect to them once they were available.

### Luckiest Family in the Universe

If this is accurate, then we were very lucky - a serious power fluctuation on running drives can damage them badly, but ours are fine.

This means one of three things:
1. The power fluctuation was small enough that it affected the docks' ability to connect to Overkill, but not the ability to run the hard drives.
2. The power fluctuation may have stopped the docks from running the hard drives, but it happened while there were no read or write commands, so the hard drives were not running and were not damaged by the sudden power loss.
3. Our theory is wrong.

We don't have another theory, so we're going to thank our lucky stars, acknowledge that we were **very dumb** for not putting this system on a UPS, and do some work to prevent relying on luck in the future.

## The Plan

We have 3 parts to this plan.

### Short Term - UPS

We're going to put Overkill and the hard drive docks onto a UPS.  We want them to have a nice, stable power source.  If the power goes out, the UPS will yell, and we can safely shut down Overkill ourselves.

This will hopefully prevent data loss.

### Medium Term - Backup Systems

We're still working on a 3-2-1 backup system.  That means 3 copies of the data, in 2 different formats, with 1 copy offsite.

There's a reason Overkill's drive is named `fragile:\`.  We don't have that set up yet.

We've purchased some 16 TB hard drives for a full backup system, and we're working on a cloud solution as well.  We'll update when we have this finished.

This wil protect us when we _do_ have data loss.

### Long-Term - Monitoring

We already want to add monitoring to Overkill[^coming-soon2].  We're expanding that plan to include UPS monitoring.

If the UPS activates, we want Overkill to immediately cancel any read/write commands to the external hard drives.

If the UPS gets below 50%, we want Overkill to safely shut down. 

This may require a new UPS.  We're still looking into it.  We'll update as we have more info on this.

This would automate our protection.

## Conclusion

Like I mentioned, the internet warns against using USB docks for RAID arrays of hard drives.  We're doing it with the full knowledge that it could all come crashing down.

But we do think we can make it work.

And if adding a UPS doesn't prevent this issue, we'll try something else.

---
[^at-time-of-writing]: At time of writing.

[^coming-soon]: Or for anyone who visited this page _before_ we have the rest of the blog posts up.  Once they're ready, we'll link to our series about setting up our NAS.  But this was too interesting to wait on.

[^nas]: **Network-Attached Storage**:  It's storage you can access from your computer, but is stored in a server or similar.  If you have a Dropbox folder on your computer, it's that same sort of concept.  If you've ever had a school or company server that you need to be connected to their WiFi to access, you've definitely interacted with a NAS.

[^raid]:  **Redundant Array of Independent Disks**:  Several hard drives working together to act like a single, larger hard drive.  Usually (and in our case) set up so that if any one hard drive fails, the data can still be recovered and rebuilt. 

[^ups]: **Uninterruptible Power Supply**: A UPS is ssentially a power strip with a battery and a surge protector. If the power ever goes out, the UPS keeps providing power to the devices plugged into it, and usually starts beeping.  They come in a variety of sizes, from "just enough stored power to let you turn the computer off safely" to "big enough to keep everything charged for a couple days.  <br>
    We own two UPSs - one for downstairs and one for upstairs.  They're each about the size of a car battery.  The one upstairs will keep our router on most of a day, so we can use the internet if it's still available.  The one downstairs charges our entire family's phones and tablets.

[^coming-soon2]: Coming soon.  Will update with links when available.