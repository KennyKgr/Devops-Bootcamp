## Elite Corporations Project

### AIM: Automate, Manage and Deploy Database and Webservers with Ansible

# Setting up the environment 

- Created 5 Ec2 server Instances on the Aws service running on the Ubuntu Os as below

![Ec2](/Advance-Pj1/Images/ScreenShot_Tool.jpg)

-The public Ip Addresses for the provisioned servers were as follows



    Master Node 18.227.140.76

    Web_Server1 18.220.14.113

    Web_Server2 18.220.135.234

    Database_Server1 18.117.106.201

    Database_Server2 3.17.176.234




- SSh into the master Node using the key Pair I created named Ansible.pem I updated my ubuntu on the master Node using

**sudo apt update** to update my ubuntu server 

![sudo](/Advance-Pj1/Images/sudo_aprt_update_ubuntu.jpg)

**sudo install ansible** to install ansible to my master node

![install_ansible](/Advance-Pj1/Images/sudo_apt_install_ansible.jpg)

- verify ansible install with **ansible --version**

![verify_ansible](/Advance-Pj1/Images/verify_ansible_install_verion.jpg)

- In my Master Node I generated a key with the command **ssh-keygen**

![keygen](/Advance-Pj1/Images/create_keygen.jpg)

- Proceeded to the key location to view my public key on my master node in view of copying

![viewkey](/Advance-Pj1/Images/on_master_node_i_get_to_my_directory_to_view_and-copy_my_key.jpg)

- I cat and copied my public key and updated in the **authorized_keys** on the 4 target server systems.

![target](/Advance-Pj1/Images/cat_and_copied_my_authorized_key_from_my_master_node.jpg)

- Accesses and edited authorized keys on all target systems with public key from my master node on all  

![key](/Advance-Pj1/Images/edited_authorized_keys_on_target_system.jpg)

- Connected to y target server to test 

![test](/Advance-Pj1/Images/from_master_node_i_connect_directly_after_pasting_key-in_authorized_keys.jpg)

- On my master node I went on to create an ansible directory in my **/home/ubuntu/** for easy accessibiity and an inventory file

![create](/Advance-Pj1/Images/create_ansible_dir_and_inventory_file.jpg)

- In my newly created ansible directory where the inventory file is located I updated the various Public Ip adrresses from the target systems, grouping them in **Web_servers** and **database_servers**

![grouping](/Advance-Pj1/Images/setup_my_inventory-list.jpg)

# Automation

- I created 2 playbooks being 

      playbook.yml(web_servers) 
      playbook2.yml(database_servers)

where I wrote scripts to carry out the following automated tasks

  - Install nginx on web servers
  - Install apache on database servers
  - Get the total free disk space
  - Get available disk space

![set](/Advance-Pj1/Images/playbook1_webserver_playbook.jpg)

![set1](/Advance-Pj1/Images/playbook2_config.jpg)

# Deployment

- Executing the playbooks with **ansible-playbook -i inventory playbook.yml** 

![play1](/Advance-Pj1/Images/playbook1_done_webservers.jpg)

- executed **ansible-playbook -i inventory playbook2.yml** 

![deploy2](/Advance-Pj1/Images/playbook2_executed_successfully.jpg)

- All from within my ansible folder deployed the intended scripts

- visiting the various public Web_server Ip addresses shows both nginx live.

![nginx1](/Advance-Pj1/Images/nginx_active_on_first_web_server.jpg)

![nginx2](/Advance-Pj1/Images/nginx_active_on_second%20_web_server.jpg)

- Apache was running on the database servers equally

![apache1](/Advance-Pj1/Images/apache1.jpg)

![apache2](/Advance-Pj1/Images/apache2_live.jpg)



