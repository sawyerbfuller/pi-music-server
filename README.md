# A raspberry pi-based music server for Sonos

Have a few gigs of music you'd like to play through your Sonos from your phone? You used to be able to store music online using Google Music for free, but they've cancelled that service. You could use a Network Addressed Storage (NAS) server e.g. from Synology, but they're overkill and bulky if you just have a couple of gigs. 

Much better: serve them from a $10, credit-card sized raspberry pi zero! 

I've put down the steps I used to set it up, and my server has been running without a hitch for months. (please post if I've missed something) A few remarks: 
* these instructions assume you will add music by inserting the card into your computer and adding files to the /music folder. Therefore, the samba server running on the pi is not configured to allow write access. 
* getting a pi up and running without connecting a monitor to it is tricky. Its a pretty good idea to use a monitor or TV with an HDMI input to get started. Unfortunately, many low-end monitors don't have HDMI so you might have to trek over to the TV.  

Here are steps. 
1. buy equipment: 
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
* go to "Settings .. system ... Music Library ... Music Library Setup ... + Add Shared Music Folder" and type in ``//<IP address from step 4>/music`` 
* note: on a Mac, you can check that you can access the file server by, in Finder, "go to file … connect to server", and entering ``smb:<IP address from step 4>\``. 
11. The files should appear under "Music Library" when you open the Browse menu at the bottom of the screen, and play with a tap. 
