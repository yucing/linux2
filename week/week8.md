# 2022/10/24 Linux2 第八週

# sort
## 參數
* -k \[num\] : 指定第幾行排序

![](https://github.com/yucing/linux2/blob/main/picture/89.png)

* -r : 從大到小

![](https://github.com/yucing/linux2/blob/main/picture/90.png)

* -n / -g : 比較數字
* -t "選項" : 精簡的 tr

![](https://github.com/yucing/linux2/blob/main/picture/91.png)

# cat 合併檔案
* cat filename1 filename2 filename3 .. > directFilename

![](https://github.com/yucing/linux2/blob/main/picture/92.png)

# split 分割檔案
* split -b 分割大小 filename

![](https://github.com/yucing/linux2/blob/main/picture/93.png)

# ping
## 參數
* -c \[num\]
    * ping n 次

![](https://github.com/yucing/linux2/blob/main/picture/78.png)

* -i \[ms\]
    * 幾毫秒 ping

![](https://github.com/yucing/linux2/blob/main/picture/77.png)

# mail
1. echo "文字" > filenmae
2. mail -s "Title" example@com.tw < filename

![](https://github.com/yucing/linux2/blob/main/picture/95.png)

![](https://github.com/yucing/linux2/blob/main/picture/94.png)

# alias