# 2022/11/14 Linux2 第十一週

# 網路設定模式
* NetworkManager
    * 適合動態網路設定
* Network
    * 適合固定位址的主機
## 查看網路設定模式
* 預設 NetworkManager : active , network : failed
* systemctl status NetworkManager

![](https://github.com/yucing/linux2/blob/main/picture/116.png)

* systemctl status network

![](https://github.com/yucing/linux2/blob/main/picture/117.png)

## Linux 網路手動設定
1. systemctl stop NetworkManager
2. systemctl start network
3. cd /etc/sysconfig/network-scripts/
4. gedit ifcfg-網路名稱
    * Ex: gedit ifcfg-enp0s3
5. 加入
```
DEVICE="網路名稱"
NAME="網路名稱"
HWADDR="網路卡卡號"
ONBOOT="yes"  # 開機時是否開啟
BOOTPROTO=static
IPADDR= # ifconfig : 查看IP位址
NETMASK=255.255.255.0
GATEWAY= # ip route show / netstat -rn : 查看內定路由器
```

![](https://github.com/yucing/linux2/blob/main/picture/118.png)

6. systemctl disable NetworkManager
7. systemctl enable network
8. reboot
9. systemctl status network

![](https://github.com/yucing/linux2/blob/main/picture/119.png)

# 修改 dns server
* vim /etc/resolv.conf

![](https://github.com/yucing/linux2/blob/main/picture/120.png)

# 在實體介面建立虛擬IP
## ifconfig
* ifconfig enp0s3:數字 \[IPaddress\] netmask \[NetworkMask\]
    * Ex: ifconfig enp0s3:10 10.0.2.10 netmask 255.255.255.0
* ip addr show enp0s3

![](https://github.com/yucing/linux2/blob/main/picture/121.png)

### 刪除虛擬網路卡
* ifconfig enp0s3:數字 0

## ip addr
* ip addr add \[IPaddress/NetworkMask\] brd + dev enp0s3
    * Ex: ip addr add 10.0.2.10/24 brd + dev enp0s3
* ip addr show enp0s3

![](https://github.com/yucing/linux2/blob/main/picture/122.png)

### 刪除虛擬網路卡
* ip addr del \[IPaddress/NetworkMask\] brd + dev enp0s3
    * Ex: ip addr del 10.0.2.10/24 brd + dev enp0s3

# 關閉/開啟介面卡
## 關閉介面卡
* ifconfig \[網路\] down
    * Ex: ifconfig enp0s3 down

## 開啟介面卡
* ifconfig \[網路\] up
    * Ex: ifconfig enp0s3 up

# 更改網路卡卡號
* ifconfig \[網路\] hw ether \[網路卡卡號\]
    * Ex: ifconfig enp0s3 hw ether 00:01:02:03:04:05
* 真正的網路卡卡號沒有被更動

# mtu 封包大小
* 封包傳輸大小
* 預設為 1500
## 修改 mtu
* ifconfig \[網路\] mtu \[大小\]
    * Ex: ifconfig enp0s3 mtu 500

# 設備統計資料
* ip -s link show \[網路\]
    * Ex: ip -s link show enp0s3
* ifconfig \[網路\]
    * Ex: ifconfig enp0s3