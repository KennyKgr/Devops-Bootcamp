#**PROJECT ONE**

##**setting up an nginx static server**

- Following all the tasks we were given, we had to use all this 

process to successfuly accomplish building and securing a static 

website.

**First task was to Create an Ubuntu server**

- I logged into my Iam user account on the aws console, seached for

 **Ec2** and created an intance with an **Ubuntu server**.

![UbuntuServer](/Project1/img/ubuntuserv1.png)


 - Created a **key pair** for access firstly and saving the **.pem** to my  download folder 
 
![pemkey](/project1/img/create-key-pair2.png)

- I allowed ssh, http and https access when creating the instance

![allowed](/Project1/img/selected-allow-ssh,http,https3.png)

- I went on to launch an Ec2 instance

![instancel](/Project1/img/launch-the-instance.png)

- Then I ssh to my **ubuntu server with the command I got from the

  **ssh tab** of the instance which I executed from my powershell
  
  in the key location source download folder on my pc by navigating in

 powershell open
  
![connect](/Project1/img/connect-to-the-instance-with-your-pem-key.png)

- I created an elastic ip for my server on the aws console

  by going to the network and security portion and selected elastic 

  ips and selected **allocate elastic ip address** which I then 

  associated with my instance and ssh again into my ubuntu server 

- When prompted I took yes to connect and on my server 

![elasticip](/Project1/img/elastic-ip-creation-and-association-to-instance.png)

- I then proceeded to update with **sudo apt update** and upgraded with
 
  **sudo apt upgrade** and installed the **nginx** with 
  
  **sudo apt install nginx** then started the nginx server with 
  
  **sudo systemctl start nginx** then enabled it to autostart with 
  
  **sudo systemctl enable nginx** and verified the status with 
  
  **sudo systemctl status nginx**  
  
- I proceeded to copy my public Ip 
  
  address from the aws console **54.189.239.33** 
  
![publicip](/Project1/img/publicip.png)
  
  and went on to  visit it on a browser window and the 
  
  **nginx server** was live and running

![nginxserv](/Project1/img/nginx-server-live.png)

- I proceeded to download a template from **www.tooplate.com** and 
  
  selected the **Waso Strategy template** which from the ubuntu server 
  
  I used the **curl** command to download the zip file to my **/var/www/html**
   
  directory with the command **sudo curl -0 /var/www/html/
   
  2130_waso_strategy.zip https://www.tooplate.com/zip-templates/
   
  2130_waso_strategy.zip**

 ![template](/Project1/img/tooplate-template.png)  

- proceding to install the unzip utility, I installed with **sudo apt install unzip** 
   
- I navigated to the download directory with **cd /var/www/html**

   unzipped the file with **sudo unzip 2130_waso_strategy.zip**

- I went on to update my **nginx server** with the command 

   **sudo nano /etc/nginx/sites-available/default** where I edited
   
    the root server block to the directory of my website files, restarted my 
    
   **nginx server** with **sudo systemctl restart nginx** then went 
    
    ahead and visited my public ipv4 address and the site was up, to 
    
    get the site accessible via a domain name I procured a domain 
    
**cloucconnect.click** from my domain name registrar 
    
 **Hostinger** at **www.hostinger.com**  
    
![Domainm](/Project1/img/domain-purchased.png)

- Proceeded to my aws console using **route53** to input my domain name, 

  selected **public hosted zones**  and selected **public hosted zones** 
  
- I then copied the assigned values and went to my domain name registrar 

  to input the name servers in the custom Dns fields

 ![dmnservs](/Project1/img/domain-name-and-name-servers.png)


- I went back on my aws console and created a record selecting the
   
   **create record**  field and creating one for my domain and sub domain 


- went on  with **sudo nano /etc/nginx/sites-available/default** and updated 
 
   the server block with the domain name and sub domain 
    
   **www.cloudconnect.click** and **cloudconnect.click** 
    
- I proceeded to restart the **nginx server** with 
    
    **sudo systemctl restart nginx** went ahead to verify if my website was accessible 
    
    via the domain name and it was yet still unsecure, 
  
- Proceeded to install and request for an ssl/tls certificate installing with 

   **sudo apt update** 
      
    and **sudo apt install certbot python3-certbot -nginx**

    with **sudo certbot --nginx** deployed the certificates to domain
   
    and subdomains 
    
![ssldep](/Project1/img/ssldeploy.png)

- verified the website ssl using the openssl utility with 

  **openssl s_client -connect cloudconnect.click:443**

![test](/Project1/img/openssl-test.png)

- visited the website **www.cloudconnect.click** and the website was live and secured.

![sitesec](/Project1/img/final-secured-site.png)


###End of the project








