---
title: Metrics for our Priorities
draft: true
layout: single
header:
  overlay_color: "#000000"
  overlay_filter: 0.5
  overlay_image: /assets/images/MetricsHeader.png
  teaser: /assets/images/List_(89045)_-_The_Noun_Project.svg
tagline: >-
  What does it mean to be enshittified? What policies, features, and protections are we looking for when we try to find alternatives? <br /><br />
toc: true
toc_sticky: true
---
## Our Priorities

We judge the products and services we use, recommend, and disrecommend based on compliance with the following priorities.

### Freely Shared and Freely Accessed {#priority-free}

We prioritize supporting projects and products that are released openly and freely, or under licenses that encourage collaboration and access.

#### (F)OSS Software {#metrics-free-software}

Relevant to software products.

"FOSS" refers to Free <sup>as in Speech, not Beer</sup> and/or Open-Source software.
<table>
  <tr>
    <th>Ideal</th>
    <td>Software is distributed under an <a href="https://opensource.org/licenses" > Open Source Initiative</a> approved license.</td>
  </tr>
  <tr>
    <th>Acceptable</th>
    <td>Software is released as free binaries, or under a freeware license. <br><br> Available under a license that allows you to view and/or use the source code, but not modify it.</td>
  </tr>
  <tr>
    <th>Bad</th>
    <td>Software is only available under restrictive licenses. Source code is not accessible. Most commercial software is not (F)OSS. Any software with DRM is not (F)OSS.</td>
  </tr>
</table>

> <small>Note: This site is not affiliated with or endorsed by the <a href="https://opensource.org/licenses" > Open Source Initiative.</a></small>

#### Public Domain or Creative Commons Data {#metrics-free-data}

Relevant to text, images, and other non-software data.
<table>
  <tr>
    <th>Ideal</th>
    <td>Data is in the <span markdown="1">public domain[^PublicDomain]</span> or distributed under a <a href="https://creativecommons.org/share-your-work/cclicenses/" > Creative Commons or equivalent license</a>.</td>
  </tr>
  <tr>
    <th>Acceptable</th>
    <td> Data is available under freeware licenses or some non-restrictive paid licenses.</td>
  </tr>
  <tr>
    <th>Bad</th>
    <td>Data is distributed only under highly restrictive licenses.  Access is limited via DRM.</td>
  </tr>
</table>
[^PublicDomain]: Public Domain data may have become public domain by being categorically ineligible for copyright, by entering public domain due to age or lawsuit, or by being <a href="https://creativecommons.org/publicdomain/zero/1.0/" > dedicated to the public domain</a> by its creator(s).

#### Open-Source Hardware {#metrics-free-hardware}

Relevant to physical items and other hardware products.
<table>
  <!-- <tr>
    <th>Priority</th>
    <td><b>Public Domain or Creative Commons Data<br></b> <small>Text, images, and other non-software data</small></td>
  </tr> -->
  <tr>
    <th>Ideal</th>
    <td>Hardware is not patented, and/or is licensed for free and open recreation and modification.  For example, per the Open Source Hardware Definition <a href="https://oshwa.org/resources/open-source-hardware-definition/" > Open Source Hardware definition</a>  from the <a href="https://oshwa.org/about/" >Open Source Hardware Association (OSHWA)</a>. Data necessary to recreate and use hardware is free, accessible, and available per the<a href="#metrics-free-data"> Free Data metrics</a> and the <a href="#metrics-free-software"> Free Software metrics </a></td>
  </tr>
  <tr>
    <th>Acceptable</th>
    <td>Hardware is partially proprietary.  Information about its contents, manufacturing methods, maintenance processes, and the software needed for its use is available for purchase for free or at a reasonable price. </td>
  </tr>
  <tr>
    <th>Bad</th>
    <td>Hardware is proprietary.  Patent holder may aggressively litigate its patent protections. <br>Information about the hardware's contents, manufacturing methods, maintenance processes are unavailable to users or available only at high cost or under highly restrictive licenses.  The software needed to use the hardware is controlled via DRM, unavailable to users, or distributed under highly restrictive licenses.</td>
  </tr>
</table>

### User Ownership and Control {#priority-ownership}

We prioritize the user having ownership of the software and hardware that they use, and the ability to customize the settings and abilities of the products that they use.  Additionally, we prioritize the user having control over the types and amount of data they share with service providers.

#### Product Ownership {#metrics-product-owner}

Relevant to software and other products composed primarily of data
<table>
  <tr>
    <th>Ideal</th>
    <td>The user owns the product. They are able to freely give, loan, sell, trade, or modify their instance of the product at will (e.g. loaning a game to a friend, selling a DVD).</td>
  </tr>
  <tr>
    <th>Acceptable</th>
    <td>The user has a perpetual license for software products. The user can transfer the data between their own devices (e.g. moving software or music from one computer to another) at will.  The user can change the format of the data at will (e.g. ripping audio from a movie, printing out an ebook).Importantly, the user must be able to access or create a version of the product that the distributor does not have access to and cannot take away.</td>
  </tr>
  <tr>
    <th>Bad</th>
    <td>The user's access to the product is limited via DRM or other means. The distributor has the ability to remove the user's access to the product.
    Alternatively, the product is not a service, yet is only available via a subscription (i.e., the user's access to the product does not cause ongoing costs to the distributor that would justify charging a subscription, or the ongoing costs to the distributor are DRM-related or otherwise self-inflicted).</td>
  </tr>
</table>

#### Data Control {#metrics-data-control}

Relevant to personal data
<table>
  <tr>
    <th>Ideal</th>
    <td>No data exits the user's home network. Software that needs user data can be self-hosted.  Companies providing services or software do not request or collect user data.</td>
  </tr>
  <tr>
    <th>Acceptable</th>
    <td>Minimal data leaves the user's home network and is sent to external service providers.  Any data sent to external providers is anonymized to the greatest degree possible. Users have the ability to control what data is sent to external providers.</td>
  </tr>
  <tr>
    <th>Bad</th>
    <td>External providers require more data from the user than is necessary to provide the service. Data that is sent to external providers is not anonymized.  Users do not have the ability to limit data sent to external providers.</td>
  </tr>
</table>

#### Hardware Ownership {#metrics-hardware-owner}

Relevant to hardware.
<table>
  <tr>
    <th>Ideal</th>
    <td>Hardware is owned by the user.  User can freely give, sell, loan, trade, repair, or modify the hardware (within the limits of local law)</td>
  </tr>
  <tr>
    <th>Acceptable</th>
    <td>Hardware is leased to the user or otherwise provided by subscription. The lease or subscription does not have limitations on the usage of the hardware, and is overall beneficial to the user, both financially and practically.<br>
    The ongoing nature of the subscription is is well-justified by ongoing non-hardware services such as technical support, high-priority repair services, and/or free supplies. The total cost of the subscription over the lifetime of the hardware is less than the cost of the hardware (including supplies provided during the subscription).</td>
  </tr>
  <tr>
    <th>Bad</th>
    <td>Hardware is leased to the user or otherwise provided by subscription.  There is little or no service provided to the user to justify the lease or subscription, or the ongoing cost is exploitative.<br>
    Alternatively, the user technically owns the hardware, but the allowed use of the hardware is limited by distributor. The distributor may use DRM to lock the device to a specific user and prevent resale, or to lock a feature behind a subscription - both of these practices may mean the hardware is nonfunctional if it does not have internet access. In other cases, identical hardware may be sold as two different models, at two different prices, with locked-down software deactivating some features for the lower priced model. In rare cases, the limitation on the hardware usage may be contractual, rather than practical.<br>
</td>
  </tr>
</table>

#### Right To Repair {#metrics-hardware-repair}

Relevant to hardware.
<table>
  <tr>
    <th>Ideal</th>
    <td>Hardware is designed to be repairable at low cost and skill. All parts and tools required to repair the hardware are readily available from multiple suppliers and are non-proprietary. Instructions for repairs are free and easily accessible.</td>
  </tr>
  <tr>
    <th>Acceptable</th>
    <td>Hardware is mostly repairable, but may require equipment, tools, or knowledge that laypeople do not usually have.  Independent hardware repair does not void the manufacturer's warranty.<br>
    The design may include some proprietary parts which are available at reasonable prices from the manufacturer, and which have alternatives available from vendors other than the manufacturer or distributor.<br>
    Low-cost or expendable hardware might be unrepairable, but must be available at a low cost from multiple suppliers, or available for replacement for free or at-cost from the manufacturer or distributor.</td>
  </tr>
  <tr>
    <th>Bad</th>
    <td>Hardware is intentionally designed to not be repairable (e.g. parts are glued or welded), or is designed for repairs to require specialty tools and equipment (e.g., brand-specific security screws). Repairs may only be performed by authorized repair facilities (e.g. unauthorized repairs void the device warranty), using proprietary parts (e.g. unregistered serial numbers on replacement parts lead to arbitrary features of the device being disabled). The manufacturer or distributor actively fights customers' right to repair their hardware.<br>
</td>
  </tr>
</table>
