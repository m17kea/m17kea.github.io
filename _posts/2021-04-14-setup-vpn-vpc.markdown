---
layout: post
title:  "Developer setup - the basics"
date:   2021-04-10 14:50:21 +0100
categories: DevSetup
---
https://medium.com/aws-factory/create-a-aws-vpn-client-endpoint-with-cdk-f0f4db221336 

            new VpnConnection(this, "vpn", new VpnConnectionProps
            {
                Vpc = vpc,
                Ip = "81.156.224.240",
                StaticRoutes = new []
                {
                    "192.168.1.0/24"
                }
            });

https://aws.amazon.com/blogs/networking-and-content-delivery/simulating-site-to-site-vpn-customer-gateways-strongswan/

https://github.com/aws-samples/vpn-gateway-strongswan/blob/main/README.md

https://www.edge-cloud.net/2019/07/18/aws-site-2-site-vpn-with-strongswan-frrouting/#transit-gateway-and-site-to-site-vpn-setup 

https://hackernoon.com/setup-raspberry-pi-3-as-aws-vpn-customer-gateway-7432f653707 
sudo apt-get install -y strong swan
sudo nano /etc/ipsec.conf

```
conn Tunnel1
        auto=start
        left=%defaultroute
        leftid=86.183.146.3
        right=54.221.250.218
        type=tunnel
        leftauth=psk
        rightauth=psk
        keyexchange=ikev1
        ike=aes128-sha1-modp1024
        ikelifetime=8h
        esp=aes128-sha1-modp1024
        lifetime=1h
        keyingtries=%forever
        leftsubnet=0.0.0.0/0
        rightsubnet=0.0.0.0/0
        dpddelay=10s
        dpdtimeout=30s
        dpdaction=restart
        ## Please note the following line assumes you only have two tunnels in your Strongswan configuration file. This "mark" value must be unique and may need to be changed based on other entries in your configuration file.
        mark=100
        ## Uncomment the following line to utilize the script from the "Automated Tunnel Healhcheck and Failover" section. Ensure that the integer after "-m" matches the "mark" value above, and <VPC CIDR> is replaced with the CIDR of your VPC
        ## (e.g. 192.168.1.0/24)
        leftupdown="/etc/ipsec.d/aws-updown.sh -ln Tunnel1 -ll 169.254.236.62/30 -lr 169.254.236.61/30 -m 100 -r 10.0.0.0/16"

conn Tunnel2
        auto=start
        left=%defaultroute
        leftid=86.183.146.3
        right=54.237.184.170
        type=tunnel
        leftauth=psk
        rightauth=psk
        keyexchange=ikev1
        ike=aes128-sha1-modp1024
        ikelifetime=8h
        esp=aes128-sha1-modp1024
        lifetime=1h
        keyingtries=%forever
        leftsubnet=0.0.0.0/0
        rightsubnet=0.0.0.0/0
        dpddelay=10s
        dpdtimeout=30s
        dpdaction=restart
        ## Please note the following line assumes you only have two tunnels in your Strongswan configuration file. This "mark" value must be unique and may need to be changed based on other entries in your configuration file.
        mark=200
        ## Uncomment the following line to utilize the script from the "Automated Tunnel Healhcheck and Failover" section. Ensure that the integer after "-m" matches the "mark" value above, and <VPC CIDR> is replaced with the CIDR of your VPC
        ## (e.g. 192.168.1.0/24)
        leftupdown="/etc/ipsec.d/aws-updown.sh -ln Tunnel2 -ll 169.254.216.238/30 -lr 169.254.216.237/30 -m 200 -r 10.0.0.0/16"



```

- **left:** Your Raspberry PI private IP.
- **leftid:** Your Home Router public-facing IP.
- **leftsubnet:** CIDR of your Home Subnet.
- **right:** Virtual Private Gateway Tunnel IP.
- **rightsubnet:** CIDR of your VPC.

sudo nano /etc/ipsec.secrets

https://d1.awsstatic.com/whitepapers/hybrid-cloud-dns-options-for-vpc.pdf?did=wp_card&trk=wp_card
https://aws.amazon.com/blogs/security/how-to-set-up-dns-resolution-between-on-premises-networks-and-aws-by-using-unbound/
https://docs.aws.amazon.com/prescriptive-guidance/latest/patterns/set-up-integrated-dns-resolution-for-hybrid-networks-in-amazon-route-53.html
https://geektechstuff.com/2020/11/17/raspberry-pi-dhcp-server-linux-raspberry-pi/
https://serverfault.com/questions/1015309/strongswan-client-can-connect-to-the-internet-through-the-vpn-but-cannot-ssh-t 
https://www.tecmint.com/setup-a-dns-dhcp-server-using-dnsmasq-on-centos-rhel/
