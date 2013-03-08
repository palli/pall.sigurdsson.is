---
layout: blog_entry
title: Dealing with Nagios segfault because of a corrupted retention.dat
---
<p>
I was at a customer's site recently because their Nagios 3.4.4 was no longer starting up. init script would say nagios
 started successfully but running "service nagios status" afterwards indicated it was in fact not running. running
 "nagios /etc/nagios/nagios.cfg" in strace showed that nagios was segfaulting soon after opening retention.dat
</p>
<p>
Obvious solution to the problem might be to remove retention.dat, but that meant losing all acknowledgements,downtimes, etc.
There must have been a corruption somewhere in the file, we could not spot it by hand.
Luckily i had a module in pynag that was originally designed for parsing status.dat that could parse retention.dat just fine.
</p>
<p>
This short python stub helped generating a new retention.dat which solved the problem for us:
<pre>
#/usr/bin/python
import pynag.Parsers
retention = pynag.Parsers.retention(cfg_file='/etc/nagios/nagios.cfg')
retention.parse()
open('retention.dat.new','w').write(str(retention))
</pre>
Problem fixed!
</p>