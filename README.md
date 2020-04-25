# cfn-foldingathome
> CloudFormation template for Folding@home on AWS spot instances.

This template creates an AWS spot instance fleet for running the [Folding@Home](https://foldingathome.org/) client.
Folding@home is a computing platform to assist disease research, for instance to find a cure for the COVID-19 virus.
The template uses G4-type instances with NVIDIA TESLA GPUs.
Please only deploy it on accounts where you have the permissions to do so.

The template installs the following software:

 - Ubuntu 18.04 LTS
 - NVidia CUDA 10.2
 - Folding@home client 7.6.9

Folding@home client is started automatically after instance initialization is complete.
Client runs until the template is removed, auto scaling group is scaled in or spot instance is reclaimed.
The template bids 100% of on-demand price and instances are unlikely to be reclaimed.
Spot instance pricing varies: expect approximately 60-70% discount for G4 instance type.

WIP Please check whether the solution works for you.

## Usage

### Launch from AWS Console

Create stack using the template S3 URL: `https://cfn-foldingathome.s3.amazonaws.com/foldingathome.yml`

| Parameter              | Description                                                                                                 |
|------------------------|-------------------------------------------------------------------------------------------------------------|
| `Anonymous`            | Folding@home fold anonymously (default true for anonymous)                                                  |
| `FoldingAtHomePasskey` | Folding@home pass key (leave empty for anonymous user)                                                      |
| `FoldingAtHomeTeam`    | Folding@home team number (default 0 for no team)                                                            |
| `FoldingAtHomeUser`    | Folding@home user name (default Anonymous for anonymous)                                                    |
| `InstanceCount`        | Scale-out count of `g4dn.xlarge` instances to run the Folding@home client                                   |
| `KeyName`              | SSH [key name](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ec2-key-pairs.html) for `ubuntu` user    |
| `Subnets`              | Subnets in VPC (for example the default VPC subnets `172.31.0.0/20`, `172.31.16.0/20` and `172.31.32.0/20`) |
| `VpcId`                | VPC for the stack (for example the default VPC `172.31.0.0/16`)                                             |

Cost of spot instances may vary by availability zone. Auto scaling group may launch instances in higher cost AZs.

| Region         | Create Stack              |
|----------------|---------------------------|
| US East (N. Virginia) `us-east-1` | [Launch Stack](https://us-east-1.console.aws.amazon.com/cloudformation/home?region=us-east-1#/stacks/create/review?templateURL=https://cfn-foldingathome.s3.amazonaws.com/foldingathome.yml&stackName=FoldingAtHome) |
| US East (Ohio) `us-east-2` | [Launch Stack](https://us-east-2.console.aws.amazon.com/cloudformation/home?region=us-east-2#/stacks/create/review?templateURL=https://cfn-foldingathome.s3.amazonaws.com/foldingathome.yml&stackName=FoldingAtHome) |
| US West (N. California) `us-west-1`| [Launch Stack](https://us-west-1.console.aws.amazon.com/cloudformation/home?region=us-west-1#/stacks/create/review?templateURL=https://cfn-foldingathome.s3.amazonaws.com/foldingathome.yml&stackName=FoldingAtHome) |
|US West (Oregon) `us-west-2` | [Launch Stack](https://us-west-2.console.aws.amazon.com/cloudformation/home?region=us-west-2#/stacks/create/review?templateURL=https://cfn-foldingathome.s3.amazonaws.com/foldingathome.yml&stackName=FoldingAtHome) |
| Africa (Cape Town) `af-south-1`| [Launch Stack](https://af-south-1.console.aws.amazon.com/cloudformation/home?region=af-south-1#/stacks/create/review?templateURL=https://cfn-foldingathome.s3.amazonaws.com/foldingathome.yml&stackName=FoldingAtHome) |
| Asia Pacific (Hong Kong) `ap-east-1`| [Launch Stack](https://ap-east-1.console.aws.amazon.com/cloudformation/home?region=ap-east-1#/stacks/create/review?templateURL=https://cfn-foldingathome.s3.amazonaws.com/foldingathome.yml&stackName=FoldingAtHome) |
| Asia Pacific (Mumbai) `ap-south-1` | [Launch Stack](https://ap-south-1.console.aws.amazon.com/cloudformation/home?region=ap-south-1#/stacks/create/review?templateURL=https://cfn-foldingathome.s3.amazonaws.com/foldingathome.yml&stackName=FoldingAtHome) |
| Asia Pacific (Seoul) `ap-northeast-2`| [Launch Stack](https://ap-northeast-2.console.aws.amazon.com/cloudformation/home?region=ap-northeast-2#/stacks/create/review?templateURL=https://cfn-foldingathome.s3.amazonaws.com/foldingathome.yml&stackName=FoldingAtHome) |
| Asia Pacific (Singapore) `ap-southeast-1` | [Launch Stack](https://ap-southeast-1.console.aws.amazon.com/cloudformation/home?region=ap-southeast-1#/stacks/create/review?templateURL=https://cfn-foldingathome.s3.amazonaws.com/foldingathome.yml&stackName=FoldingAtHome) |
| Asia Pacific (Sydney) `ap-southeast-2` | [Launch Stack](https://ap-southeast-2.console.aws.amazon.com/cloudformation/home?region=ap-southeast-2#/stacks/create/review?templateURL=https://cfn-foldingathome.s3.amazonaws.com/foldingathome.yml&stackName=FoldingAtHome) |
| Asia Pacific (Tokyo) `ap-northeast-1` | [Launch Stack](https://ap-northeast-1.console.aws.amazon.com/cloudformation/home?region=ap-northeast-1#/stacks/create/review?templateURL=https://cfn-foldingathome.s3.amazonaws.com/foldingathome.yml&stackName=FoldingAtHome) |
| Canada (Central) `ca-central-1` | [Launch Stack](https://ca-central-1.console.aws.amazon.com/cloudformation/home?region=ca-central-1#/stacks/create/review?templateURL=https://cfn-foldingathome.s3.amazonaws.com/foldingathome.yml&stackName=FoldingAtHome) |
|Europe (Frankfurt) `eu-central-1` | [Launch Stack](https://eu-central-1.console.aws.amazon.com/cloudformation/home?region=eu-central-1#/stacks/create/review?templateURL=https://cfn-foldingathome.s3.amazonaws.com/foldingathome.yml&stackName=FoldingAtHome) |
| Europe (Ireland) `eu-west-1` | [Launch Stack](https://eu-west-1.console.aws.amazon.com/cloudformation/home?region=eu-west-1#/stacks/create/review?templateURL=https://cfn-foldingathome.s3.amazonaws.com/foldingathome.yml&stackName=FoldingAtHome) |
| Europe (London) `eu-west-2` | [Launch Stack](https://eu-west-2.console.aws.amazon.com/cloudformation/home?region=eu-west-2#/stacks/create/review?templateURL=https://cfn-foldingathome.s3.amazonaws.com/foldingathome.yml&stackName=FoldingAtHome) |
| Europe (Paris) `eu-west-3` | [Launch Stack](https://eu-west-3.console.aws.amazon.com/cloudformation/home?region=eu-west-3#/stacks/create/review?templateURL=https://cfn-foldingathome.s3.amazonaws.com/foldingathome.yml&stackName=FoldingAtHome) |
| Europe (Stockholm) `eu-north-1`| [Launch Stack](https://eu-north-1.console.aws.amazon.com/cloudformation/home?region=eu-north-1#/stacks/create/review?templateURL=https://cfn-foldingathome.s3.amazonaws.com/foldingathome.yml&stackName=FoldingAtHome) |
| Middle East (Bahrain) `me-south-1` | [Launch Stack](https://me-south-1.console.aws.amazon.com/cloudformation/home?region=me-south-1#/stacks/create/review?templateURL=https://cfn-foldingathome.s3.amazonaws.com/foldingathome.yml&stackName=FoldingAtHome) |
| South America (São Paulo) `sa-east-1` | [Launch Stack](https://sa-east-1.console.aws.amazon.com/cloudformation/home?region=sa-east-1#/stacks/create/review?templateURL=https://cfn-foldingathome.s3.amazonaws.com/foldingathome.yml&stackName=FoldingAtHome) |

### Launch from CLI

To launch one instance with anonymous folding, replace the `KeyName`, `Subnets` and `VpcId` values with your SSH key name and default VPC network parameters:

```sh
aws cloudformation create-stack \
  --stack-name FoldingAtHome \
  --template-url https://cfn-foldingathome.s3.amazonaws.com/foldingathome.yml \
  --parameters \
    ParameterKey="KeyName",ParameterValue="mykeyname" \
    ParameterKey="Subnets",ParameterValue="subnet-12345678\,subnet-56781234" \
    ParameterKey="VpcId",ParameterValue="vpc-abcdefgh" \
--capabilities CAPABILITY_IAM
```

### Access Web UI

Forward port 7396 from the instance to localhost (replace `public-ip` with public IP address of the instance):

```sh
ssh ubuntu@public-ip -L 7396:localhost:7396
```

Now access the Web UI from: http://localhost:7396/

### Installation paths

Folding@home configuration is output to`/etc/fahclient/config.xml` .
Folding progress log output is written to `/var/lib/fahclient/log.txt`.
Show status of the service with `systemctl status fahclient` .

## Release History

* 20.4.25
    * Updated base Ubuntu AMI image
    * Added launch link for Africa (Cape Town) region
* 20.4.23+1
    * Prepopulate GPUs.txt to remove the need for restart 
* 20.4.23
    * Added Folding@home user name and team as optional parameters 
* 20.4.19
    * Updated client to 7.6.9
* 20.3.21
    * Add custom health check to auto-scaling group, marking instance unhealthy on Folding@home client failure
    * Changed from init script included with the package to systemd service
    * Signal failure of instance initialization script using `cfn-signal`
    * Log user instance initialization script output
* 20.3.19
    * Use instance store for `/var/lib/fahclient`
    * Improved parameter descriptions
* 20.3.17
    * Updated client to 7.5.1
    * Optimized GPU settings
    * Reviewed security group ingress
* 20.3.16
    * Initial version

## Resources

 - [Folding@home COVID-19 efforts](https://github.com/FoldingAtHome/coronavirus)
 - [Manual installation for Folding@home](https://foldingathome.org/support/faq/installation-guides/linux/manual-installation-advanced/)
 - [Ubuntu cloud images locator](https://cloud-images.ubuntu.com/locator/ec2/)
 - [Installation Instructions for CUDA Toolkit 10.2](https://developer.nvidia.com/cuda-downloads?target_os=Linux&target_arch=x86_64&target_distro=Ubuntu&target_version=1804&target_type=debnetwork)
 - [Optimize GPU Settings](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/optimize_gpu.html)

## Meta

Janne Kataja – [@jkataja](https://twitter.com/jkataja) – fistname.lastname at gmail

This software is provided "as is", without warranty of any kind.

Distributed under the Apache License v2 license. See ``LICENSE`` for more information.

GitHub [jkataja/cfn-foldingathome](https://github.com/jkataja/cfn-foldingathome)


