# Setting Up Prometheus Using Docker Compose & Terraform

- Launched an EC2 Instance running Ubuntu 24.04

![instanc](/Project10/img/2_Launch_successful.png)

- Attached an **IAM role** to my Ec2 Instance giving it **VPC and EC2 full Access**

![iamrole](/Project10/img/4_Iam_role_attached%20_to_instance.png)

- SSH into my Instance

![ssh](/Project10/img/3_SSh_into_instance.png)

- Cloned the **github repo** of the project

```
git clone https://github.com/TobiOlajumoke/prometheus-observability-stack
```

- cd into the project code directory

```
cd prometheus-observability-stack
```

![cd](/Project10/img/7-cd_into-directory_with_prometheus_stack_config_file.png)


- carried out my **terraform** Install with the following command

```
sudo snap install terraform --classic
```

![install](/Project10/img/5_install_sudo_snap_install_Terraform.png)

- cd into the vars directory with 

```
cd terraform-aws/vars
```

![cdpatgh](/Project10/img/9_cd-into_stack_directory.png)

- proceeded with Vi editor to edit the **Ec2.tfvars** file Inputing appropriate variables in the **Ami_Id**, **Key_name**, **VPC_Id** and **Subnet_Id** fields accordingly

```
vi Ec2.tfvars
```

![edit](/Project10/img/8_edited_variables_pertaining_to-my_project_with_vi_editor.png)

- Provisioned the Ec2 and security group with terraform

```
Terraform fmt
```

![terraformfmt](/Project10/img/10_Terreform_fmt.png)

- Initialized terraform 

```
terraform init
```

![terraforminit](/Project10/img/11_Terraform_init.png)

- Proceeded to Validate 

```
terraform validate
```
![terraformvalidate](/Project10/img/12_Terraform_validated.png)

- Executed the Plan

```
terraform plan --var-file=../vars/ec2.tfvars
```

![Plan](/Project10/img/13_Terraform_plan.png)

- Proceeded to Apply

```
terraform apply --var-file=../vars/ec2.tfvars
```

![apply](/Project10/img/14_Terraform_Apply.png)

- Results after I applied.

![Applycmpl](/Project10/img/15_terraform_apply_completed.png)

- SSh into my newly created Instance

![newssh](/Project10/img/16_ssh_into_new-instance.png)

- checked the cloud init logs and realised the user data script did not run successfully

```
tail /var/log/cloud-init-output.log
```

![tails](/Project10/img/17_ran_tail_command_and_saw_docker_command-was_not_successful.png)

- updated my newly created ubuntu instance with **sudo apt update**.

![update](/Project10/img/18_sudo_apt_update_my_new_instance.png)

- Installed docker with command

```
sudo apt install -y docker.io
```
- Installed Docker-Compose with command

```
sudo curl -L 'https://github.com/docker/compose/releases/latest/download/docker-compose-$(uname -$)-$(uname -m)' -o /usr/local/bin/docker-compose
sudo chmod -x /usr/local/bin/docker-compose
```

![two](/Project10/img/19_Install_docker_and_docker-compose.png)

- Started docker with command

```
sudo systemctl start docker
```

![startdocker](/Project10/img/20_started_docker.png)

- View docker version

![dockversion](/Project10/img/21a_docker_version_view.png)

- Docker compose version and rights added as it shows access was not gotten

![compose](/Project10/img/21a_docker-compose_version_view_and_Rights_added.png)

- Cloned project repo to new instance

![clonedrepo](/Project10/img/22_cloned_repo_to_new_terraform-spun_instance.png)

- Cd into the stack directory on new instance

![cdnewinst](/Project10/img/23_cd_into_the_stack.png)

- Execute **make all** command to update my server ip in prometheus

![makeall](/Project10/img/24_make_all_command_executed_success.png)

- **Make all** command execution being carried out

![makeallworking](/Project10/img/25_make-all_execution.png)

- Brought up the stack with docker compose to deploy **Prometheus**, **Alert manager**, **Node Explorer** and **Grafana** using command

```
sudo docker-compose up -d
```

![success](/Project10/img/26_make_all-started_success.png) 

- With my Stack deployment done I accessed Prometheus on my Public Ip **http://44.230.159.109:9090**

![prometheusaccess](/Project10/img/27_Prometheus_accessed.png)

- Validate the targets, rules and Configurations. target being my Node explorer url

![prom](/Project10/img/27_Prometheus_accessed.png)

![prom2](/Project10/img/28_prometheus_config.png)

- Executed a promQl statement to view metrics from the node explorer

```
avg by (instance,mode) (irate(node_cpu_seconds_total{mode!='idle'}[1m]))
```

![node](/Project10/img/29_executed_command.png)

- Data seen in graph

![datagraph](/Project10/img/30_Prometheus_Graph.png)

- Using my login details I accesed Grafana on the public ip **http://44.230.159.109:3000**

![Grafana](/Project10/img/31_Grafana.png)

- Creating a new Dashboard, I added the prometheus url as my data source, 

![dashb](/Project10/img/31_Grafana_createdashboard_entry_and_execution.png)

- Grafana dashboard metrics

![metrics](/Project10/img/32_Info.png)

- To simulate and test the Alert manager accessible on my public ip **http://44.230.159.109:9093**

- Shows my alert rules already backed in my configuration **alertrules.yaml** which are inactive as seen.

![alert](/Project10/img/33_Alerts%20open.png)

- Also checked rules with command

```
sudo docker exec -it prometheus promtool check rules /etc/prometheus/alertrules.yml
```

- 4 rules successfully found

![rules](/Project10/img/34_populate%20the%20ec2_instance_to-generate_error.png)

- To check the alert manager user interface and confirm any fired alerts I simulated a high storage and cpu alert test with

```
dd if=/dev/zero of=testfile_16GB bs=1M count=16384; openssl speed -multi $(nproc --all) &
```

- The test simulation went on for a while

![test](/Project10/img/35_file_creation-ongoing.png)

- Confirmation the Alert was fired up.

![alertfired](/Project10/img/36_Alert-visible.png)

![alertmanager](/Project10/img/37_Alert_Manager.png)

- Roll back the changes to check if fired up alerts were resolved, with command

```
rm testfile_16GB && kill $(pgrep openssl)
```
![killscript](/Project10/img/38-kill-script-generating_error.png)

- with project completion I return to my initial workstation's project directory, proceeding to destroy and confirm with yes

![destroy](/Project10/img/39_Destroy-Terraform_infrastruscture.png)

- Confirmation destroy was carried out

![destroyed](/Project10/img/40_destroy_carried_out.png)