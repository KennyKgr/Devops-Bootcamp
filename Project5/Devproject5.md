# Setting up service discovery using Nginx and consul

- I created 4 *Ec2* Instances and allocated elastic Ip's

- went ahead to rename them for proper identification namely:-

    Devserver1

    Devserver2

    Consul3

    Loadbalancer4

    ![servers](/Project5/img/1_4_servers_renamed.png)

- I edited my security group to open a series of ports on my consul ec2 instance as follows

![ports](/Project5/img/2_custom_ports_config.png)

## I setup my Consul server

- ssh into my consul server and started by updating with

    **sudo apt update**

![sudoupdate](/Project5/img/3_sudo_apt_update.png) 

- visited download page and copied the series of commands needed to download consul and setup

![download](/Project5/img/4_copy_consul_download_command.png)

- Copied the link and went ahead to download the file to my desired directory

...

wget -O- https://apt.releases.hashicorp.com/gpg | gpg --dearmor | sudo tee /usr/share/keyrings/hashicorp-archive-keyring.gpg

echo "deb [signed-by=/usr/share/keyrings/hashicorp-archive-keyring.gpg] https://apt.releases.hashicorp.com $

(lsb_release -cs) main" | sudo tee /etc/apt/sources.list.d/hashicorp.list

sudo apt update && sudo apt install consul

...

![downloadconsul](/Project5/img/5_get_consul_file.png)

![installing](/Project5/img/7_consul%20installing.png)

- verified the installation version with **consul --version**

![verify](/Project5/img/8_consul_version_verify.png)

- configured my server, first backing up the default configuration with

    **sudo mv /etc/consul.d/consul.hcl /etc/consul.d/consul.hcl.back**

![backup](/Project5/img/9_backup-consul_config_file.png)

- I proceeded to generate my encryption key using **consul keygen** and the key result was

    **XTxSZ0m6zNTuQlTrislENXWBeQnioakymBLQUhCcGTY=**

![keygen](/Project5/img/10_generate_key.png)

- Created a new file *consul.hcl* with the command **sudo vi /etc/consul.d/consul.hcl**

![createfile](/Project5/img/11_sudo_vi_create_hcl-file_to_paste-script.png)

- pasted the edited script with my *encrytion key*

...

"bind_addr" = "0.0.0.0"
"client_addr" = "0.0.0.0"
"data_dir" = "/var/consul"
"encrypt" = "XTxSZ0m6zNTuQlTrislENXWBeQnioakymBLQUhCcGTY="
"datacenter" = "dc1"
"ui" = true
"server" = true
"log_level" = "INFO"

...

![encryted](/Project5/img/12_paste_script_correct_option.png)

- Started my consul server with the command **sudo nohup consul agent -dev -config-dir /etc/consul.d/ &**

![startedserver](/Project5/img/13_sudo-nohup_dev_mode_activate.png)

- checked the status of my *consul server* with **consul members**

![checkedstat](/Project5/img/14_consul_members.png)

- I accessed my *Ec2* consul server from my browser **52.41.232.241:8500** and my server was live

![serverlive](/Project5/img/15_consul_live_with_just_1instance.png)

### I setup my backend servers

- On my two backend servers I did practically the same set of tasks on both to achieve my objective

- SSh into the servers and updated **sudo apt-get update -y**

![update](/Project5/img/16_backends_sudo_apt_update_on_the.png)

- Installed *nginx* on both servers with **sudo apt install nginx -y** 

- with cd I navigated to the */var/www/html* directory where I ran **sudo vi index.html**

![installinnediting](/Project5/img/17_backends_cd_then_sudo_vi_index.html.png)

- copied the html script for *server 01* and *server 02* accordingly

...

<!DOCTYPE html>
<html>
<head>
	<title>Kanekis Backend Server </title>
</head>
<body>
	<h1>This is Backend SERVER-01</h1>
</body>
</html>

&

<!DOCTYPE html>
<html>
<head>
	<title>Kanekis Backend Server </title>
</head>
<body>
	<h1>This is Backend SERVER-02</h1>
</body>
</html>

...

- Download consul with the command 

...

wget -O- https://apt.releases.hashicorp.com/gpg | gpg --dearmor | sudo tee /usr/share/keyrings/hashicorp-archive-keyring.gpg

echo "deb [signed-by=/usr/share/keyrings/hashicorp-archive-keyring.gpg] https://apt.releases.hashicorp.com $(lsb_release -cs) main" | sudo tee /etc/apt/sources.list.d/hashicorp.list

...

![getconsul](/Project5/img/18_download-client_consul_on_backends.png)

- updated and installed *consul* with **sudo apt update && sudo apt install consul**


![installconsul](/Project5/img/19_sudo_apt_update_sudo_apt_install_consul.png)

- verified my installation with **consul members**

![verifyonbackend](/Project5/img/20_consul_version_check.png)

- replaced the default configuration file  *config.hcl* with my own configuration

- firstly I renamed the default file and created a new one with the following commands

    **sudo mv /etc/consul.d/consul.hcl /etc/consul.d/consul.hcl.back**

    **sudo vi /etc/consul.d/consul.hcl** to create the blank new file

![create](/Project5/img/21_modify_initial_file_and_create_consul.hcl.png)

- I pasted and edited the script with the **encryption key and ip address "52.41.232.241"**

![script](/Project5/img/22_script_that_is_pasted.png)

- next I created *backend.hcl* file which I saved with a script copied to both servers.

- I used **sudo vi /etc/consul.d/backend.hcl** pasted the script and saved.

...

    "service" = {
  "Name" = "backend"
  "Port" = 80
  "check" = {
    "args" = ["curl", "localhost"]
    "interval" = "3s"
  }
}

...
    
- I verified the status of the server with **consul validate /etc/consul.d**

- I then started the consul agent with **sudo nohup consul agent -config-dir /etc/consul.d/ &**

- also ran **consul members** and it was successful

![nohup](/Project5/img/24_sudo_nohup_and_consul_members_on_backends.png)

- I visited the UI and saw the updated instances all live

![updated](/Project5/img/25_consul_with_all_instances.png)

#### Setup My Load balancer

- updated the system and installed unzip with the commands **sudo apt-get update -y**
    

![update](/Project5/img/26_update-load-balancer.png)

- To install *unzip* **sudo apt-get install unzip -y**

![unzip](/Project5/img/27_sudo_apt_get_unzip.png)

- I installed *Nginx* with **sudo apt install nginx -y**

![nginx](/Project5/img/28_install_nginx.png)

- went ahead to download the consul-template binary with 

...

sudo curl -L  https://releases.hashicorp.com/consul-template/0.30.0/consul-template_0.30.0_linux_amd64.zip -o /opt/consul-template.zip

sudo unzip /opt/consul-template.zip -d  /usr/local/bin/

...

![curl](/Project5/img/29_use_curl_download_template_for_consul.png)

- verified the installation with **consul-template --version**

![template](/Project5/img/30_consul_template_version.png)

- I created and edited a new file named *load-balancer.conf.ctmpl*

- used **sudo vi /etc/nginx/conf.d/load-balancer.conf.ctmpl**

![vi](/Project5/img/31_sudo_vi_balancer_to_edit_paste-script.png)

- used this script which I pasted and saved to my newly created configuration

![scriptpasted](/Project5/img/32_script_pasted.png)

- With need to create a configuration for the *consul-template* 

- I had to create *consul-template.hcl* to have details on the consul server Ip and other configurations

- I used the command **sudo vi /etc/nginx/conf.d/consul-template.hcl**

- pasted the script with my *consul server's* Ip Ip address **"52.41.232.241"** embedded in the detail.

...

- consul {
 address = "52.41.232.241:8500"

 retry {
   enabled  = true
   attempts = 12
   backoff  = "250ms"
 }
}
template {
 source      = "/etc/nginx/conf.d/load-balancer.conf.ctmpl"
 destination = "/etc/nginx/conf.d/load-balancer.conf"
 perms       = 0600
 command = "service nginx reload"
}

...

- I deleted the default configuration using **sudo rm /etc/nginx/sites-enabled/default**

![delete](/Project5/img/33_remove_default_config.png)

- restart nginx with **sudo systemctl restart nginx**

![restart](/Project5/img/34_restart_nginx.png)

- once all configurations done I had to get consul to monitor for changes so I ran

**sudo nohup consul-template -config=/etc/nginx/conf.d/consul-template.hcl &**

- After creating a load balancer config with al the required information from my *consul* registry

- I visited my ip addresses on my browser and could refresh and visit both servers

![serv1](/Project5/img/35_load_balancer_output1.png)

![serv2](/Project5/img/36_load_balancer_output2.png)

##### Carried out a Service Discovery Test

- with Everything working normally 

![working](/Project5/img/25_consul_with_all_instances.png)

- I shut down nginx on *server 1* as a test and the result was immediate as an error was detected 

- All nodes checks failed and only server 02 was reachable after refreshing severally.

![error](/Project5/img/37_Load_balancer_after_taking_server1_down.png)

- The load balancer directed all traffic to the second server

![serverup](/Project5/img/38_consul_server_shows_the_one%20active_backend.png)


###### End Of Project