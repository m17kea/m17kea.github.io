---
layout: post
title:  "Developer setup - the basics"
date:   2021-04-10 14:50:21 +0100
categories: DevSetup
---

## Lambda debugging locally 
### .Net Core setup and configuration
https://docs.aws.amazon.com/sdk-for-net/latest/developer-guide/net-dg-config-netcore.html

### Jetbrains toolkit 
https://aws.amazon.com/rider/
https://docs.aws.amazon.com/toolkit-for-jetbrains/latest/userguide/welcome.html
https://docs.aws.amazon.com/toolkit-for-jetbrains/latest/userguide/run-debug-configurations-dialog-local.html

### SAM
https://docs.aws.amazon.com/serverless-application-model/latest/developerguide/building-layers.html
https://docs.aws.amazon.com/lambda/latest/dg/lambda-runtimes.html
https://docs.aws.amazon.com/serverless-application-model/latest/developerguide/sam-cli-command-reference-sam-build.html
https://hub.docker.com/r/amazon/aws-sam-cli-build-image-provided.al2
https://docs.aws.amazon.com/serverless-application-model/latest/developerguide/serverless-image-repositories.html

### SAM Layers
https://aws.amazon.com/blogs/compute/working-with-aws-lambda-and-lambda-layers-in-aws-sam/
https://docs.aws.amazon.com/serverless-application-model/latest/developerguide/sam-resource-layerversion.html

### AWS credentials 
https://docs.aws.amazon.com/cli/latest/userguide/cli-configure-envvars.html

### Connecting to localhost services 
https://github.com/aws/aws-sam-cli/issues/260

Swap localhost with docker.for.mac.localhost 

### Lambda layers
https://docs.aws.amazon.com/serverless-application-model/latest/developerguide/building-layers.html
https://docs.aws.amazon.com/serverless-application-model/latest/developerguide/serverless-sam-cli-layers.html

### Step functions 
docs
https://aws.amazon.com/getting-started/hands-on/create-a-serverless-workflow-step-functions-lambda/
https://docs.aws.amazon.com/step-functions/latest/dg/callback-task-sample-sqs.html
https://docs.aws.amazon.com/sdkfornet/v3/apidocs/items/StepFunctions/TStepFunctionsClient.html
https://docs.aws.amazon.com/step-functions/latest/dg/concepts-input-output-filtering.html
https://docs.aws.amazon.com/step-functions/latest/dg/sample-map-state.html

cdk
https://github.com/cdk-patterns/serverless/blob/main/the-saga-stepfunction/typescript/lambda-fns/sagaLambda.ts

invoke
https://github.com/sachabarber/AWS/blob/master/Compute/SimpleStepFunction/InvokeStatemachine/Program.cs

articlees
https://medium.com/swlh/step-functions-dynamic-parallelism-fan-out-explained-83f911d5990
https://aws.amazon.com/blogs/aws/new-step-functions-support-for-dynamic-parallelism/


## Dependency on libgdiplus

### Lambda layers
https://github.com/aws/aws-lambda-dotnet/issues/516#issuecomment-675653204
https://github.com/rv-dtomaz/lambda-layer-system-drawing/blob/master/bv-lambda-layer.zip


### Lambda runtimes 
https://docs.aws.amazon.com/lambda/latest/dg/lambda-runtimes.html

### Lambda layers with SAM
https://aws.amazon.com/blogs/compute/working-with-aws-lambda-and-lambda-layers-in-aws-sam/

### dll import failing 
https://stackoverflow.com/questions/58506682/dllimport-not-working-on-docker-dllnotfoundexception


### find dependencies
https://stackoverflow.com/questions/16806745/how-to-find-dependent-libraries
https://unix.stackexchange.com/questions/120015/how-to-find-out-the-dynamic-libraries-executables-loads-when-run

linux - ldd file_name
mac otool -L 

