## WebSocket API简介 ##

### 产品列表(公开接口) ###

- 参数:<br/>可选参数:       **symbol:产品代码**
- 返回:  
{   
   &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;'data': [{   
		&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;'symbol':  '6001001',     // 产品编号<br/>
		&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;'name': '十八大双联',      // 产品名称<br/>
		&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;'status': 'END_OF_DAY',      // 交易状态<br/>
        &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;'close': '2982',      // 最新价<br/>
		&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;'volume': '7999',      // 成交价<br/>
		&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;'open':  '2524.5',            // 开盘价<br/>
        &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;'high': '3060',              // 最高价<br/>
        &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;'low': '2524.5',             // 最低价<br/>
        &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;'prevClose':' 2805',       // 昨日收盘价<br/>
        &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;'maxPrice': '3085.5',       // 涨停价<br/>
        &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;'minPrice': '2524.5',       // 跌停价<br/>
		&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;'circulation': '47757',        // 流通量<br/>
        &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;'total': '67740',           // 总量<br/>
        &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;'activeBuy': '1909',       // 主买外盘<br/>
        &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;'activeSell': '5990',          // 主卖内盘<br/>
        &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;'withdrawFee': '0',       // 提货费<br/>
        &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;'pic': '/file/resources/img/20160523/image_1463934124996.png',<br/>
        &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;'lastAggTradeId': '116828',   // 上次行情ID<br/>
        &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;'productType': '1',           //产品类型<br/>
        &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;'active': true,              // 产品是否可用<br/>
        &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;'tradedMoney': '2.2481619270000007E7',  // 成交额<br/>
        &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;'lastTradeId': '116961',<br/>
        &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;'tickSize': '0.01',          // 最小价格变动<br/>
        &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;'avgQty': 8765.8
  <br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;}]
<br/>} 
- 说明:<br/>
不传参数**symbol** , 返回所有产品记录记录不包含 **desc** 产品详情字段<br/>
如果提供参数**symbol** , 返回匹配的产品记录包含 **desc** 产品详情字段。
 
 
- 产品状态:<br/>
  NEW: 未成交<br>
  PARTIALLY_FILLED: 部分成交<br>
  REJECTED: 已拒绝<br>
  CANCELED: 已取消<br>
  FILLED: 全部成交<br>
  EXPIRED: 已过期<br>

- 交易状态:<br>
  TRADING: 交易中<br>
  END_OF_DAY: 休市<br>
  BREAK: 停盘

### 请求说明（分时成交）(公开接口) ###

- 参数:<br/>
  symbol产品代码<br/>
  limit (可选)限定返回数据的数量默认和最大都是10<br/>
  startTime (可选)开始时间1970.01.01 开始的毫秒时间包含自身。如1468825537732<br/>
  endTime (可选) 结束时间1970.01.01 开始的毫秒时间包含自身。如1468825537732<br/>
- 说明：<br/>
  **开始时间和结束时间只差不可大于一天**
- 返回:<br/>
[{<br/>
  &nbsp;&nbsp;&nbsp;&nbsp;"a":320,       //交易id<br/>
  &nbsp;&nbsp;&nbsp;&nbsp;"p":"25.95",  //价格<br/>
  &nbsp;&nbsp;&nbsp;&nbsp;"q":"1.0",     //数量<br/>
  &nbsp;&nbsp;&nbsp;&nbsp;"f":320,       //可忽略<br/>
  &nbsp;&nbsp;&nbsp;&nbsp;"l":320,       //可忽略<br/>
  &nbsp;&nbsp;&nbsp;&nbsp;"T":1481162783458,     //交易时间<br/>
  &nbsp;&nbsp;&nbsp;&nbsp;"m":true     //true,卖;false,买<br/>
}]

### 产品行情推送接口 ###

- 返回<br/>
{<br/>
   &nbsp;&nbsp;&nbsp;&nbsp;status code: 200,<br/>
   &nbsp;&nbsp;&nbsp;&nbsp;headers {<br/>
	&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"Content-Type" = "text/html;<br/>
	&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;charset = utf-8";<br/>
    &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Date = "Fri, 17 Feb 2017 02:26:00 GMT";<br/>
    &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Expires = "Thu, 01 Jan 1970 00:00:00 GMT";<br/>
    &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Server = "Jetty(9.3.z-SNAPSHOT)";<br/>
    &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"Set-Cookie" = "mbxSecWssTkn= ";<br/>
    &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"Transfer-Encoding" = Identity;<br/>
&nbsp;&nbsp;&nbsp;&nbsp;}<br/>
}<br/>
得到Set-Cookie;
- websocket<br/>
&nbsp;&nbsp;&nbsp;&nbsp;通过**ws://121.196.244.121:9090/ws/!1dStat**得到websocket地址;<br/>
&nbsp;&nbsp;&nbsp;&nbsp;将第一步中得到的Set-Cookie放到http header: Cookie中, 建立websocket连接;<br/>
&nbsp;&nbsp;&nbsp;&nbsp;推送数据返回<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[[<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"2000007",                //产品编号<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;1488778189855,        //最新价时间<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;1484184600000,        //开盘时间<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;-1,    //休盘时间  (-1 为持续开盘中)<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"256.97",       //最新价<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"2714",         //主动买量<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"697419.77",     //主动买额<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"608",                       //主动卖量<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"156230.89",             //主动卖额<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"256.96",                  //开<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"256.98",                  //高<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"251.00"                   //低<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;]]
