---
layout: post
title:  "Migrating my domains to AWS Route 53"
date:   2021-04-10 14:50:21 +0100
categories: DNS
---
Once I configured an AWS account using Control Tower, I next wanted to look at migrating my domains. There are several great reasons to transfer your domains. The `.co.uk` and `.uk` domains, like many of mine, are free to transfer and free to renew. So go save yourself some money! Not only that but once migrated into the AWS ecosytem, guess what, they become code. The will be a common theme to my blog posts and as the title of the blog should suggest,  everything is code. 

The first step in migrating a domain to Route 53 is to replicate the DNS from your existing provider. This is a quite complicated process so I would only tackle it if you understand everything in this [post](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/migrate-dns-domain-in-use.html#migrate-dns-create-hosted-zone). 

Let's look at steps 2/3, we need to create a hosted zone with all the required records. I use g-suite for all my email domains so I'm going to use a great feature of the CDK, inheritance. I'm going to extend the HostedZone to encapsulate all of the common setup I need to do for g-suite mx and verification records. Create a folder in the root of the project called `Route53` add a new class called `GoogleHostedZoneProps` as follows: 

{% highlight csharp %}
using Amazon.CDK.AWS.Route53;

namespace CleancodersCdk.Route53
{
    internal class GoogleHostedZoneProps : IHostedZoneProps
    {
        public string GoogleSiteVerification { get; set; }
        public string ZoneName { get; set; }
        public string ForwardingDomain { get; set; }
    }
}
{% endhighlight %}

and another called `GoogleHostedZone`:

{% highlight csharp %}
using Amazon.CDK;
using Amazon.CDK.AWS.Route53;

namespace CleancodersCdk.Route53
{
    internal class GoogleHostedZone : HostedZone
    {
        public GoogleHostedZone(Construct scope, string id, GoogleHostedZoneProps props) : base(scope,id,props)
        {
            var hostedZone = new HostedZone(this, id, new HostedZoneProps
            {
                ZoneName = props.ZoneName
            });
          
            new TxtRecord(this, $"{id}-txt", new TxtRecordProps
            {
                Zone = hostedZone,
                Values = new[]
                {
                    props.GoogleSiteVerification
                }
            });
            
            new MxRecord(this, $"{id}-mx", new MxRecordProps
            {
                Zone = hostedZone,
                Values = new IMxRecordValue[]
                {
                    new MxRecordValue
                    {
                        HostName = "ASPMX.L.GOOGLE.COM.",
                        Priority = 1
                    },
                    new MxRecordValue
                    {
                        HostName = "ALT1.ASPMX.L.GOOGLE.COM.",
                        Priority = 5
                    },
                    new MxRecordValue
                    {
                        HostName = "ALT2.ASPMX.L.GOOGLE.COM.",
                        Priority = 5
                    },
                    new MxRecordValue
                    {
                        HostName = "ASPMX2.GOOGLEMAIL.COM.",
                        Priority = 10
                    },
                    new MxRecordValue
                    {
                        HostName = "ASPMX3.GOOGLEMAIL.COM.",
                        Priority = 10
                    }
                }
            });

            new CnameRecord(this, $"{id}-cname-calendar", new CnameRecordProps
            {
                Zone = hostedZone,
                RecordName = "calendar",
                DomainName = "ghs.googlehosted.com."
            });
            
            new CnameRecord(this, $"{id}-cname-drive", new CnameRecordProps
            {
                Zone = hostedZone,
                RecordName = "drive",
                DomainName = "ghs.googlehosted.com."
            });
            
            new CnameRecord(this, $"{id}-cname-mail", new CnameRecordProps
            {
                Zone = hostedZone,
                RecordName = "mail",
                DomainName = "ghs.googlehosted.com."
            });
            
            new CnameRecord(this, $"{id}-cname-sites", new CnameRecordProps
            {
                Zone = hostedZone,
                RecordName = "sites",
                DomainName = "ghs.googlehosted.com."
            });
        }
    }
}
{% endhighlight %}

[Choosing between alias and non-alias records](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/resource-record-sets-choosing-alias-non-alias.html)

https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/SOA-NSrecords.html 
aws route53 list-resource-record-sets --hosted-zone-id Z101149925M41O0SKBGA2 --profile cleancoders
https://docs.aws.amazon.com/cli/latest/reference/route53/list-resource-record-sets.html 
https://www.cyberciti.biz/faq/how-to-see-time-to-live-ttl-for-a-dns-record/ 
#TODO : extract NS record with jq, edit TTL to 60 seconds and push back up


Change NS at existing DNS:

test -  
`dig +nocmd +noall +answer +ttlid NS ss9developments.co.uk`
| Domain                  | TTL     | X     | Type  | Url                         |  
| ----------------------- | ------- | ----- | ----- | --------------------------- |
| ss9developments.co.uk.  |	  60	|   IN  |	NS  | ns-1960.awsdns-53.co.uk.    |
| ss9developments.co.uk.  |   60	|   IN	|   NS  | ns-847.awsdns-41.net.       |
| ss9developments.co.uk.  |   60	|   IN	|   NS	| ns-235.awsdns-29.com.       |
| ss9developments.co.uk.  |   60	|   IN	|   NS	| ns-1431.awsdns-50.org.      |

https://aws.amazon.com/premiumsupport/knowledge-center/redirect-domain-route-53/


Set the Gandi IPS flag with your existing provider. 


Enable dnssec

https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/dns-configuring-dnssec-enable-signing.html 


https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/dns-configuring-dnssec-cli.html

```

```

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
 