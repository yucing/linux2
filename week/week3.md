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
10. 在資料夾輸入 "\\IPAdress"

![](https://github.com/yucing/linux2/blob/main/picture/21.png)

11. 如要在本機加入資料, Linux 需先打 chmod 777 /test_samba

![](https://github.com/yucing/linux2/blob/main/picture/22.png)

12. 如要登入其他帳號, 需於 cmd 輸入: net use * /delete

## 內容意思
1. read only = no
    可寫可讀
2. guest ok = yes
    一般使用者可用
3. browserable = yes
    可瀏覽

# Linux 指令
## 建立群組
1. groupadd 群組 : 建立群組
2. gpassed -a 使用者 群組 : 將使用者加入群組

# quota 磁碟配額
## 準備工作
1. vim /etc/default/grub
2. timeout 設定為 5 

    Ex: 也可改為 10

3. grub2-mkconfig -o /boot/grub2/grub.cfg
4. reboot
5. 在進入畫面時按下 E

![](https://github.com/yucing/linux2/blob/main/picture/24.png)

6. 往下找 quiet 後面加 1

![](https://github.com/yucing/linux2/blob/main/picture/23.png)

7. 輸入 superuser 的密碼, 進入單人模式
8. vim /etc/fstab
9. 加入
```
,usrquota,grpquota
```

![](https://github.com/yucing/linux2/blob/main/picture/25.png)

![](https://github.com/yucing/linux2/blob/main/picture/27.png)

## 意思
1. usrquota : 使用者上限
2. grpquota : 群組上限