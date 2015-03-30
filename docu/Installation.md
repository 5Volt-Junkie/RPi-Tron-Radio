RPi-Tron-Radio
==============

Small web radio with Raspberry Pi and 2.8" 320x240 TFT Touchscreen. The interface of the web radio was written in python/pygame and can be started on boot without entering X.

To run the web radio, mpc, mpd and FBTFT are required.





#Installation

## Prepare SD-Card
Download the newest Raspbian Image with preinstalled FBTFT (8Bit Version) https://github.com/watterott/RPi-Display

Copy the Image to SD-Card with dd or Win32DiskImager.
Turn on your Raspberry and connect it to the internet

## First Boot

* Login with 
User: pi
Password: raspberry

```
sudo raspi-config
```
* Expand filesystem, language, keyboard layout and time zone
* Reboot your Raspberry

### Touchscreen calibration
* After reboot:
```
sudo TSLIB_FBDEVICE=/dev/fb1 TSLIB_TSDEVICE=/dev/input/touchscreen ts_calibrate
```
* touch the five crosshairs

### Install MPC and MPD
```
sudo apt-get install mpc mpd
```
### Add stream/file to playlist
```
sudo mpc add <file or URL>
```
#### Example: 
Let's add one stream from [somafm.com](http://uwstream3.somafm.com:6200) ;-)
[Def Con Radio - Music for Hacking](http://somafm.com/defcon/)
```
sudo mpc add http://uwstream3.somafm.com:6200
```
For more mpc commands see http://linux.die.net/man/1/mpc

### Install RPi-tron-radio
Copy the folder "tron-radio" to /home/pi

```
sudo chmod 755 /home/pi/tron-radio/launcher.sh
```

### Start RPi-Tron-Radio on boot
```
sudo nano /etc/rc.local
```
Insert the following command, just above exit0
```
(home/pi/tron-radio/launcher.sh)&
```
Save the file

```
sudo reboot
```

## Install the "Favorite" function 

### Install appache and php
```
sudo apt-get update
sudo apt-get install apache2 php5 libapache2-mod-php5
```

Then enter the IP-address of your radio in the address field of your webbrowser.
You can find the IP-address on the second menu screen.
If the site shows "It works!", than it really works ;)

### Add favorite list to /var/www/

```
cd /var/www/
sudo touch favorite.txt
```

### Create simple webfront

```
cd /var/www/
sudo nano index.html
```

Now insert this simple html code and save the file
```
<html>
<head><title>Tron Radio</title></head>
<body>
<h1>Raspberry Pi Tron Radio</h>
<p><a href="favorite.txt">Show my favorites</a></p>

</body>
</html>
```

```sudo reboot```

to show the favorites, just type the ip address of your tron-radio in your browser and click the file.
