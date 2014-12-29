mbp5ubuntu
==========

tested with ubuntu 14.04

copy everything as root to your root directory

so what's in here?

/sbin/igd<br>
switches the gmux to the 9400M and disables the 9600M GT

/sbin/dgd<br>
switches the gmux to the 9600M GT

/sbin/gpuboot<br>
script launched by /etc/rc2.d/S80gpuboot on bootup<br>
checks /etc/gpu and calls the respectable (x)gd executable described above

/etc/gpu<br>
just plain text with "i" or "d" in it so gpuboot knows what to do

/sbin/gpuchange<br>
changes the /etc/gpu flag if run as root<br>
if run as a user a file ~/.gpu is craeted. gpuboot will also have look there first.

/sbin/gpuresume<br>
script launched by /etc/pm/sleep.d/gpuresume everytime your laptop resumes from sleep or hibernation do set the gmux again (and again power off the 9600M GT if needed)

/sbin/macfanctld<br>
this is compiled by myself the read the GPU- and CPU-DIE instead of the proximity temps.<br>
gets called by upstart on bootup at /etc/init/macfanctld.conf

/etc/macfanctl.conf_d / _i<br>
/etc/X11/xorg.conf_d / _i<br>
the config files copied to the default location (xorg.conf or macfanctl.conf)

/var/lib/polkit-1/localauthority/50-local.d/com.ubuntu.enable-hibernate.pkla<br>
enables hibernation (for me it works flawlessly with complete harddrive lvm encryption)


you won't get any virtual terminal if the nvidia blob is loaded. so if something goes pretty wrong you always can boot with the parameter "text". nvidia is blacklisted by default and only gets loaded by gpuboot (without "text" parameter). the blacklist is important because of issues with the 9400M (restarting X without blacklisting first results in corruption - 9600M GT has to be deactivated before loading nvidia - gpuboot and /etc/modprobe.d/nvidia-mbp.conf take care of this)
