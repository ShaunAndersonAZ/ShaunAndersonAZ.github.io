---
defaults:
  # _posts
  - scope:
      path: ""
      type: posts
    values:
      layout: single
      author_profile: true
      read_time: true
      comments: true
      share: true
      related: true
header:
  overlay_image: /assets/images/touchpad.jpeg
---

# 4 Finger Swipe
## Figuring it out on KDE 5

###Install 
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

Start the program with the command line:
```
libinput-gestures-setup start
```


