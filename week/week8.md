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

![](https://github.com/yucing/linux2/blob/main/picture/96.png)

## 顯示原型
* 加上 \

![](https://github.com/yucing/linux2/blob/main/picture/97.png)

## 將指令縮減成短指令
* alias 短指令='指令 --color=auto'

![](https://github.com/yucing/linux2/blob/main/picture/98.png)

## 取消指令
* unalias 短指令

![](https://github.com/yucing/linux2/blob/main/picture/99.png)

## 新增指令
1. vim .bashrc
2. 新增
```
alias 短指令='指令 --color=auto'
```

![](https://github.com/yucing/linux2/blob/main/picture/100.png)

3. source .bashrc / . .bashrc

![](https://github.com/yucing/linux2/blob/main/picture/101.png)

# echo
## 單引號 v.s 雙引號的差別
* ' : 解析出特殊字元
* " : 顯示

![](https://github.com/yucing/linux2/blob/main/picture/102.png)

## 大括號

![](https://github.com/yucing/linux2/blob/main/picture/103.png)

## 參數
* -e : 特殊指令生效

![](https://github.com/yucing/linux2/blob/main/picture/104.png)

# 特殊變數
## env
* 顯示系統的環境變數

![](https://github.com/yucing/linux2/blob/main/picture/105.png)

## UID
* root UID = 0

## history
* echo $HISTFILESIZE : 查看 history 存放指令量

![](https://github.com/yucing/linux2/blob/main/picture/106.png)

### 改變儲存的指令量
* HISTFILESIZE=數字

![](https://github.com/yucing/linux2/blob/main/picture/107.png)

## 產生亂數
* echo $RANDOM

![](https://github.com/yucing/linux2/blob/main/picture/108.png)

### 產生固定長度的亂數
* echo $RANDOM |　md5sum | cut -c 1-數字

![](https://github.com/yucing/linux2/blob/main/picture/109.png)