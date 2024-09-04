# My Project 4

## I had to Set up a wordpress website using Lamp stack

- I began by Creating an Ubuntu instance, and granting ssh access

![create ec2 instance](/Project4/img/Ubuntu_instance.png)

- went ahead to also allocate an elastic ip to my running ec2 instance

![allocateip](/Project4/img/Allocated_elastic_Ip_successfully.png)

- I set an inbound rules for mysql, adding a new rule

![inboundrule](/Project4/img/Mysql_security_setting_allowing_access.png)

- I ssh to my server and installed apache with a combination of commands as follows

  **sudo apt update && sudo apt install apache2**

  ![installapache](/Project4/img/sudoaptupdate_sudoaptinstall_apache.png)

  - went ahead to enable and verify the status with the command **sudo systemctl enable apache2**

      **sudo systemctl status apache2**

- to verify if my server was running and accessible both locally and from the internet I ran the command

...
   **curl http://localhost:80**
...

![localhost](/Project4/img/curl_localhost_80.png)

- I tested my apache server by accessing the public Ip since installation was a success I saw the apache page.

![apachepuc](/Project4/img//Ip_shows_apache_server.png)

- I went on to install *mysql* using 

    **sudo apt install install mysql-server** proceeding to accept the prompt with a **Y** for yes

    ![installmysql](/Project4/img/install_mysql_server.png)

- **sudo mysql** to log into the console

