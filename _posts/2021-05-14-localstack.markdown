---
layout: post
title:  "Developer setup - the basics"
date:   2021-04-10 14:50:21 +0100
categories: DevSetup
---


# Localstack
https://github.com/localstack/localstack
https://github.com/localstack/localstack/issues/1557

### AWS CLIs for Localstack
https://github.com/localstack/aws-cdk-local
https://github.com/localstack/amplify-js-local
https://github.com/localstack/awscli-local

https://github.com/localstack/aws-sam-cli-local
due to having gcc install i needed to force clang gcc to install the watchdog package: 
CC=/usr/bin/gcc && pip install aws-sam-cli-local

### Visibility of deployed services in Localstack

https://getcommandeer.com/

### SAM
https://docs.aws.amazon.com/serverless-application-model/latest/developerguide/what-is-sam.html
https://docs.aws.amazon.com/serverless-application-model/latest/developerguide/sam-cli-command-reference-sam-deploy.html
https://aws.amazon.com/blogs/compute/best-practices-for-organizing-larger-serverless-applications/


### Lambda .Net core configuration
https://docs.aws.amazon.com/sdk-for-net/latest/developer-guide/net-dg-config-netcore.html

### Synchronous Lambda from within c#
https://bobtomlin-70659.medium.com/how-to-invoke-an-aws-lambda-function-node-js-from-c-f777b31ec307

### Subscribe to SNS
https://docs.aws.amazon.com/sdkfornet/latest/apidocs/items/MSNSSNSSubscribeSubscribeRequestNET35.html
https://aws.amazon.com/blogs/developer/subscribing-websites-to-amazon-sns-topics/

### Debug remote lambda 
https://zaccharles.medium.com/remotely-debugging-net-in-aws-lambda-with-breakpoints-88ff57aae1c6 


