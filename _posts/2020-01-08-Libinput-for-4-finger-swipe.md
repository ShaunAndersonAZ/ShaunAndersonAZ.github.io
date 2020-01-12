---
header:
  overlay_image: /assets/images/touchpad.jpeg
---

Enabling 4 finger swipe on KDE 5

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
Edit the ```libinput-gestures.conf``` file.

Add the following in the 'SWIPE GESTURES' section:
```
gesture swipe up 4 xdotool key ctrl+F9
```

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

