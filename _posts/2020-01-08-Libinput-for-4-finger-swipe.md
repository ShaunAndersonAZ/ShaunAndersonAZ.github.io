---
header:
  overlay_image: /assets/images/touchpad.jpeg
---

Enabling 4 finger swipe on KDE 5

I have to use Windows for my work laptop.  While I'm not a fan of using Windows, one of the features I actually like is the ability to 4 finger swipe up to expose all windows on the desktop.  I have typically enabled this in the past by using hot-corners and this works great, however I like the ability to do it from the touchpad as well.  I found a few different links online and ended up getting this to work by following these steps.

### Install 
Install the prerequisites:
```
sudo apt install libinput-tools xdotool wmctrl
```

Clone the GH Repo:
```
git clone https://github.com/bulletmark/libinput-gestures
```

Change to the directory and install:
```
sudo make install
```
*-OR-*
```
sudo ./libinput-gestures-setup install
```

### Configure
Edit the ``` libinput-gestures.conf ``` file.

Add the following in the "SWIPE GESTURES" section:

```
gesture swipe up 4 xdotool key ctrl+F9
```
This is the entry to enable 4 finger swipe to call xdotool to simulate the ctrl+F9 keypress. You could similarly make entries here to perform other touchpad gestures.

Save and close the file.

The program requires you to be part of the ``` input ``` group:
```
usermod -aG input <username>
```

Start the program with the command line:
```
libinput-gestures-setup start
```
<script src="https://utteranc.es/client.js"
        repo="shaunandersonaz/shaunandersonaz.github.io"
        issue-term="pathname"
        theme="github-dark"
        crossorigin="anonymous"
        async>
</script>

