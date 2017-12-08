## 今天終於要來Coding啦～

---

有了API Key之後，在Day2時有說到Google Maps API頁面有一些範例可以搭配使用[傳送門](https://developers.google.com/maps/documentation/javascript/tutorial)
**今天就來創建一個有Marker的地圖吧～**
~~終於啊~~![/images/emoticon/emoticon02.gif](/images/emoticon/emoticon02.gif)

---

> #### 起始式

參照[Day2](https://ithelp.ithome.com.tw/articles/10190718)結尾的程式碼，我們要先引入Google API的網址，接著把API Key嵌入到網址**key參數**裡~
**即`key="API金鑰"`**

```
<script src="https://maps.googleapis.com/maps/api/js?key=YOUR_API_KEY&callback=initMap"
    async defer></script>
```

> #### Hello Maps

Google提供了簡單的範例，那我們就用範例稍微作修改，凡是從複製開始學習嘛XD～

我的程式練習方法是假設自己是客戶，`**練習給自己訂一個需求目標來實作練習**：`
假設K客戶的需求是：
- 網頁裡要一個Title "King Tzeng的鐵人地圖"
- 地圖要寬要滿版、高佔網頁的四分之三
- 網頁的下半部顯示地圖
- 初始地圖位置顯示台北車站的位置

那我們來搭配範例來Coding K客戶的需求～

**1.網頁裡要一個Title "King Tzeng的鐵人地圖"**

這個需求超簡單，就是在Html寫一個H1的標題即
```
<h1>King Tzeng的鐵人地圖</h1>
```
**2.地圖要寬要滿版、高佔網頁的四分之三**

Day2有說到一定要給地圖一個高度和寬度，所以我們就寫在CSS裡面
```
  #map {
  	height: 75%;
  	width: 100vw;
   }
```
**3.網頁的下半部顯示地圖**

這一點的話就要使用到CSS的定位了，~~因為現在工作比較少寫CSS，有錯請鞭一下~~...
如果是我的話會先在外層包一個`div`命名為body，用`相對定位(position: relative;)`
**先設定好頁面的寬高**

父層是`div id=body`接下來把h1和#map包進去成為`子層`，使用`絕對定位(position: absolute;)`來定位。

**html部分即**
```
<body>
	<div class="body">
		<h1>King Tzeng的鐵人地圖</h1>
		<div id="map"></div>
	</div>
</body>
```
**CSS部分**
```
html{
	height: 100%;
	width: 100%;
}
#body{
	position: relative;	/*相對定位*/
	height: 100%;
	width: 100vw;
	top: 0;
	left: 0;
}
#map {
	position: absolute;
	top: 25%;	/*地圖佔頁面的3/4，即 頁面高 - 地圖高 = 定位點高度 (100%-75%=25%) */
	left: 0;
    height: 75%;	/*地圖高*/
    width: 100vw;
}
```
這邊就不深入討論CSS了，如果想學CSS3我推薦我的師父AMOS老師～一聽觀念就秒懂啊
好啦～我們重點放在API應用上XD

**4.初始地圖位置顯示台北車站的位置**

在API呼叫地圖初始化時，一定要給Google一組經緯度，他才能正常的顯示！

> ##### 小Tip:特定位置的經緯度要怎麼找呢？

到Google地圖搜尋你要的位置，網址列就有經緯度囉～
![https://ithelp.ithome.com.tw/upload/images/20171207/20103130gCbjKdw2y4.png](https://ithelp.ithome.com.tw/upload/images/20171207/20103130gCbjKdw2y4.png)

**JavaScript部分**

```
function initMap() {
    var Station_latlng = { lat: 25.0501101, lng: 121.5255337 };	// 台北車站的經緯度
    var map = new google.maps.Map(document.getElementById('map'), {
        zoom: 11,	//放大的倍率
        center: Station_latlng	//初始化的地圖中心位置
    });

//--------下面是呼叫一個新marker------

    var marker = new google.maps.Marker({
        position: Station_latlng,	//marker的放置位置
        map: map //這邊的map指的是第四行的map變數
    });

}
```
> #### 結果呈現：

**一個動態的地圖就出現啦～**  (本來要錄gif，可是我的軟體怪怪的...Orz

![https://ithelp.ithome.com.tw/upload/images/20171207/201031306LZoW1Qza4.png](https://ithelp.ithome.com.tw/upload/images/20171207/201031306LZoW1Qza4.png)

這是最`基本的地圖示範`，當然還可以在裝飾一下頁面讓變好看一點～
**地圖還有很多很好玩的東西可以操作，大家可以先作一個出來玩玩看～**

**待下回我們再來實作別的項目吧～今天先到此結束囉～（傳說中的又要斷尾了...**

---

> 附上完整程式碼

**Demo連結：**[https://tinatyc.github.io/King-Ironman-30Day-Challenge/page/Day_2/](https://tinatyc.github.io/King-Ironman-30Day-Challenge/page/Day_2/)
```
<!DOCTYPE html>
<html lang="zh-tw">

<head>
    <meta charset="utf-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <title>King Tzeng的鐵人地圖</title>
    <style type="text/css" media="screen">
    html {
        height: 100%;
        width: 100%;
    }

    #map {
        position: absolute;
        top: 25%;
        left: 0;
        height: 75%;
        width: 100vw;
    }

    #body {
        height: 100%;
        width: 100vw;
        position: relative;
        top: 0;
        left: 0;
    }
    </style>
</head>

<body>
    <div class="body">
        <h1>King Tzeng的鐵人地圖</h1>
        <div id="map"></div>
    </div>
    <script src="https://ajax.googleapis.com/ajax/libs/jquery/1.11.3/jquery.min.js"></script>
    <script>
    function initMap() {
        var Station_latlng = { lat: 25.046891, lng: 121.516602 }; // 台北車站的經緯度
        var map = new google.maps.Map(document.getElementById('map'), {
            zoom: 14, //放大的倍率
            center: Station_latlng //初始化的地圖中心位置
        });

        //--------下面是呼叫一個新marker------

        var marker = new google.maps.Marker({
            position: Station_latlng, //marker的放置位置
            map: map //這邊的map指的是第四行的map變數
        });

    }
    </script>
    <script async defer src="https://maps.googleapis.com/maps/api/js?key=AIzaSyC_Za7RqKvUuEg2Nln0EcpUVN3k2fZtDuE&callback=initMap">
    </script>
</body>

</html>

```
---
## 文後-

可能還有很多東西還沒講到，小妹之後會陸續補上的！！
實作以後都會放在我的GitHub上面喔～第一次用GitHub Page請多多指教～
[https://tinatyc.github.io/King-Ironman-30Day-Challenge/](https://tinatyc.github.io/King-Ironman-30Day-Challenge/)

同步刊登於[King 學習前端之人生](https://kingweblife.blogspot.com/)
[ 著作權為King Tzeng所有，請勿抄襲或致敬＝口＝]
