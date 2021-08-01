---
layout: post
title:  "Beginning my GSoC Journey"
date:   2021-05-31 10:08:01 +0530
comments: True
categories: GSoC'21
collectionpage: gsoc-1
feature: True
excerpt: "This is going to be an introductory blog where I will talk about the project on which I’ll be working this summer in GNOME Foundation."
---


*This was my reaction after finding out that I was selected for GSoC :)*

<div style="text-align:center">
<img src="https://media.giphy.com/media/b5LTssxCLpvVe/giphy.gif">
<p style="font-size: 15px;text-align:center">source: Giphy</p>
</div>

I am starting a new blog series, for covering my GSoC’21 journey with [GNOME Foundation](https://www.gnome.org/){:target="_blank"}. This is going to be an introductory blog where I will talk about the project on which I’ll be working this summer. Before we get started let me introduce myself to the folks reading from the GNOME planet. I am Nishit Patel, an undergraduate Computer Engineering student from India.

I began my pre GSoC journey back in November 2020 when I opened my first [MR](https://gitlab.gnome.org/GNOME/tracker/-/merge_requests/346) in tracker project. It was a small bug fix in the README.md file which I came across while setting up my local environment. Later, I began keeping a watch on the #tracker IRC and used to ask maintainers for help whenever I was stuck at something. Maintainers were very helpful and polite with their prompt replies even if I was asking some stupid question that was already addressed somewhere in the documentation. One thing that I noticed is it is better to first google, and check the docs before asking the question as it saves the maintainers precious time, and you also get to learn something new in the process.

## Project details

I will be working on the [Tracker-miner](https://wiki.gnome.org/Projects/Tracker/WhatIsTracker) project which is an indexer, and also used for extracting the metadata from different file formats. Tracker currently doesn’t store the creation time in the database as it was historically not tracked on UNIX file systems, and it’s not part of [POSIX specification](https://www.gnu.org/software/coreutils/manual/html_node/File-timestamps.html#:~:text=28%20File%20timestamps,to%20the%20file's%20meta%2Dinformation.). However, Since [kernel version 4.11](https://kernelnewbies.org/Linux_4.11) the new [statx](https://github.com/torvalds/linux/commit/a528d35) system call provides the file creation timestamp. Based on this, the project aims to provide the support of storing file creation time in the tracker database and later, provide the [feature](https://gitlab.gnome.org/GNOME/nautilus/-/issues/1761) of searching by creation time in Nautilus.


I will be writing short posts as and when I get time in between so


<div style="text-align:center">
<img src="https://media.giphy.com/media/kyLptBNdyMHftuqoNy/giphy.gif">
<p style="font-size: 15px;text-align:center">source: Giphy</p>
</div>
