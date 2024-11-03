# TryHackMe-env

## Settings

### update locale to English
```
sudo locale-gen en_US.UTF-8
sudo update-locale LANG=en_US.UTF-8
```

### install Japanese Package
```
sudo apt update

sudo apt install -y task-japanese task-japanese-desktop

sudo apt install -y fcitx-mozc

# select Input Method in Start Menu
OK -> Yes (Do you explicitly select the user configuration?) -> select "fcitx" -> reboot

# kali -> Settings -> Fcitx Configuration -> input method Tab -> click "+"
Keyboard - Japanese
Mozc
```


### Shared Folder
```
sudo modprobe 9p

lsmod | grep 9p

sudo mount -t 9p -o trans=virtio,version=9p2000.L share /mnt/shared/repos
```

#### Add this line to "/etc/fstab"　for auto mount after reboot
```
nano /etc/fstab

# Add this line
share /mnt/shared/repos 9p trans=virtio,version=9p2000.L,rw,_netdev 0 0
```
