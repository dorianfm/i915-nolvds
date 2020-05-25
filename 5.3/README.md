# i915-nolvds
For use with x220/x230 nitrocaster or K.K. fhd mod. If you want to disable LVDS ghost display in linux, this is what you want. 

It's really simple, instead of rebuilding your kernel every time there's an update, or being locked in to using just 1 kernel, now you can just rebuild this i915 against your own kernel headers.

## [X220 Specific Fork](https://github.com/dorianfm/i915-nolvds)

I created this fork from [alexdelifer/i915-nolvds](https://github.com/alexdelifer/i915-nolvds) as I needed to update the product IDs to work with my X220, and to fix the makefile to work with Kernel V5.0

## [5.3 Version](https://github.com/dorianfm/i915-nolvds/tree/master/5.3)

This is a version I've addapted for Kernel V5.3 (Ubuntu 19.10), to the best of my abilities. I've not made a DKMS install for it. Yet. I'm not the original author of this patch, and have no idea of how it works, I've justed worked out how to apply the original patch
to the newer kernel in what seems to be a slightly clenaer way, with a more explicit description of the hardware. See also my notes om [my fork](https://github.com/dorianfm/i915-nolvds)

### [5.3.0-50+]

I could no longer get this patch to work on kernerl 5.3.0-50+ (Ubuntu 19.10), no idea why. After lots of messing around a simpler solution appeares here:
https://unix.stackexchange.com/questions/399739/disable-laptop-screen-and-use-only-vga

Specifically @Dmitry's comment:

To make the change permanent one can edit the file ```/etc/default/grub``` followed by the command ```update-grub```, and disable laptop's display changing this parameter: ```GRUB_CMDLINE_LINUX_DEFAULT="quiet splash video=LVDS-1:d"```

I also experimented with trying to disable the LVDS display on X11 init by adding a file:
```/usr/share/X11/xorg.conf.d/50-disable-lvds.conf``` with the contents 

```
Section "Monitor"
	Identifier 	"lvds monitor"
	Option	"ignore"	"true"
EndSection
Section "Device"
	Identifier	"onboard"
	Option	"LVDS-1"	"lvds monitor"
EndSection
```

which also helped. YMMV


### Make
```
make
sudo make install
reboot # so module can load
```
## Did it load?
How do I know it worked?

You won't have an unreachable first monitor, but you can run this to be sure.
``` 
$ dmesg | grep nitrocaster
[    4.678805] [drm] Skipping LVDS initialization for Lenovo ThinkPad X220 moded with nitrocaster FHD Board
```
## Uninstalling

Don't like it? No problem.

### Make
```
sudo make uninstall
```

Note: This was tested on Ubuntu 19.10 using a Lenovo X220 with a self installed [nitrocaster FHD kit](https://nitrocaster.me/store/x220-x230-fhd-mod-kit.html),  your mileage may vary. 

