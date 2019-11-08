# i915-nolvds
For use with x220/x230 nitrocaster or K.K. fhd mod. If you want to disable LVDS ghost display in linux, this is what you want. 

It's really simple, instead of rebuilding your kernel every time there's an update, or being locked in to using just 1 kernel, now you can just rebuild this i915 against your own kernel headers.

## [X220 Specific Fork](https://github.com/dorianfm/i915-nolvds)

I created this fork from [alexdelifer/i915-nolvds](https://github.com/alexdelifer/i915-nolvds) as I needed to update the product IDs to work with my X220, and to fix the makefile to work with Kernel V5.0

## 5.3 Version

This is a version I've addpted for Kernel V5.3 (Ubuntu 19.10), to the best of my abilities. I've not made a DKMS install for it. Yet. I'm not the original author of this patch, and have no idea of how it works, I've justed worked out how to apply the original patch
to the newer kernel in what seems to be a slightly clenaer way, with a more explicit description of the hardware. See also my notes om [my fork](https://github.com/dorianfm/i915-nolvds)

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

Note: This was tested on Ubuntu 19.10 using a Lenovo X220 with a self installed [Nitrocasteri FHD kit](https://nitrocaster.me/store/x220-x230-fhd-mod-kit.html),  your mileage may vary. 

