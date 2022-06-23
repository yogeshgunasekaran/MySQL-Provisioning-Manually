# MySQL-Provisioning-Manually
Installation of MySQL in CentOS7
### Login to the db vm
 ```sh
 vagrant ssh db01
 ```
### Verify Hosts entry, if entries missing update the it with IP and hostnames
```sh 
cat /etc/hosts 
```
### Update OS with latest patches
 ```sh 
 yum update -y 
 ```
### Set Repository
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
systemctl enable mariadb
```
### RUN mysql secure installation script.
 ```sh
 mysql_secure_installation
 ```
