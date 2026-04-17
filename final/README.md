# CD12352 - Infrastructure as Code Project Solution
# Michael Ly

## Spin up instructions

Start with provisioning the network infrastructure

```sh
aws cloudformation create-stack --stack-name udagram-network \
  --template-body file://final/network.yml \
  --parameters file://final/network-parameters.json
```

Followed by the resources needed for the webapp. 

**NOTE:** The ```--capabilities``` flag is needed to create IAM resource

```sh
aws cloudformation create-stack --stack-name udagram-webapp \
  --template-body file://final/udagram.yml \
  --parameters file://final/udagram-parameters.json \
  --capabilities CAPABILITY_NAMED_IAM
```

## Tear down instructions

```sh
aws cloudformation delete-stack --stack-name udagram-webapp \
&& aws cloudformation delete-stack --stack-name udagram-network

```

## Verify CloudFormation Stack

After a successful execution of the Cloudformation stack for **udagram-webapp**, 
navigate to the link provided in the output by **WebAppLBDNSName**.

[Link to Udagram](http://udagra-webap-mnqbkwa6up29-1074075706.us-east-1.elb.amazonaws.com/)

## Other considerations

### Updating stack

This ```--create-stack``` only works for creating the stack for the first time. 
When updates are needed, switch to ```--update-stack``` .

### Debuggin server instances

I found that the easy and secure way to connect to the EC2 server instances was 
using Cloudshell from the AWS Console and Session Manager. Role that the EC2 instances
can assume includes SSM permissions.

To connect use the following command in Cloudshell:
```
aws ssm start-session --target i-0fe35ab458
```