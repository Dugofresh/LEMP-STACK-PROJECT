# LEMP Stack Project on Ubuntu 20.04

Welcome to the **LEMP Stack** project repository! This project walks through the process of setting up a LEMP stack (Linux, Nginx, MySQL, PHP) on an Ubuntu 20.04 server. This environment provides a foundation for developing, testing, and deploying web applications using Nginx as the web server and PHP as the scripting language.

**Project Repository**: [GitHub Repository Link](https://github.com/Dugofresh/LEMP-STACK.git)

## Table of Contents
1. [Project Overview](#project-overview)
2. [Technologies Used](#technologies-used)
3. [Prerequisites](#prerequisites)
4. [Installation and Setup](#installation-and-setup)
   - [Step 1: Connect to Server](#step-1-connect-to-server)
   - [Step 2: Install Nginx](#step-2-install-nginx)
   - [Step 3: Install MySQL](#step-3-install-mysql)
   - [Step 4: Install PHP](#step-4-install-php)
5. [Configuration](#configuration)
6. [Project Structure](#project-structure)
7. [Usage](#usage)
8. [Learning Outcomes](#learning-outcomes)
9. [Screenshots](#screenshots)
10. [License](#license)

## Project Overview
The objective of this project was to implement a secure, optimized LEMP stack on Ubuntu 20.04. By setting up Linux, Nginx, MySQL, and PHP, this project achieves a robust environment that is scalable and reliable for web applications.

## Technologies Used
- **Linux (Ubuntu 20.04)**: Base operating system.
- **Nginx**: Web server to handle HTTP requests efficiently.
- **MySQL**: Relational database management system.
- **PHP**: Scripting language for dynamic content.

## Prerequisites
- AWS EC2 instance with Ubuntu 20.04.
- SSH access to the server using a private key (e.g., `project1-key.pem`).
- Basic knowledge of command-line operations.

## Installation and Setup

### Step 1: Connect to Server
1. **Access the server** using SSH:
   ```bash
   ssh -i "project1-key.pem" ubuntu@13.48.55.145


2. Update and upgrade the package lists:
````
sudo apt update && sudo apt upgrade -y
````
### Step 2: Install Nginx

1. Install Nginx:
````
sudo apt install nginx -y
````
2. Allow HTTP and HTTPS traffic:
```
sudo ufw allow 'Nginx Full'
````
3. Test Nginx Installation by visiting the server’s IP in a web browser (e.g., http://13.48.55.145). You should see the Nginx welcome page.

### Step 3: Install MySQL
1. Install MySQL:
```
sudo apt install mysql-server 
````
2. Secure MySQL:
```
sudo mysql_secure_installation
````
3. Log in to MySQL as root:
````
sudo mysql -u root -p
````
### Step 4: Install PHP
1. Install PHP and PHP-FPM:
```` 
sudo apt install php-fpm php-mysql
````
2. Configure Nginx to use PHP:

 - Open the Nginx default config file
 ````
 sudo nano /etc/nginx/sites-available/default
````
Create Web Directory and Permissions

Create a root web directory for your_domain

````
sudo mkdir /var/www/your_domain
````
2. Assign ownership of the directory to the current user
````
sudo chown -R $USER:$USER /var/www/your_domain
````
Assign ownership of the directory to the current user

````
sudo chown -R $USER:$USER /var/www/your_domain
````
Set Up Nginx Server Block for PHP Processing

1. Open a new configuration file in Nginx’s sites-available directory
````
sudo nano /etc/nginx/sites-available/your_domain
````
2. Add the following configuration to the file to define the server block:
````
server {
    listen 80;
    server_name your_domain www.your_domain;
    root /var/www/your_domain;

    index index.html index.htm index.php;

    location / {
        try_files $uri $uri/ =404;
    }

    location ~ \.php$ {
        include snippets/fastcgi-php.conf;
        fastcgi_pass unix:/var/run/php/php7.4-fpm.sock;
    }

    location ~ /\.ht {
        deny all;
    }
}
````
Enable the Server Block and Reload Nginx

1. Activate the configuration by creating a symbolic link to sites-enabled
````
sudo ln -s /etc/nginx/sites-available/your_domain /etc/nginx/sites-enabled/
````
2. Unlink the default configuration:
````
sudo unlink /etc/nginx/sites-enabled/default
````
3. Test Nginx configuration for syntax errors:
````
sudo nginx -t
````
If any errors are reported, go back to your configuration file to review its contents before continuing.

4. When you are ready, reload Nginx to apply the changes
````
sudo systemctl reload nginx
````
### Step 5: Verify Your Setup
Now go to your browser and access your server’s domain name or IP address, as listed within the server_name directive in your server block configuration file:
````
http://13.48.55.145
````

# Project Structure
````
LEMP-STACK
├── README.md
├── config
│   ├── nginx-your_domain.conf  # Nginx server block configuration for your_domain
├── public
│   └── index.html              # Landing page for your_domain
└── screenshots                 # Directory for setup screenshots

````



