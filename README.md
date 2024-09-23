# asus-vlan-script

## Overview

Goal: Setup a isolate port(s) under the Asus-wrt router

Use case: I want to create a isolate networks under existing network enviroment

The Asus 3005 version+ support vlan nativily, but not all the router is supporting that


## Quick Start

1. copy all the script to `/jffs/scripts`
2. execute below command
```sh
echo 'sh /jffs/scripts/vlan-start' > /jffs/scripts/services-start
echo 'sh /jffs/scripts/vlan-firewall-start' > /jffs/scripts/firewall-start
echo 'sh /jffs/scripts/vlan-nat-start' > /jffs/scripts/firewall-start
# below is configure DHCP assign IP to 192.168.150.0/24
touch /jffs/configs/dnsmasq.conf.add
cat <<EOF >> /jffs/configs/dnsmasq.conf.add
interface=br1
# DHCPv4 range: 192.168.150.2 - 192.168.150.254, netmask: 255.255.255.0
# DHCPv4 lease time: 86400s (1 day)
dhcp-range=br1,192.168.150.2,192.168.150.254,255.255.255.0,86400s
# DHCPv4 router (option 3): 192.168.150.1
dhcp-option=br1,3,192.168.150.1
EOF
service restart_dnsmasq

```

## Referance and Thanks

1. Renjie Wu's blog: https://wu.renjie.im/blog/network/ax88u-vlan/
