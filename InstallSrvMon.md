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
## Installation de MariaDB 11
### Ajout MariaDB Repositories
```bash
[Input]

sudo nano /etc/apt/sources.list.d/mariadb.sources

[Output]

```
### Lignes a ajouter dans le fichier créer précédement
```bash
[Input]

# MariaDB 11.1 repository list - created 2023-11-20 07:47 UTC
# https://mariadb.org/download/
X-Repolib-Name: MariaDB
Types: deb
# deb.mariadb.org is a dynamic mirror if your preferred mirror goes offline. See https://mariadb.org/mirrorbits/ for details.
# URIs: https://deb.mariadb.org/11.1/debian
URIs: https://mirrors.aliyun.com/mariadb/repo/11.1/debian
Suites: bookworm
Components: main
Signed-By: /etc/apt/keyrings/mariadb-keyring.pgp

[Output]

```
### Confirmation de authenticité des packages

```bash
[Input]

sudo apt install apt-transport-https curl
sudo mkdir -p /etc/apt/keyrings
sudo curl -o /etc/apt/keyrings/mariadb-keyring.pgp 'https://mariadb.org/mariadb_release_signing_key.pgp'

[Output]
(pour la derniere commande)
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100  4797  100  4797    0     0  33463      0 --:--:-- --:--:-- --:--:-- 33781

```
### Installation de MariaDB 11

```bash
[Input]

sudo apt install mariadb-server

[Output]

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

### Installation de PHP
```bash
[Input]



[Output]
```



## Etape 3 Installation d'Icinga 2

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

### Installation de Icinga 2 API

```bash
[Input]

[Output]

```
```bash
[Input]

[Output]

```
```bash
[Input]

[Output]

```
```bash
[Input]

[Output]

```
```bash
[Input]

[Output]

```
```bash
[Input]

[Output]

```


