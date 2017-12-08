## 開始講述一些Google Maps APIs的串接應用
---

因為在工作上需要撰寫一些與地圖相關的應用（~~詳情請看上一篇的結尾XD~~，
所以學會了大量的Google Map的各種應用方法，此篇主要講述申請API KEY的流程與Map基本的串接應用
就搬張板凳坐下來慢慢看吧～![/images/emoticon/emoticon25.gif](/images/emoticon/emoticon25.gif)
---
> ### 平台先以Web來作示範

首先我們要先到 https://developers.google.com/maps/
選擇我們需要什麼平台的api，做申請api key的動作～

`如果用錯了api key服務就會起不來，啟用api key扮演重要的角色，這邊需要注意一下～`

那我們這次就選擇用Web來作開發，所以在頁面選擇`Web`後，Google會讓你選擇需要的相關API集～
個人我是用JS在做開發故選擇`Google Maps JavaScript API`

![https://ithelp.ithome.com.tw/upload/images/20171205/20103130uCIJ8NZknX.png](https://ithelp.ithome.com.tw/upload/images/20171205/20103130uCIJ8NZknX.png)
![https://ithelp.ithome.com.tw/upload/images/20171205/20103130x02aLmDHEN.png](https://ithelp.ithome.com.tw/upload/images/20171205/20103130x02aLmDHEN.png)

今天的目標～先把基本的地圖先做出來就好，選擇任一個範例，就不截圖囉XD（~~好懶~~XD
我是選擇`新增含標記的 Google 地圖到您的網站`的這個範例

因為是最基本的，所以Google其實也寫的蠻仔細的～step by step教你從零到有一個地圖出來
那程式要好基本功要打好，我也再做一次放上來給大家鞭一下XD
---

> #### 來圖解一下頁面
![https://ithelp.ithome.com.tw/upload/images/20171205/20103130vfVauUw6qW.png](https://ithelp.ithome.com.tw/upload/images/20171205/20103130vfVauUw6qW.png)
有些範例要到英文版的MAP的頁面去看，應用與講解的比較多（經驗談~

#### 那就不廢話了XD，開始實作

由於Google教的蠻仔細了，我說一些比較需要`注意`的！可以搭配Google範例一起觀看～

1.&2.建立HTML頁面並嵌入JS

```
<!DOCTYPE html>
<html>
  <head>
    <style>
      #map {
        height: 400px;
        width: 100%;
       }
    </style>
  </head>
  <body>
    <h3>My Google Maps Demo</h3>
    <div id="map"></div>
    <script>
      function initMap() {
        var uluru = {lat: -25.363, lng: 131.044};
        var map = new google.maps.Map(document.getElementById('map'), {
          zoom: 4,
          center: uluru
        });
        var marker = new google.maps.Marker({
          position: uluru,
          map: map
        });
      }
    </script>
    <script async defer
    src="https://maps.googleapis.com/maps/api/js?key=YOUR_API_KEY&callback=initMap">
    </script>
  </body>
</html>
```
直接看[第二步](https://developers.google.com/maps/documentation/javascript/adding-a-google-map)的程式碼
需要注意的有
- `CSS一定要給地圖一個寬度和高度`，不然他會不知道要給你多大張的地圖~
- html裡，`<div id="map"></div>`是**必要的元素**！
- `<script async defer
    src="https://maps.googleapis.com/maps/api/js?key=YOUR_API_KEY&callback=initMap">
    </script>`
    一定要掛載於你要讓地圖出現的頁面中！並**置入你申請回來的API Key也就是金鑰！**(稍候解說)

- `initMap()`函式代表**初始化地圖**，`地圖在初始化的過程中一定要給一組經緯度`，讓他來作初始化的動作！

- 掛載的JS裡有一個函數`callback=initMap`，原理是他先去請求你的API Key也就是金鑰
	> 1. 第一點正不正確
	> 2. 配額到了沒，這邊解說一下，因為Google APIs是要收費的，但是都請求額度～如果不是大量很誇張的用，相信我都很夠用了...
	> 3. 如果都正確配額也OK，`callback`便會呼叫`initMap()`函式，~~開始展開你人生的地圖吧~~在函式裡就可以作很多事情，以後再慢慢說道～（XD

#### 以上幾個概念和該注意的事項，和大家分享～

#### 今天先這樣斷尾好了，本來想實作一個地圖的，發現我好碎念喔XD
---

## 文後 -

因為想講解很多東西，結果講不完....(被打)![/images/emoticon/emoticon21.gif](/images/emoticon/emoticon21.gif)

同步刊登於[King 學習前端之人生](https://kingweblife.blogspot.com/)
[ 著作權為King Tzeng所有，請勿抄襲或致敬＝口＝]
