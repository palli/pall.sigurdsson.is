---
layout: blog_entry
title: Helping to patch iceland for heartbleed
---
<p>
    So, <a href="http://heartbleed.com">heartbleed</a> happened. That pretty much ruined the day for most people running
    mission critical services online. Being a consultant meant helping quite a lot of customers, friends, and
    colleagues to scan for vulnerable services, which meant that my day (and in fact week) was also ruined by the
    unexpected interuption.
</p>

<p>
    I found out that the vulnerability script that were found online for nmap and masscan had a lot of false
    negatives so i decided to wrap up <a href="http://github.com/palli/heartbleed-masstest">my own</a> vulnerability
    scanner, meant for scanning and maintaining vulnerability status of Iceland.

    As a result, the <a href="http://iceland.adagios.org/heartbleed">Monitor Iceland Project</a> now has a graph showing in
    real-time the number of vulnerable servers in Iceland. After doing a fair bit of
    <a href="http://176.10.36.158/summary.txt">name and shame</a> the icelandic service providers found great motivation
    to contact their vulnerable customers. As of this writing there are only 183 vulnerable web servers left in the
    whole country. Pretty good job if you ask me.

</p>
