# pi-music-server
A raspberry pi-based music server for sonos

Have a few gigs of music you'd like to play through your sonos from your phone and Google Music is shut down? Don't buy a big bulky NAS server ($200+), store and serve your music from the SD card on a raspberry pi! Here are steps to set it up (please post if I've missed something)

To do this, you'll need a monitor or TV with an HDMI input. 
1. buy: 
* a raspberry pi (a zero W is $10 https://www.raspberrypi.org/products/raspberry-pi-zero-w/)
* micro-usb power supply, case, micro-SD card, and card reader, USB and HDMI adaptors (see https://www.adafruit.com/product/2885)
2. connect the SD card to your computer and flash it with the latest version of the operating system at https://www.raspberrypi.org/downloads/
3. plug it into monitor and keyboard to perform standard setup operations it asks you when it first boots (e.g. time zone and set up wifi)
4. configure it to have a static IP address https://pimylifeup.com/raspberry-pi-static-ip-address/
5. create your music directory 
```
sudo mkdir /music
sudo chown pi /music
```
6. install the samba file server software
```
sudo apt-get install samba
sudo 
```
9. on your sonos phone app, add the new music library to sonos: https://support.sonos.com/s/article/257?language=en_US
