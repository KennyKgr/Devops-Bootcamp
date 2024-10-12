# AWS VPC using Terraform

- In automating resource creation using Terraform as manually executed in the previuos project and understanding terraform, I proceeded thus

- launched an Ec2 Instance

![LaunchedEc2](/Project8/img/1-Create-instance.png)

- Attached the following **Iam role** that granted **Ec2Full access** and **VpcFullAccess**

![iamrole](/Project8/img/2-Modify-iam-role.png)

- I SSh into my Ec2 instance
![sshinstinstance](/Project8/img/3-Ssh-into-instance.png)

- installed terraform with

```
- sudo snap install terraform --classic
```

- Cloned the Terraform repository with

```
 git clone https://github.com/TobiOlajumoke/Terraform-VPC.git
 ```

 ![cloned](/Project8/img/4-Cloned-the-terraform-setup-repo.png)

- Cd in the terraform vpc folder with

```
cd Terraform-VPC
```

![cdterraformfolder](/Project8/img/5-Cd-into-terraform-dir.png)

- cd into the vars/dev/ where the vpc.tfvars is located and used the nano editor changing tag Owner to **DevServ**

```
sudo nano vpc.tfvars
```

![tfvars](/Project8/img/6-Editing-config.png)

- cd into the infra/vpc with

```
cd infra/vpc
```

![infra](/Project8/img/7-Cd-into-infra.png)

- Proceeded to setup Terraform for my project by initializing it with

```
Terraform init
```

![intiTerraform](/Project8/img/8-Initiate-Terraform.png)

- view changes to be carried out by terraform to my AWS resources with plan,  pointing to the file containing the specific values for my development environment and got an output that showed all the resources to be created

```
execute plan -var-file=../../vars/dev/vpc.tfvars
```

![plan](/Project8/img/9-Showing-config-after-next-step.png)

- Created resources with terraform Apply  from the **vpc.tfvars** file carrying out the resource creation confirming with yes when prompted.

```
terraform apply -var-file=../../vars/dev/vpc.tfvars
```

![createresources](/Project8/img/10-Okayed-the-changes.png)

- Resources created and completed

![resourcecreation](/Project8/img/11-Changes-taking-place.png)

![completed](/Project8/img/12-Changes-Completed.png)

- Finally logged into my **AWS Console** to view the **Resource map** which had successfully been created with

15 Subnets

6 Route Tables

Internet Gateway

Nat Gateway as shown below

![resourcemap](/Project8/img/13-viewed-created-vpc-active.png)

![Rmap](/Project8/img/14-Resource-map.png)

- To Clean the resources created by terraform I executed

```
terraform destroy -var-file=../../vars/dev/vpc.tfvars
```

![Destroy](/Project8/img/15-Terraform-destroy-initiated.png)

![detroyed](/Project8/img/16-67Resources-destroyed.png)

## End Of Project}
