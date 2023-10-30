# Setup Coral Dev Board

## Overview

Following these [instructions](https://coral.ai/docs/dev-board/get-started)


## Setup

### Flash Mendel Linux

* Downloaded the image from [this link](https://dl.google.com/coral/mendel/enterprise/enterprise-eagle-flashcard-20211117215217.zip)

* I'm writing this image on a Mac so I ran something like this

```
sudo diskutil list
sudo diskutil unmountDisk /dev/disk22
sudo dd if=flashcard_arm64.img of=/dev/rdisk9 bs=1M status=progress
```

* Changed the 4 mode switches (1-4) so that all were on except switch 2.  I needed a magnifying glass to see the switches clearly, they are very small
* Insert SD card 
* Apply power and then wait around 3mins until the red light goes out - looks like it's stoopped/broken
* Unplug power, remove SD card 
* Switch DIP switches to 1 on and all others off - this will then boot from eMMC


### Boot Board

* Connect data cable between host computer and Coral Dev Board.  This creates a USB network interface when the board starts up
* Apply power to the board
* Create a Python virtual environment using the following command

```
python3 -mvenv .matrix
. .matrix/bin/activate
```

* Install tools

```
pip install mendel-development-tool
```

* Once the board is running run this command on the host machine

```
mdt devices
```

* For this to work for my setup (which has many iptables rules) I needed the following

```
sudo iptables -I INPUT -i usb0 -j ACCEPT
```

* The `mdt devices` command should output something like this

```
mdt devices
queen-yarn		(192.168.100.2)
```

* Connect over `mdt` shell

```
mdt shell
```




## References

### Linux

* [iptables firewall commands](https://www.digitalocean.com/community/tutorials/iptables-essentials-common-firewall-rules-and-commands)
