## MAC changer: 

* Install command
``` Bash
sudo apt install macchanger
```

* List all network interfaces on device
``` Bash
# List all interfaces and choose on which one you want to change MAC address
ifconfig
```

* Change MAC address of specific interface to random one
``` Bash
# Note: netowrk adapter for interface that is targeted should be turned off 
# while change is happening
macchanger -r <interface_name>
```

* Change MAC address of specific interface to specific MAC address
``` Bash
# Note: netowrk adapter for interface that is targeted should be turned off 
# while change is happening
macchanger --mac=<new_mac_address> <interface_name>
```

* Change MAC address of specific interface to original MAC address
``` Bash
# Note: netowrk adapter for interface that is targeted should be turned off 
# while change is happening
macchanger -p <interface_name>
```

