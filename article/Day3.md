## 上篇講述一些Google Maps APIs的概念
---

接續上一篇解說到一些串接地圖時必須注意的事項，今天繼續創造我們人生的地圖XD![/images/emoticon/emoticon30.gif](/images/emoticon/emoticon30.gif)
昨天說到使用Google APIs的請求不是免費的，都有一定的配額給你使用，每個API配額也都不一樣
~~使用前請詳閱公開說明書~~(被打XD

**那今天的目標來一步一步申請API，創造一個地圖出來！**

---

> #### 創立專案

要用Google的服務，前提是要有Google的帳號
想必現代人都一定有一個以上的帳號，沒有的話快去辦一個吧～

登入Google後，請先到這邊(https://console.developers.google.com/)
![https://ithelp.ithome.com.tw/upload/images/20171206/20103130XNvpC3VnkG.png](https://ithelp.ithome.com.tw/upload/images/20171206/20103130XNvpC3VnkG.png)
這是我們未來可以監控API使用狀況的主控台，舉凡`監控流量、更換金鑰、查看請求額度`等動作都可以在這裡做操作~
`如果沒有專案的人，請先建立新專案`，我這邊也用鐵人賽當範例來創造一個專案～

> **建立專案** -> **建立**

![https://ithelp.ithome.com.tw/upload/images/20171206/20103130uEJiiGXDK3.png](https://ithelp.ithome.com.tw/upload/images/20171206/20103130uEJiiGXDK3.png)

> **請填入專案名稱**

在此注意`專案名稱`日後是`可以更改`的，但是`專案ID`建立專案成功後就`無法更變`了
如果有用到專案id的人，這邊需要多注意一下！（目前我是沒有用到啦～）
![https://ithelp.ithome.com.tw/upload/images/20171206/20103130V6WMkIJx7U.png](https://ithelp.ithome.com.tw/upload/images/20171206/20103130V6WMkIJx7U.png)

按建立之後，Google會跑一下，你就可以看到你的專案建立成功的畫面了～
框框裡是你的專案，要注意一點就是`每個專案啟用的金鑰都是獨立的金鑰，請求配額也是各自算各自算的`。
![https://ithelp.ithome.com.tw/upload/images/20171206/20103130P7bOybyrPl.png](https://ithelp.ithome.com.tw/upload/images/20171206/20103130P7bOybyrPl.png)

> #### 申請API啟用服務

現在要來申請`Google Maps JavaScript API`的服務，到剛剛的dashboard按下[ `啟用API和服務` ]
Google會連結到眾多功能的API程式庫頁面，而我們需要用到地圖的功能所以點擊`Google Maps JavaScript API`
下一頁是解說頁面按下`啟用`，Google便幫你開通這項功能~
不過還有幾點需要設定的，繼續GOGO~![/images/emoticon/emoticon08.gif](/images/emoticon/emoticon08.gif)

![https://ithelp.ithome.com.tw/upload/images/20171206/20103130ElyJKXktOz.png](https://ithelp.ithome.com.tw/upload/images/20171206/20103130ElyJKXktOz.png)
![https://ithelp.ithome.com.tw/upload/images/20171206/201031306t3l4hweCH.png](https://ithelp.ithome.com.tw/upload/images/20171206/201031306t3l4hweCH.png)

> #### 設定服務以及建立憑證

啟用服務後，還需要建立憑證也就是`API金鑰`(重要)，拿著這把鑰匙你才能去開啟世界的地圖啊～
點選建立憑證之後，因為接下來就是一直點下一步，所以我就用截圖來說明了～
![https://ithelp.ithome.com.tw/upload/images/20171206/20103130vkpMzEBIYV.png](https://ithelp.ithome.com.tw/upload/images/20171206/20103130vkpMzEBIYV.png)
![https://ithelp.ithome.com.tw/upload/images/20171206/2010313060xTAMFe1T.png](https://ithelp.ithome.com.tw/upload/images/20171206/2010313060xTAMFe1T.png)
![https://ithelp.ithome.com.tw/upload/images/20171206/20103130PXF1W2reG7.png](https://ithelp.ithome.com.tw/upload/images/20171206/20103130PXF1W2reG7.png)
![https://ithelp.ithome.com.tw/upload/images/20171206/201031300Ho8hteQ7v.png](https://ithelp.ithome.com.tw/upload/images/20171206/201031300Ho8hteQ7v.png)
完成後，`Google就會給你一組API金鑰，就是我有馬賽克的地方，那這組鑰匙要自己保存好不要外洩`～
**你總不會把你家的鑰匙丟在外面，這樣別人就可以拿你家的鑰匙去開你家的門啊～**
（這要報警處理了XD

好吧～萬一不幸你發現你明明沒用服務，但為什麼還是`一直有請求數`或者`請求數爆高`....
那就按下金鑰旁邊的那一枝筆吧！
`重新產生一組金鑰，記得你程式端的金鑰也要換成重新產生的這組`，不然服務是起不來的喔！

關於金鑰的安全性，可以到剛剛的編輯金鑰頁面來設定金鑰的限制
像Web服務的話你又有Domain就可以設定`HTTP 參照網址 (網站)`這項限制，之後會我們部屬到網站上的時候會舉例說明。

#### 今天想偷懶到此斷尾了XD (謎之音：蝦咪....ಠ_ಠ)

那就有看這篇文章的看官們，想練習的話可以先去申請看看喔～哈哈
我們明天見了～(ㆆᴗㆆ)
---
## 文後-

這個進度這樣要什麼時候才有地圖出現(;´༎ຶД༎ຶ`)

同步刊登於[King 學習前端之人生](https://kingweblife.blogspot.com/)
[ 著作權為King Tzeng所有，請勿抄襲或致敬＝口＝]
