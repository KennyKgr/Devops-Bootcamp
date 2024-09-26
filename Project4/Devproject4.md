# My Project 4

## Set up a wordpress website using Lamp stack

- I began by Creating an Ubuntu instance, and granting ssh access

![create ec2 instance](/Project4/img/Ubuntu_instance.png)

- went ahead to also allocate an elastic ip to my running ec2 instance

![allocateip](/Project4/img/Allocated_elastic_Ip_successfully.png)

- I set an inbound rule for mysql, adding a new rule

![inboundrule](/Project4/img/Mysql_security_setting_allowing_access.png)

- I ssh to my server and installed apache with a combination of commands as follows

  **sudo apt update && sudo apt install apache2**

  ![installapache](/Project4/img/sudoaptupdate_sudoaptinstall_apache.png)

- went ahead to enable and verify the status with the command 

  **sudo systemctl enable apache2**

  **sudo systemctl status apache2**

- To verify if my server was running and accessible, locally and from the internet I ran the command

  **curl http://localhost:80**

![localhost](/Project4/img/curl_localhost_80.png)

- I tested my apache server by accessing the public Ip:80 since installation was a success I saw the apache page.

![apachepuc](/Project4/img//Ip_shows_apache_server.png)

- I went on to install *mysql* using 

  **sudo apt install install mysql-server** proceeding to accept the prompt with a **Y** for yes

![installmysql](/Project4/img/install_mysql_server.png)

```
  sudo mysql to log into the console to set the password, with 

  ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'Clover'; exit 

  when I was done

```

![sql](/Project4/img/sudo_mysql.png)

- Ran command **sudo mysql_secure_installation** and answered with Y to enable validation policies and create access account to use.

![secureinstall](/Project4/img/mysql_secure_installation_put_password_policy.png)

- went on to set my validation policy level and enabled mysql by executing the 

  **sudo systemctl enable mysql** and verified status with 

  **sudo systemctl status mysql**

- I went ahead to install *PHP* with required extensions with command 

  **sudo apt install php-curl php-gd php-mbstring php-xml php-xmlrpc php-soap php-intl php-zip** 

![phpinstall](/Project4/img/Install_php.png)

  **sudo apt install php libapache2-mod-php php-mysql**

![phpextensions](/Project4/img/Install_apache_lib_mysql.png)

- confirmed the php version with **php-v**

![phpversion](/Project4/img/Verify_php_version.png)

## Created a Virtual Host for my website using apache

- created a project lamp directory 

  **sudo mkdir /var/www/projectlamp** 

and assigned ownership of my created directory to my currect system using

  **sudo chown -R $USER:$USER /var/www/projectlamp**

- created a new configuration file in apache's site-available directory using a command line editor

  **sudo vi /etc/apache2/sites-available/projectlamp.conf**

- This gave me a blank file where I then pasted the configuration provided to it.

![vitrhostscript](/Project4/img/virtual_host_script_pasted_project_lamp.png)

- I went ahead to save and exit my changes with *esc* and then *":wq"* and *"Enter"*

- I ran the command **sudo ls /etc/apache2/sites-available** to verify if the configuration was available which was the case.

![config](/Project4/img/list_apache_configuration.png)

- I enabled the new virtual host with **sudo a2ensite projectlamp**

![a2ensite](/Project4/img/Activating_wordpress_site.png)

-Needing to disable apache's default website I used **sudo a2dissite 000-default** and test the configuration which was *"syntax ok"*

![a2dissite](/Project4/img/activate_project_lamp_config_disable_default_and_then_test_config.png)

-For changes to take effect I ran **sudo systemctl relaod apache2**

![reload](/Project4/img/Reload_Apache.png)

- Since my web root folder is empty I needed to create an *index.html* file with **"Hello lamp from kennyKgr"** with

  **sudo echo 'Hello Lamp from Kennykgr' > /var/www/projectlamp/index.html**

- went to my browser to access my work using my public *Ip:80* and it was live.

![ipprojectlamp](/Project4/img/Hello_lamp_with_my_text_visible_via_public_ip.png)

-I now needed to remove the *index.html* file so I used the command **sudo rm /var/www/projectlamp/index.html**

![indexdel](/Project4/img/Delete_index.html.png)

#### Enabled my PHP on the Website

- Since my default settings on apache will always give priority to an *index.html* over an *index.php* 

- I had to edit the *dir.conf* file using my text editor 

  **sudo nano /etc/apache2/mods-enabled/dir.conf**

- There I corrected the order and made the php priority

![phppriority](/Project4/img/Editing_to_prioritize_index.php.png)

- used *ctrl and x* to save and exited, confirming with a *y* for yes and when prompted I saved with the name

- Reloaded apache for changes to take effect

  **sudo systemctl reload apache2**

![phpapreload](/Project4/img/reload_apache_server_after_config_to_view_my_php_text.png)

- I did **nano /var/www/projectlamp/index.php** this created an *index.php* file which 

- I went ahead to copy and paste the php code to the line

![phpcode](/Project4/img/Create_php_to_edit.png)

- After saving and exiting, I had the following output after a refresh.

![phplive](/Project4/img/Php_on_my_ip_address.png)

- Now that I can confirm my php is working I went ahead to remove the *index.php* file 

![remvphp](/Project4/img/Delete_index.php.png)

##### Install wordpress

- I used **cd /var/www/html** to change directory to where I intended to use 

- used **sudo wget -c http://wordpress.org/latest.tar.gz** to download wordpress

![downloadwp](/Project4/img/Download_wordpress.png)

- Extracted the downloaded archive using **sudo tar -xzvf latest.tar.gz**

![extractwp](/Project4/img/installing_wordpress.png)

- used **ls -l** to show directory one level up and confirmed the directory was existing in */var/www/html*

![show](/Project4/img/Show_wordpress_directory_one_step_up.png)

- To grant ownership I had to verify the running web server with **ps aux | grep apache | grep -v grep** 

- I granted ownership of the wordpress directory and contents to the web server with 

  **sudo chown -R www-data:www-data /var/www/html/wordpress**

## Created a database for wordpress

- Needing to access my MySQL root account with the  command 

  **sudo mysql -u root -p** 

![grep](/Project4/img/show_wordpress_directory_and_grep_to_show_security_previleges_then_enter_mysql.png)

- I input the password I set previously upon creating the root account for the database

- I created a database with **CREATE DATABASE mov_db;** to create *mov.db*

- accessing my new database, I created a MySQL user account with a strong password using  

  **CREATE USER kennykgr@localhost IDENTIFIED BY 'clover@7';**

![allcommands](/Project4/img/show_wordpress_directory_and_grep_to_show_security_previleges_then_enter_mysql.png)

- Granted my created user *kennykgr@localhost* to grant it access to the created database with 

 ```

 GRANT ALL PRIVILEGES ON mov_db.* TO kennykgr@localhost;
 FLUSH PRIVILEGES;

 ```

 - exited the mysql shell with **exit**

 - Granted executable permissions recursively (-R) to the wordpress folder with **sudo chmod -R 777 wordpress/**

 ![chmod](/Project4/img/Cmod_security_allocations.png)

 - Changed into the WordPress directory with **cd wordpress**

 - Renamed the sample wordpress configuration with **mv wp-config-sample.php wp-config.php**

 - Edited the *wp-config.php* file with **sudo nano wp-config.php** and updated with my configurations then saved

 ![wordpress](/Project4/img/Wordpress_configuration_edited.png)

 - modified the configuration file *projectlamp.conf* to update the document root to my wordpress directory 

  **sudo nano /etc/apache2/sites-available/projectlamp.conf** 

 - I changed */var/www/html* to my wordpress location, then saved

 ![root](/Project4/img/virtual_host_script_pasted_project_lamp.png)

 - I reloaded with **sudo systemctl reload apache2**

 ![reloadapache](/Project4/img/Reloaded_apache_finallly_to%20visit_website_url.png)

 - I proceeded to open my browser page and accessed *http://44.229.36.29/wordpress/* and wordpress was accessible

 ![wordpress](/Project4/img/Wordpress_welcome_install_page.png)

 - I installed with the required information including password

 ![instelledwordpress](/Project4/img/wordpress_information_for_installation.png)

 - My installation was successful and I logged in

 ![installationwp](/Project4/img/Successful_installation_for_wordpress.png)

 - Got to login page where I used my credentials

 ![loginwp](/Project4/img/IPv4_wordpress_login_page.png)

 - Logged in and it was successful to my dashboard

 ![iploggedin](/Project4/img/IPv4_wordpress_logged_in.png)

 - Created *A record* on *route53* with my Ip **44.229.36.29** for domain and sub domain

 ![arecords](/Project4/img/A_records.png)

 - Updated my apache server in my projectlamp configuration with
 
  **sudo nano /etc/apache2/sites-available/projectlamp.conf**

![apacheupdate](/Project4/img/script_and_location_for_db_server.png)

- Updated my *wp-config.php* file with DNS settings, used **sudo nano wp-config.php** adding lines to my cofiguration

![dnd](/Project4/img/Vitual_host_config_with_web_info.png)

- Reloaded my apache server **sudo systemctl reload apache2**

![reloadfinal](/Project4/img/Reloaded_apache_finallly_to%20visit_website_url.png)

- Visited my domain and my wordpress was live yet unsecured

![wordpresslive](/Project4/img/Site_live_unsecured.png)

- Accessed my login page for wordpress with **http://cloudconnect/wp-admin** and all was okay

![wpaccess](/Project4/img/login_page_unsecured_website.png)

- Logged in and wordpress was properly configured as I logged into my dashboard

![dashboard](/Project4/img/login_but_website_unsecured.png)

- To secure my website I install certbot to deploy certificate with 

  **sudo apt update sudo apt install certbot python3-certbot-apache** 

- Then ran **sudo certbot --apache** to request the certificate 

![installcertbot](/Project4/img/update_and_deploy_cert_with_cerbot.png)

- Deployed certificates successfully

![certdeplyed](/Project4/img/encription_success.png)

- Accessed my website and it was secured

![websecured](/Project4/img/website_accessed_secured.png)

![loggedin](/Project4/img/sign_in_successful_and_sie_secured.png) 

## End of Project