## ND9991 - Project2: Deploy a high-availability web app using CloudFormation
The project scenario is to deploy a new web application to the AWS infrastructure.
The deployment is done from a local computer via the AWS Command Line Interface (CLI). The AWS CloudFormation service is used for the creation and configuration of all infrastructure.

The content within the scripts folder is partially based on the supporting material and starter code from the repository [nd9991-c2-Infrastructure-as-Code-v1](https://github.com/udacity/nd9991-c2-Infrastructure-as-Code-v1).

### Overview on CloudFormation Stacks
The infrastructure is divided into two CloudFormation stacks:
1. Network (Network.yml): creates all network infrastructure for the web applications.
2. Servers (servers.yml): creates the web application servers.

Please note that the infrastructure for the network needs to be created prior to the servers. The servers require the output from the network stacks.
A detailed overview of scripts, templates and parameters is found below in section [Project Content](#project-content)

### Dependencies
##### 1. AWS account
You would require to have an AWS account to be able to build cloud infrastructure.

##### 2. System setup
The shell scripts have been written for a Linux operation system. Additionally is necessary to have the AWS CLI installed.

##### 3. VS code editor
An editor would be helpful to visualize the image as well as code. Download the VS Code editor [here](https://code.visualstudio.com/download).

##### 4. An account on www.lucidchart.com for the adaptation of the diagram
A free user-account on [www.lucidchart.com](www.lucidchart.com) is required to be able to draw the web app architecture diagrams for AWS.

### Configuration
#### Configure profile "udacity" in AWS CLI
```bash
# configure profile
aws configure --profile AWS_PROFILE_NAME
# set aws session token (if required)
aws configure --profile AWS_PROFILE_NAME set aws_session_token YOUR-TOKEN
```

#### Create EC2 key value pair (not stored in code repository)
```bash
# create EC2 key pair
aws ec2 create-key-pair --key-name EC2ServerKeyPair --query 'KeyMaterial' --output text > EC2ServerKeyPair.pem --profile AWS_PROFILE_NAME
```

### How to run the scripts?
You can run the supporting material in two easy steps:
```bash
# Ensure that the AWS CLI is configured before running the command below
# AWS_PROFILE_NAME refers to a user profile for the destined AWS account
# Create the network infrastructure
# Check the region in the create.sh file
./create.sh myFirstStack network.yml network-parameters.json AWS_PROFILE_NAME
# Create servers
# Change the AMI ID and key-pair name in file server-parameters.json
# Check the region in the update.sh file
./update.sh mySecStack servers.yml server-parameters.json AWS_PROFILE_NAME
# Delete stack
./delete.sh myFirstStack AWS_PROFILE_NAME
```

<a name="project-content"></a>
### Project Content

#### Folder diagram
Diagram of the AWS web architecture

#### Folder scripts
- Shell scripts:
    - create&#46;sh: creates CloudFormation stack.
    - update&#46;sh: updates CloudFormation stack.
    - delete&#46;sh: deletes CloudFormation stack.
- CloudFormation templates for infrastructure
    - network&#46;yml: VPC, Internetgateway, public/ private subnets, NAT gateways, route tables.
    - servers&#46;yml: security groups, load balancer, launch configuration, auto-scaling group for EC2 application servers, server IAM instance profile, role and policy.
- Cloudformation parameter files
    - network-parameters&#46;json: environment name, CIDRs for VPC and public/ private subnets.
    - server-parameters&#46;json: environment name, autoscaling ec2 image-id, autoscaling key name.