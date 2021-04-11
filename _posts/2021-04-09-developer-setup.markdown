---
layout: post
title:  "AWS Control Tower"
date:   2021-04-10 14:50:21 +0100
categories: DevSetup
---

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
