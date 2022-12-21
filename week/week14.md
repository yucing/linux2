# 2022/12/5 Linux2 第十四週

# httpd
## 目錄位置
* 配置目錄 : /etc/httpd
* 家目錄 : /var/www/html
* 記錄檔 : /var/log/httpd
* 有些配置會放在 /etc/httpd/conf.d

## 操作
1. getenforce : 檢查 SELinux 是否關閉
    * 如果不是 disable : cd /etc/selinux/config \-> SELINUX 改成 disabled \-> reboot
2. systemctl status firewalld 是否關閉
3. rpm -qa | grep httpd
    * 如果沒有 : yum install httpd -y

## 有多少人來查看此網站
* cat /var/log/httpd/access_log
* cat /var/log/httpd/access_log | awk '{print $1}' | sort | uniq

![](https://github.com/yucing/linux2/blob/main/picture/130.png)

## 錯誤訊息
* cat /var/log/httpd/error_log

# PidFile : 查看 process id
1. gedit /etc/httpd/conf/httpd.conf
2. 加入
```
PidFile "/run/httpd.pid"
```
3. systemctl restart httpd
4. netstat -tunpl | grep 80 或 cat /run/httpd.pid

![](https://github.com/yucing/linux2/blob/main/picture/131.png)

# 使用者專用網頁空間
1. cd /etc/httpd/conf.d
2. gedit userdir.conf &
3. 修改
```
User disabled -> #User disabled
#User public_html -> User public_html
```

![](https://github.com/yucing/linux2/blob/main/picture/132.png)

![](https://github.com/yucing/linux2/blob/main/picture/133.png)

4. 開啟新的 terminal
5. mkdir public_html
6. cd public_html
7. echo "hello world" >hi.htm
8. chmod 755 /home/user
9. systemctl restart httpd
10. 於本機輸入 IPaddress/~user/hi.htm

![](https://github.com/yucing/linux2/blob/main/picture/134.png)

# 連結檔案
## ln -s 軟連結
1. mkdir /mydata
2. echo "123" > /mydata/1.htm
3. cd /var/www/html
4. ln -s /mydata mydata
5. 於本機輸入 IPaddress/mydata/1.htm

![](https://github.com/yucing/linux2/blob/main/picture/135.png)

## Alias
1. mkdir /mydata2
2. echo "456" > /mydata2/1.htm
3. gedit /etc/httpd/conf/httpd.conf &
4. 在最下面加入
```
Alias /mydata2 /mydata2
<Directory /mydata2>
 Require all granted
</Directory>
```
5. systemctl restart httpd
6. 於本機輸入 IPaddress/mydata2/1.htm

![](https://github.com/yucing/linux2/blob/main/picture/136.png)