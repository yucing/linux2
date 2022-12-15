# 2022/12/12 Linux2 第十五週

1. cd /var/www
2. mkdir a.com b.com
3. cd a.com
4. echo "www.a.com" > index.html
5. cd ..
6. cd b.com
7. echo "www.b.com" > index.html
8. cd /etc/httpd/conf.d
9. ls -> 會看到 a.com.conf b.com.conf
10. gedit a.com.conf b.com.conf
11. 加入 a.com.conf
```
<VirtualHost *:80>
    ServerName a.com
    ServerAlias www.a.com
    ServerAdmin webmaster@a.com
    DocumentRoot /var/www/a.com/public_html

    <Directory /var/www/a.com/public_html>
        Options -Indexes +FollowSymLinks
        AllowOverride All
    </Directory>

    ErrorLog /var/log/httpd/a.com-error.log
    CustomLog /var/log/httpd/a.com-access.log combined
</VirtualHost>
```

12. 加入 b.com.conf
```
<VirtualHost *:80>
    ServerName b.com
    ServerAlias www.b.com
    ServerAdmin webmaster@b.com
    DocumentRoot /var/www/b.com/public_html

    <Directory /var/www/b.com/public_html>
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
16. 到本機輸入 www.a.com www.b.com