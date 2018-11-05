## AWS EC2 虛擬主機設定子網域
---

因為還沒找到AWS之前，我是用Open Shift的主機...
先前因為Open Shift服務要更新，發公告說不再提供免費帳號後苦尋不到穩定的主機商，   
剛好AWS正在推廣免費試用一年虛擬機，也就剛好試用看看了～   
用了兩年覺得很穩很不錯，上傳FTP或是打開網頁的速度都很快，一年免費服務到期了就決定繼續用下去到現在了～

分享之前在個人部落格寫的"AWS EC2 虛擬主機設定Domain與指定資料夾"的隨手筆記
本文連結：(https://kingweblife.blogspot.com/2018/04/aws-ec2.html )

這個是設定子網域的紀錄
因為我自己有買一個Domain連結個人作品網站，
而在建造Give Me Find這個網站時，不想要讓他網址變成資料夾路徑底下的網站，舉例來說：
```https://www.tzeng17.com/xxx/GiveMeFind/index.html```

這樣的網址名稱很沒特色，加上又讓人很難記住
在DNS服務商那邊偶然看到有子網域這個功能，決定來試試看！
設定完之後連上Give Me Find網站網址為：
```https://givemefind.tzeng17.com```

在閱讀性和記憶上都大大的改善，詳細可以搜尋子網域的公用！

首先用CLI去連線到aws的主機上
aws 上 Apache的環境為LAMP

官方教程：(http://docs.aws.amazon.com/zh_cn/AWSEC2/latest/UserGuide/install-LAMP.html )

輸入指令
```ssh -i ~/.ssh/MyKeyPair.pem ec2-user@35.166.xx.xx```
會連線到aws ubutu 虛擬機上，因為太久沒有作更新了，所以先執行指令
```sudo yum update```

跑完更新後 找到路徑
```/etc/httpd/conf```

編輯~~httpd.conf~~檔 因為httpd.conf檔為唯讀檔，所以輸入指令的時候記得要加~~sudo~~
```
[ec2-user@ip-xxx-xxx-xx-172 conf]$ sudo vi httpd.conf
```
找到 # Use name-based virtual hosting.這一行
   
  
```
#
# VirtualHost example:
# Almost any Apache directive may go into a VirtualHost container.
# The first VirtualHost section is used for requests without a known
# server name.
#
#<VirtualHost *:80>
#    ServerAdmin webmaster@dummy-host.example.com
#    DocumentRoot /www/docs/dummy-host.example.com
#    ServerName dummy-host.example.com
#    ErrorLog logs/dummy-host.example.com-error_log
#    CustomLog logs/dummy-host.example.com-access_log common
#</VirtualHost>
```

在aws的路徑下要設為

```
<VirtualHost *:80>
    DocumentRoot /var/www/html/
    ServerName www.tzeng17.com
    ServerAlias www.tzeng17.com
</VirtualHost>
<VirtualHost *:80>
    DocumentRoot /var/www/html/game/GivemeFind/
    ServerName givemefind.tzeng17.com
    ServerAlias givemefind.tzeng17.com
</VirtualHost>
```

**設定完後記得要重啟Apache的服務**
```
$ sudo service httpd restart
```

系統會跑
```
[ec2-user@ip-xxx-xx-xx-172 conf]$ sudo service httpd restart
Stopping httpd:                                            [  OK  ]
Starting httpd:                                            [  OK  ]
[ec2-user@ip-xxx-xx-xx-172 conf]$
```
再連上自己設定的子網域上確認看看有沒有成功囉～

---

以上是今天的假日分享～希望可以幫助到各位^^
**希望大家有什麼想知道的內容，歡迎在底下留言讓我知道，感激不盡！**

## 文後

---

剩10天了.....TAT

---

### 團隊主題連結

> CssCoke - **Amos 老師**
>
> - 影片教學組- **[金魚都能懂的網頁設計入門 - 金魚都能懂了你還怕學不會嗎](https://ithelp.ithome.com.tw/users/20112550/ironman/2072)**
> - Modern Web- **[連續 30 天的超實務網頁設計的垂直置中教學](https://ithelp.ithome.com.tw/users/20112550/ironman/2092)**

> 塔塔默
>
> - Modern Web- **[使用 Leaflet 及 Folium 開啟網頁地圖大門](https://ithelp.ithome.com.tw/users/20112552/ironman/2074)**

---
