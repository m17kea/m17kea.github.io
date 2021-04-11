---
layout: post
title:  "Migrating my domains to AWS Route 53"
date:   2021-04-10 14:50:21 +0100
categories: DNS
---
Once I configured an AWS account using Control Tower, I next wanted to look at migrating my domains. There are several great reasons to transfer your domains. The `.co.uk` and `.uk` domains, like many of mine, are free to transfer and free to renew. So go save yourself some money! Not only that but once migrated into the AWS ecosytem, guess what, they become code. The will be a common theme to my blog posts and that as the title of the blog should suggest is that everything is code. 

In the base stack add the following: 

{% highlight csharp %}
            var cleancodersCoUkZone = new HostedZone(this, "cleancoders.co.uk", new HostedZoneProps
            {
                ZoneName = "cleancoders.co.uk"
            });
            
            var cleancodersUKZone = new HostedZone(this, "cleancoders.uk", new HostedZoneProps
            {
                ZoneName = "cleancoders.uk"
            });
            
            var m17keaCoUkZone = new HostedZone(this, "m17kea.co.uk", new HostedZoneProps
            {
                ZoneName = "m17kea.co.uk"
            });
            
            var m17keaUkZone = new HostedZone(this, "m17kea.uk", new HostedZoneProps
            {
                ZoneName = "m17kea.uk"
            });
            
            var ss9DevelopmentsCoUkZone = new HostedZone(this, "ss9developments.co.uk", new HostedZoneProps
            {
                ZoneName = "ss9developments.co.uk"
            });
{% endhighlight %}


Now let's deploy: 

```
cdk deploy
```

Let's commit that: 
```
git add -A
git commit -m'add hosted zones'
git push
```

Now to transfer the domains:

https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/domain-transfer-to-route-53.html
 