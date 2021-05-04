# change mac address  


# environment  

kali linux  

change mac address manually
```terminal
# show interface information
ifconfig

# disable eth0 
ifconfig eth0 down

# setting eth0 ether
ifconfig eth0 hw ether XX:XX:XX:XX:XX:XX

# enable eth0
ifconfig eth0 up
```

change mac address automatically using python  

using module: subprocess  

mac_change.py
```python

#! /usr/bin/env python3

import subprocess

def main():
  
  subprocess.call("ifconfig eth0 down", shell=True)
  subprocess.call("ifconfig eth0 hw ether 00:11:22:33:44:55", shell=True)
  subprocess.call("ifconfig eth0 up", shell=True)
  
if __name__ == "__main__":
  main()
```
