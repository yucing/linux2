# 2022/9/26 Linux2 第四週 

# Linux 指令
1. df -h : 查看磁碟空間
2. wget 網址 : 直接從網路下載

# quota
1. 進入單人模式
2. vi /etc/fstab
3.  加入
```
,usrquota,grpquota
```

![](https://github.com/yucing/linux2/blob/main/picture/28.png)

4. reboot
5. cat /etc/mtab | grep usrquota

![](https://github.com/yucing/linux2/blob/main/picture/29.png)

## 查看使用情形
1. xfs_quota -xc 'report -h' /home : 可察看目前 /home 使用情形

![](https://github.com/yucing/linux2/blob/main/picture/30.png)

```
soft : 超過會警告
hard : 不能超過此使用量
0 : 沒有限制
```

2. xfs_quota -xc 'free -h' /home : 可察看 /home 總共多少 使用多少 

![](https://github.com/yucing/linux2/blob/main/picture/31.png)

3. xfs_quota -xc 'quota -h user' /home : 查看 /home 使用者使用情形

![](https://github.com/yucing/linux2/blob/main/picture/32.png)

## 限制使用者上限
1. xfs_quota -xc 'limit bsoft=10m bhard=12m user' /home

![](https://github.com/yucing/linux2/blob/main/picture/33.png)

### 產生特定大小檔案
* dd if=/dev/zero of=test bs=1M count=13
```
dd : 產生一個特定大小的檔案
if : input file
/dev/zero : 可產生 0 的裝置
of : output file
bs : 讀一次的量 1M
count : 產生 13 次
    -> 產生 13M 大小的檔案
```

![](https://github.com/yucing/linux2/blob/main/picture/34.png)

* 因為上限為 12M, 因此只能產生 12M 的檔案

# rpm 查詢
1. rpm -qa : 查詢系統已安裝套件清單

![](https://github.com/yucing/linux2/blob/main/picture/35.png)

2. rpm -qi 套件 : 查詢特定套件的安裝資訊

![](https://github.com/yucing/linux2/blob/main/picture/36.png)

3. rpm -ql 套件 : 查詢套監所安裝的檔案清單

![](https://github.com/yucing/linux2/blob/main/picture/37.png)

4. rpm -qf : 查詢系統特定檔案的來源安裝套件

![](https://github.com/yucing/linux2/blob/main/picture/38.png)

5. rpm -ivh 檔案 : 查看下載進度條
6. rpm -e 檔案 : 移除以下載的套件

# yum
1. yum install 套件 : 安裝套件
2. yum update 套件 : 更新套件
3. yum remove 套件 : 移除套件
4. yum search 文字 : 搜尋含有特定文字的套件
5. yum list : 列出所有套件資訊

# htop
1. wget https://src.fedoraproject.org/lookaside/extras/htop/htop-2.2.0.tar.gz/sha512/ec1335bf0e3e0387e5e50acbc508d0effad19c4bc1ac312419dc97b82901f4819600d6f87a91668f39d429536d17304d4b14634426a06bec2ecd09df24adc62e/htop-2.2.0.tar.gz
2. yum groupinstall "Development Tools"
3. tar xvfz htop-2.2.0.tar.gz
4. cd htop-2.2.0
5. ./configure

```md
不成功
1. yum install ncurses-devel
2. ./configure
```

6. make
7. make install
8. htop

![](https://github.com/yucing/linux2/blob/main/picture/39.png)

9. 案 q 可以離開