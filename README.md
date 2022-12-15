# `devbox`

`devbox` is the EC2 instance I use for development for all of my work. Right now it probably doesn't hold much value for anyone else.

## What this does
This repo will create an EC2 instance and associated VPC in Amazon EC2 that you can use for development work. It will install:
- Go
- Rust
- AWS CLI
- Docker
- Git

## What this doesn't do
It doesn't create unicorns or configure your dev environment's dotfiles. Batteries aren't included.

## Deployment
There's a number of steps to run through to deploy this in your AWS Account.

### Prerequisites
1. VSCode
3. An AWS account
4. An EC2 keypair (see: https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/create-key-pairs.html)

### Install

You will need to [deploy the two AWS CloudFormation templates](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/cfn-console-create-stack.html) in the `stacks` folder. 
Start by deploying the `documents.yaml` file, once that has reached the status of `CREATE_COMPLETE` in the CloudFormation console, you can deploy `devbox.yaml` in the same way.

The devbox will take a while to provision with all of the software that it's told to install, you can follow along in the [SSM console](https://eu-west-1.console.aws.amazon.com/systems-manager/state-manager). After five minutes or so, your instance will be ready, you can go find the IP address for SSH connections in the [EC2 console](https://console.aws.amazon.com/ec2/home#Instances:instanceState=running;tag:Name=:devbox;v=3;$case=tags:true%5C,client:false;$regex=tags:false%5C,client:false).

### Connect VSCode to `devbox`

Install the [VSCode Remote SSH extension](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-ssh) in VSCode, and then follow the [docs for it](https://code.visualstudio.com/docs/remote/ssh).

The AMI in use is Ubuntu, so you'll need to use a SSH command similar to:
```sh
ssh ubuntu@<ip> -i <full path to keypair pem file>
```
