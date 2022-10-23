# 2022/10/17 Linux2 第七週

# VPN install
# [pptp VPN](https://help.aliyun.com/document_detail/41345.html)
1. yum install -y ppp pptpd
2. vi /etc/pptpd.conf
3. 移到最下面，加入
```md
localip 192.168.0.1
remoteip 192.168.0.100-238,192.168.0.200
```

![](https://github.com/yucing/linux2/blob/main/picture/68.png)

4. vi /etc/ppp/options.pptpd
5. 輸入 /ms-dns 找到 ms-dns 10.0.0.1 ，加入
```md
ms-dns 8.8.8.8
ms-dns 9.9.9.9
```

![](https://github.com/yucing/linux2/blob/main/picture/69.png)

6. vi /etc/ppp/chap-secrets
7. 加入 account | server secret | IP address
```md
test pptpd 密碼 *
```

![](https://github.com/yucing/linux2/blob/main/picture/67.png)

8. vi /etc/ppp/ip-up
9. 在 [ -x /etc/ppp....] 下方，加入
```md
ifconfig ppp0 mtu 1472
```

![](https://github.com/yucing/linux2/blob/main/picture/70.png)

10. vi /etc/sysctl.conf
11. 加入
```md
net.ipv4.ip_forward = 1
```

![](https://github.com/yucing/linux2/blob/main/picture/71.png)

12. sysctl -p
13. 檢查防火牆 / SELinux 是否關閉
14. systemctl restart pptpd
15. 進到電腦的網路設定
16. 新增VPN

![](https://github.com/yucing/linux2/blob/main/picture/72.png)

# ssh 遠端登入
* ssh root@hostname \[指令\]

![](https://github.com/yucing/linux2/blob/main/picture/73.png)

# seq 產生序列數字
## seq start end
* 產生一個累加的數
    Ex: seq 1 10

![](https://github.com/yucing/linux2/blob/main/picture/74.png)

## seq start step end
* 產生 
