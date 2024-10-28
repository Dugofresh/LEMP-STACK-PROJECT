# LEMP Stack Implementation on Ubuntu 20.04 (Linux, Nginx, MySQL, PHP)
### This guide documents the steps to set up a LEMP stack on Ubuntu 20.04, including Linux, Nginx, MySQL, and PHP configurations. It follows DigitalOcean’s tutorial with additional details on setup, troubleshooting, and screenshots.

#### Project Repository: LEMP Stack Project

##### Prerequisites
Ubuntu 20.04 LTS on a cloud server (e.g., EC2, DigitalOcean).
SSH Access and a secure key pair.
Firewall Settings: Ensure HTTP (port 80), HTTPS (port 443), and SSH (port 22) traffic are permitted.
Step 1: Connect to Server and Update Packages
SSH into Your Server

## Steps
### Step 1: Update the Server Packages
First, I updated the server’s package list to ensure the latest software versions:

````
sudo apt update && sudo apt upgrade
`````
[this are the screenshots 1](photos-lemp/a.png)

 [screenshots2](photos-lemp/a1.png)

[screenshots3](photos-lemp/a2.png)

### Step 2: Install Nginx
Next, I installed the Nginx web server and verified its status to ensure it was running:
````
sudo apt install nginx 
sudo systemctl status nginx
````

[screenshots4](photos-lemp/b.png)


### Step 3: Install MySQL
To handle data storage, I installed MySQL:
````
sudo apt install mysql-server 
````
After installation, I ran a security script to remove insecure settings and set up a secure MySQL environment:

````
sudo mysql_secure_installation
````
Challenge: Ensuring MySQL had a strong root password and configuring it for secure access. Solution: Followed recommended secure installation options, including setting a root password and removing test databases.

### Step 4: Install PHP
With MySQL and Nginx set up, I moved on to install PHP:

````
sudo apt install php-fpm php-mysql -y
````
[screenshots5](photos-lemp/c.png)
[screenshots6](photos-lemp/d.png)

### Step 5: Configure Nginx to Use the PHP Processor
This step involved configuring Nginx to process PHP files correctly. I created a new directory for my domain within /var/www/ to keep site files organized:
````
sudo mkdir /var/www/your_domain
sudo chown -R $USER:$USER /var/www/your_domain
````
````
sudo nano /etc/nginx/sites-available/your_domain
````
[screenshots7](photos-lemp/e.png)

[screenshots8](photos-lemp/f.png)

[screenshots9](photos-lemp/g.png)

[screenshots10](photos-lemp/h.png)