---
layout: blog_entry
title: Dealing with a corrupted gnome keyring
---
<p>This was bound to happen at some point. Local hard disk was full and google chrome was trying to save a password.
End result was a corrupted gnomekeyring which meant i was effectively without any vpn or browser password, or even access
to my ssh key.
</p>

<p>
keyring source repository some code buried within its internal tests called
<a href="https://git.gnome.org/browse/gnome-keyring/tree/pkcs11/secret-store/tests/dump-keyring0-format.c">dump-keyring0-format.c</a> which
showed partial success in printing most of my passwords. So i had some hope that my keyring was not completely lost.

One method available would be to print out all the passwords and store them in a new file. However when i noticed there were python bindings
out there i eventually came up with a much nicer solution:
</p>
<pre>
import gnomekeyring

for keyring in gnomekeyring.list_keyring_names_sync():
    for i in gnomekeyring.list_item_ids_sync(keyring):
        try:
            # This will file if the keyring file is corrupted
            # at that point in the file
            item = gnomekeyring.item_get_info_sync(keyring, i)
            #print item.get_display_name(), item.get_secret()
        except Exception:
            # Left commented out for obvious reasons
            #gnomekeyring.item_delete_sync(keyring, i)
            print "%s: item %s deleted." % (keyring, i)
</pre>