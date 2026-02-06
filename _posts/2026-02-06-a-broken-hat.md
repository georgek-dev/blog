---
layout: post
title: "Hats can also break"
date: 2026-02-06 13:10 +0100
categories: other-linux fedora recovery rescue dnf package-manager
---
Well, Arch is in fact pretty comfortable. But I went and searched in my ~~trash can~~**top-notch electronics box** and found an old, nearly untouched stick with Fedora 42. I know, this **is** my first post, and some reader will say: "Your blog is about Arch, what's Fedora doing here?". Well, to answer that before that, my curiosity is **extremely** - let's say, extreme. And I wondered to see if it still worked. 

So I plugged it into - I know, not good - a **Microsoft** Surface laptop (I have "de-Windows-ified" it) and booted. Wow, it worked so fluid and nice. But F42 is quite a while back, and I wanted to migrate to 43, which was recently released.
I opened a terminal and typed the dnf command. Now, I must confess something beforehand. I **_HATE_** backups. And I know, it was a bad idea to do it like this. (More on that later on.)

The offline preparations finished smoothly, and all that kept me away from my beautiful new Fedora 43 was a reboot. But I saw a dnf process was blocking the system. I rebooted with ignoring inhibitors (btw, that's the ```systemctl reboot -i```) command.
And about roughly 1.5 hours later, it was finished. Well, I went and entered into my _shiny_ new Fedora 43 and of course, I needed to reupgrade my packages that had stayed on the 42 repo. No problem, I thought. But here's the catch: It needed to repair some packages that were broken by - do you remeber? - the reboot.
So I also started that. And in the middle of the process, my PC crashed. It came out of the blue. And when I started it again, my WiFi card was not detected. Seems like the crash and the reboot had broken my packages.

Thankfully, I had my *beautiful* Arch live USB, so after I booted from it and mounted the root and /boot/efi partitions, ```arch-chroot``` gave me access to my broken system.
But dnf wanted me to remove my kernel to fix the problem. Well, the first thing I learned about Linux was **exactly that**. So to be sure, I made a full backup using [Timeshift](https://github.com/linuxmint/timeshift). It's a GREAT tool and can save your life (like it did save mine - ok, not exactly, but my peace of mind).
So I did that. And dnf must've gotten crazy, because it wanted me to remove systemd and grub too. _Wait, what?!_ Well, it did. I'm not lying. So I went and reset the cache (nice handy tip, ```dnf5 clean all```) and it finally was detetecting what it had done and offered to reinstall my kernel and all critical system packages, while upgrading all the other ones.
Well, if that isn't pretty neat. I've got 1.5k packages to upgrade (process still running in background at the time of writing), but I hope you learned something and liked this post.

Stay safe (especially on Linux!).
