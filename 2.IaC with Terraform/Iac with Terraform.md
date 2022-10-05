### IaC with Terraform 

#### Terrafrom workflow
- WRITE (generally starts with creating github repo as best common practise)
- PLAN (Continually  add and review changes to code in your project )
- APPLY (Read to provision real infrastructure)
![image](https://user-images.githubusercontent.com/76193921/194004953-37a24646-289f-477b-9de5-17bd8492e9df.png)

_________

#### Terraform init (intializing the working directory)
- 1) Initializes the working directory that contains your terraform codes
- 2) Downloads ancillary components ( modules + plugins)
- 3) Sets up backend  (sets backend for storing terraform state file , a mechanism by which terraform tracks resources)
_________

#### Terraform Key Concepts  (Plan, Apply and Destroy)
##### terraform plan
- reads the code and then creates and shows a "plan" for execution/deployment
- this command doesnt deplooy anything , consider as read command

#### terraform apply
- deploys the instructions and statements in the code
- and updates the state file( terraform.tfstate file)

#### terraform destroy
- looks at the state file created during deployment and destorys all the resources created by your code
- should be used with caution as it is non reversible command
_________

#### Resource addressing in Terraform : Understanding Terraform Code

``` 
	provider "aws" {
		region  = "us-east-1"
	}
```

```
resource "aws_instance"  "web"(user provided arbitrary resource name) {
	ami  =  "ami_01033",
	instance_type = "t2.micro"
}

```
-- reads the data of already created resources
```
data  "aws_instance"  	"web" {
	instance_id =. "i-9209e2"
}
```

