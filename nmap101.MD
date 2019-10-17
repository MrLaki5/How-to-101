## How to nmap:

* Search network for all devices, replace # to match with network ip
``` Bash
    nmap -sn 192.168.#.0/24
```

* Search network for all devices and down ips
``` Bash
    nmap -sn 192.168.#.0/24 -v
```

* Show open tcp ports of specific device
	* -p- runs for every port, if not specified, runs on some lower velue default ports. (without it its much faster)
	* -v gives more info
``` Bash
    nmap -sS -sV -p- device_ip -v
```

* Show open udp ports of specific device
	* -p- runs for every port, if not specified, runs on some lower velue default ports. (without it its much faster)
	* -v gives more info
``` Bash
    nmap -sU -sV -p- device_ip -v
```