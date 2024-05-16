# Etapes pour l'installation de Icinga 2
## Etape 1 : Préparation de la machine virtuelle Debian 12 en local
Configuration hardware de la machine sur VMware
- OS : Debian 12 (12.5)
- Config réseau : NAT
- RAM : 4 Go
- Espace disque : 50 Go 

## Etape 2  : Préparation des prérequis (Apache; MariaDB)
### Faire la mise a jour de la liste des packages

```bash
[Input]

sudo apt update

[Output]

Hit:1 http://deb.debian.org/debian bookworm InRelease
Hit:2 http://deb.debian.org/debian bookworm-updates InRelease
Get:3 http://security.debian.org/debian-security bookworm-security InRelease [48.0 kB]
Fetched 48.0 kB in 1s (68.3 kB/s)
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
All packages are up to date.

```
### Installation d'Apache 2 (Output raccourci)
```bash
[Input]

sudo apt install apache2

[Output]

Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
The following additional packages will be installed:
  apache2-bin apache2-data apache2-utils libapr1 libaprutil1 libaprutil1-dbd-sqlite3
  libaprutil1-ldap libcurl4 liblua5.3-0 ssl-cert
Suggested packages:
  apache2-doc apache2-suexec-pristine | apache2-suexec-custom www-browser
The following NEW packages will be installed:
  apache2 apache2-bin apache2-data apache2-utils libapr1 libaprutil1 libaprutil1-dbd-sqlite3
  libaprutil1-ldap libcurl4 liblua5.3-0 ssl-cert
0 upgraded, 11 newly installed, 0 to remove and 0 not upgraded.
Need to get 2,717 kB of archives.
After this operation, 9,214 kB of additional disk space will be used.
Do you want to continue? [Y/n] y
Get:1 http://security.debian.org/debian-security bookworm-security/main amd64 apache2-bin amd64 2.4.59-1~deb12u1 [1,380 kB]
Get:2 http://deb.debian.org/debian bookworm/main amd64 libapr1 amd64 1.7.2-3 [102 kB]
Get:3 http://deb.debian.org/debian bookworm/main amd64 libaprutil1 amd64 1.6.3-1 [87.8 kB]
Get:4 http://deb.debian.org/debian bookworm/main amd64 libaprutil1-dbd-sqlite3 amd64 1.6.3-1 [13.6 kB]
Get:5 http://deb.debian.org/debian bookworm/main amd64 libaprutil1-ldap amd64 1.6.3-1 [11.8 kB]
Get:6 http://deb.debian.org/debian bookworm/main amd64 libcurl4 amd64 7.88.1-10+deb12u5 [390 kB]
[...]
Enabling conf localized-error-pages.
Enabling conf other-vhosts-access-log.
Enabling conf security.
Enabling conf serve-cgi-bin.
Enabling site 000-default.
Created symlink /etc/systemd/system/multi-user.target.wants/apache2.service → /lib/systemd/system/apache2.service.
Created symlink /etc/systemd/system/multi-user.target.wants/apache-htcacheclean.service → /lib/systemd/system/apache-htcacheclean.service.
Processing triggers for man-db (2.11.2-2) ...
Processing triggers for libc-bin (2.36-9+deb12u6) ...

```
### Vérifiaction du status d'Apache 2
```bash
[Input]

sudo systemctl status apache2

[Output]

● apache2.service - The Apache HTTP Server
     Loaded: loaded (/lib/systemd/system/apache2.service; enabled; preset: enabled)
     Active: active (running) since Tue 2024-04-30 11:13:22 CEST; 4min 14s ago
       Docs: https://httpd.apache.org/docs/2.4/
   Main PID: 1469 (apache2)
      Tasks: 55 (limit: 4603)
     Memory: 17.0M
        CPU: 185ms
     CGroup: /system.slice/apache2.service
             ├─1469 /usr/sbin/apache2 -k start
             ├─1470 /usr/sbin/apache2 -k start
             └─1471 /usr/sbin/apache2 -k start

Apr 30 11:13:22 MonSrv systemd[1]: Starting apache2.service - The Apache HTTP Server...
Apr 30 11:13:22 MonSrv apachectl[1468]: AH00558: apache2: Could not reliably determine the server's f>
Apr 30 11:13:22 MonSrv systemd[1]: Started apache2.service - The Apache HTTP Server.

```
## Installation de MariaDB
### Ajout MariaDB
```bash
[Input]

sudo apt install mariadb-server

[Output]

```

### Installation de MariaDB (Raccourcis)

```bash
[Input]

sudo apt install mariadb-server

[Output]

Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
The following additional packages will be installed:
  galera-4 gawk libcgi-fast-perl libcgi-pm-perl libclone-perl libconfig-inifiles-perl libdaxctl1 libdbd-mariadb-perl libdbi-perl libencode-locale-perl libfcgi-bin libfcgi-perl libfcgi0ldbl libgpm2
  libhtml-parser-perl libhtml-tagset-perl libhtml-template-perl libhttp-date-perl libhttp-message-perl libio-html-perl liblwp-mediatypes-perl liblzo2-2 libmariadb3 libmpfr6 libncurses6 libndctl6 libnuma1
  libpmem1 libregexp-ipv6-perl libsigsegv2 libsnappy1v5 libterm-readkey-perl libtimedate-perl liburi-perl liburing2 mariadb-client mariadb-client-core mariadb-common mariadb-plugin-provider-bzip2
  mariadb-plugin-provider-lz4 mariadb-plugin-provider-lzma mariadb-plugin-provider-lzo mariadb-plugin-provider-snappy mariadb-server-core mysql-common pv rsync socat
Suggested packages:
  gawk-doc libmldbm-perl libnet-daemon-perl libsql-statement-perl gpm libdata-dump-perl libipc-sharedcache-perl libbusiness-isbn-perl libwww-perl mailx mariadb-test netcat-openbsd doc-base
  python3-braceexpand
The following NEW packages will be installed:
  galera-4 gawk libcgi-fast-perl libcgi-pm-perl libclone-perl libconfig-inifiles-perl libdaxctl1 libdbd-mariadb-perl libdbi-perl libencode-locale-perl libfcgi-bin libfcgi-perl libfcgi0ldbl libgpm2
  libhtml-parser-perl libhtml-tagset-perl libhtml-template-perl libhttp-date-perl libhttp-message-perl libio-html-perl liblwp-mediatypes-perl liblzo2-2 libmariadb3 libmpfr6 libncurses6 libndctl6 libnuma1
  libpmem1 libregexp-ipv6-perl libsigsegv2 libsnappy1v5 libterm-readkey-perl libtimedate-perl liburi-perl liburing2 mariadb-client mariadb-client-core mariadb-common mariadb-plugin-provider-bzip2
  mariadb-plugin-provider-lz4 mariadb-plugin-provider-lzma mariadb-plugin-provider-lzo mariadb-plugin-provider-snappy mariadb-server mariadb-server-core mysql-common pv rsync socat
0 upgraded, 49 newly installed, 0 to remove and 0 not upgraded.
[...]
Setting up socat (1.7.4.4-2) ...
Setting up libncurses6:amd64 (6.4-4) ...
Setting up libio-html-perl (1.004-3) ...
Setting up libmariadb3:amd64 (1:10.11.6-0+deb12u1) ...
Setting up libdaxctl1:amd64 (76.1-1) ...
Setting up libtimedate-perl (2.3300-2) ...
Setting up libregexp-ipv6-perl (0.03-3) ...
Setting up libnuma1:amd64 (2.0.16-1) ...
Setting up pv (1.6.20-1) ...
Setting up libndctl6:amd64 (76.1-1) ...
Setting up libfcgi-perl (0.82+ds-2) ...
Setting up libterm-readkey-perl (2.38-2+b1) ...
Setting up liburing2:amd64 (2.3-3) ...
Setting up libpmem1:amd64 (1.12.1-2) ...
Setting up liburi-perl (5.17-1) ...
Setting up libdbi-perl:amd64 (1.643-4) ...
Setting up rsync (3.2.7-1) ...
rsync.service is a disabled or a static unit, not starting it.
Setting up libhttp-date-perl (6.05-2) ...
Setting up mariadb-client-core (1:10.11.6-0+deb12u1) ...
Setting up libdbd-mariadb-perl (1.22-1+b1) ...
Setting up libhtml-parser-perl:amd64 (3.81-1) ...
Setting up mariadb-server-core (1:10.11.6-0+deb12u1) ...
Setting up libhttp-message-perl (6.44-1) ...
Setting up mariadb-client (1:10.11.6-0+deb12u1) ...
Setting up libcgi-pm-perl (4.55-1) ...
Setting up libhtml-template-perl (2.97-2) ...
Setting up mariadb-server (1:10.11.6-0+deb12u1) ...
Created symlink /etc/systemd/system/multi-user.target.wants/mariadb.service → /lib/systemd/system/mariadb.service.
Setting up mariadb-plugin-provider-bzip2 (1:10.11.6-0+deb12u1) ...
Setting up mariadb-plugin-provider-lzma (1:10.11.6-0+deb12u1) ...
Setting up mariadb-plugin-provider-lzo (1:10.11.6-0+deb12u1) ...
Setting up mariadb-plugin-provider-lz4 (1:10.11.6-0+deb12u1) ...
Setting up libcgi-fast-perl (1:2.15-1) ...
Setting up mariadb-plugin-provider-snappy (1:10.11.6-0+deb12u1) ...
Processing triggers for man-db (2.11.2-2) ...
Processing triggers for libc-bin (2.36-9+deb12u7) ...
Processing triggers for mariadb-server (1:10.11.6-0+deb12u1) ...

```

### Installation Secure MariaDB

```bash
[Input]

sudo mysql_secure_installation

[Output]


NOTE: RUNNING ALL PARTS OF THIS SCRIPT IS RECOMMENDED FOR ALL MariaDB
      SERVERS IN PRODUCTION USE!  PLEASE READ EACH STEP CAREFULLY!

In order to log into MariaDB to secure it, we'll need the current
password for the root user. If you've just installed MariaDB, and
haven't set the root password yet, you should just press enter here.

Enter current password for root (enter for none):
OK, successfully used password, moving on...

Setting the root password or using the unix_socket ensures that nobody
can log into the MariaDB root user without the proper authorisation.

You already have your root account protected, so you can safely answer 'n'.

Switch to unix_socket authentication [Y/n] n
 ... skipping.

You already have your root account protected, so you can safely answer 'n'.

Change the root password? [Y/n] y
New password:
Re-enter new password:
Password updated successfully!
Reloading privilege tables..
 ... Success!


By default, a MariaDB installation has an anonymous user, allowing anyone
to log into MariaDB without having to have a user account created for
them.  This is intended only for testing, and to make the installation
go a bit smoother.  You should remove them before moving into a
production environment.

Remove anonymous users? [Y/n] y
 ... Success!

Normally, root should only be allowed to connect from 'localhost'.  This
ensures that someone cannot guess at the root password from the network.

Disallow root login remotely? [Y/n] y
 ... Success!

By default, MariaDB comes with a database named 'test' that anyone can
access.  This is also intended only for testing, and should be removed
before moving into a production environment.

Remove test database and access to it? [Y/n] y
 - Dropping test database...
 ... Success!
 - Removing privileges on test database...
 ... Success!

Reloading the privilege tables will ensure that all changes made so far
will take effect immediately.

Reload privilege tables now? [Y/n] y
 ... Success!

Cleaning up...

All done!  If you've completed all of the above steps, your MariaDB
installation should now be secure.

Thanks for using MariaDB!

```
### Vérification de l'installation de MariaDB

```bash
[Input]

mysql --version

[Output]

mysql  Ver 15.1 Distrib 10.11.6-MariaDB, for debian-linux-gnu (x86_64) using  EditLine wrapper

```
### Vérification du status de MariaDB

```bash
[Input]

sudo systemctl status mariadb

[Output]

● mariadb.service - MariaDB 10.11.6 database server
     Loaded: loaded (/lib/systemd/system/mariadb.service; enabled; preset: enabled)
     Active: active (running) since Tue 2024-04-30 11:44:59 CEST; 3min 50s ago
       Docs: man:mariadbd(8)
             https://mariadb.com/kb/en/library/systemd/
   Main PID: 1821 (mariadbd)
     Status: "Taking your SQL requests now..."
      Tasks: 9 (limit: 4603)
     Memory: 186.1M
        CPU: 826ms
     CGroup: /system.slice/mariadb.service
             └─1821 /usr/sbin/mariadbd

Apr 30 11:44:59 MonSrv mariadbd[1821]: 2024-04-30 11:44:59 0 [Note] InnoDB: log sequence number 45614>
Apr 30 11:44:59 MonSrv mariadbd[1821]: 2024-04-30 11:44:59 0 [Note] InnoDB: Loading buffer pool(s) fr>
Apr 30 11:44:59 MonSrv mariadbd[1821]: 2024-04-30 11:44:59 0 [Note] Plugin 'FEEDBACK' is disabled.
Apr 30 11:44:59 MonSrv mariadbd[1821]: 2024-04-30 11:44:59 0 [Warning] You need to use --log-bin to m>
Apr 30 11:44:59 MonSrv mariadbd[1821]: 2024-04-30 11:44:59 0 [Note] Server socket created on IP: '127>
Apr 30 11:44:59 MonSrv mariadbd[1821]: 2024-04-30 11:44:59 0 [Note] InnoDB: Buffer pool(s) load compl>
Apr 30 11:44:59 MonSrv mariadbd[1821]: 2024-04-30 11:44:59 0 [Note] /usr/sbin/mariadbd: ready for con>
Apr 30 11:44:59 MonSrv mariadbd[1821]: Version: '10.11.6-MariaDB-0+deb12u1'  socket: '/run/mysqld/mys>
Apr 30 11:44:59 MonSrv systemd[1]: Started mariadb.service - MariaDB 10.11.6 database server.
Apr 30 11:44:59 MonSrv /etc/mysql/debian-start[1837]: Upgrading MySQL tables if necessary.

```

### Installation de PHP (Output Raccourcis)
```bash
[Input]

sudo apt intall php

[Output]

Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
The following additional packages will be installed:
  apache2 apache2-bin apache2-data apache2-utils libapache2-mod-php8.2 libapr1 libaprutil1 libaprutil1-dbd-sqlite3 libaprutil1-ldap libcurl4 liblua5.3-0 libsodium23 php-common php8.2 php8.2-cli php8.2-common
  php8.2-opcache php8.2-readline psmisc ssl-cert
Suggested packages:
  apache2-doc apache2-suexec-pristine | apache2-suexec-custom www-browser php-pear
The following NEW packages will be installed:
  apache2 apache2-bin apache2-data apache2-utils libapache2-mod-php8.2 libapr1 libaprutil1 libaprutil1-dbd-sqlite3 libaprutil1-ldap libcurl4 liblua5.3-0 libsodium23 php php-common php8.2 php8.2-cli
  php8.2-common php8.2-opcache php8.2-readline psmisc ssl-cert
0 upgraded, 21 newly installed, 0 to remove and 0 not upgraded.
Need to get 7,634 kB of archives.
After this operation, 31.8 MB of additional disk space will be used.
Do you want to continue? [Y/n] y
Get:1 http://deb.debian.org/debian bookworm/main amd64 libapr1 amd64 1.7.2-3 [102 kB]
Get:2 http://deb.debian.org/debian bookworm/main amd64 libaprutil1 amd64 1.6.3-1 [87.8 kB]
Get:3 http://deb.debian.org/debian bookworm/main amd64 libaprutil1-dbd-sqlite3 amd64 1.6.3-1 [13.6 kB]
Get:4 http://deb.debian.org/debian bookworm/main amd64 libaprutil1-ldap amd64 1.6.3-1 [11.8 kB]
Get:5 http://deb.debian.org/debian bookworm/main amd64 libcurl4 amd64 7.88.1-10+deb12u5 [390 kB]
Get:6 http://deb.debian.org/debian bookworm/main amd64 liblua5.3-0 amd64 5.3.6-2 [123 kB]
Get:7 http://security.debian.org/debian-security bookworm-security/main amd64 apache2-bin amd64 2.4.59-1~deb12u1 [1,380 kB]
Get:8 http://deb.debian.org/debian bookworm/main amd64 psmisc amd64 23.6-1 [259 kB]
Fetched 7,634 kB in 3s (2,573 kB/s)
Preconfiguring packages ...
Selecting previously unselected package libapr1:amd64.
(Reading database ... 33660 files and directories currently installed.)
Preparing to unpack .../00-libapr1_1.7.2-3_amd64.deb ...
Unpacking libapr1:amd64 (1.7.2-3) ...
Selecting previously unselected package libaprutil1:amd64.
Preparing to unpack .../01-libaprutil1_1.6.3-1_amd64.deb ...
Unpacking libaprutil1:amd64 (1.6.3-1) ...
Selecting previously unselected package libaprutil1-dbd-sqlite3:amd64.
Preparing to unpack .../02-libaprutil1-dbd-sqlite3_1.6.3-1_amd64.deb ...
Unpacking libaprutil1-dbd-sqlite3:amd64 (1.6.3-1) ...
Selecting previously unselected package libaprutil1-ldap:amd64.
[...]
Enabling module autoindex.
Enabling module env.
Enabling module mime.
Enabling module negotiation.
Enabling module setenvif.
Enabling module filter.
Enabling module deflate.
Enabling module status.
Enabling module reqtimeout.
Enabling conf charset.
Enabling conf localized-error-pages.
Enabling conf other-vhosts-access-log.
Enabling conf security.
Enabling conf serve-cgi-bin.
Enabling site 000-default.
info: Switch to mpm prefork for package libapache2-mod-php8.2
Module mpm_event disabled.
Enabling module mpm_prefork.
info: Executing deferred 'a2enmod php8.2' for package libapache2-mod-php8.2
Enabling module php8.2.
Created symlink /etc/systemd/system/multi-user.target.wants/apache2.service → /lib/systemd/system/apache2.service.
Created symlink /etc/systemd/system/multi-user.target.wants/apache-htcacheclean.service → /lib/systemd/system/apache-htcacheclean.service.
Setting up php8.2 (8.2.18-1~deb12u1) ...
Setting up php (2:8.2+93) ...
Processing triggers for man-db (2.11.2-2) ...
Processing triggers for libc-bin (2.36-9+deb12u7) ...
Processing triggers for php8.2-cli (8.2.18-1~deb12u1) ...
Processing triggers for libapache2-mod-php8.2 (8.2.18-1~deb12u1) ...
```

### Installation des modules PHP (Output raccourcis)
```bash
[Input]

sudo apt install php-gd php-mbstring php-mysqlnd php-curl php-xml php-cli php-soap php-intl php-xmlrpc php-zip  php-common php-opcache php-gmp php-imagick php-pgsql -y

[Output]

Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
Note, selecting 'php8.2-mysql' instead of 'php-mysqlnd'
Note, selecting 'php8.2-opcache' instead of 'php-opcache'
php-common is already the newest version (2:93).
php-common set to manually installed.
php8.2-opcache is already the newest version (8.2.18-1~deb12u1).
php8.2-opcache set to manually installed.
The following additional packages will be installed:
  fontconfig-config fonts-dejavu-core fonts-droid-fallback fonts-noto-mono fonts-urw-base35 ghostscript gsfonts imagemagick-6-common libabsl20220623 libaom3 libavahi-client3 libavahi-common-data
  libavahi-common3 libavif15 libcups2 libdav1d6 libde265-0 libdeflate0 libfftw3-double3 libfontconfig1 libfontenc1 libgav1-1 libgd3 libgomp1 libgs-common libgs10 libgs10-common libheif1 libice6 libidn12
  libijs-0.35 libjbig0 libjbig2dec0 libjpeg62-turbo liblcms2-2 liblerc4 liblqr-1-0 libltdl7 libmagickcore-6.q16-6 libmagickwand-6.q16-6 libonig5 libopenjp2-7 libpaper-utils libpaper1 libpq5 librav1e0 libsm6
  libsvtav1enc1 libtiff6 libwebp7 libwebpdemux2 libwebpmux3 libx265-199 libxmlrpc-epi0 libxpm4 libxt6 libyuv0 libzip4 php8.2-curl php8.2-gd php8.2-gmp php8.2-imagick php8.2-intl php8.2-mbstring php8.2-pgsql
  php8.2-soap php8.2-xml php8.2-xmlrpc php8.2-zip poppler-data x11-common xfonts-encodings xfonts-utils
Suggested packages:
  fonts-noto fonts-freefont-otf | fonts-freefont-ttf fonts-texgyre cups-common libfftw3-bin libfftw3-dev libgd-tools liblcms2-utils libmagickcore-6.q16-6-extra poppler-utils fonts-japanese-mincho
  | fonts-ipafont-mincho fonts-japanese-gothic | fonts-ipafont-gothic fonts-arphic-ukai fonts-arphic-uming fonts-nanum
The following NEW packages will be installed:
  fontconfig-config fonts-dejavu-core fonts-droid-fallback fonts-noto-mono fonts-urw-base35 ghostscript gsfonts imagemagick-6-common libabsl20220623 libaom3 libavahi-client3 libavahi-common-data
  libavahi-common3 libavif15 libcups2 libdav1d6 libde265-0 libdeflate0 libfftw3-double3 libfontconfig1 libfontenc1 libgav1-1 libgd3 libgomp1 libgs-common libgs10 libgs10-common libheif1 libice6 libidn12
  libijs-0.35 libjbig0 libjbig2dec0 libjpeg62-turbo liblcms2-2 liblerc4 liblqr-1-0 libltdl7 libmagickcore-6.q16-6 libmagickwand-6.q16-6 libonig5 libopenjp2-7 libpaper-utils libpaper1 libpq5 librav1e0 libsm6
  libsvtav1enc1 libtiff6 libwebp7 libwebpdemux2 libwebpmux3 libx265-199 libxmlrpc-epi0 libxpm4 libxt6 libyuv0 libzip4 php-cli php-curl php-gd php-gmp php-imagick php-intl php-mbstring php-pgsql php-soap
  php-xml php-xmlrpc php-zip php8.2-curl php8.2-gd php8.2-gmp php8.2-imagick php8.2-intl php8.2-mbstring php8.2-mysql php8.2-pgsql php8.2-soap php8.2-xml php8.2-xmlrpc php8.2-zip poppler-data x11-common
  xfonts-encodings xfonts-utils
0 upgraded, 86 newly installed, 0 to remove and 0 not upgraded.
Need to get 36.5 MB of archives.
After this operation, 134 MB of additional disk space will be used.
Get:1 http://security.debian.org/debian-security bookworm-security/main amd64 libdav1d6 amd64 1.0.0-2+deb12u1 [513 kB]
Get:2 http://security.debian.org/debian-security bookworm-security/main amd64 imagemagick-6-common all 8:6.9.11.60+dfsg-1.6+deb12u1 [166 kB]
Get:3 http://deb.debian.org/debian bookworm/main amd64 fonts-droid-fallback all 1:6.0.1r16-1.1 [1,807 kB]
Get:4 http://deb.debian.org/debian bookworm/main amd64 libgomp1 amd64 12.2.0-14 [116 kB]
Get:5 http://deb.debian.org/debian bookworm/main amd64 libfftw3-double3 amd64 3.3.10-1 [776 kB]
Get:6 http://security.debian.org/debian-security bookworm-security/main amd64 libmagickcore-6.q16-6 amd64 8:6.9.11.60+dfsg-1.6+deb12u1 [1,785 kB]
Get:7 http://security.debian.org/debian-security bookworm-security/main amd64 libmagickwand-6.q16-6 amd64 8:6.9.11.60+dfsg-1.6+deb12u1 [408 kB]
Get:8 http://security.debian.org/debian-security bookworm-security/main amd64 libpq5 amd64 15.6-0+deb12u1 [188 kB]
Get:9 http://security.debian.org/debian-security bookworm-security/main amd64 php8.2-curl amd64 8.2.18-1~deb12u1 [35.8 kB]
Get:10 http://deb.debian.org/debian bookworm/main amd64 fonts-dejavu-core all 2.37-6 [1,068 kB]
Get:11 http://security.debian.org/debian-security bookworm-security/main amd64 php8.2-gd amd64 8.2.18-1~deb12u1 [28.8 kB]
Get:12 http://security.debian.org/debian-security bookworm-security/main amd64 php8.2-gmp amd64 8.2.18-1~deb12u1 [21.9 kB]
Get:13 http://deb.debian.org/debian bookworm/main amd64 libfontenc1 amd64 1:1.1.4-1 [24.3 kB]
Get:14 http://security.debian.org/debian-security bookworm-security/main amd64 php8.2-intl amd64 8.2.18-1~deb12u1 [138 kB]
Get:15 http://deb.debian.org/debian bookworm/main amd64 x11-common all 1:7.7+23 [252 kB]
Get:16 http://security.debian.org/debian-security bookworm-security/main amd64 php8.2-mbstring amd64 8.2.18-1~deb12u1 [444 kB]
Get:17 http://security.debian.org/debian-security bookworm-security/main amd64 php8.2-pgsql amd64 8.2.18-1~deb12u1 [57.7 kB]
Get:18 http://security.debian.org/debian-security bookworm-security/main amd64 php8.2-soap amd64 8.2.18-1~deb12u1 [124 kB]
Get:19 http://security.debian.org/debian-security bookworm-security/main amd64 php8.2-xml amd64 8.2.18-1~deb12u1 [112 kB]
Get:20 http://deb.debian.org/debian bookworm/main amd64 xfonts-encodings all 1:1.0.4-2.2 [577 kB]
Get:21 http://security.debian.org/debian-security bookworm-security/main amd64 php8.2-zip amd64 8.2.18-1~deb12u1 [26.2 kB]
Get:22 http://deb.debian.org/debian bookworm/main amd64 xfonts-utils amd64 1:7.7+6 [93.0 kB]
Get:23 http://security.debian.org/debian-security bookworm-security/main amd64 php8.2-mysql amd64 8.2.18-1~deb12u1 [117 kB]
[...]
Preparing to unpack .../76-php-mbstring_2%3a8.2+93_all.deb ...
Unpacking php-mbstring (2:8.2+93) ...
Selecting previously unselected package php8.2-pgsql.
Preparing to unpack .../77-php8.2-pgsql_8.2.18-1~deb12u1_amd64.deb ...
Unpacking php8.2-pgsql (8.2.18-1~deb12u1) ...
Selecting previously unselected package php-pgsql.
Preparing to unpack .../78-php-pgsql_2%3a8.2+93_all.deb ...
Unpacking php-pgsql (2:8.2+93) ...
Selecting previously unselected package php8.2-soap.
Preparing to unpack .../79-php8.2-soap_8.2.18-1~deb12u1_amd64.deb ...
Unpacking php8.2-soap (8.2.18-1~deb12u1) ...
Selecting previously unselected package php-soap.
Preparing to unpack .../80-php-soap_2%3a8.2+93_all.deb ...
Unpacking php-soap (2:8.2+93) ...
Selecting previously unselected package php8.2-xml.
Preparing to unpack .../81-php8.2-xml_8.2.18-1~deb12u1_amd64.deb ...
Unpacking php8.2-xml (8.2.18-1~deb12u1) ...
Selecting previously unselected package php-xml.
Preparing to unpack .../82-php-xml_2%3a8.2+93_all.deb ...
Unpacking php-xml (2:8.2+93) ...
Selecting previously unselected package php8.2-zip.
Preparing to unpack .../83-php8.2-zip_8.2.18-1~deb12u1_amd64.deb ...
Unpacking php8.2-zip (8.2.18-1~deb12u1) ...
Selecting previously unselected package php-zip.
Preparing to unpack .../84-php-zip_2%3a8.2+93_all.deb ...
Unpacking php-zip (2:8.2+93) ...
Selecting previously unselected package php8.2-mysql.
Preparing to unpack .../85-php8.2-mysql_8.2.18-1~deb12u1_amd64.deb ...
Unpacking php8.2-mysql (8.2.18-1~deb12u1) ...
Setting up liblcms2-2:amd64 (2.14-2) ...
Setting up libpaper1:amd64 (1.1.29) ...

Creating config file /etc/papersize with new version
Setting up libaom3:amd64 (3.6.0-1) ...
Setting up libabsl20220623:amd64 (20220623.1-1) ...
Setting up imagemagick-6-common (8:6.9.11.60+dfsg-1.6+deb12u1) ...
Setting up php8.2-mysql (8.2.18-1~deb12u1) ...

Creating config file /etc/php/8.2/mods-available/mysqlnd.ini with new version

Creating config file /etc/php/8.2/mods-available/mysqli.ini with new version

Creating config file /etc/php/8.2/mods-available/pdo_mysql.ini with new version
Setting up liblerc4:amd64 (4.0.0+ds-2) ...
Setting up fonts-noto-mono (20201225-1) ...
Setting up libxpm4:amd64 (1:3.5.12-1.1+deb12u1) ...
Setting up libzip4:amd64 (1.7.3-1+b1) ...
Setting up libijs-0.35:amd64 (0.35-15) ...
Setting up libxmlrpc-epi0:amd64 (0.54.2-1.3+b1) ...
Setting up libgs-common (10.0.0~dfsg-11+deb12u3) ...
Setting up x11-common (1:7.7+23) ...
Setting up libpq5:amd64 (15.6-0+deb12u1) ...
Setting up libdeflate0:amd64 (1.14-1) ...
Setting up libpaper-utils (1.1.29) ...
Setting up libsvtav1enc1:amd64 (1.4.1+dfsg-1) ...
Setting up libgomp1:amd64 (12.2.0-14) ...
Setting up libjbig0:amd64 (2.1-6.1) ...
Setting up php8.2-intl (8.2.18-1~deb12u1) ...

Creating config file /etc/php/8.2/mods-available/intl.ini with new version
Setting up librav1e0:amd64 (0.5.1-6) ...
Setting up poppler-data (0.4.12-1) ...
Setting up php-intl (2:8.2+93) ...
Setting up libfontenc1:amd64 (1:1.1.4-1) ...
Setting up php8.2-curl (8.2.18-1~deb12u1) ...

Creating config file /etc/php/8.2/mods-available/curl.ini with new version
Setting up libjpeg62-turbo:amd64 (1:2.1.5-2) ...
Setting up php8.2-xmlrpc (3:1.0.0~rc3-6) ...
Setting up libjbig2dec0:amd64 (0.19-3) ...
Setting up php8.2-xml (8.2.18-1~deb12u1) ...

Creating config file /etc/php/8.2/mods-available/dom.ini with new version

Creating config file /etc/php/8.2/mods-available/simplexml.ini with new version

Creating config file /etc/php/8.2/mods-available/xml.ini with new version

Creating config file /etc/php/8.2/mods-available/xmlreader.ini with new version

Creating config file /etc/php/8.2/mods-available/xmlwriter.ini with new version

Creating config file /etc/php/8.2/mods-available/xsl.ini with new version
Setting up libavahi-common-data:amd64 (0.8-10) ...
Setting up xfonts-encodings (1:1.0.4-2.2) ...
Setting up libidn12:amd64 (1.41-1) ...
Setting up fonts-dejavu-core (2.37-6) ...
Setting up libgav1-1:amd64 (0.18.0-1+b1) ...
Setting up php-xmlrpc (3:1.0.0~rc3-6) ...
Setting up libdav1d6:amd64 (1.0.0-2+deb12u1) ...
Setting up libltdl7:amd64 (2.4.7-5) ...
Setting up libfftw3-double3:amd64 (3.3.10-1) ...
Setting up libx265-199:amd64 (3.5-2+b1) ...
Setting up libwebp7:amd64 (1.2.4-0.2+deb12u1) ...
Setting up php-cli (2:8.2+93) ...
update-alternatives: using /usr/bin/php.default to provide /usr/bin/php (php) in auto mode
update-alternatives: using /usr/bin/phar.default to provide /usr/bin/phar (phar) in auto mode
update-alternatives: using /usr/bin/phar.phar.default to provide /usr/bin/phar.phar (phar.phar) in auto mode
Setting up liblqr-1-0:amd64 (0.4.2-2.1) ...
Setting up libtiff6:amd64 (4.5.0-6+deb12u1) ...
Setting up php8.2-gmp (8.2.18-1~deb12u1) ...

Creating config file /etc/php/8.2/mods-available/gmp.ini with new version
Setting up libopenjp2-7:amd64 (2.5.0-2) ...
Setting up fonts-droid-fallback (1:6.0.1r16-1.1) ...
Setting up libde265-0:amd64 (1.0.11-1+deb12u2) ...
Setting up libwebpmux3:amd64 (1.2.4-0.2+deb12u1) ...
Setting up php8.2-soap (8.2.18-1~deb12u1) ...

Creating config file /etc/php/8.2/mods-available/soap.ini with new version
Setting up libyuv0:amd64 (0.0~git20230123.b2528b0-1) ...
Setting up libonig5:amd64 (6.9.8-1) ...
Setting up php-xml (2:8.2+93) ...
Setting up libice6:amd64 (2:1.0.10-1) ...
Setting up php-curl (2:8.2+93) ...
Setting up php8.2-pgsql (8.2.18-1~deb12u1) ...

Creating config file /etc/php/8.2/mods-available/pgsql.ini with new version

Creating config file /etc/php/8.2/mods-available/pdo_pgsql.ini with new version
Setting up libavif15:amd64 (0.11.1-1) ...
Setting up php8.2-zip (8.2.18-1~deb12u1) ...

Creating config file /etc/php/8.2/mods-available/zip.ini with new version
Setting up fontconfig-config (2.14.1-4) ...
Setting up libwebpdemux2:amd64 (1.2.4-0.2+deb12u1) ...
Setting up php8.2-mbstring (8.2.18-1~deb12u1) ...

Creating config file /etc/php/8.2/mods-available/mbstring.ini with new version
Setting up libheif1:amd64 (1.15.1-1) ...
Setting up libavahi-common3:amd64 (0.8-10) ...
Setting up php-soap (2:8.2+93) ...
Setting up xfonts-utils (1:7.7+6) ...
Setting up php-mbstring (2:8.2+93) ...
Setting up php-pgsql (2:8.2+93) ...
Setting up php-gmp (2:8.2+93) ...
Setting up php-zip (2:8.2+93) ...
Setting up libfontconfig1:amd64 (2.14.1-4) ...
Setting up libsm6:amd64 (2:1.2.3-1) ...
Setting up libavahi-client3:amd64 (0.8-10) ...
Setting up fonts-urw-base35 (20200910-7) ...
Setting up libmagickcore-6.q16-6:amd64 (8:6.9.11.60+dfsg-1.6+deb12u1) ...
Setting up gsfonts (2:20200910-7) ...
Setting up libgd3:amd64 (2.3.3-9) ...
Setting up libxt6:amd64 (1:1.2.1-1.1) ...
Setting up libcups2:amd64 (2.4.2-3+deb12u5) ...
Setting up libmagickwand-6.q16-6:amd64 (8:6.9.11.60+dfsg-1.6+deb12u1) ...
Setting up php8.2-gd (8.2.18-1~deb12u1) ...

Creating config file /etc/php/8.2/mods-available/gd.ini with new version
Setting up php-gd (2:8.2+93) ...
Setting up libgs10-common (10.0.0~dfsg-11+deb12u3) ...
Setting up php8.2-imagick (3.7.0-4) ...
Setting up php-imagick (3.7.0-4) ...
Setting up libgs10:amd64 (10.0.0~dfsg-11+deb12u3) ...
Setting up ghostscript (10.0.0~dfsg-11+deb12u3) ...
Processing triggers for libapache2-mod-php8.2 (8.2.18-1~deb12u1) ...
Processing triggers for libc-bin (2.36-9+deb12u7) ...
Processing triggers for man-db (2.11.2-2) ...
Processing triggers for php8.2-cli (8.2.18-1~deb12u1) ...

```
### Edition du fichier php.ini
```bash 
[Input]
sudo nano /etc/php/8.2/apache2/php.ini

[Öutput]
//Ces changement ont été effectuer dans le fichier
memory_limit = 256M 
post_max_size = 64M
upload_max_filesize = 100M	
max_execution_time = 300
default_charset = "UTF-8"
date.timezone = "Europe/Zurich"
cgi.fix_pathinfo=0
```
### Restart Apache2
```bash
[Input]

sudo systemctl restart apache2

```


## Etape 3 Installation d'Icinga 2

## Création de deux scritps
### Utilisation des repositories officiel d'icinga 2 pour Debian 
```bash
[Input]

apt update
apt -y install apt-transport-https wget gnupg

wget -O - https://packages.icinga.com/icinga.key | gpg --dearmor -o /usr/share/keyrings/icinga-archive-keyring.gpg

DIST=$(awk -F"[)(]+" '/VERSION=/ {print $2}' /etc/os-release); \
 echo "deb [signed-by=/usr/share/keyrings/icinga-archive-keyring.gpg] https://packages.icinga.com/debian icinga-${DIST} main" > \
 /etc/apt/sources.list.d/${DIST}-icinga.list
 echo "deb-src [signed-by=/usr/share/keyrings/icinga-archive-keyring.gpg] https://packages.icinga.com/debian icinga-${DIST} main" >> \
 /etc/apt/sources.list.d/${DIST}-icinga.list

apt update

[Output]

```
### Debian Backports Repository
Debian Stretch

```bash
[Input]

DIST=$(awk -F"[)(]+" '/VERSION=/ {print $2}' /etc/os-release); \
 echo "deb https://deb.debian.org/debian ${DIST}-backports main" > \
 /etc/apt/sources.list.d/${DIST}-backports.list

apt update

[Output]

```

### Installation de Icinga 2 (Output raccourcis)

```bash
[Input]

apt install icinga2

[Output]

Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
The following additional packages will be installed:
  icinga2-bin icinga2-common icinga2-doc libboost-context1.74.0 libboost-coroutine1.74.0
  libboost-filesystem1.74.0 libboost-iostreams1.74.0 libboost-program-options1.74.0
  libboost-regex1.74.0 libboost-thread1.74.0 monitoring-plugins-basic monitoring-plugins-common
Suggested packages:
  vim-icinga2
The following NEW packages will be installed:
  icinga2 icinga2-bin icinga2-common icinga2-doc libboost-context1.74.0 libboost-coroutine1.74.0
  libboost-filesystem1.74.0 libboost-iostreams1.74.0 libboost-program-options1.74.0
  libboost-regex1.74.0 libboost-thread1.74.0 monitoring-plugins-basic monitoring-plugins-common
0 upgraded, 13 newly installed, 0 to remove and 13 not upgraded.
Need to get 13.1 MB of archives.
After this operation, 45.9 MB of additional disk space will be used.
Do you want to continue? [Y/n] y
Get:1 http://deb.debian.org/debian bookworm/main amd64 libboost-context1.74.0 amd64 1.74.0+ds1-21 [219 kB]
Get:2 http://deb.debian.org/debian bookworm/main amd64 libboost-thread1.74.0 amd64 1.74.0+ds1-21 [257 kB]
Get:3 https://packages.icinga.com/debian icinga-bookworm/main amd64 icinga2-common all 2.14.2-1+debian12 [171 kB]
Get:4 http://deb.debian.org/debian bookworm/main amd64 libboost-coroutine1.74.0 amd64 1.74.0+ds1-21 [234 kB]
Get:5 http://deb.debian.org/debian bookworm/main amd64 libboost-filesystem1.74.0 amd64 1.74.0+ds1-21 [258 kB]
[...]
Setcap for check_icmp and check_dhcp worked!
Setting up libboost-coroutine1.74.0:amd64 (1.74.0+ds1-21) ...
Setting up icinga2-bin (2.14.2-1+debian12) ...
enabling default icinga2 features
Enabling feature checker. Make sure to restart Icinga 2 for these changes to take effect.
Enabling feature notification. Make sure to restart Icinga 2 for these changes to take effect.
Enabling feature mainlog. Make sure to restart Icinga 2 for these changes to take effect.
Setting up icinga2 (2.14.2-1+debian12) ...
Processing triggers for man-db (2.11.2-2) ...
Processing triggers for libc-bin (2.36-9+deb12u6) ...

```

### Installation des plugins de monitoring (raccourcis)

```bash
[Input]

apt install monitoring-plugins

[Output]

Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
The following additional packages will be installed:
  libarchive13 libavahi-client3 libavahi-common-data libavahi-common3 libcups2 libdbi1 libgpgme11
  libldb2 libnet-snmp-perl libpq5 libpython3.11 libradcli4 libsensors-config libsensors5
  libsmbclient libsnmp-base libsnmp40 libtalloc2 libtdb1 libtevent0 liburiparser1 libwbclient0
  monitoring-plugins-standard python3-gpg python3-ldb python3-samba python3-talloc python3-tdb
  rpcbind samba-common samba-common-bin samba-dsdb-modules samba-libs smbclient snmp
Suggested packages:
  lrzip cups-common libcrypt-des-perl libdigest-hmac-perl libio-socket-inet6-perl lm-sensors
  snmp-mibs-downloader nagios-plugins-contrib fping postfix | sendmail-bin | exim4-daemon-heavy
  | exim4-daemon-light qstat heimdal-clients python3-markdown python3-dnspython cifs-utils
The following NEW packages will be installed:
  libarchive13 libavahi-client3 libavahi-common-data libavahi-common3 libcups2 libdbi1 libgpgme11
  libldb2 libnet-snmp-perl libpq5 libpython3.11 libradcli4 libsensors-config libsensors5
  libsmbclient libsnmp-base libsnmp40 libtalloc2 libtdb1 libtevent0 liburiparser1 libwbclient0
  monitoring-plugins monitoring-plugins-standard python3-gpg python3-ldb python3-samba
  python3-talloc python3-tdb rpcbind samba-common samba-common-bin samba-dsdb-modules samba-libs
  smbclient snmp
0 upgraded, 36 newly installed, 0 to remove and 13 not upgraded.
Need to get 19.6 MB of archives.
After this operation, 81.6 MB of additional disk space will be used.
Do you want to continue? [Y/n] y
Get:1 http://security.debian.org/debian-security bookworm-security/main amd64 libpq5 amd64 15.6-0+deb12u1 [188 kB]
Get:2 http://deb.debian.org/debian bookworm/main amd64 rpcbind amd64 1.2.6-6+b1 [48.3 kB]
Get:3 http://deb.debian.org/debian bookworm/main amd64 libarchive13 amd64 3.6.2-1 [343 kB]
Get:4 http://deb.debian.org/debian bookworm/main amd64 libavahi-common-data amd64 0.8-10 [107 kB]
Get:5 http://deb.debian.org/debian bookworm/main amd64 libavahi-common3 amd64 0.8-10 [41.6 kB]
Get:6 http://deb.debian.org/debian bookworm/main amd64 libavahi-client3 amd64 0.8-10 [45.5 kB]
Get:7 http://deb.debian.org/debian bookworm/main amd64 libcups2 amd64 2.4.2-3+deb12u5 [245 kB]
Get:8 http://deb.debian.org/debian bookworm/main amd64 libdbi1 amd64 0.9.0-6 [28.9 kB]
Get:9 http://deb.debian.org/debian bookworm/main amd64 libgpgme11 amd64 1.18.0-3+b1 [300 kB]
[...]
Setting up snmp (5.9.3+dfsg-2) ...
Setting up libsmbclient:amd64 (2:4.17.12+dfsg-0+deb12u1) ...
Setting up smbclient (2:4.17.12+dfsg-0+deb12u1) ...
Setting up libcups2:amd64 (2.4.2-3+deb12u5) ...
Setting up samba-dsdb-modules:amd64 (2:4.17.12+dfsg-0+deb12u1) ...
Setting up python3-samba (2:4.17.12+dfsg-0+deb12u1) ...
Setting up samba-common-bin (2:4.17.12+dfsg-0+deb12u1) ...
Processing triggers for man-db (2.11.2-2) ...
Processing triggers for libc-bin (2.36-9+deb12u6) ...


```

### Activation de icinga2

```bash
[Input]

sudo systemctl start icinga2
sudo systemctl enable icinga2

[Output]

```
### Afficher le status d'Icinga2
```bash
[Input]
sudo systemctl status icinga2
[Output]

```

### Installation de Icinga2 IDO MySQl
```bash
[Input]

sudo apt install icinga2-ido-mysql -y

[Output]

Interface bleu apparait repondre "Yes" aux deux questions puis entrer un mot de passe pour connecter a la DB.

```
## Création d'un base de données pour IDO
### Connection a MariaDB
```bash
[Input]

sudo mysql -u root -p

[Output]

```
### Création de la DB (taper ligne par ligne dans mariadb)
```bash
[Input]

> CREATE DATABASE icinga_ido_db;
> GRANT ALL ON icinga_ido_db.* TO 'icinga_ido_user'@'localhost' IDENTIFIED BY 'Pa$$w0rd';
> FLUSH PRIVILEGES;
> EXIT;

[Output]

```

### Importation du schema de la DB IDO
```bash
[Input]

sudo mysql -u root -p icinga_ido_db < /usr/share/icinga2-ido-mysql/schema/mysql.sql

[Output]

```

### Edition du fichier de configuration d'IDO
```bash
[Input]

sudo nano /etc/icinga2/features-available/ido-mysql.conf

[Output]
# Verification que les information soient les bonnes (user,mdp,db) et modificiation s'il le faut

```

### Activer IDO

```bash
[Input]

sudo icinga2 feature enable ido-mysql

[Output]

```
### Restart Icinga2
```bash
[Input]

sudo systemctl restart icinga2

[Output]

```
## Installation de Icingaweb2
### Installation de Incingaweb2 et ingcinga cli en meme temps
```bash
[Input]

sudo apt install icingaweb2 icingacli -y

[Output]

```
## Création de la base de données pour icingaweb2
### Connetion a mariadb
```bash
[Input]

sudo mysql -u root -p

[Output]

```
### Création de la base de données
```bash
[Input]

> CREATE DATABASE icingaweb2;
> GRANT ALL ON icingaweb2.* TO 'icingaweb2user'@'localhost' IDENTIFIED BY 'Pa$$w0rd';
> FLUSH PRIVILEGES;
> EXIT;

[Output]

```
### Création d'un tokens pour la configuration avec l'interface web
```bash
[Input]

sudo icingacli setup token create

[Output]

```




