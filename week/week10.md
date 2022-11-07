# 2022/11/07 Linux2 第十週

# 1
* 需3台虛擬機
## 步驟
1. Network \-> Adapter1 : InternalNetwork Name1
2. Network \-> Adapter2 : InternalNetwork Name2
3. yum install wireshark-* -y
4. wireshark : 查看是否安裝完成
5. halt -p 
6. clone 2台 虛擬機
### 第一台
7. ip addr add 192.168.1.1/24 brd + dev ens33
8. ip route add default via 192.168.1.254
9. ip route show
### 中繼伺服器
10. ip addr add 192.168.1.254/24 brd + dev ens33
11. ip addr add 10.0.0.1/24 brd + dev ens36
### 第三台
12. ip route add default via 10.0.0.1
13. ip route show
14. ip addr add 10.0.0.2/24 brd + dev ens33
### 中繼伺服器
15. ping 10.0.0.2
16. ping 192.168.1.1
17. iptables -t nat -A POSTROUTING -s 192.168.1.0/24 -o ens36 -j MASQUERADE
18. iptables -t nat -L

```
-s : source
-o : output
-j : jump
MASQUERADE : 192.168.1.1 -> 10.0.0.1 -> 10.0.0.2
```