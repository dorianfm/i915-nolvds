# i915-nolvds
For use with x220/x230 nitrocaster or K.K. fhd mod. If you want to disable LVDS ghost display in linux, this is what you want. 

It's really simple, instead of rebuilding your kernel every time there's an update, or being locked in to using just 1 kernel, now you can just rebuild this i915 against your own kernel headers.

There's two ways you can install this, DKMS or just plain make. To use dkms, you must have it installed.

## [X220 Specific Fork](https://github.com/dorianfm/i915-nolvds)

I created this fork from [alexdelifer/i915-nolvds](https://github.com/alexdelifer/i915-nolvds) as I needed to update the product IDs to work with my X220, and to fix the makefile to work with Kernel V5.0

## [Kernel V5.3 Install](https://github.com/dorianfm/i915-nolvds/tree/master/5.3)

There is seperate [5.3](https://github.com/dorianfm/i915-nolvds/tree/master/5.3) directory with makefile and patches for Kernel 5.3, see the included README.md for more info. 

## Product IDs

In patches/i915-no-lvds-multi.patch the original `DMI_PRODUCT_NAME` was `4290FP2`, I've updated this to match my laptop's product id which is `4291T25` - you may need to change this to fit your device. I found this ID via the following:

```
$ dmesg | grep ThinkPad | grep model
[    4.431800] thinkpad_acpi: Lenovo ThinkPad X220, model 4291T25
```

### DKMS

```
sudo ./dkms-install.sh
reboot # so module can load
```

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
$ dmesg | grep i915
[    1.150666] i915: loading out-of-tree module taints kernel.
```
## Uninstalling

Don't like it? No problem.

### DKMS
```
sudo ./dkms-remove.sh
```

### Make
```
sudo make uninstall
```

Note: This was tested on Arch Linux on a K.K. X220 from Taobao, your mileage may vary.
