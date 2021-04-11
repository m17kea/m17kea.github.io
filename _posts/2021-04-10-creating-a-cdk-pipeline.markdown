---
layout: post
title:  "Creating a CDK pipeline"
date:   2021-04-10 14:50:21 +0100
categories: DNS
---


Let's start out by making a new repository...

- Create github private repo 
  - license
  - no readme 
  - no gitignore
- configure aws cli with creds and profile

```
git clone git@github.com:m17kea/cleancoders-aws.git
cd cleancoders-aws
rm LICENSE
cdk init app --language csharp
git checkout LICENSE
git add -A
git commit -m'add cdk'
git push
```

We will be using the latest pipeline features of the CDK to better align with our git workflow. We therefore need to add a new row in our `cdk.json` context:

{% highlight json %}
  "context": {
    ...
    "@aws-cdk/core:newStyleStackSynthesis": true
  }
{% endhighlight %}

Let's commit that too: 
```
git add -A
git commit -m'add default synthesizer'
git push
```

To save us adding `--profile cleancoders` to our cdk calls going forward we can add the profile in our `cdk.json` too:

{% highlight json %}
  "profile": "cleancoders"
{% endhighlight %}

Let's commit that too: 
```
git add -A
git commit -m'add default profile'
git push
```

To prepare our root AWS account for the CDK deployment we need to bootstrap it: 

```
aws sso login cleancoders-sso
cdk bootstrap 

```

One of the biggest advantages of the CDK is intellisense. To take true advantage of this, everything in the CDK ideally needs to be visible to the IDE. To make this happen and to make our lifes a great deal easier it's simpler to just add every CDK nuget packages to our project csproj: 

{% highlight xml %}
  <ItemGroup>
    <!-- CDK Construct Library dependencies -->
    <PackageReference Include="Amazon.CDK" Version="1.97.0" />
    <PackageReference Include="Amazon.CDK.Alexa.Ask" Version="1.97.0" />
    <PackageReference Include="Amazon.CDK.AppDelivery" Version="1.97.0" />
    <PackageReference Include="Amazon.CDK.Assets" Version="1.97.0" />
    <PackageReference Include="Amazon.CDK.AWS.AccessAnalyzer" Version="1.97.0" />
    <PackageReference Include="Amazon.CDK.AWS.ACMPCA" Version="1.97.0" />
    <PackageReference Include="Amazon.CDK.AWS.AmazonMQ" Version="1.97.0" />
    <PackageReference Include="Amazon.CDK.AWS.Amplify" Version="1.97.0" />
    <PackageReference Include="Amazon.CDK.AWS.APIGateway" Version="1.97.0" />
    <PackageReference Include="Amazon.CDK.AWS.APIGatewayv2" Version="1.97.0" />
    <PackageReference Include="Amazon.CDK.AWS.APIGatewayv2.Authorizers" Version="1.97.0" />
    <PackageReference Include="Amazon.CDK.AWS.APIGatewayv2.Integrations" Version="1.97.0" />
    <PackageReference Include="Amazon.CDK.AWS.AppConfig" Version="1.97.0" />
    <PackageReference Include="Amazon.CDK.AWS.AppFlow" Version="1.97.0" />
    <PackageReference Include="Amazon.CDK.AWS.ApplicationAutoScaling" Version="1.97.0" />
    <PackageReference Include="Amazon.CDK.AWS.ApplicationInsights" Version="1.97.0" />
    <PackageReference Include="Amazon.CDK.AWS.AppMesh" Version="1.97.0" />
    <PackageReference Include="Amazon.CDK.AWS.AppStream" Version="1.97.0" />
    <PackageReference Include="Amazon.CDK.AWS.AppSync" Version="1.97.0" />
    <PackageReference Include="Amazon.CDK.AWS.Athena" Version="1.97.0" />
    <PackageReference Include="Amazon.CDK.AWS.AuditManager" Version="1.97.0" />
    <PackageReference Include="Amazon.CDK.AWS.AutoScaling" Version="1.97.0" />
    <PackageReference Include="Amazon.CDK.AWS.AutoScaling.Common" Version="1.97.0" />
    <PackageReference Include="Amazon.CDK.AWS.AutoScaling.HookTargets" Version="1.97.0" />
    <PackageReference Include="Amazon.CDK.AWS.AutoScalingPlans" Version="1.97.0" />
    <PackageReference Include="Amazon.CDK.AWS.Backup" Version="1.97.0" />
    <PackageReference Include="Amazon.CDK.AWS.Batch" Version="1.97.0" />
    <PackageReference Include="Amazon.CDK.AWS.Budgets" Version="1.97.0" />
    <PackageReference Include="Amazon.CDK.AWS.Cassandra" Version="1.97.0" />
    <PackageReference Include="Amazon.CDK.AWS.CE" Version="1.97.0" />
    <PackageReference Include="Amazon.CDK.AWS.CertificateManager" Version="1.97.0" />
    <PackageReference Include="Amazon.CDK.AWS.Chatbot" Version="1.97.0" />
    <PackageReference Include="Amazon.CDK.AWS.Cloud9" Version="1.97.0" />
    <PackageReference Include="Amazon.CDK.AWS.CloudFormation" Version="1.97.0" />
    <PackageReference Include="Amazon.CDK.AWS.CloudFront" Version="1.97.0" />
<!--    <PackageReference Include="Amazon.CDK.AWS.CloudFront.Experimental" Version="1.97.0" />-->
    <PackageReference Include="Amazon.CDK.AWS.CloudFront.Origins" Version="1.97.0" />
    <PackageReference Include="Amazon.CDK.AWS.CloudTrail" Version="1.97.0" />
    <PackageReference Include="Amazon.CDK.AWS.CloudWatch" Version="1.97.0" />
    <PackageReference Include="Amazon.CDK.AWS.CloudWatch.Actions" Version="1.97.0" />
    <PackageReference Include="Amazon.CDK.AWS.CodeArtifact" Version="1.97.0" />
    <PackageReference Include="Amazon.CDK.AWS.CodeBuild" Version="1.97.0" />
    <PackageReference Include="Amazon.CDK.AWS.CodeCommit" Version="1.97.0" />
    <PackageReference Include="Amazon.CDK.AWS.CodeDeploy" Version="1.97.0" />
    <PackageReference Include="Amazon.CDK.AWS.CodeGuruProfiler" Version="1.97.0" />
    <PackageReference Include="Amazon.CDK.AWS.CodeGuruReviewer" Version="1.97.0" />
    <PackageReference Include="Amazon.CDK.AWS.CodePipeline" Version="1.97.0" />
    <PackageReference Include="Amazon.CDK.AWS.CodePipeline.Actions" Version="1.97.0" />
    <PackageReference Include="Amazon.CDK.AWS.CodeStar" Version="1.97.0" />
    <PackageReference Include="Amazon.CDK.AWS.CodeStarConnections" Version="1.97.0" />
    <PackageReference Include="Amazon.CDK.AWS.CodeStarNotifications" Version="1.97.0" />
    <PackageReference Include="Amazon.CDK.AWS.Cognito" Version="1.97.0" />
    <PackageReference Include="Amazon.CDK.AWS.Config" Version="1.97.0" />
    <PackageReference Include="Amazon.CDK.AWS.DataBrew" Version="1.97.0" />
    <PackageReference Include="Amazon.CDK.AWS.DataPipeline" Version="1.97.0" />
    <PackageReference Include="Amazon.CDK.AWS.DataSync" Version="1.97.0" />
    <PackageReference Include="Amazon.CDK.AWS.DAX" Version="1.97.0" />
    <PackageReference Include="Amazon.CDK.AWS.Detective" Version="1.97.0" />
    <PackageReference Include="Amazon.CDK.AWS.DevOpsGuru" Version="1.97.0" />
    <PackageReference Include="Amazon.CDK.AWS.DirectoryService" Version="1.97.0" />
    <PackageReference Include="Amazon.CDK.AWS.DLM" Version="1.97.0" />
    <PackageReference Include="Amazon.CDK.AWS.DMS" Version="1.97.0" />
    <PackageReference Include="Amazon.CDK.AWS.DocDB" Version="1.97.0" />
    <PackageReference Include="Amazon.CDK.AWS.DynamoDB" Version="1.97.0" />
    <PackageReference Include="Amazon.CDK.AWS.DynamoDB.Global" Version="1.97.0" />
    <PackageReference Include="Amazon.CDK.AWS.EC2" Version="1.97.0" />
    <PackageReference Include="Amazon.CDK.AWS.ECR" Version="1.97.0" />
<!--    <PackageReference Include="Amazon.CDK.AWS.Ecr.Assets" Version="1.97.0" />-->
    <PackageReference Include="Amazon.CDK.AWS.ECS" Version="1.97.0" />
    <PackageReference Include="Amazon.CDK.AWS.ECS.Patterns" Version="1.97.0" />
    <PackageReference Include="Amazon.CDK.AWS.EFS" Version="1.97.0" />
    <PackageReference Include="Amazon.CDK.AWS.EKS" Version="1.97.0" />
    <PackageReference Include="Amazon.CDK.AWS.EKS.Legacy" Version="1.97.0" />
    <PackageReference Include="Amazon.CDK.AWS.ElastiCache" Version="1.97.0" />
    <PackageReference Include="Amazon.CDK.AWS.ElasticBeanstalk" Version="1.97.0" />
    <PackageReference Include="Amazon.CDK.AWS.ElasticLoadBalancing" Version="1.97.0" />
    <PackageReference Include="Amazon.CDK.AWS.ElasticLoadBalancingV2" Version="1.97.0" />
    <PackageReference Include="Amazon.CDK.AWS.ElasticLoadBalancingV2.Actions" Version="1.97.0" />
    <PackageReference Include="Amazon.CDK.AWS.ElasticLoadBalancingV2.Targets" Version="1.97.0" />
    <PackageReference Include="Amazon.CDK.AWS.Elasticsearch" Version="1.97.0" />
    <PackageReference Include="Amazon.CDK.AWS.EMR" Version="1.97.0" />
    <PackageReference Include="Amazon.CDK.AWS.EMRContainers" Version="1.97.0" />
    <PackageReference Include="Amazon.CDK.AWS.Events" Version="1.97.0" />
    <PackageReference Include="Amazon.CDK.AWS.Events.Targets" Version="1.97.0" />
    <PackageReference Include="Amazon.CDK.AWS.EventSchemas" Version="1.97.0" />
    <PackageReference Include="Amazon.CDK.AWS.FMS" Version="1.97.0" />
    <PackageReference Include="Amazon.CDK.AWS.FSx" Version="1.97.0" />
    <PackageReference Include="Amazon.CDK.AWS.GameLift" Version="1.97.0" />
    <PackageReference Include="Amazon.CDK.AWS.GlobalAccelerator" Version="1.97.0" />
    <PackageReference Include="Amazon.CDK.AWS.Glue" Version="1.97.0" />
    <PackageReference Include="Amazon.CDK.AWS.Greengrass" Version="1.97.0" />
    <PackageReference Include="Amazon.CDK.AWS.GreengrassV2" Version="1.97.0" />
    <PackageReference Include="Amazon.CDK.AWS.GuardDuty" Version="1.97.0" />
    <PackageReference Include="Amazon.CDK.AWS.IAM" Version="1.97.0" />
    <PackageReference Include="Amazon.CDK.AWS.ImageBuilder" Version="1.97.0" />
    <PackageReference Include="Amazon.CDK.AWS.Inspector" Version="1.97.0" />
    <PackageReference Include="Amazon.CDK.AWS.IoT" Version="1.97.0" />
    <PackageReference Include="Amazon.CDK.AWS.IoT1Click" Version="1.97.0" />
    <PackageReference Include="Amazon.CDK.AWS.IoTAnalytics" Version="1.97.0" />
    <PackageReference Include="Amazon.CDK.AWS.IoTEvents" Version="1.97.0" />
    <PackageReference Include="Amazon.CDK.AWS.IoTSiteWise" Version="1.97.0" />
    <PackageReference Include="Amazon.CDK.AWS.IoTThingsGraph" Version="1.97.0" />
    <PackageReference Include="Amazon.CDK.AWS.IoTWireless" Version="1.97.0" />
    <PackageReference Include="Amazon.CDK.AWS.IVS" Version="1.97.0" />
    <PackageReference Include="Amazon.CDK.AWS.Kendra" Version="1.97.0" />
    <PackageReference Include="Amazon.CDK.AWS.Kinesis" Version="1.97.0" />
    <PackageReference Include="Amazon.CDK.AWS.KinesisAnalytics" Version="1.97.0" />
    <PackageReference Include="Amazon.CDK.AWS.KinesisAnalyticsFlink" Version="1.97.0" />
    <PackageReference Include="Amazon.CDK.AWS.KinesisFirehose" Version="1.97.0" />
    <PackageReference Include="Amazon.CDK.AWS.KMS" Version="1.97.0" />
    <PackageReference Include="Amazon.CDK.AWS.LakeFormation" Version="1.97.0" />
    <PackageReference Include="Amazon.CDK.AWS.Lambda" Version="1.97.0" />
    <PackageReference Include="Amazon.CDK.AWS.Lambda.Destinations" Version="1.97.0" />
    <PackageReference Include="Amazon.CDK.AWS.Lambda.EventSources" Version="1.97.0" />
    <PackageReference Include="Amazon.CDK.AWS.Lambda.Nodejs" Version="1.97.0" />
    <PackageReference Include="Amazon.CDK.AWS.Lambda.Python" Version="1.97.0" />
    <PackageReference Include="Amazon.CDK.AWS.LicenseManager" Version="1.97.0" />
    <PackageReference Include="Amazon.CDK.AWS.Logs" Version="1.97.0" />
    <PackageReference Include="Amazon.CDK.AWS.Logs.Destinations" Version="1.97.0" />
    <PackageReference Include="Amazon.CDK.AWS.LookoutVision" Version="1.97.0" />
    <PackageReference Include="Amazon.CDK.AWS.Macie" Version="1.97.0" />
    <PackageReference Include="Amazon.CDK.AWS.ManagedBlockchain" Version="1.97.0" />
    <PackageReference Include="Amazon.CDK.AWS.MediaConnect" Version="1.97.0" />
    <PackageReference Include="Amazon.CDK.AWS.MediaConvert" Version="1.97.0" />
    <PackageReference Include="Amazon.CDK.AWS.MediaLive" Version="1.97.0" />
    <PackageReference Include="Amazon.CDK.AWS.MediaPackage" Version="1.97.0" />
    <PackageReference Include="Amazon.CDK.AWS.MediaStore" Version="1.97.0" />
    <PackageReference Include="Amazon.CDK.AWS.MSK" Version="1.97.0" />
    <PackageReference Include="Amazon.CDK.AWS.MWAA" Version="1.97.0" />
    <PackageReference Include="Amazon.CDK.AWS.Neptune" Version="1.97.0" />
    <PackageReference Include="Amazon.CDK.AWS.NetworkFirewall" Version="1.97.0" />
    <PackageReference Include="Amazon.CDK.AWS.NetworkManager" Version="1.97.0" />
    <PackageReference Include="Amazon.CDK.AWS.OpsWorks" Version="1.97.0" />
    <PackageReference Include="Amazon.CDK.AWS.OpsWorksCM" Version="1.97.0" />
    <PackageReference Include="Amazon.CDK.AWS.Pinpoint" Version="1.97.0" />
    <PackageReference Include="Amazon.CDK.AWS.PinpointEmail" Version="1.97.0" />
    <PackageReference Include="Amazon.CDK.AWS.QLDB" Version="1.97.0" />
    <PackageReference Include="Amazon.CDK.AWS.QuickSight" Version="1.97.0" />
    <PackageReference Include="Amazon.CDK.AWS.RAM" Version="1.97.0" />
    <PackageReference Include="Amazon.CDK.AWS.RDS" Version="1.97.0" />
    <PackageReference Include="Amazon.CDK.AWS.Redshift" Version="1.97.0" />
    <PackageReference Include="Amazon.CDK.AWS.ResourceGroups" Version="1.97.0" />
    <PackageReference Include="Amazon.CDK.AWS.RoboMaker" Version="1.97.0" />
    <PackageReference Include="Amazon.CDK.AWS.Route53" Version="1.97.0" />
    <PackageReference Include="Amazon.CDK.AWS.Route53.Patterns" Version="1.97.0" />
    <PackageReference Include="Amazon.CDK.AWS.Route53.Targets" Version="1.97.0" />
    <PackageReference Include="Amazon.CDK.AWS.Route53Resolver" Version="1.97.0" />
    <PackageReference Include="Amazon.CDK.AWS.S3" Version="1.97.0" />
    <PackageReference Include="Amazon.CDK.AWS.S3.Assets" Version="1.97.0" />
    <PackageReference Include="Amazon.CDK.AWS.S3.Deployment" Version="1.97.0" />
    <PackageReference Include="Amazon.CDK.AWS.S3.Notifications" Version="1.97.0" />
    <PackageReference Include="Amazon.CDK.AWS.S3Outposts" Version="1.97.0" />
    <PackageReference Include="Amazon.CDK.AWS.Sagemaker" Version="1.97.0" />
    <PackageReference Include="Amazon.CDK.AWS.SAM" Version="1.97.0" />
    <PackageReference Include="Amazon.CDK.AWS.SDB" Version="1.97.0" />
    <PackageReference Include="Amazon.CDK.AWS.SecretsManager" Version="1.97.0" />
    <PackageReference Include="Amazon.CDK.AWS.SecurityHub" Version="1.97.0" />
    <PackageReference Include="Amazon.CDK.AWS.ServiceCatalog" Version="1.97.0" />
    <PackageReference Include="Amazon.CDK.AWS.ServiceCatalogAppRegistry" Version="1.97.0" />
    <PackageReference Include="Amazon.CDK.AWS.ServiceDiscovery" Version="1.97.0" />
    <PackageReference Include="Amazon.CDK.AWS.SES" Version="1.97.0" />
    <PackageReference Include="Amazon.CDK.AWS.SES.Actions" Version="1.97.0" />
    <PackageReference Include="Amazon.CDK.AWS.Signer" Version="1.97.0" />
    <PackageReference Include="Amazon.CDK.AWS.SNS" Version="1.97.0" />
    <PackageReference Include="Amazon.CDK.AWS.SNS.Subscriptions" Version="1.97.0" />
    <PackageReference Include="Amazon.CDK.AWS.SQS" Version="1.97.0" />
    <PackageReference Include="Amazon.CDK.AWS.SSM" Version="1.97.0" />
    <PackageReference Include="Amazon.CDK.AWS.SSO" Version="1.97.0" />
    <PackageReference Include="Amazon.CDK.AWS.StepFunctions" Version="1.97.0" />
    <PackageReference Include="Amazon.CDK.AWS.StepFunctions.Tasks" Version="1.97.0" />
    <PackageReference Include="Amazon.CDK.AWS.Synthetics" Version="1.97.0" />
    <PackageReference Include="Amazon.CDK.AWS.Timestream" Version="1.97.0" />
    <PackageReference Include="Amazon.CDK.AWS.Transfer" Version="1.97.0" />
    <PackageReference Include="Amazon.CDK.AWS.WAF" Version="1.97.0" />
    <PackageReference Include="Amazon.CDK.AWS.WAFRegional" Version="1.97.0" />
    <PackageReference Include="Amazon.CDK.AWS.WAFv2" Version="1.97.0" />
    <PackageReference Include="Amazon.CDK.AWS.WorkSpaces" Version="1.97.0" />
    <PackageReference Include="Amazon.CDK.CdkAssets.Schema" Version="1.97.0" />
    <PackageReference Include="Amazon.CDK.CloudAssembly.Schema" Version="1.97.0" />
    <PackageReference Include="Amazon.CDK.CloudFormation.Include" Version="1.97.0" />
<!--    <PackageReference Include="Amazon.CDK.CustomResources" Version="1.97.0" />-->
    <PackageReference Include="Amazon.CDK.CXAPI" Version="1.97.0" />
    <PackageReference Include="Amazon.CDK.LambdaLayer.AwsCli" Version="1.97.0" />
    <PackageReference Include="Amazon.CDK.LambdaLayer.Kubectl" Version="1.97.0" />
    <PackageReference Include="Amazon.CDK.Pipelines" Version="1.97.0" />
    <PackageReference Include="Amazon.CDK.RegionInfo" Version="1.97.0" />
    <PackageReference Include="Amazon.CDK.Yaml.Cfn" Version="1.97.0" />

    <!-- jsii Roslyn analyzers (un-comment to obtain compile-time checks for missing required props
    <PackageReference Include="Amazon.Jsii.Analyzers" Version="*" PrivateAssets="all" />
    -->
    <PackageReference Include="Amazon.Jsii.Analyzers" Version="*" PrivateAssets="all" />
    <PackageReference Include="Microsoft.CodeAnalysis" Version="3.9.0" />

  </ItemGroup>
{% endhighlight %}

Obviously replacing 1.97.0 with what ever the latest version may be. 

Let's commit that: 
```
git add -A
git commit -m'add all cdk packages'
git push
```

The guys at AWS have already taken this on board and in version 2 of the SDK everything will be contained in a single package, making the above 200 lines redundent. 

Finally, let do what we came here to do...

In the base stack, let's add a test bucket:

{% highlight csharp %}
using Amazon.CDK;
using Amazon.CDK.AWS.S3;

namespace CleancodersCdk
{
    public class CleancodersCdkStack : Stack
    {
        internal CleancodersCdkStack(Construct scope, string id, IStackProps props = null) : base(scope, id, props)
        {
            var bucket = new Bucket(this, "mgmt", new BucketProps
            {
                BucketName = "cleancoders-test",
                RemovalPolicy = RemovalPolicy.DESTROY
            });
        }
    }
}
{% endhighlight %}

We'll add a new class for the pipeline stage: 

{% highlight csharp %}
#nullable enable
using Amazon.CDK;
using Construct = Constructs.Construct;

namespace CleancodersCdk
{
    public class CleancodersCdkStage : Stage
    {
        public CleancodersCdkStage(Construct scope, string id, IStageProps? props = null) : base(scope, id, props)
        {
            var stack = new CleancodersCdkStack(this, $"{id}-stack");
        }
    }
}
{% endhighlight %}

Finally let's add the pipeline: 

{% highlight csharp %}
using Amazon.CDK;
using Amazon.CDK.AWS.CodePipeline;
using Amazon.CDK.AWS.CodePipeline.Actions;
using Amazon.CDK.Pipelines;

namespace CleancodersCdk
{
    public class PipelineStack : Stack
    {
        internal PipelineStack(Construct scope, string id, IStackProps props = null) : base(scope, id, props)
        {
            var sourceArtifact = new Artifact_();
            var cloudAssemblyArtifact = new Artifact_();

            var sourceAction = new GitHubSourceAction(new GitHubSourceActionProps
            {
                ActionName = "GitHub",
                Output = sourceArtifact,
                OauthToken = SecretValue.SecretsManager("GitHubToken"),
                Owner = "m17kea",
                Repo = "cleancoders-cdk",
                Branch = "main", 
                Trigger = GitHubTrigger.WEBHOOK
            });

            var synthAction = new SimpleSynthAction(new SimpleSynthActionProps
            {
                SourceArtifact = sourceArtifact,
                CloudAssemblyArtifact = cloudAssemblyArtifact,
                InstallCommands = new[]
                {
                    "npm install -g aws-cdk"
                },
                BuildCommands = new[]
                {
                    "dotnet build src"
                },
                SynthCommand = "cdk synth"
            });

            var pipeline = new CdkPipeline(this, "pipeline", new CdkPipelineProps
            {
                CloudAssemblyArtifact = cloudAssemblyArtifact,
                SourceAction = sourceAction,
                SynthAction = synthAction
            });
            
            var cleancodersStage = new CleancodersCdkStage(this, "cleancoders");

            pipeline.AddApplicationStage(cleancodersStage);
        }
    }
}
{% endhighlight %}

You'll notice that we are using AWS Secrets manager to store the GitHub token allowing access to the repo. Once you've created one ([instructions here](https://docs.github.com/en/github/authenticating-to-github/creating-a-personal-access-token)), run the following command in terminal to upload it. 

```
aws sso login --profile cleancoders-sso
aws secretsmanager create-secret --name GitHubToken --secret-string ghp_NEVERPASTEITSOMEWHEREUNSAFE --profile cleancoders 
history -c
```

The last command there clears you shell history to protect that secret token.

For the last piece of the puzzle let's shore up the `Program.cs` to use the new PipelineStack:

{% highlight csharp %}
using Amazon.CDK;
using System;
using System.Collections.Generic;
using System.Linq;

namespace CleancodersCdk
{
    sealed class Program
    {
        public static void Main(string[] args)
        {
            var app = new App();
            new PipelineStack(app, "PipelineStack");

            app.Synth();
        }
    }
}

{% endhighlight %}

Now let's deploy: 

```
cdk deploy
```

This is the last cdk deploy that we'll ever need to run. From this point forward pushing commits to the git repo will trigger this pipeline to update the
assets.

Let's commit that: 
```
git add -A
git commit -m'switch to git based workflow'
git push
```

