# Elite Corporations Project

## AIM: Automate infrastructure with Terraform, create cloud infrastructure to ensure scalability and realiability

### Using Terraform to provision an Ec2 instance on AWS.


Plan and Preparation for project execution

- In view of carrying out this project there was need to put togethere a series of requirements being;

    Access key        = "AKIA**********BVGLH2"
    Secret access key = "tKxI203CR*******************************0"
    availability zone = "us-east-1"
    Ami               = "ami-04b4f1a9cf54c11d0"  (Ubuntu 20.04 LTS)
    instance_type     = "t2micro"
    key_name          = "Elitecorp"
    subnet ID         = "subnet-03b4c1e5d05587598"
    tag               = "elitecp1-HR"

- with the defined requirements stated above in mind, 
  
- I went ahead to configure access to my aws cli with **aws configure** and set my credentials andother information to complete my setup.

![awsconfig](/DevAdv/Pj2/images/1_configure_aws_cli.jpg)

#### Deployment

- went on to create my **main.tf** file with my required variables defined in my **variables.tf** 
  
  ![Main](/DevAdv/Pj2/images/2_main_file_tf.jpg)

- Setup my variables I decided not to hardcode on my **main.tf** file

![Variables](/DevAdv/Pj2/images/3_variables_file_tf.jpg)

- I decided to setup a **Terraform.tfvars file** which was optional to define where I could Change the default region and instance type if needed
  
![terraform.tfvars](/DevAdv/Pj2/images/4_tfvars_optional_tf.jpg)

- With all this configurations set I initiated *Terraform* with **terraform init**

![init](/DevAdv/Pj2/images/5_terraform_init.jpg)

- I used **terraform fmt** to format my code and **terraform validate** to check for errors

![check](/DevAdv/Pj2/images/6_teffarorm_fmt_n_validate.jpg)

- proceeded with **terraform plan** when i saw codes had no errors 

![plan](/DevAdv/Pj2/images/7_terraform_plan.jpg)

- Next I used **terraform Apply** and my Apply was successful

![apply](/DevAdv/Pj2/images/8_terraform_apply_success.jpg)

- After applying my terraform code i used state management to verify if my infrastructure was being tracked
  
  with **terraform state list** and the EC2 instance was being tracked as seen below

![state](/DevAdv/Pj2/images/9_terraform_state_list_tracking.jpg)

- logged into my console on AWS and could see my Ec2 instance active with a *t2micro* ami with the tag *Elitecp1-HR*

![elite](/DevAdv/Pj2/images/10_elitrcp1_with_t2micro_created.jpg)

- Modified my Ec2 instance type from **t2micro** to **t2small**

![modified](/DevAdv/Pj2/images/12_t2small_modified_on_instance_elitecp1.jpg)

- Ec2 instance type was modified to t2small successfully

![modifiedok](/DevAdv/Pj2/images/15_modified_on_aws_to_t2small.jpg)

- Having achieved the desired requirements set from the begining of the project I went on to use **terraform destroy**

![destroy](/DevAdv/Pj2/images/14_terraform_destroy.jpg)

**END**