## 本地端測試環境若需要SSL(https)的開發環境

昨天兩邊平台設定好後，想說試寫一下sample的登入，可是居然跑出`請用加密的方式`去載入api...
![img](https://github.com/tinatyc/King-Ironman-30Day-Challenge/blob/master/2018/article/img/day28_5.png?raw=true)

因為現在越來越注重隱私權了，網站送出去的內容如果沒有加密的話，很容易就會被攔截下來內容被看光光，所以許多知名的服務都限定使用https來做連線，不然不是報錯就是警告跑出來...

在今年7月Google也發布Chrome瀏覽器的更新把未加密的網站都列入不安全裡，安全性的觀念在未來會越來越吃重，
所以作為前端開發人員也要懂一些關於SSL的概念，在自己架網站上或者是開發上會有相當大的幫助！

> 相關閱讀
 - [Google 發布 Chrome 68，HTTP 網站全面標記為不安全](http://technews.tw/2018/07/25/google-chrome-68-http-website-not-secure/)
 - [使用 HTTPS 確保網站安全無虞](https://support.google.com/webmasters/answer/6073543?hl=zh-Hant)

今天就來紀錄一下剛剛踩到的雷，把本機的開發環境變成https連線


先說開發環境會因系統別而不同，我的開發環境為

> 系統：MaxOS
開發環境：[MAMP Ver3.4 ](https://www.mamp.info/en/)
![img](https://github.com/tinatyc/King-Ironman-30Day-Challenge/blob/master/2018/article/img/day29_5.png?raw=true)

一開始我是看這一篇youtube教學的：
> [Free HTTPS / SSL Support for MAMP over localhost](https://youtu.be/886Pea2ljm0)

搭配這篇：
> [How to get HTTPS working on your local development environment in 5 minutes](https://medium.freecodecamp.org/how-to-get-https-working-on-your-local-development-environment-in-5-minutes-7af615770eec)

因為設定完還是有`無效的簽證`等問題，這邊要來紀錄一下設定歷程

---

### 1. 建立憑證

- 先創立新資料夾存放SSL的簽證，進入該資料夾底下輸入指令建立`rootCA.key`
```
openssl genrsa -des3 -out 自己的路徑/rootCA.key 2048
```
![img](https://github.com/tinatyc/King-Ironman-30Day-Challenge/blob/master/2018/article/img/day29_4.png?raw=true)
按下enter後，他會出現`Enter pass phrase for rootCA.key`，這邊輸入自己想要的密碼就好了，會在驗證一次你是否輸入正確，建立好後會產生`rootCA.key`檔案
![img](https://github.com/tinatyc/King-Ironman-30Day-Challenge/blob/master/2018/article/img/day29_2.png?raw=true)

- 接下來一樣的路徑，輸入指令建立`rootCA.pem`
```
openssl req -x509 -new -nodes -key rootCA.key -sha256 -days 1024 -out rootCA.pem
```
建立期間他會先問剛剛的密碼，密碼key完後會叫你輸入憑證`相關的資料`，建立好後會產生`rootCA.pem`檔案
![img](https://github.com/tinatyc/King-Ironman-30Day-Challenge/blob/master/2018/article/img/day29_3.png?raw=true)

---

### 2. 建立Domain SSL certificate

- 路徑不變，手動建立檔案，檔案命名為`server.csr.cnf`並寫入
```
[req]
default_bits = 2048
prompt = no
default_md = sha256
distinguished_name = dn

[dn]
C=US
ST=RandomState
L=RandomCity
O=RandomOrganization
OU=RandomOrganizationUnit
emailAddress=hello@example.com
CN = localhost
```
- 路徑不變，手動建立檔案，檔案命名為`v3.ext`並寫入
```
authorityKeyIdentifier=keyid,issuer
basicConstraints=CA:FALSE
keyUsage = digitalSignature, nonRepudiation, keyEncipherment, dataEncipherment
subjectAltName = @alt_names

[alt_names]
DNS.1 = localhost
```
- 路徑不變，在輸入指令建立`server.key`
```
openssl req -new -sha256 -nodes -out server.csr -newkey rsa:2048 -keyout server.key -config <( cat server.csr.cnf )
```
這隻檔會依附在`server.csr.cnf`底下所產生的，所以`server.csr.cnf`有問題的話，就會無法產生`server.key`，這邊要注意！

- 路徑不變，在輸入指令建立`server.crt`
```
openssl x509 -req -in server.csr -CA rootCA.pem -CAkey rootCA.key -CAcreateserial -out server.crt -days 500 -sha256 -extfile v3.ext
```

到這邊為止應該會有8支檔案
- rootCA.key
- rootCA.pem
- rootCA.srl
- server.crt
- server.csr
- server.csr.cnf
- server.key
- v3.ext
![img](https://github.com/tinatyc/King-Ironman-30Day-Challenge/blob/master/2018/article/img/day29_6.png?raw=true)

接下來要設定apache的`httpd.conf`和`httpd-ssl.conf`設定檔
> **記得在變更前請先備份檔案，以免設定錯誤整個壞掉**

- 設定`httpd.conf`

1. 在開放哪個port的地方原本應該是80或是其他的，改成`443 port`
```
Listen 443
```
![img](https://github.com/tinatyc/King-Ironman-30Day-Challenge/blob/master/2018/article/img/day29_7.png?raw=true)

2. LoadModule的地方找到`mod_ssl.so`，如果前面有#的註解記得拿掉
```
LoadModule ssl_module modules/mod_ssl.so
```
3. ServerName的port也要改成443
```
ServerName localhost:443
```
4.開啟讀取httpd-ssl.conf，如果Include前面有#也拿掉
```
# Secure (SSL/TLS) connections
Include /Applications/MAMP/conf/apache/extra/httpd-ssl.conf
```
存檔，接下來要處理`httpd-ssl.conf`

- 設定`httpd-ssl.conf`

![img](https://github.com/tinatyc/King-Ironman-30Day-Challenge/blob/master/2018/article/img/day29_8.png?raw=true)

1.在SSL Virtual Host Context地方修改，`<VirtualHost _default_:443>`為`<VirtualHost *:443>`
```
<VirtualHost *:443>
```
2.**General setup for the virtual host**的地方`ServerName www.example.com:443`改成
```
ServerName localhost:443
```
3.打開SSL Engine
在SSL Engine Switch處，SSLEngine on前面若有#請拿掉，開啟SSLEngine

4.Server Certificate路徑
將Server Certificate的SSLCertificateFile路徑改為當初存放憑證的位置，前面若有#請拿掉
```
SSLCertificateFile "放憑證的路徑/server.crt"
```

5.Server Private Key路徑
將Server Certificate的SSLCertificateFile路徑改為當初存放憑證的位置，前面若有#請拿掉
```
SSLCertificateKeyFile "放憑證的路徑/server.crt"
```
存檔，**重新啟動apache讓設定生效**。

---
   
### 3. 信任憑證

重新開啟瀏覽器後連上localhost還是會有無效的憑證錯誤，接下來要把憑證加入信任裡。
![img](https://github.com/tinatyc/King-Ironman-30Day-Challenge/blob/master/2018/article/img/day29_1.jpg?raw=true)

1.把憑證拖拉到桌面，雙擊兩下開啟"鑰匙圈存取"(MacOS)，再把剛剛的憑證拖進"系統"憑證裡(記得要把左上的鎖打開給權限)。
![img](https://github.com/tinatyc/King-Ironman-30Day-Challenge/blob/master/2018/article/img/day29_1_2.jpg?raw=true)
![img](https://github.com/tinatyc/King-Ironman-30Day-Challenge/blob/master/2018/article/img/day29_9.png?raw=true)

2.打開信任選項，選擇"使用此憑證時：「永遠信任」"選項
![img](https://github.com/tinatyc/King-Ironman-30Day-Challenge/blob/master/2018/article/img/day29_10.png?raw=true)

--- 

### 4. 完成


打開`https:localhost/`，憑證已生效，代表完成，已經可以用https來做連線了～
![img](https://github.com/tinatyc/King-Ironman-30Day-Challenge/blob/master/2018/article/img/day29_11.png?raw=true)
![img](https://github.com/tinatyc/King-Ironman-30Day-Challenge/blob/master/2018/article/img/day29_12.png?raw=true)
   
---

其實除了這樣設定外，還有別種比較快速的作法，像是使用ngrok等...如果需要的人可以參考看看
我做到現在會有一個新問題，就是`https://localhost`下會找不到路徑...Orz
先做到這邊了，今天實在太累了狂截圖做圖....Orz

**希望大家有什麼想知道的內容，歡迎在底下留言讓我知道，感激不盡！**    
    

## 文後

---

啊啊～第29天啦～～可是雪恥戰還沒寫完.....

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
