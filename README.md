# k480_conf
Configuration utility for setting up function keys on ubuntu for Logitech k480 keyboard.

Inspiration came from this place:

http://www.trial-n-error.de/posts/2012/12/31/logitech-k810-keyboard-configurator/

Mario made this tool for k810, I simply re-traced his steps for k480.
My current configuration is Ubuntu 14.10 with k480 connected through some old d-link bluetooth adapter (on a desktop machine). 
Steps:
check which hidraw device is your logitech keyboard:

$cat /sys/class/hidraw/hidraw*/device/uevent

Identify which one it is, e.g. hidraw2.
Then run (after downloading files from here)
$./build.sh
$sudo ./k480_conf -d /dev/hidraw2 -f on

to make function keys behave as function keys by default. You can also revert this behaviour by running:

$sudo ./k480_conf -d /dev/hidraw2 -f off

which will make media keys default and function keys accessible by (fn + function key).
