# My first project - WEB Stack Implementation in AWS

###### Setup a new EC2 instance on AWS

![Screenshot (52)](https://github.com/animalchin24/Devops-Projects-1/assets/114111560/9976e679-315f-4f75-995a-21144c0a7001)

## Step 1: Connect to EC2 Instance

## Step 2: Install Apache Web Server
```
#update a list of packages in package manager
sudo apt update

#run apache2 package installation
sudo apt install apache2
```
![Screenshot (57)](https://github.com/animalchin24/Devops-Projects-1/assets/114111560/db9b316b-87a5-4dac-ba53-e22f6f998f6a)

To verify that apache2 is running as a Service in our OS, use following command
```
sudo systemctl status apache2
```
First, let us try to check how we can access it locally in our Ubuntu shell, run:
```
curl http://localhost:80
```
or
```
 curl http://127.0.0.1:80
```
 Now it is time for us to test how our Apache HTTP server can respond to requests from the Internet. Open a web browser of your choice and try to access following url

http://<Public-IP-Address>:80
![Screenshot (58)](https://github.com/animalchin24/Devops-Projects-1/assets/114111560/bc39b9dc-5c8f-498f-8b43-f2e9580221d1)

## STEP 2 — INSTALLING MYSQL
```
$ sudo apt install mysql-server
```
![Screenshot (59)](https://github.com/animalchin24/Devops-Projects-1/assets/114111560/5fa015f9-04e7-4909-9cbd-2ad958316d14)

When the installation is finished, log in to the MySQL console by typing:
```
$ sudo mysql
```
```
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 11
Server version: 8.0.22-0ubuntu0.20.04.3 (Ubuntu)

Copyright (c) 2000, 2020, Oracle and/or its affiliates. All rights reserved.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

mysql>
```
![Screenshot (60)](https://github.com/animalchin24/Devops-Projects-1/assets/114111560/ca8eeafd-4fb5-4310-b33b-e39e42995bd0)


It’s recommended that you run a security script that comes pre-installed with MySQL. This script will remove some insecure default settings and lock down access to your database system. Before running the script you will set a password for the root user, using mysql_native_password as default authentication method. We’re defining this user’s password as PassWord.1.
```
ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'PassWord.1';
```
Exit the MySQL shell with:
```
mysql> exit
```
Start the interactive script by running:
```
$ sudo mysql_secure_installation
```
This will ask if you want to configure the VALIDATE PASSWORD PLUGIN.

Note: Enabling this feature is something of a judgment call. If enabled, passwords which don’t match the specified criteria will be rejected by MySQL with an error. It is safe to leave validation disabled, but you should always use strong, unique passwords for database credentials.

Answer Y for yes, or anything else to continue without enabling.

VALIDATE PASSWORD PLUGIN can be used to test passwords
and improve security. It checks the strength of password
and allows the users to set only those passwords which are
secure enough. Would you like to setup VALIDATE PASSWORD plugin?

Press y|Y for Yes, any other key for No:

Regardless of whether you chose to set up the VALIDATE PASSWORD PLUGIN, your server will next ask you to select and confirm a password for the MySQL root user. This is not to be confused with the system root. The database root user is an administrative user with full privileges over the database system. Even though the default authentication method for the MySQL root user dispenses the use of a password, even when one is set, you should define a strong password here as an additional safety measure. We’ll talk about this in a moment.

If you enabled password validation, you’ll be shown the password strength for the root password you just entered and your server will ask if you want to continue with that password. If you are happy with your current password, enter Y for “yes” at the prompt:

Estimated strength of the password: 100 
Do you wish to continue with the password provided?(Press y|Y for Yes, any other key for No) : y
![Screenshot (62)](https://github.com/animalchin24/Devops-Projects-1/assets/114111560/a1febcd7-e6bc-48d5-85eb-a7334a414512)


When you’re finished, test if you’re able to log in to the MySQL console by typing:
```
$ sudo mysql -p
```
Notice the -p flag in this command, which will prompt you for the password used after changing the root user password.

To exit the MySQL console, type:
```
mysql> exit
```
## Step 3 Installing PHP

To install these 3 packages at once, run:
```
sudo apt install php libapache2-mod-php php-mysql
```
Once the installation is finished, you can run the following command to confirm your PHP version:
```
php -v
```
![Screenshot (63)](https://github.com/animalchin24/Devops-Projects-1/assets/114111560/6f775e28-6e1f-461d-8372-8b74841600da)

At this point, your LAMP stack is completely installed and fully operational.

Linux (Ubuntu)
Apache HTTP Server
MySQL
PHP
To test your setup with a PHP script, it’s best to set up a proper Apache Virtual Host to hold your website’s files and folders. Virtual host allows you to have multiple websites located on a single machine and users of the websites will not even notice it.

We will configure our first Virtual Host in the next step.

## STEP 4 — CREATING A VIRTUAL HOST FOR YOUR WEBSITE USING APACHE

Create the directory for projectlamp using ‘mkdir’ command as follows:
```
sudo mkdir /var/www/projectlamp
```
![Screenshot (64)](https://github.com/animalchin24/Devops-Projects-1/assets/114111560/809f8143-939d-4a3b-a1f6-61e83bca0e10)

Next, assign ownership of the directory with your current system user:
```
sudo chown -R $USER:$USER /var/www/projectlamp
```
![Screenshot (65)](https://github.com/animalchin24/Devops-Projects-1/assets/114111560/b40adfc7-735b-4a69-a6fa-888bb26cacf7)

Then, create and open a new configuration file in Apache’s sites-available directory using your preferred command-line editor. Here, we’ll be using vi or vim (They are the same by the way):
```
sudo vi /etc/apache2/sites-available/projectlamp.conf
```
This will create a new blank file. Paste in the following bare-bones configuration by hitting on i on the keyboard to enter the insert mode, and paste the text:
```
<VirtualHost *:80>
    ServerName projectlamp
    ServerAlias www.projectlamp 
    ServerAdmin webmaster@localhost
    DocumentRoot /var/www/projectlamp
    ErrorLog ${APACHE_LOG_DIR}/error.log
    CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>
```
![Screenshot (66)](https://github.com/animalchin24/Devops-Projects-1/assets/114111560/aeff459b-7faa-41e4-989c-28c583bd4765)

To save and close the file, simply follow the steps below:

Hit the esc button on the keyboard
Type :
Type wq. w for write and q for quit
Hit ENTER to save the file

You can use the ls command to show the new file in the sites-available directory
```
sudo ls /etc/apache2/sites-available
```
![Screenshot (67)](https://github.com/animalchin24/Devops-Projects-1/assets/114111560/6e6c9734-6f7d-4186-8128-e7f1f137111c)

With this VirtualHost configuration, we’re telling Apache to serve projectlamp using /var/www/projectlampl as its web root directory. If you would like to test Apache without a domain name, you can remove or comment out the options ServerName and ServerAlias by adding a # character in the beginning of each option’s lines. Adding the # character there will tell the program to skip processing the instructions on those lines.

You can now use a2ensite command to enable the new virtual host:
```
sudo a2ensite projectlamp
```
![Screenshot (69)](https://github.com/animalchin24/Devops-Projects-1/assets/114111560/0eae9875-5242-4136-9406-ca36eb86b21e)

You might want to disable the default website that comes installed with Apache. This is required if you’re not using a custom domain name, because in this case Apache’s default configuration would overwrite your virtual host. To disable Apache’s default website use a2dissite command , type:
```
sudo a2dissite 000-default
```
To make sure your configuration file doesn’t contain syntax errors, run:
```
sudo apache2ctl configtest
```
Finally, reload Apache so these changes take effect:
```
sudo systemctl reload apache2
```
![Screenshot (70)](https://github.com/animalchin24/Devops-Projects-1/assets/114111560/99c25707-7709-4adc-b61f-8e2eebd3d096)

Your new website is now active, but the web root /var/www/projectlamp is still empty. Create an index.html file in that location so that we can test that the virtual host works as expected:
```
sudo echo 'Hello LAMP from hostname' $(curl -s http://169.254.169.254/latest/meta-data/public-hostname) 'with public IP' 
$(curl -s http://169.254.169.254/latest/meta-data/public-ipv4) > /var/www/projectlamp/index.html
```
![Screenshot (71)](https://github.com/animalchin24/Devops-Projects-1/assets/114111560/aed89d45-b469-494f-a093-51f7ad4b98f9)
![Screenshot (72)](https://github.com/animalchin24/Devops-Projects-1/assets/114111560/50d4dc1e-1a59-4f7b-b4e7-73e87ec58f97)


Now go to your browser and try to open your website URL using IP address:

http://<Public-IP-Address>:80

If you see the text from ‘echo’ command you wrote to index.html file, then it means your Apache virtual host is working as expected. In the output you will see your server’s public hostname (DNS name) and public IP address. You can also access your website in your browser by public DNS name, not only by IP – try it out, the result must be the same (port is optional)

http://<Public-DNS-Name>:80
![Screenshot (73)](https://github.com/animalchin24/Devops-Projects-1/assets/114111560/2d410af6-4c30-4604-acce-3b640103f264)


You can leave this file in place as a temporary landing page for your application until you set up an index.php file to replace it. Once you do that, remember to remove or rename the index.html file from your document root, as it would take precedence over an index.php file by default.


## Step 5: Enable PHP on the website

In case you want to change this behavior, you’ll need to edit the /etc/apache2/mods-enabled/dir.conf file and change the order in which the index.php file is listed within the DirectoryIndex directive:
```
sudo vim /etc/apache2/mods-enabled/dir.conf
```
```
<IfModule mod_dir.c>
        #Change this:
        #DirectoryIndex index.html index.cgi index.pl index.php index.xhtml index.htm
        #To this:
        DirectoryIndex index.php index.html index.cgi index.pl index.xhtml index.htm
</IfModule>
```
Make sure to reload apache server
```
sudo systemctl reload apache2
```
![Screenshot (75)](https://github.com/animalchin24/Devops-Projects-1/assets/114111560/8f23d094-c474-44d2-900b-c67af16b1f06)
![Screenshot (76)](https://github.com/animalchin24/Devops-Projects-1/assets/114111560/9564a454-980c-4119-9e00-7c8caecdf2c6)


Finally, we will create a PHP script to test that PHP is correctly installed and configured on your server.

Now that you have a custom location to host your website’s files and folders, we’ll create a PHP test script to confirm that Apache is able to handle and process requests for PHP files.

Create a new file named index.php inside your custom web root folder:
```
vim /var/www/projectlamp/index.php
```
This will open a blank file. Add the following text, which is valid PHP code, inside the file:
```
<?php
phpinfo();
```
![Screenshot (77)](https://github.com/animalchin24/Devops-Projects-1/assets/114111560/1e6df10b-3c05-4a37-80ef-bdce5adba89a)

This page provides information about your server from the perspective of PHP. It is useful for debugging and to ensure that your settings are being applied correctly.

If you can see this page in your browser, then your PHP installation is working as expected.
![Screenshot (78)](https://github.com/animalchin24/Devops-Projects-1/assets/114111560/dfcfb324-87cf-4e10-b8f2-37efeccdb119)


After checking the relevant information about your PHP server through that page, it’s best to remove the file you created as it contains sensitive information about your PHP environment -and your Ubuntu server. You can use rm to do so:
```
sudo rm /var/www/projectlamp/index.php
```
Congratulations! You have finished your very first REAL LIFE PROJECT by deploying a LAMP stack website in AWS Cloud!
