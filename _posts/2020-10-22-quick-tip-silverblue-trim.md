---
layout: post
title: Speed up a LUKS-encrypted Fedora Silverblue by enabling TRIM
---

My system has been going sluggish lately. After getting suspicious, I decided
to check if TRIM was working.

It wasn’t.

## How to check and enable

This only applies if you have a LUKS-encrypted root partition. To see if it
is correctly set up, [run][archwiki][^1]

```sh
$ sudo dmsetup table
…
luks-123abcdef-etc: 0 1234567 crypt aes-xts-plain64 000etc000 0 8:2 4096 1 allow_discards
…
```

If you see `allow_discards` on every relevant entry (like above), you’re all
set. If not, [run][bug]

```sh
$ rpm-ostree kargs --append=rd.luks.options=discard
```

This applies the ‘discards’ flag at boot time, enabling it for all partitions
on the root drive. (If you only want this for some, use
`rd.luks.options=<LUKS partition ID>=discard`). Restart and run
`fstrim.service`. On my machine, it was a difference between light and day.

[^1]: This has some [security implications][security-implications]. For me, security is not paramount, so I do not mind this -- you might.

[archwiki]: https://wiki.archlinux.org/index.php/Dm-crypt/Specialties#Discard/TRIM_support_for_solid_state_drives_(SSD)
[bug]: https://bugzilla.redhat.com/show_bug.cgi?id=1801539
[security-implications]: https://asalor.blogspot.com/2011/08/trim-dm-crypt-problems.html
