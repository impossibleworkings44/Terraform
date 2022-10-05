### Terraform CLI
- Terraform fmt, taint, and import Commands
- Terraform Workspaces
- Debugging Terraform
- Practicing Terraform CLI Commands (fmt, taint, and import)
- Using Terraform CLI Commands (workspace and state) to Manipulate a Terraform Deployment

## Terraform fmt, taint, and import Commands
 #### Terraform fmt (syntax : terraform fmt)
 - Formats terraform code for readability
 - helps in keeping code consistent
- can be run when made changes to code, before pushing changes to version control

#### Terraform taint [syntax : terraform taint RESURCE_ADDRESS)
- taints a resource , forcing it to be destroyed and recreated
- modifies the state file, which causes the recreation workflow
- tainting a resource may cause other resources to be modified(eg change in public ip address)

- Scenario : 1) to cause provisoners to run (terraform doesnt track provisioners, provisioners run only when resource created or destroyed, so we can attach provisioner to the resource)</br>
2) replace misbehaving resources forcefully <br/>
3) to mimic side effects of recreation not modeled by any attributes of the resource.(eg ec2 machine starting up and hitting an api)

## terraform import
- Maps exisiting resources to Terraform using an "ID"
- "ID" is independent of underlying vendor , for eg to import an AWS EC2 instace you'll need to provide the instance ID
- Importing same resource to multiple terraform resources can cause unknown behaviour and is not recommended

Scenario :
1) When you need to work with exisiting resources
2) Not allowd to create new resources 
3) when not in control of creation process of infrastructure

### terraform configuration block
- a special configuration block for controlling terraform own behaviour
- this block only allows constant values, names resoruces, and variables not allowed in it

Eg includes :
- configuring backend for storing state files
- specifiying terraform version
- sepcifying terraform providers version and its requirements

```
terraform {
  required_version = ">=013.0"
  required_providers  {
    aws = ">=3.0.0"
    }
 }


```
