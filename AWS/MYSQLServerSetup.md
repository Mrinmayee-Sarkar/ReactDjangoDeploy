### Install MySql 8.0 on Ubuntu 20.04 ###

In this Document, we will learn how to use the Debian package repository to install MySql 8.0 on Ubuntu 20.04 with the apt package manager.


Prerequisites -

1) Server with Ubuntu 20.04 installed (EC2 instance can also work)

2) User with sudo permission

#### Step 1 — Installing MySQL ####

On Ubuntu 20.04, you can install MySQL using the APT package repository. At the time of this writing, the version of MySQL available in the default Ubuntu repository is version 8.0.19.

1) To install it, update the package index on your server if you’ve not done so recently:

```
sudo apt update -y

```
![update](screenshots/apt-get-update.JPG)

2) To install the mysql-server package:

```
sudo apt install mysql-server -y

```
![install mysql-server](screenshots/apt-get-install-mysql-server.JPG)

---
**NOTE**

This will install MySQL, but will not prompt you to set a password.
We will set the password in the next step (step-2).

---

#### Step 2 — Configuring MySQL ####

For fresh installations of MySQL, you’ll want to run the DBMS’s included security script.
This script changes some of the less secure default options for things like remote root logins remove test database etc.

Run the below security script:

```
sudo mysql_secure_installation

```

---
**NOTE**

This will ask you series of prompts where you can make some changes to your MySQL installation’s security options.

---

1) The first prompt will ask whether you’d like to set up the Validate Password Plugin, Please press y/Y

![Validate Password Plugin](screenshots/mysql_secure_installation-validate-plugin-1.JPG)


2) Now you have to choose password validation policy, please press 2

![password validation policy](screenshots/mysql_secure_installation-validate-plugin-2.JPG)

3) Now you have to set root password, Please set a strong password which is 8 or more in length, and contains numeric, mixed case, special characters, in our case I have used password for root "TEk9#TC5hJv" after entering this please press y/Y when it is asking for Do you wish to continue with the password provided?

![set root password](screenshots/mysql_secure_installation-validate-plugin-3.JPG)

4) The next prompt will ask whether you’d like to remove some anonymous users, please press y/Y

![remove some anonymous users](screenshots/mysql_secure_installation-validate-plugin-remove-user.JPG)

5) The next prompt will ask whether you’d like to disable remote root logins, please press y/Y

![disable remote root logins](screenshots/mysql_secure_installation-validate-plugin-disallow-root.JPG)

6) The next prompt will ask whether you’d like to remove test database, please press y/Y

![remove test database](screenshots/mysql_secure_installation-validate-plugin-remove-testdb.JPG)

7) The next prompt will ask whether you’d like to load these new rules so that MySQL, please press y/Y

![load these new rules so that MySQL](screenshots/mysql_secure_installation-validate-plugin-reload.JPG)


#### Step 3 — Creating a Dedicated MySQL User and Granting Privileges ####

1) Create new MySQL user with below command
```
sudo mysql
```

2) Now inside my MySQL Prompt, please run the below commands

* CREATE USER 'username'@'host' IDENTIFIED BY 'password';

For example if username is "dbadmin" and  password is "*=q42EeUxp9"  then run the below command

```
CREATE USER 'dbadmin'@'localhost' IDENTIFIED BY '*=q42EeUxp9';


CREATE USER 'dbadmin'@'%' IDENTIFIED BY '*=q42EeUxp9';
```

---
**NOTE**

In Host, we can opt from 2 values like localhost or %. 'localhost' is only for localhost and '%' is for world wide

---

* GRANT CREATE, ALTER, DROP, INSERT, UPDATE, DELETE, SELECT, REFERENCES, RELOAD on *.* TO 'username'@'host' WITH GRANT OPTION;

For example if username is "dbadmin" and you want to grant the PRIVILEGES on every database present then

```
GRANT CREATE, ALTER, DROP, INSERT, UPDATE, DELETE, SELECT, REFERENCES, RELOAD on *.* TO 'dbadmin'@'localhost' WITH GRANT OPTION;


GRANT CREATE, ALTER, DROP, INSERT, UPDATE, DELETE, SELECT, REFERENCES, RELOAD on *.* TO 'dbadmin'@'%' WITH GRANT OPTION;
```
---
**NOTE**

If you want to grant ALL PRIVILEGES privilege then run below commands

* GRANT ALL PRIVILEGES ON *.* TO 'username'@'host' WITH GRANT OPTION;

For example if username is "dbadmin"

```
GRANT ALL PRIVILEGES ON *.* TO 'dbadmin'@'localhost' WITH GRANT OPTION;


GRANT ALL PRIVILEGES ON *.* TO 'dbadmin'@'%' WITH GRANT OPTION;
```

---

* Run the below command to free up any memory that the server cached as a result of the preceding CREATE USER and GRANT statements
```
FLUSH PRIVILEGES;
```

* Run the below command to exit the MySQL client
```
exit;
```


#### Step 4 — Creating a Database ####


1) Login to MYSql using below command

mysql -h <db-hostname/ip> -u <username> -p

For example if username is "dbadmin" and  password is "*=q42EeUxp9"  and database is ip is localhost then

```
mysql -h localhost -u dbadmin -p
```

2) Now it will provide you MySQL prompt, please enter below command to create database in it.

CREATE DATABASE <database_name> CHARACTER SET = 'utf8' COLLATE = 'utf8_unicode_ci';

For example if database_name is "5gaasnetwork" then

```
CREATE DATABASE 5gaasnetwork CHARACTER SET = 'utf8' COLLATE = 'utf8_unicode_ci';
```

---
**NOTE**

To check the available databases please run the below commands.

```
SHOW DATABASES;
```
---

#### Step 5 — Import and export Database ####

1) For Exporting the database dump on local system

Use mysqldump to export your database this will export it to 5gaasnetwork.sql

mysqldump -h <db-hostname/ip> -u <username> -p <database_name> > 5gaasnetwork.sql

- username is the username you can log in to the database with
- database_name is the name of the database to export
- 5gaasnetwork.sql is the file in the current directory that stores the output.

for example if database name is 5gaasnetwork and username is "dbadmin" and  password is "*=q42EeUxp9"  and database is ip is localhost then
```
mysqldump -h localhost -u dbadmin -p 5gaasnetwork > 5gaasnetwork.sql
```
---
**NOTE**

This will ask for the password at last

---


2) For Importing the database from dump present on local system (5gaasnetwork.sql)


mysql -h <db-hostname/ip>  -u <username> -p <database_name> < 5gaasnetwork.sql

- username is the username you can log in to the database with
- database_name is the name of the freshly created database on which you want to import dump
- 5gaasnetwork.sql is the data dump file to be imported, located in the current directory


for example if database_name is 5gaasnetwork and username is "dbadmin" and  password is "*=q42EeUxp9"  and database is ip is localhost then
```
mysql -h localhost  -u dbadmin -p 5gaasnetwork < 5gaasnetwork.sql
```
---
**NOTE**

This will ask for the password at last

---

#### Step 6 — (Optional) Open mysql to be accessed from outside ####

1) Open mysqld.cnf file to edit
```
sudo vi /etc/mysql/mysql.conf.d/mysqld.cnf
```

2) Comment below lines in mysqld.cnf file

from
```
bind-address           = 127.0.0.1
mysqlx-bind-address    = 127.0.0.1
```
to
```
#bind-address           = 127.0.0.1
#mysqlx-bind-address    = 127.0.0.1
```

3) Restart mysql
```
sudo /etc/init.d/mysql restart
```

### Who do I talk to? ###

* jenkins.devops@amantyatech.com