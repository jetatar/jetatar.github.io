# Installing and Configuring Nextcloud on CentOS 7

## Introduction

Nextcloud is a file sharing server that permits you to store your personal content, like documents and pictures, in a centralized location, much like Dropbox. The difference with Nextcloud is that it is free and open-source, which allows anyone to use and examine it. It also returns the control and security of your sensitive data back to you, thus eliminating the utilization of a third-party cloud hosting service.

## Prerequisits 

* A user with sudo priveleges is necessary.
* A LAMP (Linux, Apache, MySQL, and PHP) stack: Nextcloud requires a web server, a database, and PHP to function properly.  Setting up a LAMP stack server fulfills all of these requirements.

### Install Apache
```
sudo yum install httpd
sudo systemctl start httpd.service
sudo systemctl enable httpd.service
```
Apache should be installed and the service started on boot.  To verify, one should be able to open a browser and go to http://your_server_IP_address/ and see the default Apache page.


### Install MySQL (MariaDB)
```
sudo yum install mariadb-server mariadb
sudo systemctl start mariadb
sudo systemctl enable mariadb.service
```

Now that our MySQL database is running, we want to run a simple security script that will remove some dangerous defaults and lock down access to our database system a little bit. Start the interactive script by running:
```
sudo mysql_secure_installation
```
The prompt will ask you for your current root password. Since you just installed MySQL, you most likely won’t have one, so leave it blank by pressing enter. Then the prompt will ask you if you want to set a root password. Go ahead and enter _Y_, and follow the instructions:
```
Enter current password for root (enter for none):
OK, successfully used password, moving on...

Setting the root password ensures that nobody can log into the MariaDB
root user without the proper authorization.

New password: password
Re-enter new password: password
Password updated successfully!
Reloading privilege tables..
 ... Success!
```
For the rest of the questions, you should simply hit the "ENTER" key through each prompt to accept the default values. This will remove some sample users and databases, disable remote root logins, and load these new rules so that MySQL immediately respects the changes we have made.
