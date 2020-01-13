---
header:
  overlay_image: /assets/images/kodi.jpg
  caption: #"[CC License](https://creativecommons.org)"
---

# Installing travel Pi/Kodi

~~Using Buster distro downloaded from~~ Using stretch distro from [raspberrypi.org](https://raspberrypi.org/downloads/)

* Burn .zip file, not the extracted .img file using etcher *

## Enable ssh
Create empty file in /boot
``` touch ssh ```


## Configure with raspi-config
Run raspi-config to set network and other associated settings
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

Perform basic Linux-y stuff
  - Create ``` kodi ``` account
    - ``` useradd kodi  ```
    - ``` sudo passwd kodi ```
    - ``` usermod -aG <groups to match pi user> kodi ```
    - ``` sudo visudo ```
 

## Install Packages
**Using apt, install the following**
  - ``` lightdm ```
  - ``` usbmount ```
  - ``` neovim ```
  - ``` kodi ```

### Configure Packages

**usbmount**
  - (Buster) Modify the ``` /lib/systemd/system/systemd-udevd.service ``` file and change the line that says ```PrivateMounts=yes ``` to ``` PrivateMounts=No ``` and then reboot.  After the reboot the USB attached external drive mounted at /media/usb0
  - (Jessie) Modify the ``` /lib/systemd/system/systemd-udevd.service ``` file and change the line that says ``` MountFlags=slave ``` to ``` MountFlags=shared ``` and reboot. USB attached external drive will mount at /media/usb0 (this can be modified in the ``` /etc/usbmount/usbmount.conf ``` config file.

**kodi**
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


### Some stones on the path....
  - https://superuser.com/questions/1432570/limit-pcmanfm-or-udisks2-automount-usb-drive-read-only
  - https://feldspaten.org/2019/04/04/getting-kodi-to-run-nicely-on-raspbian/
  - https://github.com/billz/raspap-awesome
  - https://howtoraspberrypi.com/create-a-wi-fi-hotspot-in-less-than-10-minutes-with-pi-raspberry/


# Script required for comments to be enabled.
<script src="https://utteranc.es/client.js"
        repo="[ENTER REPO HERE]"
        issue-term="pathname"
        theme="github-dark"
        crossorigin="anonymous"
        async>
</script>
