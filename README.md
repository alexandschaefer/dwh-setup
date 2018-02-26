Tested with ubuntu 16.04 and Homebrew on a Mac.

## Base packages

#### Mac

Install [Homebrew](http://brew.sh/). Then

    $ brew install -v dialog
    $ brew install -v coreutils
    $ brew install -v rsync
    $ brew install -v watch
    $ brew install -v igraph
    $ brew install -v graphviz
    $ brew tap homebrew/versions

#### Ubuntu 

    $ sudo apt install git dialog coreutils rsync watch graphviz igraph


## Python 3.6

#### Mac

    $ brew install -v python3

#### Ubuntu

    $ sudo apt install python3.6 python3.6-dev python3.6-venv



## Postgresql 10.0

#### Mac

    $ brew install -v postgresql
     
#### Ubuntu

Follow instructions on [https://www.postgresql.org/download/linux/ubuntu/](https://www.postgresql.org/download/linux/ubuntu/)

#### Install PostgreSQL Extensions

Install [https://github.com/citusdata/cstore_fdw](https://github.com/citusdata/cstore_fdw) and [https://github.com/citusdata/postgresql-hll](https://github.com/citusdata/postgresql-hll) from source.

#### Configuration

To get the best performance, update your [postgresql.conf](postgresql.conf).

#### Create Postgres User

    $ psql postgres

    CREATE ROLE mloetzsch SUPERUSER LOGIN;



## Java

#### Mac

Download and install Java SE Development Kit 8 from: http://www.oracle.com/technetwork/java/javase/downloads/index.html

#### Ubuntu

Download and install Java SE Development Kit 8 as described here: https://wiki.ubuntuusers.de/Java/Installation/Oracle_Java/Java_8/

## (Zed only )Php 5.6

#### Mac 

    $ brew tap homebrew/homebrew-php
    $ brew update

    $ brew install -v php56 --with-homebrew-apxs --with-postgresql --with-apache
    $ brew install -v php56-memcache
    $ brew install -v php56-memcached
    $ brew install -v php56-redis
    $ brew install -v php56-xdebug
    $ brew install -v php56-intl

#### Ubuntu

    $ sudo add-apt-repository -y ppa:ondrej/php
    $ sudo apt update
    $ sudo apt install php5.6 php5.6-curl php5.6-intl php5.6-memcache php5.6-memcached php5.6-mysql php5.6-xml php5.6-pgsql php5.6-xdebug libapache2-mod-php5.6 php5.6-soap php5.6-mbstring


#### Configuration

Update [php.ini](php.ini).


## (Zed only) MariaDB 10

#### Mac

    $ brew install -v mariadb

#### Ubuntu

    $ sudo apt install mariadb-server
    
#### Configuration 
    
Update [my.cnf](my.cnf)

 
#### Create database user 

    $ mysql -u root

    CREATE USER mloetzsch@localhost;
    GRANT ALL PRIVILEGES ON *.* TO mloetzsch@localhost;



## (Zed only) Apache 2

#### Mac

    $ brew install -v httpd24


#### Ubuntu

    $ sudo apt install apache2 libapache2-mod-php5.6



## (Zed only) DNSMasq

#### Mac

    $ brew install dnsmasq

#### Ubuntu
    
    $ sudo apt install dnsmasq
    
#### Configuration

    $ echo "address=/localhost/127.0.0.1" | sudo tee /etc/dnsmasq.conf
    $ echo "8.8.8.8" | sudo tee /etc/resolvconf/resolv.conf.d/base
    $ systemctl restart dnsmasq

add DNS server 127.0.0.1 to network connection System Preferences

add alternative DNS (eg. 8.8.8.8 and 4.4.4.4 after 127.0.0.1)



## (Zed only) NodeJS and Grunt

#### Mac 

    $ brew install odejs npm
    $ npm install -g grunt-cli

#### Ubuntu

    # nodejs-legacy installs /usr/bin/node
    # the nodejs packages only has /usr/bin/nodejs
    $ sudo apt install nodejs-legacy npm

On ubuntu 17.10 it's 

    $ sudo apt install nodejs npm

Install the grunt-cli package

    $ npm install -g grunt-cli




## SQSH

Only needed when SQL Server is used

#### Mac
    
    $ brew install homebrew/versions/freetds091 --with-sybase-compat --with-unixodbc
    
Then compile and install sqsh from [source](https://sourceforge.net/projects/sqsh/)
 
    $ LD_LIBRARY_PATH=/usr/local/opt/readline/lib:$LD_LIBRARY_PATH SYBASE=/usr/local/opt/freetds@0.91 ./configure

Apply [this patch](https://raw.githubusercontent.com/SharkBaitDLS/macports-ports/c28c2be448c2eff5631cc37f36d6760b13ca4b01/sysutils/sqsh/files/patch-cmd_connect.diff) and then
    
    $ make 
    $ make install
    
#### Ubuntu


    $ sudo apt install freetds (or freetds-bin on newer ubuntus) 
    # sqsh 2.5.16 because of a bug in handling quotes in strings in the ubuntu/debian version
    $ sudo add-apt-repository ppa:jasc/sqsh 
    $ sudo apt update
    $ sudo apt install sqsh

#### Configuration 
 
Add project specific connections to [freetds.conf](freetds.conf).
