# 2022/9/5 Linux2 第一週 

# 考試
1. Linux installation
2. network settings
 ⋅⋅⋅* network manager
> * networking
3. ssh server
> * no password
> * scp
4. ftp server
5. sambo
6. nfs
7. www
> * apache
> * nginx
> * openresty
8. php
9. mysql
10. DNS
11. IPv6
12. NAT
13. DHCP

# 固定IP
* 進入IP介面
* Automatic -> manual
* address 輸入此機器的 ip
* netmask 輸入 255.255.255.0 

![](https://github.com/yucing/linux2/blob/main/picture/ip1.png)

# 更改主機名稱
* 需使用 superuser
1. hostnamectl set-hostname 名稱
2. 重開 terminal

![](https://github.com/yucing/linux2/blob/main/picture/2.png)

# ping hostname

1. gedit /etc/hosts
2. 加入 address hostname

![](https://github.com/yucing/linux2/blob/main/picture/3.png)

3. ping hostname

![](https://github.com/yucing/linux2/blob/main/picture/4.png)

# ssh server / client
* no password
## server

1. getenforce -> 是某為 disable
2. systemctl status firewalld -> 是否關閉
3. systemctl status sshd -> 是否開啟

![](https://github.com/yucing/linux2/blob/main/picture/5.png)

4. ssh-keygen -> 產生金鑰
> * 金鑰儲存在 /root/.ssh/id_rsa

![](https://github.com/yucing/linux2/blob/main/picture/6.png)

5. ssh-copy-id root@hostname -> 將 ssh 拷貝到另一台主機
6. ssh root@hostname

![](https://github.com/yucing/linux2/blob/main/picture/7.png)

# 複製檔案
* scp 檔案 root@hostname:位置

![](https://github.com/yucing/linux2/blob/main/picture/8.png)