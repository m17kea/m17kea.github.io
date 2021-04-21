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
conn home-to-aws
 type=tunnel
 authby=secret
 #left=%defaultroute
 left=192.168.1.236
 leftid=81.156.224.240
 leftnexthop=%defaultroute
 leftsubnet=192.168.1.0/24
 right=52.47.119.151
 rightsubnet=10.0.0.0/16
 pfs=yes
 auto=start

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
