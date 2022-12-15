# 2022/11/28 Linux2 第十三週

# 網頁伺服器 httpd
## [網址](https://lab.twidc.net/lamplinuxapachemysql-php-centos7/)
1. rpm -qa | grep httpd
2. 如果沒有 : yum install httpd
3. getenforce
    * 如果不是 disable : cd /etc/selinux/config \-> SELINUX 改成 disabled \-> reboot
4. systemctl status firewalld : 查看防火牆是否關閉
5. cat /etc/httpd/conf/httpd.conf | grep 80
    * 如果 Listen不是 80 : cd /etc/httpd/conf/httpd.conf 找到 Listen 改成 80

![](https://github.com/yucing/linux2/blob/main/picture/125.png)

6. 於本機輸入 IPaddress 

![](https://github.com/yucing/linux2/blob/main/picture/124.png)

# 安裝 MySQL
1. yum install mariadb-server mariadb
2. systemctl start mariadb
3. mysql_secure_installation
4. enter \-> Y \-> 1234 \-> 1234 \-> Y \-> n  \-> n \-> Y
5. systemctl enable mariadb
6. mysql -u root -p
7. 1234

![](https://github.com/yucing/linux2/blob/main/picture/126.png)

# 安裝 PHP
1. yum install php php-mysql
2. yum install php-fpm
3. systemctl restart httpd
4. cd /var/www/html
5. gedit test.php
```php
<?php
phpinfo();
?>
```
6. 於本機輸入 IPaddress/test.php

# 實作
1. cd /var/www/html
2. gedit idnex.php &
```php
<?php
$servername="127.0.0.1";
$username="root";
$password="123456";
$dbname="testdb";

$conn = new mysqli($servername, $username, $password, $dbname);

if($conn->connect_error){
  die("connection failed:" . $conn->connect_error);
}

$sql="select name, phone from addrbook";
$result = $conn->query($sql);

if($result->num_rows >0){
  while($row = $result->fetch_assoc()){
    echo "name:" . $row["name"]." phone:".$row["phone"]."<br>";
  }
} else {
  echo "0 result";
}

?>
```
3. 於本機輸入 IPaddress/index.php

# database 語法
## [語法](https://clay-atlas.com/blog/2019/11/21/sql-table-create-insert-update-remove-delete/)
* show databases; -> 查看資料庫資料

![](https://github.com/yucing/linux2/blob/main/picture/127.png)

* create database \[Name\]; -> 建立 database

![](https://github.com/yucing/linux2/blob/main/picture/128.png)

* use \[Name\]; -> 進入 資料庫
* create table \[Table\](Record); -> 建立 table
    * Ex: create table addrbook(name varchar(50) not null, phone char(10));
* insert into \[Table](Record) values (Record); -> 新增資料
    * Ex: insert into addrbook(name, phone) values ("Tom","0912345678");
* select \[option\] from \[Table\];
    * Ex: select name,phone from addrbook;

![](https://github.com/yucing/linux2/blob/main/picture/129.png)