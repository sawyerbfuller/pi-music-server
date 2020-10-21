# pi-music-server
A raspberry pi-based music server for sonos

Have a few gigs of music you'd like to play through your sonos from your phone and Google Music is shut down? Don't buy a big bulky NAS server ($200+), store and serve your music from the SD card on a raspberry pi! Here are steps to set it up (please post if I've missed something)

A few remarks: 
* these instructions assume you will add music by inserting the card into your computer and adding files to the /music folder. Therefore, the samba server running on the pi is configured to not allow write access. 
* getting a pi up and running without connecting a monitor to it is pretty tricky. Here, we will assume you'll use a monitor or TV with an HDMI input. 

Here are steps. 
1. buy: 
* a raspberry pi (a zero W is $10 https://www.raspberrypi.org/products/raspberry-pi-zero-w/)
* micro-usb power supply, case, micro-SD card, and card reader, USB and HDMI adaptors (see https://www.adafruit.com/product/2885)
2. connect the SD card to your computer and flash it with the latest version of the operating system at https://www.raspberrypi.org/downloads/
3. plug it into monitor and keyboard to perform standard setup operations it asks you when it first boots (e.g. time zone and set up wifi)
4. configure it to have a static IP address and note down the IP address you chose: https://pimylifeup.com/raspberry-pi-static-ip-address/
5. create your music directory 
```
sudo mkdir /music
sudo chown pi /music
```
6. install the samba file server software (accept defaults)
```
sudo apt-get install samba samba-common-bin
```
7. configure samba server (source: https://en.community.sonos.com/troubleshooting-228999/raspberry-pi-nas-with-sonos-configuration-issues-help-6805556)
```
sudo nano /etc/samba/smb.conf
```
and add the following
* just under ``[global]`` add a line ``ntlm auth=yes``
* at the bottom of the file, add the following: 
```
[music]
Comment = Pi shared folder
Path = /music
Browseable = yes
Writeable = No
only guest = No
Public = yes
Guest ok = yes 
```
8. shutdown the pi ``sudo shutdown now``
9. copy music onto the /music folder of the card from your desktop computer and then restart the pi
10. on your sonos phone app, add the new music library to sonos (from https://support.sonos.com/s/article/257?language=en_US)
* go to "Settings .. system ... Music Library ... Music Library Setup ... + Add Shared Music Folder" and type in ``//<IP address from step 4>/music`` and the files should appear under "Music Library" when you open the Browse menu at the bottom of the screen. 
* note: on a Mac, you can check that you can access the file server by, in Finder, "go to file … connect to server", and entering ``smb:<IP address from step 4>\``. 
