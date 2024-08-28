#Project Three

##I was required to setup reverse proxy load Balancing for a static website using mginx 

- I launched a total of 3 *Ubuntu instances* and associated an elastic ip address for the servers

![3servers](/Project3/img/create3servers.png)

- I installed **Nginx by executing the following commands
 
   **sudo apt update**

   **sudo apt upgrade**

   **sudo apt install nginx**

- I proceeded to start the server 

  **sudo start nginx**

- I enabled the server by executing the command
 
  **sudo systemctl enable nginx**

- to confirm the server was running I lastly ran the command

  **sudo systemctl status nginx** it was live and running.

  ![enable](/Project3/img/start-enable-status-of-nginx-server1n2.png)

- To install unzip I executed the command

  **sudo apt install unzip**

- I went ahead to download the zip files for the websites from it's various locations, I choose to go with

 the Job and agency templates being

**2128_tween_agency.zip** and **2134_gotto_jobs.zip** which I had to right click on inspect on the download

 button to obtain file locations.

- I proceeded to run the *curl* command and a series of commands in unison to download, unzip and 

delete the zip file when done

  **sudo curl -o /var/www/html/2134_gotto_job.zip https://www.tooplate.com/zip-templates/134_gotto_job.
  
  zip && sudo unzip -d /var/www/html /var/www/html/2134_gotto_job.zip && sudo -rm -f /var/www/html/
  
  2134_gotto_job.zip**

![curl](/Project3/img/curl-zip-and-unzip-job-files.png)

and **sudo curl -o /var/www/html/2128_tween_agency.zip https://www.tooplate.com/zip-templates/

2128_tween_agency.zip && sudo unzip -d /var/www/html /var/www/html/2128_tween_agency.zip && sudo -rm -f 

/var/www/html/2128_tween_agency.zip**

![curlagency](/Project3/img/download-zip-and-unzip-files-agency.png)

for the second server.

- After carrying out all these on *server 1* and *server 2* I went ahead to launch my text editor with the following command

   **sudo nano /etc/nginx/sites-available/job**

 where I copied the script and edited with the proper information for my server 1 block to point to the 
 
 location of my website files.

 ![servscript](/Project3/img/server-block-on-serv1n2.png)

 - created a symbolic link between both websites by running the following command

   **sudo ln -s /etc/nginx/sites-available/job /etc/nginx/sites-enabled/**

- Ran the **sudo nginx -t** to verify my syntax and it was successful.

- restarted my server with **sudo systemctl restart nginx**

- I went on to *server 2* and repeated the same procedure till my *nginx server* was  running my second server 

- I went back to *server 1* and *2* running the command 

  **sudo rm /etc/nginx/sites-enabled/default** so as to delete the site enabled configuration folder.

  ![deletedefault](/Project3/img/sysmbolic-link-test-and-delete-default-config1.png)

  ![deletedefault](/Project3/img/symblic-link-ltest-and-delete-default-config2.png)

  I restarted my nginx server with **sudo systemctl restart nginx**

- accessed my ip addresses **"35.86.164.198"** and **"54.185.210.35"** and the sites were live but unsecured.

![siteslive](/Project3/img/ip-adress-showing-sites-live%20(1).png)

![ip2live](/Project3/img/ip-adress-showing-sites-live%20(2).png)

- went to my *server 3* where I installed *nginx* and tested the status with 

**sudo systemctl status nginx** and it was running,

![serv3status](/Project3/img/server3-nginx-status.png)

- Ran **sudo nano /etc/nginx/nginx.conf** where I edited my configuration adding the following server information

![server3config](/Project3/img/server3-config.png)

- went on to test with **sudo nginx -t** 

![serv3test](/Project3/img/server3-config-test.png) and it was successful restarted the server with

 **sudo systemctl restart nginx**

- went to *Route53* where I created an *A record* for the root domain and the subdomain with my *server 3* ip address

 **"44.243.34.227"**

![createArecord](/Project3/img/Create-record1.png)

![create2ndrec](/Project3/img/create-record2.png)

- Accessed the terminals for *server 1* and *server 2* using **sudo nano /etc/nginx/sites-available job** and 

 **sudo nano /etc/nginx/sites-available/agency** for *server 2* to verify and correct any settings in the server block.

- restarted my *nginx* server with  **nginx with sudo systemctl restart nginx**

- I visited my domain name **"cloudconnect.click"** and the website was live yet unsecured

- I finally went on to secure my domain by executing the commands

   **sudo apt update**

   **sudo apt install python3-certbot-nginx**

   **sudo certbot --nginx**

   ![cert](/Project3/img/certbot-certificate.png)

- I visited my domain and refreshed and saw the changes and it was secure.

![securedserv1](/Project3/img/secured1.png)

![securedserv2](/Project3/img/secured2.png)

- I lastly tested the renew command in *dry-run mode*.

![renew](/Project3/img/dry-run.png)



###End of project