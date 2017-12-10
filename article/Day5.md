## 上班一個禮拜，終於到星期五了Orz 做一些小東西好了....
假日在寫進階一點的應用....Sorry....

---

昨兒做出我們基本的地圖之後 [傳送門](https://tinatyc.github.io/King-Ironman-30Day-Challenge/page/Day_2/)
如果覺得很無聊、單調，這些Maps API都可以做的到你想要的樣子～

**那今天就來做自訂的Marker練習吧～**

---
> #### 起始式

如果沒有另外設定的話，呼叫`google.maps.Marker`的API
基本google提供的地圖Marker(標記)就長這樣↓
![https://github.com/tinatyc/King-Ironman-30Day-Challenge/blob/master/page/day3/sample_icon/default_marker.png?raw=true](https://github.com/tinatyc/King-Ironman-30Day-Challenge/blob/master/page/day3/sample_icon/default_marker.png?raw=true)


那你一定想：
#### 大家都這樣很無聊啊～我可不可以換我自己的圖或Icon上去啊？
> **當然可以囉～今天就把Marker換成我們想要的樣子～**


提供一個可以下載Free ICON的網站，雖然好像只能下載72px的，但拿來當文章素材應該還蠻夠用的～
>  iconshock [https://www.iconshock.com/](https://www.iconshock.com/)

`想練習的話可以先下載幾個來，我先下載了4個ICON待會來做示範`
![https://github.com/tinatyc/King-Ironman-30Day-Challenge/blob/master/page/day3/sample_icon/pointer.png?raw=true](https://github.com/tinatyc/King-Ironman-30Day-Challenge/blob/master/page/day3/sample_icon/pointer.png?raw=true)![https://github.com/tinatyc/King-Ironman-30Day-Challenge/blob/master/page/day3/sample_icon/star.png?raw=true](https://github.com/tinatyc/King-Ironman-30Day-Challenge/blob/master/page/day3/sample_icon/star.png?raw=true)![https://github.com/tinatyc/King-Ironman-30Day-Challenge/blob/master/page/day3/sample_icon/wizard.png?raw=true](https://github.com/tinatyc/King-Ironman-30Day-Challenge/blob/master/page/day3/sample_icon/wizard.png?raw=true)![https://github.com/tinatyc/King-Ironman-30Day-Challenge/blob/master/page/day3/sample_icon/zoom.png?raw=true](https://github.com/tinatyc/King-Ironman-30Day-Challenge/blob/master/page/day3/sample_icon/zoom.png?raw=true)

---
> #### 你有Free Style嗎？

昨天沒有講到Marker這個API，今天來講一下～
具 Google Maps API 所[簡介](https://developers.google.com/maps/documentation/javascript/markers)的
> - `標記能識別地圖上的位置`。根據預設，標記使用標準影像。`標記可以顯示自訂影像，在這種情況下，它們通常被稱為「圖示」`。標記和圖示是 Marker 類型的物件。如果要設定自訂圖示，您可以在標記的建構函式內設定。
> - 廣泛來說，`標記是一種疊加層`。
> - `標記是以提供互動性為前提而設計的`。

所以標記是可以`增加使用者體驗的(UX)`，**譬如**：點擊標記顯示訊息、拖曳標記得到地方訊息等...
30天的應用會慢慢的一步一步實現這些功能，今天我們先來改變標記的樣式！

沿用上一篇的JS繼續實作[Here](https://ithelp.ithome.com.tw/articles/10190905)

看到Marker的部分
```
var marker = new google.maps.Marker({
    position: 放標記的經緯度,
    map: 你的地圖
});
```

可以看到[reference](https://developers.google.com/maps/documentation/javascript/3.exp/reference#Marker) Marker class的部分，`google.maps.Marker`這樣就代表你有呼叫一個marker的API。
想要Marker做什麼，下面有一些Methods可以看看他可以作一些什麼事情，初學者可以這樣練習看看...

![https://ithelp.ithome.com.tw/upload/images/20171208/20103130kEUKFHvqYv.png](https://ithelp.ithome.com.tw/upload/images/20171208/20103130kEUKFHvqYv.png)

了解Marker後，我們就可以來自訂他的樣式～
一樣是呼叫Marker API，Marker的性質是Object，在建構式裡新增一個`icon`的屬性

```

var marker = new google.maps.Marker({
  position: position,
  icon: ←這個,
  map: map,
});

```
那Google的範例是設了幾個經緯度，用陣列的方式依序用forEach印出來位置
~~ 我就不這麼做了XD，練習要創新啊～ ~~

> 練習Time

我是設定一個初始位置，因為icon我抓了四個，那我們迴圈就跑四次就好了～
 - 使用for迴圈
 - 每跑一次經度和緯度各減0.005度，並且呼叫Marker API
 - icon屬性每次都給他不一樣的圖

**初始位置**
Lat：25.046891
Lng：121.516602
Marker：![https://github.com/tinatyc/King-Ironman-30Day-Challenge/blob/master/page/day3/sample_icon/default_marker.png?raw=true](https://github.com/tinatyc/King-Ironman-30Day-Challenge/blob/master/page/day3/sample_icon/default_marker.png?raw=true)

**第一次迴圈**
Lat：25.051891
Lng：121.521602
Marker：![https://github.com/tinatyc/King-Ironman-30Day-Challenge/blob/master/page/day3/sample_icon/pointer.png?raw=true](https://github.com/tinatyc/King-Ironman-30Day-Challenge/blob/master/page/day3/sample_icon/pointer.png?raw=true)

**第二次迴圈**
Lat：25.056891
Lng：121.526602
Marker：![https://github.com/tinatyc/King-Ironman-30Day-Challenge/blob/master/page/day3/sample_icon/star.png?raw=true](https://github.com/tinatyc/King-Ironman-30Day-Challenge/blob/master/page/day3/sample_icon/star.png?raw=true)

**第三次迴圈**
Lat：25.061891
Lng：121.531602
Marker：![https://github.com/tinatyc/King-Ironman-30Day-Challenge/blob/master/page/day3/sample_icon/wizard.png?raw=true](https://github.com/tinatyc/King-Ironman-30Day-Challenge/blob/master/page/day3/sample_icon/wizard.png?raw=true)

**第四次迴圈**
Lat：25.066891
Lng：121.536602
Marker：![https://github.com/tinatyc/King-Ironman-30Day-Challenge/blob/master/page/day3/sample_icon/zoom.png?raw=true](https://github.com/tinatyc/King-Ironman-30Day-Challenge/blob/master/page/day3/sample_icon/zoom.png?raw=true)

我們的成品～
![https://media.giphy.com/media/3oxHQpAnv5lx4tuzKM/giphy.gif](https://media.giphy.com/media/3oxHQpAnv5lx4tuzKM/giphy.gif)
giphy大圖連結 [http://gph.is/2B8l2He](http://gph.is/2B8l2He)

現在我們做到`多個Marker的功能`、`Marker變成我們自訂的樣式`了～
**下一次來賦予Marker實質的互動吧～**
**先在此斷尾囉.....**

---

> 附上完整程式碼

**Demo連結：**[https://tinatyc.github.io/King-Ironman-30Day-Challenge/page/Day_2/](https://tinatyc.github.io/King-Ironman-30Day-Challenge/page/Day_2/)
```