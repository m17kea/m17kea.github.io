---
layout: post
title:  "AWS Control Tower"
date:   2021-04-10 14:50:21 +0100
categories: DevSetup
---

The CDK of CDKs
https://activate.workshop.aws/
https://github.com/awslabs/aws-bootstrap-kit
https://github.com/aws-samples/aws-bootstrap-kit-examples 


https://controltower.aws-management.tools/immersionday/
https://aws.amazon.com/solutions/implementations/customizations-for-aws-control-tower/?did=sl_card&trk=sl_card


https://controltower.aws-management.tools/core/cttasks/
https://aws.amazon.com/solutions/implementations/customizations-for-aws-control-tower/
https://www.youtube.com/watch?v=Zxrs6YXMidk 
https://aws.amazon.com/blogs/mt/how-to-automate-the-creation-of-multiple-accounts-in-aws-control-tower/ 
# Configure SSO
screenshot on desktop



# Additional Guard Rails
- Disallow access to IAM users without MFA
- Disallow console access to IAM users without MFA

# Subscribe to alerts 
https://docs.aws.amazon.com/controltower/latest/userguide/sns.html


aws sns subscribe --topic-arn arn:aws:sns:*homeregion*:*account*:aws-controltower-AggregateSecurityNotifications --protocol email --notification-endpoint aws-audit@yourdomain.com

# AWSCLI
```
aws configure sso
```


[profile cleancoders-sso]
sso_start_url = https://d-9c67121f62.awsapps.com/start
sso_region = eu-west-2
sso_account_id = 460804069377
sso_role_name = AWSAdministratorAccess
region = eu-west-2
output = json

problems with cdk 
https://www.matscloud.com/blog/2020/06/25/how-to-use-aws-cdk-with-aws-sso-profiles/ 
https://github.com/aws/aws-cdk/issues/5455 
https://docs.aws.amazon.com/cli/latest/userguide/cli-configure-sourcing-external.html 
https://github.com/aws/aws-cdk/issues/5053 
https://www.npmjs.com/package/cdk-sso-sync 
https://aws.amazon.com/blogs/devops/cdk-credential-plugin/ 
https://docs.aws.amazon.com/cli/latest/userguide/cli-configure-sso.html 

solved with 
pip install aws2-wrap

[profile cleancoders]
credential_process = aws2-wrap --process --profile cleancoders-sso
region = eu-west-2


aws sso login --cleancoders-sso
