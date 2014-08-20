#MYSQL Installation(RHEL):


1. Check version linux version:
  - $ lsb_release -a
  - output  : Description:Red Hat Enterprise Linux Server release 6.5
  - (sample): Release    : 6.5

2. Go to this [link](http://dev.mysql.com/downloads/repo/yum/)
  - Find the community server GA, based on your linux version.
  - *example* : Red Hat Enterprise Linux Server release 6.5
  - (sample): download Red Hat Enterprise Linux 6/ Oracle Linux 6(Architecture Independent), RPM Package.
  - $ wget http://repo.mysql.com/mysql-community-release-el6-5.noarch.rpm. 

3. Install the repository from the local file:
  - $ sudo yum localinstall mysql-community-release-el6-5.noarch.rpm

4. Install mysql server with yum:
  - $ sudo yum install mysql-community-server

5. Start mysql server:
  - $ sudo service mysqld start
  - output  : Starting mysqld:[ OK ]

6. Securing mysql installation:
  - **NOTE**    : default password for root: (blank/nothing) - just hit enter
  - $ mysql_secure_installation
  - output  : Follow instructions to set up mysql server

7. Find my.cnf:
  - **NOTE**    : default configration file etc/my.cnf
  - $ whereis my.cnf
  - output  : location of my.cnf

8. Change default data directory:
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

9. Set up users in mysql:
  - **NOTE**: Must be in mysql(replace **newuser** with username, **password** with a password for this user)
  - To create a user:
  - mysql> CREATE USER 'newuser'@'localhost' IDENTIFIED BY 'password';
  - To add permissions to the user: (ex: DBA)
  - mysql> GRANT ALL PRIVILEGES ON * . * TO 'newuser'@'localhost';

10. Make changes to my.cnf:
  - Depending on server resources avaliable you will want to adjust **innodb_buffer_pool_size** and **key_buffer_size**.
  - MYSQL recommends the key_buffer_size be **<25%** of physical ram, while innodb_buffer_pool_size be **70-80%** of physical ram.
  - innodb_log_file_size is important for write intensive workload(large data sets). Larger size offers better performance but increase recovery time.

11. To install additional MySQL products and components:
  - 11a.List packages for MySQL components avaliable for your platform from MYSQL Yum repository
  - $sudo yum --disablerepo=\* --enablerepo='mysql*-community*' list available
  - 11b.Install package of your choice with follow command(replace **package-name** with name of package
  - $sudo yum install package-name(**example**: $sudo yum install mysql-community-devel.x86_64)
