# freebsdkde
##Installing Xorg, Nvidia, KDE Desktop on Freebsd
##I'll put this into a script. Just wanted it up for anyone struggling to get a KDE desktop going

##This is just a quick howto to get a KDE desktop up and running on Freebsd if you're using a NVidia card.
#First get Linux loaded 
kldload linux

##For KDE
pkg install -y nvidia-driver kde5 sddm xorg xf86-video-intel plasma5-plasma-desktop nvidia-xconfig nvidia-settings git bash linux-nvidia-libs

##For Gnome 
#pkg install -y nvidia-driver gnome3 gdm xorg xf86-video-intel nvidia-xconfig nvidia-settings git bash linux-nvidia-libs

##For earlier nivdia cards with kde install 
#pkg install nvidia-driver-390-390.132 kde5 sddm xorg xf86-video-intel plasma5-plasma-desktop nvidia-xconfig nvidia-settings git bash linux-nvidia-libs-390-390.132
echo "linux_enable=YES" >> /etc/rc.conf
echo "net.local.stream.recvspace=65536" >> /etc/sysctl.conf
echo "net.local.stream.sendspace=65536" >> /etc/sysctl.conf
echo 'kld_list="nvidia-modeset"' >> /etc/rc.conf
#nvidia-xconfig

echo "proc /proc procfs rw 0 0" >> /etc/fstab 
echo "linprocfs   /compat/linux/proc  linprocfs       rw      0       0" >> /etc/fstab
echo "linsysfs    /compat/linux/sys   linsysfs        rw      0       0" >> /etc/fstab
echo "tmpfs    /compat/linux/dev/shm  tmpfs   rw,mode=1777    0       0" >> /etc/fstab
nvidia-xconfig
#reboot again



#For kde5
echo 'sddm_enable="YES"' >> /etc/rc.conf
echo 'mouse_enable="YES"' >> /etc/rc.conf
echo 'hald_enable="YES"' >> /etc/rc.conf
echo 'dbus_enable="YES"' >> /etc/rc.conf

#For gnome
#echo 'gnome_enable="YES"' >> /etc/rc.conf
#echo 'gdm_enable="YES"' >> /etc/rc.conf
#sysrc dbus_enable=yes && service dbus start
#sysrc hald_enable=yes && service hald start
