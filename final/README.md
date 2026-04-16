# CD12352 - Infrastructure as Code Project Solution
# Michael Ly

## Spin up instructions

Start with provisioning the network infrastructure

```sh
aws cloudformation create-stack --stack-name udagram-network \
  --template-body file://final/udagram-network.yml \
  --parameters file://final/udagram-network-parameters.json
```

Followed by the resources needed for the webapp
```sh
aws cloudformation create-stack --stack-name udagram-webapp \
  --template-body file://final/udagram-webapp.yml \
  --parameters file://final/udagram-webapp-parameters.json
```

## Tear down instructions

```sh
aws cloudformation delete-stack --stack-name udagram-webapp \
&& aws cloudformation delete-stack --stack-name udagram-network

```

## Other considerations

### Debuggin server instances

I found that the easy and secure way to connect to the EC2 server instances was 
using Cloudshell from the AWS Console and Session Manager. Role that the EC2 instances
can assume includes SSM permissions.

To connect use the following command in Cloudshell:
```
aws ssm start-session --target i-0fe35ab458
```