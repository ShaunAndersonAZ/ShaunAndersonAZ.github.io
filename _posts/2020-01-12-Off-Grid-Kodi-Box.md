---
header:
  overlay_image: /assets/images/kodi.jpg
  caption: #"[CC License](https://creativecommons.org)"
---
# Creating an Off-Grid Kodi Box

## Installing an off-grid Pi running Kodi for my RV/Toy Hauler. 
I recently purchased a Toy Hauler and wanted to setup a small off-grid media server that I could use while on cold-rainy nights when a fire wasn't an option. I found a few guides that helped (links that helped are below) but this is first and foremost for future me, when I want to do this again, and don't want to re-research, or re-re-research all of this.

For this guide I'm using a Raspberry Pi 3B+ and I installed Raspbian Buster on it.  I had this working for a friend on Stretch, so either should work with a few minor differences that I found.

## Pi Setup
Download your Raspbian image from [raspberrypi.org](https://raspberrypi.org/downloads/)
Depending on what OS you're using (I'm using 19.10 Kubuntu) burn this to the SD Card of the Pi.
* Burn .zip file, not the extracted .img file using etcher *
* For other methods you're on your own...I use Etcher *

Once the image is finished writing to the SD Card, you may need to eject the SD Card and reinsert it.  Your system should pick up two mount points, but we're concerned with the `/boot` one.

In order to enable ssh we'll want to create an empty file in /boot
``` touch ssh ```

Eject the SD card, insert into your Pi and boot it up. For this setup it is _probably_ best to connect to your network over the ethernet port as the next step is going to configure your wifi interface for the RaspAP software.  I haven't tried both, this is just my workflow and has been successful so...

At the time of writing the default pi login info is:
Username: `pi`
Password: `raspbian`

### Configure the pi using raspi-config
Run `sudo raspi-config` to set network and other associated settings
  - Change Password
  - Network Options
    - Configure hostname
  - Configure Boot Options
    -  Desktop / CLI
      - Console Autologin (as 'pi' user)
  - Configure localization options
    - Change Locale (US)
    - Change Timezone (Mine is Arizona)
    - Change Wi-Fi country (US) 
  - Interfacing options
    - Enable Camera
    - Enable SSH
  - Advanced Options
    - Expand Filesystem
    - Configure memory splitting (give as much memory as possible to GPU)
    - Change GL Driver (Original non-GL driver)


## RaspAP Software
I set down the path of using a customized hostapd configuration before I found this.  It is a learning experience to configure this manually, but if you want something to just work then RaspAP is the stuff. Check out their [Github page](https://github.com/billz/raspap-webui) or their [Webpage](https://raspap.com).

I opted for the super-simple **Quick Installer** method.  Please read through the documentation, I by no means condone simply piping things to bash prior to reading them.  That said, to get started with the quick installer:

```# curl -sL https://install.raspap.com | bash ```

As their documentation states the raspap software creates a wifi AP with the following:
  - IP 10.3.141.1
    - Username: admin
    - Password: secret
  - SSID: ```raspi-webgui```
  - Password: ChangeMe

I have had issues connecting to this AP while the Pi was still connected via ethernet cable.  Once you login to the RaspAP AP you can configure the settings there if you so desire.
  - Change the wifi country
  - Change the PSK key
  - Change the SSID

Restart the hotspot and you'll need to reconnect to your new SSID.

The bulk of the default settings will be fine for this application.  I'm not concerned about VPN, DHCP, etc as this is intended to be an **OFF-GRID** Kodi box.  The only reason I'm setting up an AP is so that we can control Kodi via the Kore app.  At most I think I'll have 5 devices ever connected to this AP.  If this doesn't fit your use, then dig further into the settings that will work for you.

 

## Setup RPI 
We need to intall some prerequisites. Using apt, install the following:
  - ``` lightdm ``` This is required to configure autologin
  - ``` usbmount ``` This is required to mount the external drive containing our media
  - ``` neovim ``` This is my editor of choice
  - ``` kodi ``` The reason we're all here

### Configure Packages
We need to make a few small changes to config files to get the drive to automount over USB. 

**usbmount**
  - (Buster) Modify the ``` /lib/systemd/system/systemd-udevd.service ``` file and change the line that says ```PrivateMounts=yes ``` to ``` PrivateMounts=No ``` and then reboot.  After the reboot the USB attached external drive mounted at /media/usb0
  - (Jessie) Modify the ``` /lib/systemd/system/systemd-udevd.service ``` file and change the line that says ``` MountFlags=slave ``` to ``` MountFlags=shared ``` and reboot. USB attached external drive will mount at /media/usb0 (this can be modified in the ``` /etc/usbmount/usbmount.conf ``` config file.

**Kodi**
  - Create a simple systemd unit file
    - ``` vim kodi.service ```

```
[Unit]
Description=Kodi standalone
After=systemd-user-sessions.service network-online.target sound.target
Requires=network-online.target

[Service]
Type=simple
User=pi
ExecStart=/usr/bin/kodi-standalone
Restart=on-abort

[Install]
WantedBy=multi-user.target

```
  
  - Move to  proper directory. 
     - ```  mv kodi.service /etc/systemd/system/kodi.service ```
  - Enable service
    - ``` sudo systemctl enable kodi.service ```

Once you reboot, you _should_ have the following:
  - SSID to connect to
  - USB drive automounted at /media/usb0
  - Kodi autostarted and coming through the HDMI output to whatever TV it's connected to

My use-case is to plug this in, turn it on, connect to the wifi AP and use [Kore](https://kodi.wiki/view/Kore) to control Kodi.  Sorry iPhone users...you're on your own.

## Configure Kodi
I don't change much for this.  Ensure you are able to see all of your media.  You may have to ```chmod -R 777 /media/usb0/Movies```  
### Some stones on the path....
These are a few of the articles that helped me get here.
  - https://superuser.com/questions/1432570/limit-pcmanfm-or-udisks2-automount-usb-drive-read-only
  - https://feldspaten.org/2019/04/04/getting-kodi-to-run-nicely-on-raspbian/
  - https://github.com/billz/raspap-awesome
  - https://howtoraspberrypi.com/create-a-wi-fi-hotspot-in-less-than-10-minutes-with-pi-raspberry/

<script src="https://utteranc.es/client.js"
        repo="shaunandersonaz/shaunandersonaz.github.io"
        issue-term="pathname"
        theme="github-dark"
        crossorigin="anonymous"
        async>
</script>
