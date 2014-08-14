MYSQL Installation:

1)Check version linux version:
  - command : lsb_release -a
  - output  : Description:Red Hat Enterprise Linux Server release 6.5
  - (sample): Release    : 6.5

2)Go to <http://dev.mysql.com/downloads/repo/yum/>
  - Find the community server GA, based on your linux version.
  - example : Red Hat Enterprise Linux Server release 6.5
  - (sample): download Red Hat Enterprise Linux 6/ Oracle Linux 6(Architecture Independent), RPM Package.
  - command  : wget http://repo.mysql.com/mysql-community-release-el6-5.noarch.rpm. 

3)Install mysql with Yum:
  - command: sudo yum install mysql-community-server

4)Start mysql server:
  - command : sudo service mysqld start
  - output  : Starting mysqld:[ OK ]

5)Securing mysql installation:
  - **NOTE**    : default password for root: (blank/nothing) - just hit enter
  - command : mysql_secure_installation
  - output  : Follow instructions to set up mysql server

6)Find my.cnf:
  - **NOTE**    : default configration file etc/my.cnf
  - command : whereis my.cnf
  - output  : location of my.cnf

7)Change default data directory:
  - 7a) STOP MYSQL SERVICE
  - **NOTE**    : Before making changes, stop mysql service
        - command : sudo service mysqld stop
  - 7b) Change data directory
  - NOTE: default mysql data directory /var/lib/mysql
  - command : sudo cp - rap /var/lib/mysql /nfsshare/mysql
  - output  : copy default mysql data directory to other location(/nfsshare/mysql)
  - 7c) Set the required mysql ownership on new directory
  - command : chown mysql.mysql /nfsshare/mysql
  - 7d) Update my.cnf values datadir and socket variable(under mysqld & client)
  - Change From: datadir = /var/lib/mysql , socket=/var/lib/mysql/mysql.sock(under mysqld & client)
  - Change to: datadir = /nfsshare/mysql , socket = nfsshare/mysql/mysql.sock(under mysqld)
  - Change to:socket = nfsshare/mysql/mysql.sock(under client)

8)Set up users in mysql:
  - **NOTE**: Must be in mysql(ex: mysql> .....)
  - To create a user:
  - mysql command : CREATE USER 'newuser'@'localhost' IDENTIFIED BY 'password';
  - To add permissions to the user: (ex: DBA)
  - mysql command : GRANT ALL PRIVILEGES ON * . * TO 'newuser'@'localhost';

9)Make changes to my.cnf:
  - 
