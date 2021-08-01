---
layout: post
title:  "GSoC Project update part I"
date:   2021-06-29 10:08:01 +0530
comments: True
categories: GSoC'21
collectionpage: gsoc-2
feature: False
excerpt: "Weekly update of GSoC'21 project. Include's work done on week 1, 2 and 3."
---


This is a weekly update of my GSoC project.

### Week 1

Following the proposed schedule, I began working on the first milestone, i.e Adding support for creation time in tracker-miners. While building the tracker-miner I discovered crashes in the indexer. After taking some help from mentors and debugging,
It was found that a double-free bug in the indexer was causing the crash. As the piece of code was unused, it went unnoticed.

*Merge Requests*: [!440](https://gitlab.gnome.org/GNOME/tracker/-/merge_requests/440)

### Week 2

During 2nd week, Most of the time was spent writing code. I was also working on resolving threads in the merge requests which were opened before GSoC.

*Merge Requests*: [!327](https://gitlab.gnome.org/GNOME/tracker-miners/-/merge_requests/327)

### Week 3

Opend Draft MR for the first milestone, and fixed some of the coverity warnings which were introduced after merging [!327](https://gitlab.gnome.org/GNOME/tracker-miners/-/merge_requests/327).

*Merge Requests*:
[!336](https://gitlab.gnome.org/GNOME/tracker-miners/-/merge_requests/336),
 [!340](https://gitlab.gnome.org/GNOME/tracker-miners/-/merge_requests/340)
