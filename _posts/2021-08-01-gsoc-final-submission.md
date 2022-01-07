---
layout: post
title:  "GSoC final submission"
date:   2021-08-21 12:08:01 +0530
comments: True
categories: GSoC'21
collectionpage: gsoc-4
feature: False
excerpt: "It has been a great journey working on the Tracker project. In the past 10 weeks I got to learn a lot about the project and its architecture ..."
---

It has been a great journey working on the Tracker project. In the past 10 weeks, I got to learn a lot about the project and its architecture. This is the final submission of the project. For the weekly updates, check out my previous posts [here](https://www.nishitpatel.tech/categories#gsoc-21).

### Proposed project goals 

:heavy_check_mark: Add support of file-creation time in Tracker-miners.  
:heavy_check_mark: Add feature of search by file-creation time in Nautilus.  
:heavy_check_mark: Improve nautilus-search engine tests suite.

### Contributions {#contributions}

Major contributions were done in [Tracker-miners](https://gitlab.gnome.org/GNOME/tracker-miners) and [Nautilus](https://gitlab.gnome.org/GNOME/nautilus) projects during the coding period.


#### Add support of file-creation time in Tracker-miners

This was the major primary goal of the project. After adding this feature, Tracker-miners now supports storing and querying file-creation time. While working on this feature, I also discovered and eventually fixed a double free bug in the indexer.

*Pull Requests* 
[!440 (Merged)](https://gitlab.gnome.org/GNOME/tracker/-/merge_requests/440), 
[!340 (Merged)](https://gitlab.gnome.org/GNOME/tracker-miners/-/merge_requests/340)

*Issues* 
[#158 (Closed)](https://gitlab.gnome.org/GNOME/tracker-miners/-/issues/158)

#### Add feature of search by file-creation time in Nautilus

This feature depends on previous work done in Tracker-miners. After adding this feature, Nautilus now supports searching files by file-creation time.

*Pull Requests* 
[!693 (Merged)](https://gitlab.gnome.org/GNOME/nautilus/-/merge_requests/693)

*Issues* 
[#1761 (Closed)](https://gitlab.gnome.org/GNOME/nautilus/-/issues/1761)

#### Improve nautilus-search engine tests suite.

Initially, there were only two proposed goals. After having chat with the mentors, we decided to extend the project by adding one more goal to improve the nautilus-search engine test suite. While writing tests I found a bug in the nautilus-tracker-search-engine due to improper date-time format. After fixing this bug, I added tests for searching files by modification and access time in all search engines.

*Pull Requests* 
[!697 (Merged)](https://gitlab.gnome.org/GNOME/nautilus/-/merge_requests/697), 
[!701 (Open under review)](https://gitlab.gnome.org/GNOME/nautilus/-/merge_requests/701)

*Issues* 
[#1933 (Closed)](https://gitlab.gnome.org/GNOME/nautilus/-/issues/1933)

#### Other miscellaneous contributions

This work was done during the GSoC period but is not part of the project goals.

*Pull Requests*
[!446 (Merged)](https://gitlab.gnome.org/GNOME/tracker/-/merge_requests/446), 
[!336 (Merged)](https://gitlab.gnome.org/GNOME/tracker-miners/-/merge_requests/336)


*Issues* 
[#317 (Closed)](https://gitlab.gnome.org/GNOME/tracker/-/issues/317)

#### Future Goals

Resolve any unresolved threads in the open Merge Requests. Write more tests for search by file creation time in Nautilus. Continue contributing to the projects.

#### Closing thoughts

It was an amazing experience working in GNOME Community. I would like to thank my mentors [Carlos](https://gitlab.gnome.org/carlosg) and [Sam](https://gitlab.gnome.org/sthursfield) for giving constructive suggestions and guiding me through the program, also thanks to [António](https://gitlab.gnome.org/antoniof) for quick code reviews. I enjoyed attending and giving a talk at [GUADEC conference](https://events.gnome.org/event/9/overview) and got to learn about different projects in the GNOME Circle. Looking forward to continue contributing to GNOME projects.

#### Quick links

<ul>
<li><a href="https://gitlab.gnome.org/groups/GNOME/-/merge_requests?scope=all&state=all&author_username=nis130">All Merge Requests</a></li>
<li><a href="https://gitlab.gnome.org/groups/GNOME/-/issues?scope=all&state=all&author_username=nis130">All Issues</a></li>
<li><a href="https://www.nishitpatel.tech/categories#gsoc-21">Weekly update's</a></li>
<li><a href="https://gitlab.gnome.org/nis130">My Gitlab Account</a></li>
<li><a href="https://youtu.be/DjmL5YbcPEQ?t=6701">GUADEC Talk</a></li>
</ul>

<div class="embed-responsive embed-responsive-16by9">
<iframe width="560" height="315" src="https://www.youtube.com/embed/DjmL5YbcPEQ?start=6701" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</div>
<br>
