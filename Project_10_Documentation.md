## **Project_10_Load Balancer Solution With Nginx and SSL/TLS**
___
____
### **Step-1 Configure NGINX as A Load Balancer**
___
>#### Launch 1 EC2 instance with Ubuntu 20.04 Operating System and name it NGINX-LB  Open TCP port 80 for HTTP connections, and TCP port 443 – this port is used for secured HTTPS connections)

![ec2](./Project_10_Images/EC2.PNG)
![ec2](./Project_10_Images/HTTP_HTTPS_PORT.PNG)

>#### Update /etc/hosts file 
Access the File using *`sudo vi /etc/hosts`* and update for local DNS with Web Servers’ names (e.g. Web1 and Web2) and their Private IP addresses.

![ec2](./Project_10_Images/Local%20host.PNG)

>#### Install and Configure NGINX Load Balancer

##### *Update the instance and Install Nginx:*
* *`sudo apt update`*
* *`sudo apt install nginx`*

![ec2](./Project_10_Images/apt%20update.PNG)
![ec2](./Project_10_Images/install%20NGNX.PNG)
##### *Configure Nginx LB using Web Servers’ names defined in /etc/hosts using :*
* *`sudo vi /etc/nginx/nginx.conf`*

![ec2](./Project_10_Images/ngixconf.PNG)
##### Restart Nginx and make sure the service is up and running
* *`sudo systemctl restart nginx`*
* *`sudo systemctl status nginx`*

![Apache](./Project_10_Images/nginx%20start.PNG)
### **Step-2 Register a New Domain Name**
___
Using AWS Route53 i registered a new domain name `www.olusegundevopsproject.click`

![dns](./Project_10_Images/Route53%20DNS%20Mgt.PNG)
![dns](./Project_10_Images/register%20Domainname.PNG)

>#### Assign & Allocate Elastic IP
On AWS console select Elastic IP and Assign an Elastic IP to your Nginx LB server and associate your domain name with this Elastic IP

![EIP](./Project_10_Images/ElasticIP.PNG)
![EIP](./Project_10_Images/ElasticIP2.PNG)
![EIP](./Project_10_Images/ElasticIP3.PNG)

>#### Update A record in the Registrar
In the registrar configure A record to point to Nginx LB using Elastic IP address

![EIP](./Project_10_Images/Route53%20Add%20record.PNG)

>#### Configure Nginx to recognize your new domain name
Using the *`sudo vi /etc/nginx/nginx.conf`* command to acces the nginx config file the domain name is modifedto the newly created one fron Route53

![dns](./Project_10_Images/ngixconf%20dns%20changed.PNG)

>#### Accessing the Web Server
To verify that our configuration done  works I access the Web Server from a browswer using the new Domain name; http://www.olusegundevopsproject.click


### **Step-3 Configure secured connection using SSL/TLS certificates**
____
>#### Install certbot and request for an SSL/TLS certificate