# PROJECT 2

## Setting up miltiple websites on a single sever using nginx virtual hosts

- I logged into my aws Iam user account and created an **Ubuntu server** instance

- proceeded to associate an **elastic ip** to my server instance

- went ahead to get my ssh credentials from my ssh Tab, which I used to ssh into my server

- Installed and configured my nginx server with these series of commands

   **sudo apt update** to update the server

   **sudo apt upgrade** to upgrade the server

   **sudo apt install nginx** which installed the **nginx server*

- Went ahead to start my server with **sudo systemctl start nginx**

- enabled it with **sudo systemctl enable nginx**

- verified the status of my server with **sudo systemctl status nginx** and my server was active.

- I installed the unzip utility with **sudo ap install unzip**

- Proceeded to download my website templates, using the curl command to download to my server

   **sudo curl -o /var/www/html/2135_mini-finance.zip https://www.tooplate.com/zip-templates/
  
   2135_mini_finance.zip && sudo unzip -d /var/www/html/ /var/www/html/2135_mini_finance.zip && 
  
   sudo rm -f /var/www/html/2135_mini_finance.zip** and also did the same command for my other website
  
   template to download the second website template so as to download, unzip and delete the zipped file

- I ran same command with the next website template thus.

   **sudo curl -o /var/www/html/2131_wedding-lite.zip https://www.tooplate.com/zip-templates/
  
   2131_wedding_lite.zip && sudo unzip -d /var/www/html/ /var/www/html/2131_wedding_lite.zip && 
  
   sudo rm -f /var/www/html/2131_wedding_lite.zip**

- Setting up my webdite con figuration I created a configuration file with 

  **sudo nano /etc/nginx/sites-available/finance** to open the text editor 

- I copied and pasted the server block script which I edited with my website directory on my server.

- Created the second website configuration by using same command to open editor

  **sudo nano /etc/nginx/sites-available/wedding**

- copied and edited the server block script for the second website configuration equally

- Created a symbolic link for both sites with commands

   **sudo ln -s /etc/nginx/sites-available/finance /etc/nginx/sites-enabled/** 

   **sudo ln -s /etc/nginx/sites-available/wedding /etc/nginx/sites-enabled/**

- Ran the command **sudo nginx -t** to test the syntax and it was successful

- Deleted the default files in the site-available and sites-enabled directories

- I restarted my server witn **sudo systemctl restart nginx**

- I went on to **route53** on **AWS** where I created A record for my domains and sud domains

   -finance.cloudconnect.click

   -www.finance.cloudconnect.click

   -wedding.cloudconnect.click

   -www.wedding.cloudconnect.click

- Inputting record name and my ip address "**54.201.88.235**" for both websites

- I opened my terminal to launch the editor with **sudo nano /etc/nginx/sites-available/cleaningfinance**

  to edit my setting and save the domain name and sub domain.

- I did same for the second website **sudo nano /etc/nginx/sites-available/wedding**

- After having edited and saved the various configurations I restarted **nginx* with

  **sudo systemctl restart nginx**

- I copied my public Ip to my browser and my websites were live but unsecured

- Installed **certbot** with the following commands

  **sudo apt update**

  **sudo apt install python3-certbot-nginx** 

  **sudo certbot --nginx**

  used the command sudo certbot --nginx to request and deploy the certificates for the domains where 
  
  I selected the domains 1 and 3 for certificate deployment

- went on to test the certicicate with
 
   **openssl s_client -connect finance.cloudconnect.click:443** and

   **openssl s_client -connect wedding.cloudconnect.click:443**

 All were successful

 !(testssl)

- Logged on to the various websites to verify and they were live and secured.


### End Of Project






   