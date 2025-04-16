---
# You don't need to edit this file, it's empty on purpose.
# Edit theme's home layout instead if you wanna make some changes
# See: https://jekyllrb.com/docs/themes/#overriding-theme-defaults
# layout: splash
author_profile: true
title: "Unshittify Your Stuff"
layout: splash
# permalink: /splash-page/
# date: 2016-03-23T11:48:41-04:00
header:
  overlay_color: "#000"
  overlay_filter: "0.5"
#   overlay_image: /assets/logos/Header.png
  actions:
    - label: "Our Goals"
      url: "/mission-statement/"
    - label: "About the Authors"
      url: "/about/"
#   caption: "Photo credit: [**Unsplash**](https://unsplash.com)"
excerpt: "Resources, links, and discussion to help you reclaim your life from enshittification."
intro: 
  - excerpt: "Companies are squeezing every penny of profit out of us, at the expense of our convenience, privacy, and control. \n \n We don't have to let them."
feature_row:
  - image_path: assets/logos/Header.png
    # image_caption: "Image courtesy of [Unsplash](https://unsplash.com/)"
    alt: "placeholder image 1"
    title: "Our Home"
    excerpt: "A blog discussing the work we've done to counter the enshittification in our home."
  - image_path: assets/logos/Header.png
    alt: "placeholder image 2"
    title: "The Outhouse"
    excerpt: "Companies, services, and products that suffer from enshittification or regressive social policies - and what we suggest you use instead."
    url: "#test-link"
    btn_label: "Read More"
    btn_class: "btn--primary"
  - image_path: assets/logos/Header.png
    title: "Product and Company Standards"
    excerpt: "What we look for in the products and companies that we recommend."
feature_row2:
  - image_path: /assets/images/unsplash-gallery-image-2-th.jpg
    alt: "placeholder image 2"
    title: "Placeholder Image Left Aligned"
    excerpt: 'This is some sample content that goes here with **Markdown** formatting. Left aligned with `type="left"`'
    url: "#test-link"
    btn_label: "Read More"
    btn_class: "btn--primary"
feature_row3:
  - image_path: /assets/images/unsplash-gallery-image-2-th.jpg
    alt: "placeholder image 2"
    title: "Placeholder Image Right Aligned"
    excerpt: 'This is some sample content that goes here with **Markdown** formatting. Right aligned with `type="right"`'
    url: "#test-link"
    btn_label: "Read More"
    btn_class: "btn--primary"
feature_row4:
  - image_path: /assets/images/unsplash-gallery-image-2-th.jpg
    alt: "placeholder image 2"
    title: "Placeholder Image Center Aligned"
    excerpt: 'This is some sample content that goes here with **Markdown** formatting. Centered with `type="center"`'
    url: "#test-link"
    btn_label: "Read More"
    btn_class: "btn--primary"
---

{% include feature_row id="intro" type="center" %}

{% include feature_row %}

{% include feature_row id="feature_row2" type="left" %}

{% include feature_row id="feature_row3" type="right" %}

{% include feature_row id="feature_row4" type="center" %}
