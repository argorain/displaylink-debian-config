# displaylink-debian-config
Just bunch of notes how to set up my Thinkpad X270 to work with Dell D6000 Display Link Dock.

## Environment
 * Linux 4.19.0-9-amd64
 * Debian 4.19.118-2+deb10u1 (2020-06-07)
 * Running X11

## Installed packages
I installed laptop-mode-tools, not sure if it helped or not but it started working after that.
All this is using this project https://github.com/AdnanHodzic/displaylink-debian
Install it first, follow it's how-to, anything else do after that.

## Xorg config
Only this file /etc/X11/xorg.conf.d/20-displaylink.conf 
It's pretty much based on https://wiki.archlinux.org/index.php/DisplayLink#Workaround_2:_Temporarily_disable_PageFlip_for_modesetting

``
Section "Device"
	Identifier "Intel"
	Driver "intel"
	Option "VSync" "true"
EndSection

Section "Device"
  Identifier "DisplayLink"
  Driver     "modesetting"
  Option     "PageFlip" "false"
EndSection
``

## PulseAudio config
Commented out soundcard suspending, it caused glitches and disconections of dock itself. File /etc/pulse/default.pa
Source https://wiki.archlinux.org/index.php/DisplayLink#Displays_disconnect_at_random_intervals_when_using_the_Dell_D6000_docking_station

``
### Automatically suspend sinks/sources that become idle for too long
#load-module module-suspend-on-idle
``

## Disable GDM3 Wayland
It's in file /etc/gdm3/daemon.conf
Idea is taken from here: https://www.mkleen.de/entry/displaylink-on-linux
``
# Uncomment the line below to force the login screen to use Xorg
WaylandEnable=false
``
