## Access AnyDesk or RustDesk with headless machine (no monitor connected to it) on Linux Ubuntu.

### 1 - Automatic Login:

```sh
sudo vim /etc/gdm3/custom.conf
```

```sh
# Enabling timed login
TimedLoginEnable = true
TimedLogin = MyUser # <--- modify
TimedLoginDelay = 20
```

### 2 - Install a dummy driver (virtual):

```sh
sudo apt-get install xserver-xorg-video-dummy
```

```sh
sudo vim /usr/share/X11/xorg.conf.d/xorg.conf
```

Add:

```sh
Section "Device"
    Identifier  "Configured Video Device"
    Driver      "dummy"
EndSection

Section "Monitor"
    Identifier  "Configured Monitor"
    HorizSync 31.5-48.5
    VertRefresh 50-70
EndSection

Section "Screen"
    Identifier  "Default Screen"
    Monitor     "Configured Monitor"
    Device      "Configured Video Device"
    DefaultDepth 24
    SubSection "Display"
    Depth 24
    Modes "1920x1080"
    EndSubSection
EndSectio
```

### 3 - Reboot

```sh
sudo reboot
```

### References:

- https://askubuntu.com/questions/453109/add-fake-display-when-no-monitor-is-plugged-in/463000#463000
 
- https://askubuntu.com/questions/1322937/ubuntu-20-04-shows-a-black-screen-when-connecting-through-teamviewer-but-i-stil
