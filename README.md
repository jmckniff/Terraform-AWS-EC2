# Terraform - Create AWS Instance

## Prerequisites

* Install Terraform using [chocolately](https://chocolatey.org/docs/installation#installing-chocolatey "Chocolatey"), by running the following command from the command line:
choco install terraform

  This should install "terraform" into your PATH.

  *Note*: I used Terraform v0.11.13 for this example. 

* Create an AWS account.

* Create an EC2 private key pair named "Terraform", this is used by Terraform to SSH to AWS. [Documentation](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ec2-key-pairs.html) After creating the key pair it will be automatically downloaded named "Terraform.pem".

* Copy the key pair "Terraform.pem" file to the Terraform directory next to the "aws-resources.tf" file.

* Create an AWS IAM account and make it a member of the "AmazonEC2FullAccess" security group, this will give the account permissions to create EC2 machine instances.
[Documentation](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_users_create.html)

* After creating the account go to the "Security Credentials" tab and click "Create access key", copy the "Access key id" and "Secret access key" values update the variables named "aws_access_key" and "aws_secret_key" in the "terraform.tfvars" file.

## Creating the AWS EC2 machine instance
You should now have everything you need to create your first AWS EC2 machine instance using Terraform.

Open a command prompt and change directory to the same directory containing the "terraform.tfvars" file.

We can test what Terraform will do with the instructions in the "aws-resources.tf" file by running the "plan" command from the command line like so:
terraform plan -var-file="terraform.tfvars"

*WARNING*: When using AWS EC2 instances, you pay for what resources you consume, do not leave your EC2 instance running unless you want a bill!

We can now tell Terraform to perform the changes as instructed in the "aws-resources.tf" file by running the "apply" command from the command line like so:
terraform plan -var-file="terraform.tfvars"

You should now see an instance named "terraform_example_nginx" in [AWS EC2 console](https://us-east-2.console.aws.amazon.com/ec2/v2/home?region=us-east-2#Instances:sort=instanceId)

Finally we can now tell Terraform to tear down the resources created by the "aws-resources.tf" file by running the "destroy" command from the command line like so:
terraform destroy -var-file="terraform.tfvars"







