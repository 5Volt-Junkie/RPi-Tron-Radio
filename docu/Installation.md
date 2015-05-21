RPi-Tron-Radio
==============

Small web radio with Raspberry Pi and 2.8" 320x240 TFT Touchscreen. The interface of the web radio was written in python/pygame and can be started on boot without entering X.

To run the web radio, mpc, mpd and FBTFT are required.



#Installation

#### Prepare SD-Card
Download the newest Raspbian Image with preinstalled FBTFT (8Bit Version) https://github.com/watterott/RPi-Display

You can also install the frame buffer on existing raspbian https://github.com/watterott/RPi-Display/blob/master/docu/FBTFT-Install.md

Copy the Image to SD-Card with dd or Win32DiskImager.
Turn on your Raspberry and connect it to the internet

#### First Boot

(Tip: you can also use SSH on port 22)

* Login with 
User: pi
Password: raspberry

```
sudo raspi-config
```
* Expand filesystem, 
* change password, language, keyboard layout and time zone
* Reboot your Raspberry


#### Run the installation script
```
sudo /bin/bash rpi-display.sh 270
```
reboot your Raspberry Pi

#### Touchscreen calibration
```
sudo TSLIB_FBDEVICE=/dev/fb1 TSLIB_TSDEVICE=/dev/input/touchscreen ts_calibrate
```
* touch the five crosshairs

#### Install mpc & mpd...
```
sudo apt-get update
sudo apt-get install mpc mpd apache2 php5 libapache2-mod-php5
```

#### Download RPi-Tron-Radio
```
sudo git clone https://github.com/5volt-junkie/RPi-Tron-Radio
```


#### Prepare autostart
```
sudo chmod 755 /home/pi/RPi-Tron-Radio/launcher.sh
sudo nano /etc/rc.local
```

insert this line, just above the "exit0"
```
home/pi/RPi-Tron-Radio/launcher.sh &
```
Close the file with Ctrl+X nad confirm with y


#### Prepare simple webfront and favorite.txt file for saving the name of playing song
```
sudo touch /var/www/favorite.txt
sudo nano /var/www/index.html
```
Delete the html code and insert the new as follow
```
<html>
<head><title>Tron Radio</title></head>
<body>
<h1>Raspberry Pi Tron Radio</h>
<p><a href="favorite.txt">Show my favorites</a></p>

</body>
</html>
```
Close the file with Ctrl+X and confirm with y



#### Add stream/file to playlist
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

Reboot your Rapberry Pi one more time :-)
