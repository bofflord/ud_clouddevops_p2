## ND9991 - C2- Infrastructure as Code - Supporting Material and Starter Code
This folder provides the supporting material and starter code for the "ND9991 - C2- Infrastructure as Code" course. This folder contains the following folders:
1. project_starter - It contains the starter code.
2. supporting_material - It contains the essential files (.yml, .json, .bat, .sh, and .jpeg) that were referred in the different lessons of this course.


In addition to the current repo, there is one more repository, [nd9991-c2-Infrastructure-as-Code-v1-Exercises_Solution](https://github.com/udacity/nd9991-c2-Infrastructure-as-Code-v1-Exercises_Solution) that contains the solution to the exercises and video demos.  

__ToDo: update content above__

### Dependencies
##### 1. AWS account
You would require to have an AWS account to be able to build cloud infrastructure.

##### 2. VS code editor
An editor would be helpful to visualize the image as well as code. Download the VS Code editor [here](https://code.visualstudio.com/download).

##### 3. An account on www.lucidchart.com
A free user-account on [www.lucidchart.com](www.lucidchart.com) is required to be able to draw the web app architecture diagrams for AWS.

### Configuration
#### Configure profile "udacity" in AWS CLI
```bash
# configure profile
aws configure --profile udacity
# set aws session token (if required)
aws configure --profile udacity set aws_session_token YOUR-TOKEN
```

#### Create EC2 key value pair (not stored in code repository)
```bash
# create EC2 key pair
aws ec2 create-key-pair --key-name EC2ServerKeyPair --query 'KeyMaterial' --output text > EC2ServerKeyPair.pem --profile udacity
```

### How to run the scripts?
You can run the supporting material in two easy steps:
```bash
# Ensure that the AWS CLI is configured before runniing the command below
# Create the network infrastructure
# Check the region in the create.sh file
./create.sh myFirstStack network.yml network-parameters.json
# Create servers
# Change the AMI ID and key-pair name in the servers.yml
# Check the region in the update.sh file
./update.sh mySecStack servers.yml server-parameters.json
```