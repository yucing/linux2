# 2022/9/19 Linux2 第三週 

# samba
1. su
2. yum install samba samba-client samba-common -y
3. mkdir /test_samba
4. chown nobody /test_samba/

![](https://github.com/yucing/linux2/blob/main/picture/19.png)

5. vi /etc/smaba/smb.conf
6. 加入
```
[test]
    comment = for test
    path = test_samba
    read only = no
    guest ok = yes
    browserable = yes
```

![](https://github.com/yucing/linux2/blob/main/picture/20.png)

7. systemctl start smb
8. testparm
9. smbpasswd -a user
10. 在資料夾輸入 \\IPAdress

![](https://github.com/yucing/linux2/blob/main/picture/21.png)