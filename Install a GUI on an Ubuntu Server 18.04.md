## Preparing to Install the GUI
```
sudo apt-get update

sudo apt-get upgrade -y
```

## The Choice of GUI
### Xfce
```
sudo apt-get install xfce4 xfce4-goodies xorg dbus-x11 x11-xserver-utils
sudo apt-get install xrdp
sudo adduser xrdp ssl-cert
```
> our server at pot 3389 

### 
```
sudo apt-get install lubuntu-desktop
```

## Installing VNC Server to Access your GUI
```
sudo apt-get install tightvncserver
```
> Once the server is installed start it by running:
```
vncserver
```

## install Firefox for web browsing
```
sudo apt-get install firefox
```
