# 自用脚本、重写合集
## 苹果天气空气质量数据[Apple_Weather.js](https://raw.githubusercontent.com/ventusyu/ventus/main/Script/Apple_Weather.js)  
  ```bash
  #!name= Replace Apple Weather with 🇺🇸US @waqi.info
  #!desc=切换空气质量数据源为waqi.info，并更改标准为AQI(US)
  
  [Script]
  http-response ^https?:\/\/weather-data\.apple\.com\/(v1|v2)\/weather.*(?!dataSets=forecastNextHour)(include=.*air_quality.*|dataSets=.*airQuality.*).*(country=[A-Z]{2})?.* script-path=https://raw.githubusercontent.com/ventusyu/ventus/main/Script/Apple_Weather.js, requires-body=true, tag=Apple_Weather
  
  [MITM]
  hostname = %APPEND% weather-data.apple.com
  ```
## 苹果天气质量地图
  ```bash
  #!name= Replace Apple Weather Map with 🇺🇸US @waqi.info
  #!desc=切换空气质量地图数据源为waqi.info，并更改标准为AQI(US)

  [URL Rewrite]
  # Rewrite Apple Weather Air Quality Map
  ^https?:\/\/weather-map\.apple\.com\/(v1|v2)\/mapOverlay\/airQuality\?x=(-?\d+)&y=(-?\d+)&z=(-?\d+).*(country=CN)?.* https://tiles.waqi.info/tiles/usepa-aqi/$4/$2/$3.png?&scale=2&country=US&colorFormat=agr header

  [MITM]
  hostname = %APPEND% weather-map.apple.com, tiles.waqi.info
  ```
## 微信 去除公众号文章底部广告[Wechat.js](https://raw.githubusercontent.com/ventusyu/ventus/main/Script/Wechat.js)
  ```bash
  [Script]
  http-response ^https?:\/\/mp\.weixin\.qq\.com\/mp\/getappmsgad requires-body=1,max-size=0,script-path=https://raw.githubusercontent.com/ventusyu/ventus/main/Script/Wechat.js

  [MITM]
  hostname = mp.weixin.qq.com
  ```
## 京东、淘宝比价[jd_tb_price.js](https://raw.githubusercontent.com/ventusyu/ventus/main/Script/jd_tb_price.js)
  ```bash
  [Script]
  # > 京东App 历史价格 by Small
  京东比价 = type=http-response,requires-body=1,pattern=^https?://api\.m\.jd\.com/client\.action\?functionId=(wareBusiness|serverConfig|basicConfig),script-path=https://raw.githubusercontent.com/ventusyu/ventus/main/Script/jd_tb_price.js
  # > 淘宝App 历史价格 修改Surge语法 by Small
  淘宝比价 = type=http-request,requires-body=1,pattern=^http://.+/amdc/mobileDispatch,script-path=https://raw.githubusercontent.com/ventusyu/ventus/main/Script/jd_tb_price.js
  淘宝比价 = type=http-response,requires-body=1,pattern=^https?://trade-acs\.m\.taobao\.com/gw/mtop\.taobao\.detail\.getdetail,script-path=https://raw.githubusercontent.com/ventusyu/ventus/main/Script/jd_tb_price.js

  [MITM]
  hostname = %INSERT% api.m.jd.com, trade-acs.m.taobao.com
  ```
