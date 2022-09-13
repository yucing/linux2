# 2022/9/12 Linux2 第二週 

# NFS
1. network file system
2. 主要使用在 unix-like, 檔案分享
> * unix-like : linux、unix

![](https://github.com/yucing/linux2/blob/main/picture/9.png)

# NFS install
### [centos安裝NFS](https://qizhanming.com/blog/2018/08/08/how-to-install-nfs-on-centos-7)
## Server
1. yum install nfs-utils
2. systemctl enable rpcbind
3. systemctl enable nfs
4. firewall-cmd --zone=public --permanent --add-service={rpc-bind,mountd,nfs}
> * 須注意 firewalld 是否開啟
5. firewall-cmd --reload
6. mkdir /data
7. chmod 755 /data
8. vi /etc/exports
9. 加入 /data/ 客戶端IP範圍/24(rw,sync,no_root_squash,no_all_squash)
> * Ex: /data/ 192.168.56.0/24(rw,sync,no_root_squash,no_all_squash)

![](https://github.com/yucing/linux2/blob/main/picture/10.png)

10. 重啟 nfs : systemctl restart nfs
11. 檢查共享目錄 : showmount -e hostname

![](https://github.com/yucing/linux2/blob/main/picture/11.png)

## Client
1. yum install nfs-utils
2. ystemctl enable rpcbind
3. systemctl start rpcbind

## Client connect
1. showmount -e ServerIPAddress
> * Ex: showmount -e 192.168.56.112

![](https://github.com/yucing/linux2/blob/main/picture/12.png)

2. mkdir /data
3. mount -t nfs ServerIPAddress:/data(Server) /data(Client)
4. 檢查連接狀況 : mount
5. cd /data(Client)
6. touch a
7. 於 Server 端的 /data 查看是否多了一個 a 檔案

![](https://github.com/yucing/linux2/blob/main/picture/13.png)

# 壓縮
## [壓縮參考資料](http://note.drx.tw/2008/04/command.html)

## 格式
1. .tar -> 將目錄與檔案集合成單一檔案
2. .gz / .bz2 -> 將檔案壓縮

## 打包 .tar
### 打包
* tar cvf 檔案名稱.tar 要打包的檔案

![](https://github.com/yucing/linux2/blob/main/picture/14.png)

### 解包
* tar xvf 檔案名稱.tar

![](https://github.com/yucing/linux2/blob/main/picture/15.png)

## 壓縮 .gz
### 壓縮
* gzip FileName
### 解壓縮一
* gunzip FileName.gz
### 解壓縮二
* gzip -d FileName.gz

## 打包+壓縮 .tar.gz
### 壓縮
* tar zcvf FileName.tar.gz DirName

![](https://github.com/yucing/linux2/blob/main/picture/16.png)

### 解壓縮
* tar zxvf FileName.tar.gz

![](https://github.com/yucing/linux2/blob/main/picture/17.png)

## 壓縮 .zip
### 壓縮
* zip -r FileName.zip DirName

![](https://github.com/yucing/linux2/blob/main/picture/18.png)

# Linux 指令
1. file 檔案 -> 查看檔案類別
2. stat -> 查看檔案詳細資訊
3. find -> 找有變更的檔案

rpm -qa -> 查詢安裝東西