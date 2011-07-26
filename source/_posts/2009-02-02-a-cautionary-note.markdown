--- 
wordpress_id: 40
layout: post
title: A Cautionary Note
wordpress_url: http://joncanady.com/2009/02/a-cautionary-note/
---
If you pop a DVD into your Mac and the system doesn't recognize it *and* hitting Eject doesn't work:

Instead of following my lead and wasting a half-hour playing with Disk Utility and Googling for the terminal command to eject a disc (`drutil tray eject`, btw), make sure VMWare Fusion hasn't ganked control of the drive from the OS.  If it has, just disable the CD/DVD drive on your VM.  OS X will happily mount the disc and everything will be sunshine and rainbows.

Also, VMWare: treat the optical drive like you treat USB devices; if I don't have you focused when I put in a DVD, chances are I don't want you feeding it to my VM and sucking 28.5 minutes of my day away from me.

That is all.
