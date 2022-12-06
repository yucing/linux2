# 2022/11/07 Linux2 第十週

# Internal Network 實作
* 需3台虛擬機
## 步驟
1. yum install wireshark-* -y
2. wireshark : 查看是否安裝完成
3. halt -p 
4. clone 2台 虛擬機
5. 第一台網路設定
```
Network \-> Adapter1 : InternalNetwork Name1
```
6. 中繼伺服器網路設定
```
Network \-> Adapter1 : InternalNetwork Name1
Network \-> Adapter1 : InternalNetwork Name2
```

7. 第三台網路設定
```
Network \-> Adapter1 : InternalNetwork Name2
```

8. 到第一台虛擬機
```
# ip addr add 192.168.1.1/24 brd + dev enp0s3
# ip route add default via 192.168.1.254
# ip route show
```

9. 到中繼伺服器
```
# ip addr add 192.168.1.254/24 brd + dev enp0s3
# ip addr add 10.0.0.1/24 brd + dev enp0s8
```

10. 到第三台虛擬機
```
# ip addr add 10.0.0.2/24 brd + dev enp0s3
# ip route add default via 10.0.0.1
# ip route show
```

11. 到中繼伺服器
```
# ping 10.0.0.2 : 確認是否連接
# ping 192.168.1.1 : 確認是否連接
# iptables -t nat -A POSTROUTING -s 192.168.1.0/24 -o enp0s8 -j MASQUERADE
# iptables -t nat -L
# echo 1 > /proc/sys/net/ipv4/ip_forward
```

```
-s : source
-o : output
-j : jump
MASQUERADE : 192.168.1.1 -> 10.0.0.1 -> 10.0.0.2

```

12. 到第一台虛擬機
```
# wireshark
# ping 10.0.0.2
```
13. 成功後會有以下畫面

![](https://github.com/yucing/linux2/blob/main/picture/123.png)

# 判斷比較
## 大括號
* \[a \[運算\] b \] && 事件1 || 事件2
## test
* test a \[運算\] b && 事件1 || 事件