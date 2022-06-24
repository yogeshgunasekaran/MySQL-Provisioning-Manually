# MySQL-Provisioning-Manually
Installation of MySQL in CentOS7
### Login to the root user
 ```sh
 sudo su -
 ```
### Update OS with latest patches
 ```sh 
 yum update -y 
 ```
### Set EPEL Repository
 ```sh
  yum install epel-release -y 
 ```
### Install Maria DB Package
```sh
 yum install git mariadb-server -y
 ```
### Starting & enabling mariadb-server
```sh
systemctl start mariadb
```
```sh
systemctl enable mariadb
```
### RUN mysql secure installation script
 ```sh
 mysql_secure_installation
 ```   
 ### Console <br>
> Set root password? [Y/n] Y <br> 
> New password: <br>
> Re-enter new password: <br>
> Password updated successfully! <br>
> Reloading privilege tables.. <br>
> ... Success! <br>
>>
>> By default, a MariaDB installation has an anonymous user, allowing anyone <br>
>> to log into MariaDB without having to have a user account created for <br>
>> them. This is intended only for testing, and to make the installation <br>
>> go a bit smoother. You should remove them before moving into a <br>
>> production environment.
>>  <br>
>>  
> Remove anonymous users? [Y/n] Y <br>
> ... Success! <br>
> 
>> 
>> Normally, root should only be allowed to connect from 'localhost'. This <br>
>> ensures that someone cannot guess at the root password from the network.<br>
>> 
>  Disallow root login remotely? [Y/n] n <br>
> ... skipping. <br>
>>
>> By default, MariaDB comes with a database named 'test' that anyone can <br>
>> access. This is also intended only for testing, and should be removed <br>
>> before moving into a production environment. <br>
>> 
>Remove test database and access to it? [Y/n] Y <br>
> - Dropping test database... <br>
> ... Success! <br>
> - Removing privileges on test database... <br>
> ... Success! <br>
>>
>> Reloading the privilege tables will ensure that all changes made so far <br>
>> will take effect immediately. <br>
>> 
> Reload privilege tables now? [Y/n] Y <br>
> ... Success! <br> <br>

### Set DB name and users
```sh
mysql -u root -p
```
~~~
mysql> create database accounts;
mysql> grant all privileges on accounts.* TO 'admin'@’%’ identified by 'admin123' ;
mysql> FLUSH PRIVILEGES;
mysql> exit;
~~~
> Now user "admin" can log in remotely from anywhere to this MySQL DB and he has got all the privileges with the "accounts" database created above. <br>
> <br>

### To download and intialize a Database(.sql) that exists in GitHub in our MySQL:
~~~
git clone -b <branch name> <repository link> 
mysql -u root -p admin123 accounts < <path of "db_backup.sql" file been cloned> 
mysql -u root -p admin123 accounts 
mysql> show tables; 
~~~
> The above commands are logging into the mysql as a root user with its pass: admin123 and creating a database "accounts" and intializing it with "db_backup.sql"

### Starting the firewalld and allowing the mariadb to access from port no. 3306 (Optional)
```sh
systemctl start firewalld
```
```sh
systemctl enable firewalld
```
```sh
firewall-cmd --get-active-zones
```
```sh
firewall-cmd --zone=public --add-port=3306/tcp --permanent
```
```sh
firewall-cmd --reload
```
```sh
systemctl restart mariadb
```
