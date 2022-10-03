### Building and Testing a Basic Terraform Module
```
In the files you create in the modules/vpc directory, you will need to insert the following provided code.

In the main.tf file:

provider "aws" {
  region = var.region
}

resource "aws_vpc" "this" {
  cidr_block = "10.0.0.0/16"
}

resource "aws_subnet" "this" {
  vpc_id     = aws_vpc.this.id
  cidr_block = "10.0.1.0/24"
}

data "aws_ssm_parameter" "this" {
  name = "/aws/service/ami-amazon-linux-latest/amzn2-ami-hvm-x86_64-gp2"
}
In the variables.tf file:

variable "region" {
  type    = string
  default = "us-east-1"
}
In the outputs.tf file:

output "subnet_id" {
  value = aws_subnet.this.id
}

output "ami_id" {
  value = data.aws_ssm_parameter.this.value
}
In the files you create in the terraform_project directory, you will need to insert the following provided code.

In the main.tf file:

variable "main_region" {
  type    = string
  default = "us-east-1"
}

provider "aws" {
  region = var.main_region
}

module "vpc" {
  source = "./modules/vpc"
  region = var.main_region
}

resource "aws_instance" "my-instance" {
  ami           = module.vpc.ami_id
  subnet_id     = module.vpc.subnet_id
  instance_type = "t2.micro"
}
In the outputs.tf file:

output "PrivateIP" {
  description = "Private IP of EC2 instance"
  value       = aws_instance.my-instance.private_ip
}
To get started, log in to the lab server using the credentials provided:

ssh cloud_user@<Terraform-Controller>
```
### Learning Objectives
[ ] Create the Directory Structure for the Terraform Project <br/>
[ ] Write Your Terraform VPC Module Code <br/>
[ ] Write Your Main Terraform Project Code <br/>
[ ] Deploy Your Code and Test Out Your Module <br/>

-- Deploy code and test module
```
Format the code in all of your files using the terraform fmt -recursive command.
Initialize the Terraform configuration to fetch any required providers and get the code being referenced in the module block with the terraform init command.
Validate the code using the terraform validate command.
Review the actions that will be performed when you deploy the code using the terraform plan command.
Deploy the code with the terraform apply --auto-approve command.
View the resources that were created using the terraform state command.
Tear down the infrastructure using the terraform destroy command.

```
### Output
Apply complete! Resources: 3 added, 0 changed, 0 destroyed.

Outputs:

PrivateIP = "10.0.1.24"
