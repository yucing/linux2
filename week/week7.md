# 2022/10/17 Linux2 第七週

# VPN install
# [pptp VPN](https://help.aliyun.com/document_detail/41345.html)
1. yum install -y ppp pptpd
2. vi /etc/pptpd.conf
3. 刪除
```md
#localip 192.168.0.1
#remoteip 192.168.0.234-238,192.168.0.245
```