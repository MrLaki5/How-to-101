## Raspberry Pi:



### All versions of raspbian system for download:
* http://downloads.raspberrypi.org/



### Setup SD card (with ssh and wifi connection):

* Download image flasher: [balenaEtcher](https://www.balena.io/etcher/)

* Flash image to SD card

* Remount SD card.

* Go to root of sd card:
``` bash
# On OSX under normal flashing, will be:
cd /Volumes/boot/
```

* Enable ssh with creating file or folder in root:
``` bash
touch ssh
```

* Setup wifi:
``` bash
touch wpa_supplicant.conf
nano wpa_supplicant.conf

# In editor add this text (change ssid with wifi name and psk with network password):
country=US # Your 2-digit country code
ctrl_interface=DIR=/var/run/wpa_supplicant GROUP=netdev
network={
    ssid="YOUR_NETWORK_NAME"
    psk="YOUR_PASSWORD"
    key_mgmt=WPA-PSK
}
```



### SSH connections:
* Connect with ssh:
``` bash
# Default password is: raspberry
ssh [-i <path to ssh key>] pi@<raspberry's ip address>
# -i is used if ssh key was already added to raspberry
```

* Copy files to raspberry:
``` bash
scp <local path to file> pi@<raspberry's ip address>:<path where to put it on raspberry>
```

* Copy files from raspberry:
``` bash
scp pi@<raspberry's ip address>:<path of file on raspberry> <local path where to put file>
```

* Add ssh key to raspberry:
``` bash
ssh-copy-id -i <path to ssh key> pi@<raspberry's ip address>
```

* Generate ssh keys on local machine, with (it will generate keys in current dir). In generation choose private key protection password: 
``` Bash
ssh-keygen
```



### Docker instalation:
* Install docker:
``` Bash
curl -sSL https://get.docker.com | sh
```
* Give docker sudo privilages:
``` Bash
sudo groupadd docker
```
* Change the id of rasberry pi to be seen as Debian
``` Bash
sudo vi /etc/os-release
#Edit line with ID=raspbian to ID=debian
```


### Statistics:
* Core temp:
``` bash
vcgencmd measure_temp
```

* System diagnostics:
``` bash
dmesg [-H] [-T] [-w]
# -H is humen readable output text
# -T is human readable time 
# -w is live changes
```