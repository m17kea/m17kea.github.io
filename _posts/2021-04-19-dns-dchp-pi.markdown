---
layout: post
title:  "Developer setup - the basics"
date:   2021-04-10 14:50:21 +0100
categories: DevSetup
---

Rename a host
https://thepihut.com/blogs/raspberry-pi-tutorials/19668676-renaming-your-raspberry-pi-the-hostname 

# dnsmasq setup
https://blogging.dragon.org.uk/howto-setup-dnsmasq-as-dns-dhcp/
https://fedoramagazine.org/dnsmasq-provide-dns-dhcp-services/
https://ral-arturo.org/2018/09/12/dhcp-static-route.html
https://serverfault.com/questions/922017/how-does-dnsmasq-integrate-with-my-router/922018#922018
https://www.tecmint.com/setup-a-dns-dhcp-server-using-dnsmasq-on-centos-rhel/ 

# validating
https://www.tecmint.com/install-dig-and-nslookup-in-linux/

# openwrt 
https://opensource.com/article/21/3/router-raspberry-pi

## download 
https://downloads.openwrt.org/releases/19.07.7/targets/brcm2708/bcm2710/


## luci ui
```
opkg update
opkg install luci
opkg install luci-ssl-nginx
reboot
```



## dhcp dns forwrding
https://128.0.0.1/cgi-bin/luci/admin/network/dhcp 
https://openwrt.org/docs/guide-user/base-system/dhcp
https://serverfault.com/questions/1049474/how-to-setup-dnsmasq-for-dns-for-private-and-public-hostnames-via-different-dns?noredirect=1&lq=1
https://serverfault.com/questions/624670/redirect-dns-requests-with-openwrt
https://serverfault.com/questions/922017/how-does-dnsmasq-integrate-with-my-router/922018


```

```


# ssh key 
Navigate to LuCI → System → Administration → SSH -Keys. · Copy-paste your public key and click the Add key button.



# References 
https://www.zahradnik.io/raspberry-pi-as-a-home-router
https://openwrt.org/docs/guide-user/luci/luci.essentials
