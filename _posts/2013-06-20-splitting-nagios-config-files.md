---
layout: blog_entry
title: Splitting a Nagios configuration file
---
<p>
  Have you ever inherited a nagios setup where the configuration file hierarchy is a complete mess ?
</p>
<p>
  Ever wanted to split that services.cfg with 2000 objects in it into one file per host ?
</p>
<p>It is relatively easy to do with pynag. Consider this script which copies all the nagios objects and creates an example hierarchy under /tmp/nagios/conf.d/
</p>
<pre>
#!/usr/bin/env python
#
# This pynag script will parse all your nagios configuration
# And write a copy of every single object to /tmp/nagios/conf.d
#
# This can be very handy if your configuration files are a mess
# or if you are thinking about splitting a big file of services
# into one file per host
#
# The script will only write the copy to /tmp so you will
# have to manually remove old objects before you copy this
# into your /etc/nagios/conf.d or wherever you want to keep
# your objects



import pynag.Model
from pynag.Model import ObjectDefinition

# cfg_file is where our main nagios config file is
pynag.Model.cfg_file = '/etc/nagios/nagios.cfg'

# pynag_directory is where the new objects will be saved
pynag.Model.pynag_directory = '/tmp/nagios/conf.d'

all_objects = ObjectDefinition.objects.all
# Use this instead if you only want to clean up a single directory
# config_file='/etc/nagios/all_the_services.cfg'
# all_objects = ObjectDefinition.objects.filter(filename__contains=config_file)

for i in all_objects:
    print "Saving", i.object_type, i.get_description(), "...",
    # Set a new filename for our object, None means
    # That pynag decides where it goes
    new_filename = None
    # Alternative:
    # if i.object.type == 'host' and i.host_name is not None:
    #     new_filename = '/tmp/nagios/conf.d/hosts/%s" % i.host_name
    
    i.set_filename(new_filename)
    i.save()
    print "Saved to", i.get_filename()

</pre>
