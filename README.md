# k480_conf
Configuration utility for setting up function keys on ubuntu for Logitech k480 keyboard.

Inspiration came from this place:

http://www.trial-n-error.de/posts/2012/12/31/logitech-k810-keyboard-configurator/

Mario made this tool for k810, I simply re-traced his steps for k480.
My current configuration is Ubuntu 14.10 with k480 connected through some old d-link bluetooth adapter (on a desktop machine). 

## Building the Tool

To build the tool, first run the following command:

`$ ./build.sh`

## Enable \ Disable Fn Keys

This tool can automatically scan all of your blutooth devices for a K480 keyboard.

To do so, run:

`$ sudo ./k480_conf -f on`

Or 

`$ sudo ./k480_conf -f off`

To revert this behavior.

## Specifying a Device

If you wish to specify the device to toggle, you can check which hidraw device is your logitech keyboard:

`$ cat /sys/class/hidraw/hidraw*/device/uevent`

Identify which one it is, e.g. hidraw2 (It might be any other, be sure which one it is before you proceed).

2) Then run following files to make function keys behave as function keys by default. (after downloading/cloning files from here):

`$ sudo ./k480_conf -d /dev/hidraw2 -f on`

You can also revert this behaviour by running:

`$ sudo ./k480_conf -d /dev/hidraw2 -f off`
which will make media keys default and function keys accessible by (fn + function key).

To keep this setting after a restart you need to tell Ubuntu to run the script for you.


Here is one of possible rules to be put in /etc/udev/rules.d/99-k480.rules:

`SUBSYSTEM=="hidraw", ACTION=="add", SUBSYSTEMS=="bluetooth", ATTRS{address}=="00:1f:20:e3:6c:b6", RUN+="/opt/bin/k480_conf -d /dev/%k -f on"`
