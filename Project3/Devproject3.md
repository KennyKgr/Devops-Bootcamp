#Project Three

##I was required to setup reverse proxy load Balancing for a static website using mginx 

- I created a total of 3 **Ubuntu servers and associated an elastic ip address for the servers
- I installed **Nginx by executing the following commands
 
   **sudo apt update**

   **sudo apt upgrade**

   **sudo apt install nginx**

- I proceeded to start the server 

  **sudo start nginx**

-enabled the server with 
 
  **sudo systemctl enable nginx**

- to confirm the server was running I lastly ran the command

  **sudo systemctl status nginx**

  it was live and running.

- To install unzip I executed the command

  **sudo apt install unzip**

- i went ahead to download the zip files for the websites from it's various 

locations, I choose to go with the Job and agency templates being

  **2128_tween_agency.zip and **2134_gotto_jobs.zip which i had to right click on inspect on the download button to have file locations.

- I proceeded to run the curl command and a series of commands in unison to **download, **unzip and **delete the zip file

  **sudo curl -o /var/www/html/2134_gotto_job.zip https://www.tooplate.com/zip-templates/134_gotto_job.zip && sudo unzip -d /var/www/html /var/www/html/2134_gotto_job.zip && sudo -rm -f /var/www/html/2134_gotto_job.zip**

and **sudo curl -o /var/www/html/2128_tween_agency.zip https://www.tooplate.com/zip-templates/2128_tween_agency.zip && sudo unzip -d /var/www/html /var/www/html/2128_tween_agency.zip && sudo -rm -f /var/www/html/2128_tween_agency.zip**

for the second server.

- After carrying out all these on **server 1 and **server 2 I went ahead to launch my text editor with the following command
   **sudo nano /etc/nginx/sites-available/job**

 where I copied the script and edited with the proper information for my server 1 block to point to the location of my website files.

 - created a symbolic link between both websites by running the following command
   **sudo ln -s /etc/nginx/sites-available/job /etc/nginx/sites-enabled/**

- Ran the **sudo nginx -t to verify my syntax and it was successful.

- restarted my server with **sudo systemctl restart nginx**

- I went on to server two and repeated the same procedure till my **nginx server was  running my second website 

- I went back to **server 1 and 2 running the command 

  **sudo rm /etc/nginx/sites-enabled/default so as to delete the site enabled configuration folder.

  I restarted my nginx server with **sudo systemctl restart nginx**

- accessed my ip addresses **"35.86.164.198"** and **"54.185.210.35"** and the sites were live but unsecured.

- went to my **server 3 where I installed **nginx and tested the status with 

**sudo systemctl status nginx** and it was running,

- Ran **sudo nano /etc/nginx/nginx.conf where I edited my configuration adding the following server information

- went on to test with **sudo nginx -t** and it was successful restarted the server with **sudo systemctl restart nginx**

- went to Route53 where I created an A record for the root domain and for the subdomain with my server 3 ip address **"44.243.34.227"**

- Accessed the terminals for server 1 and server 2 using **sudo nano /etc/nginx/sites-available job** and **sudo nano /etc/nginx/sites-available/agency** for server 2 to verify the and correct any settings in the server block.

- restarted my **nginx with sudo systemctl restart nginx**

- I visited my domain name **"cloudconnect.click"** and the wensite was live yet unsecured

- I finally went on to secure my domain by executing the commands

   **sudo apt update**
   **sudo apt install python3-certbot-nginx**
   **sudo certbot --nginx**

- I visited my domain and refreshed and saw the changes and all was secure.

- I lastly tested the renew command in dry-run mode.



###End of project