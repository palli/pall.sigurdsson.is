---
layout: blog_entry
title: Monitoring image contents with nagios
---
<p>When monitoring remote services, you use whatever resources you have available, right ?</p>
<p>Some days you are lucky and you get a very nice HTTP error codes or json-data with the status information you need.
Some days you have a very nasty SOAP message, and sometimes you get something right in between like status data encoded
like a .png image.
</p>

<p>We had the challenge of creating a nagios plugins that lets you know if a volcano is currently erupting in iceland or not.</p>
<p>Anyone remotely interesting in nagios plugins that monitor image contents, get mine <a href="https://github.com/palli/monitor-iceland/blob/master/nagios-plugins/check_volcano.py">here</a>.
</p>