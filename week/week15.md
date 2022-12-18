# 2022/12/12 Linux2 第十五週

# Apache 虛擬主機
## [Apache 虛擬主機](https://www.myfreax.com/how-to-set-up-apache-virtual-hosts-on-centos-7/) 
1. cd /var/www
2. mkdir a.com b.com : 第一個家目錄 a.com, 第二個家目錄 b.com
3. cd a.com
4. echo "www.a.com" > index.html
5. cd ..
6. cd b.com
7. echo "www.b.com" > index.html
8. cd /etc/httpd/conf.d
9. gedit a.com.conf b.com.conf
10. 加入 a.com.conf
```
<VirtualHost *:80>
    ServerName a.com
    ServerAlias www.a.com
    ServerAdmin webmaster@a.com
    DocumentRoot /var/www/a.com

    <Directory /var/www/a.com>
        Options -Indexes +FollowSymLinks
        AllowOverride All
    </Directory>

    ErrorLog /var/log/httpd/a.com-error.log
    CustomLog /var/log/httpd/a.com-access.log combined
</VirtualHost>
```

11. 加入 b.com.conf
```
<VirtualHost *:80>
    ServerName b.com
    ServerAlias www.b.com
    ServerAdmin webmaster@b.com
    DocumentRoot /var/www/b.com

    <Directory /var/www/b.com>
        Options -Indexes +FollowSymLinks
        AllowOverride All
    </Directory>

    ErrorLog /var/log/httpd/b.com-error.log
    CustomLog /var/log/httpd/b.com-access.log combined
</VirtualHost>
```

13. systemctl restart httpd
14. systemctl status httpd
15. 到 C:\Windows\System32\drivers\etc 的 hosts 檔案加入
```
IPaddress www.a.com
IPaddress www.b.com
```

![](https://github.com/yucing/linux2/blob/main/picture/137.png)


16. 到本機輸入 www.a.com www.b.com

![](https://github.com/yucing/linux2/blob/main/picture/138.png)

# Access Control - Option 指令 - Indexes
1. cd /var/www/a.com
2. mkdir a
3. cd a
4. touch {a..d}.txt
5. cd /etc/httpd/conf.d
6. gedit a.com.conf
```
<VirtualHost *:80>
    ServerName a.com
    ServerAlias www.a.com
    ServerAdmin webmaster@a.com
    DocumentRoot /var/www/a.com

    <Directory /var/www/a.com>
        Options Indexes

        #Options -Indexes +FollowSymLinks
        AllowOverride All
    </Directory>

    ErrorLog /var/log/httpd/a.com-error.log
    CustomLog /var/log/httpd/a.com-access.log combined
</VirtualHost>
```
7. systemctl restart httpd
8. 到本機輸入 www.a.com/a


![](https://github.com/yucing/linux2/blob/main/picture/139.png)

# Access Control - Option 指令 - FollowSymLinks
1. cd /
2. mkdir mytmp
3. cd mytmp
4. echo "hi" >hi.txt
5. cd /var/www/a.com/a
6. ln -s /mytmp mytmp
7. cd /etc/httpd/conf.d
8. gedit a.com.conf
```
<VirtualHost *:80>
    ServerName a.com
    ServerAlias www.a.com
    ServerAdmin webmaster@a.com
    DocumentRoot /var/www/a.com

    <Directory /var/www/a.com>
        Options FollowSymLinks

        #Options -Indexes +FollowSymLinks
        AllowOverride All
    </Directory>

    ErrorLog /var/log/httpd/a.com-error.log
    CustomLog /var/log/httpd/a.com-access.log combined
</VirtualHost>
```
9. systemctl restart httpd
10. 到本機輸入 www.a.com/a

# Access Control - 驗證帳號
1. cd /var/www/a.com
2. mkdir secure
3. cd /etc/httpd/conf.d
4. gedit a.com.conf
```
<VirtualHost *:80>
    ServerName a.com
    ServerAlias www.a.com
    ServerAdmin webmaster@a.com
    DocumentRoot /var/www/a.com

    <Directory /var/www/a.com>
        Options FollowSymLinks

        #Options -Indexes +FollowSymLinks
        AllowOverride All
    </Directory>

    <Directory /var/www/a.com/secure>
        AllowOverride AuthConfig
    </Directory>

    ErrorLog /var/log/httpd/a.com-error.log
    CustomLog /var/log/httpd/a.com-access.log combined
</VirtualHost>
```
5. cd /var/www/a.com/secure
6. htpasswd -c .htpasswd \[Name\] : 第一次需要 -c, 第二次就不用了
    * Ex: htpasswd -c .htpasswd tom
7. Enter passwd : 123
8. cat .htpasswd
9. gedit .htaccess
```
AuthType Basic
AuthName "Private File Area"
AuthUserFile /var/www/a.com/secure/.htpasswd
Require valid-user
```
10. systemctl restart httpd
11. 到本機輸入 www.a.com/secure
12. 輸入帳號/密碼

![](https://github.com/yucing/linux2/blob/main/picture/140.png)

# vsftpd
1. yum install vsftpd
2. cd /var/ftp/pub
3. echo 1 > 1.txt
4. echo 2 > 2.txt
5. 打開 winscp 選擇 FTP
6. 使用匿名者登入

![](https://github.com/yucing/linux2/blob/main/picture/141.png)

7. netstat -tunpl | grep 21 : 查看 vsftpd 是否開啟
8. systemctl start vsftpd
9. 打開 winscp 選擇 FTP
10. 使用匿名者登入

![](https://github.com/yucing/linux2/blob/main/picture/142.png)

## 要從本機上傳檔案
### [上傳](https://blog.csdn.net/zhaojia92/article/details/79511581)
1. chmod 777 /var/ftp/pub
2. cd /etc/vsftpd
3. gedit vsftpd.conf
```
#anon_upload_enable=yes -> anon_upload_enable=yes
```

![](https://github.com/yucing/linux2/blob/main/picture/143.png)

4. systemctl restart vsftpd