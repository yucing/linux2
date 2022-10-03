# 2022/10/3 Linux2 第五週

# 臨時伺服器架設 ngrok
* 因為免費版, 僅提供一種連線方式
## 安裝
1. rpm -qa | grep httpd : 查看網頁伺服器是否有安裝
2. systemctl start httpd : running
3. lsof -i:80 / netstat -tunlp | grep 80 : 查看 TCP/UDP 是否開啟
4. yum install epel-release
5. yum install snapd
6. systemctl enable --now snapd.socket
7. ln -s /var/lib/snapd/snap /snap
8. snap install ngrok

# du 磁碟使用狀況
1. du : 當前目錄下的使用情況
2. du -h : 當前目錄下的使用情形 -h -> 將檔案的大小以k,m顯示
3. du -hs / du -h -s : 顯示 total 使用情況
4. du -hs --max-depth=數字 目錄 : 顯示指定目錄的第幾層資料使用情況

# df 磁碟分割情形
* df -h : 查看磁碟分割情形

# wc 統計
* 