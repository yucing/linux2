# 2022/10/3 Linux2 第五週

# 臨時伺服器架設 ngrok
* 因為免費版, 僅提供一種連線方式
## [ngrok](https://askie.today/ngrok-localhost-server-settings/)
## 安裝
1. rpm -qa | grep httpd : 查看網頁伺服器是否有安裝
2. systemctl start httpd : running
3. lsof -i:80 / netstat -tunlp | grep 80 : 查看 TCP/UDP 是否開啟

![](https://github.com/yucing/linux2/blob/main/picture/40.png)

4. yum install epel-release
5. yum install snapd
6. systemctl enable --now snapd.socket
7. ln -s /var/lib/snapd/snap /snap
8. snap install ngrok
9. ngrok config add-authtoken 'Your token'
10. 如不成功 :
```
    wget https://bin.equinox.io/c/bNyj1mQVY4c/ngrok-v3-stable-linux-amd64.tgz --no-check-certificate
```
11. tar xvzf ngrok-v3-stable-linux-amd64.tgz
12. ./ngrok config add-authtoken 'Your token'
13. ./ngrok http 80

![](https://github.com/yucing/linux2/blob/main/picture/41.png)

14. 複製網址到本機上

![](https://github.com/yucing/linux2/blob/main/picture/42.png)

## 建立自己的網站
1. cd /var/www/html
2. 建立一個 hi.htm
3. 將名稱加入網站後面 /hi.htm

![](https://github.com/yucing/linux2/blob/main/picture/43.png)

## 關閉工作狀況
1. ps -aux | grep ngrok
2. kill -9 號碼

# du 磁碟使用狀況
1. du : 當前目錄下的使用情況
2. du -h : 當前目錄下的使用情形 -h -> 將檔案的大小以k,m顯示

![](https://github.com/yucing/linux2/blob/main/picture/44.png)

3. du -hs / du -h -s : 顯示 total 使用情況

![](https://github.com/yucing/linux2/blob/main/picture/45.png)

4. du  -hs --max-depth=數字 目錄 : 顯示指定目錄的第幾層資料使用情況
```
    du 與 -hs 之間有兩個空白
```

![](https://github.com/yucing/linux2/blob/main/picture/46.png)

# df 磁碟分割情形
* df -h : 查看磁碟分割情形

![](https://github.com/yucing/linux2/blob/main/picture/47.png)

## 抓特定分割
* df -h | grep /dev/shm

![](https://github.com/yucing/linux2/blob/main/picture/48.png)

* df -h | grep /dev/shm | awk '{print $5}'

![](https://github.com/yucing/linux2/blob/main/picture/49.png)

* df -h | grep /dev/shm | awk '{print $5}' | tr "%" " "

![](https://github.com/yucing/linux2/blob/main/picture/50.png)

# tr 用法
## 取代
* df -h | grep /dev/shm | awk '{print $5}' | tr "%" " "

![](https://github.com/yucing/linux2/blob/main/picture/56.png)

## 轉換
### 換成小寫
* tr [:upper:] [:lower:]

![](https://github.com/yucing/linux2/blob/main/picture/57.png)

### 換成大寫
* tr [:lower] [:upper:]

![](https://github.com/yucing/linux2/blob/main/picture/58.png)

### 字母跟數字
* tr [:alnum:]

![](https://github.com/yucing/linux2/blob/main/picture/59.png)

### 字母
* tr [:alpha:]

![](https://github.com/yucing/linux2/blob/main/picture/60.png)

### 空白
* tr [:blank:]

![](https://github.com/yucing/linux2/blob/main/picture/61.png)

### 數字
* tr [:digit:]

![](https://github.com/yucing/linux2/blob/main/picture/62.png)

## 刪除
* tr -d

![](https://github.com/yucing/linux2/blob/main/picture/63.png)

## 補充
### "/' 的差別
* 如有特殊字元, 需使用 單引號 '

![](https://github.com/yucing/linux2/blob/main/picture/64.png)

### 刪除特定範圍
* tr -d "X-xY-yZ-z"

![](https://github.com/yucing/linux2/blob/main/picture/65.png)

### 保留第幾到幾個
* cut -c X-x

![](https://github.com/yucing/linux2/blob/main/picture/66.png)

# wc 統計
* wc -l : 只顯示行數

![](https://github.com/yucing/linux2/blob/main/picture/53.png)

* wc -c : 只顯示字元數

![](https://github.com/yucing/linux2/blob/main/picture/54.png)

* wc -w : 只顯示英文字節

![](https://github.com/yucing/linux2/blob/main/picture/55.png)

# free 記憶體使用情況
* free -m

![](https://github.com/yucing/linux2/blob/main/picture/51.png)

* free -mh

![](https://github.com/yucing/linux2/blob/main/picture/52.png)