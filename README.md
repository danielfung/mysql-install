#MYSQL Installation:


1. Check version linux version:
  - $ lsb_release -a
  - output  : Description:Red Hat Enterprise Linux Server release 6.5
  - (sample): Release    : 6.5

2. Go to <http://dev.mysql.com/downloads/repo/yum/>
  - Find the community server GA, based on your linux version.
  - *example* : Red Hat Enterprise Linux Server release 6.5
  - (sample): download Red Hat Enterprise Linux 6/ Oracle Linux 6(Architecture Independent), RPM Package.
  - $ wget http://repo.mysql.com/mysql-community-release-el6-5.noarch.rpm. 
  - $ sudo yum localinstall mysql-community-release-el6-5.noarch.rpm

3. Install mysql with Yum:
  - $ sudo yum install mysql-community-server

4. Start mysql server:
  - $ sudo service mysqld start
  - output  : Starting mysqld:[ OK ]

5. Securing mysql installation:
  - **NOTE**    : default password for root: (blank/nothing) - just hit enter
  - $ mysql_secure_installation
  - output  : Follow instructions to set up mysql server

6. Find my.cnf:
  - **NOTE**    : default configration file etc/my.cnf
  - $ whereis my.cnf
  - output  : location of my.cnf

7. Change default data directory:
  - 7a. STOP MYSQL SERVICE
  - **NOTE**    : Before making changes, stop mysql service
  - $ sudo service mysqld stop
  - 7b. Change data directory
  - NOTE: default mysql data directory /var/lib/mysql
  - $ sudo cp - rap /var/lib/mysql /nfsshare/mysql
  - output  : copy default mysql data directory to other location(/nfsshare/mysql)
  - 7c. Set the required mysql ownership on new directory
  - $ chown mysql.mysql /nfsshare/mysql
  - 7d. Update my.cnf values datadir and socket variable **(under [mysqld] & [client])**
  - Change From: datadir = /var/lib/mysql , socket=/var/lib/mysql/mysql.sock **(under [mysqld] & [client])**
  - Change to: datadir = /nfsshare/mysql , socket = nfsshare/mysql/mysql.sock **(under [mysqld])**
  - Change to:socket = nfsshare/mysql/mysql.sock(under client)

8. Set up users in mysql:
  - **NOTE**: Must be in mysql(ex: mysql> .....)
  - To create a user:
  - mysql> CREATE USER 'newuser'@'localhost' IDENTIFIED BY 'password';
  - To add permissions to the user: (ex: DBA)
  - mysql> GRANT ALL PRIVILEGES ON * . * TO 'newuser'@'localhost';

9. Make changes to my.cnf:
  - Depending on server resources avaliable you will want to adjust **innodb_buffer_pool_size** and **key_buffer_size**.
  - MYSQL recommends the key_buffer_size be **<25%** of physical ram, while innodb_buffer_pool_size be **70-80%** of ram.
