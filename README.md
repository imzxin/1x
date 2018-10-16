# 1X交易所 API    

## 开始使用    

所有接口采用HTTP POST方式
    
## 请求交互    

REST访问的根URL：`http://api.1x.hk`     
所有请求基于Http协议，请求头信息中contentType需要统一设置为：`application/json;charset=UTF-8`    
    
请求交互说明    
1. 请求参数：根据接口请求参数规定进行参数封装。    
2. 提交请求参数：将封装好的请求参数通过POST 或GET 方式提交至服务器。    
3. 服务器响应：服务器首先对用户请求数据进行参数安全校验，通过校验后根据业务逻辑将响应数据以JSON格式返回给用户。    
4. 数据处理：对服务器响应数据进行处理。 

## API参考  

### 币币行情 API 

获取1X币币行情数据  

1. Get /market/symbol-thumb    获取1X币币行情

URL `http://api.1x.hk/market/symbol-thumb`

示例  

```
# Request
GET http://api.1x.hk/market/symbol-thumb
# Response
[
    {
        "symbol": "BTC/USDT",
        "open": 6642.93,
        "high": 6672.85,
        "low": 6530.56,
        "close": 6577.81,
        "chg": -0.0099,
        "change": -65.12,
        "volume": 2835.3441,
        "turnover": 562131922.34493053193665190118,
        "lastDayClose": 6643.27,
        "usdRate": 6577.81,
        "baseUsdRate": 1,
        "closeStr": "6577.8100"
    },
    {
        "symbol": "ETH/USDT",
        "open": 228.44,
        "high": 229.46,
        "low": 224.41,
        "close": 226.05,
        "chg": -0.0105,
        "change": -2.39,
        "volume": 39708.3932,
        "turnover": 470128257.53687089848911925123,
        "lastDayClose": 228.44,
        "usdRate": 226.05,
        "baseUsdRate": 1,
        "closeStr": "226.0500"
    },
    {
        "symbol": "WSS/USDT",
        "open": 0,
        "high": 0,
        "low": 0,
        "close": 0.181,
        "chg": 0,
        "change": 0,
        "volume": 0,
        "turnover": 9345.1471,
        "lastDayClose": 0.181,
        "usdRate": 0.181,
        "baseUsdRate": 1,
        "closeStr": "0.1810"
    },
    {
        "symbol": "SCEC/USDT",
        "open": 0,
        "high": 0,
        "low": 0,
        "close": 0.02,
        "chg": 0,
        "change": 0,
        "volume": 0,
        "turnover": 0,
        "lastDayClose": 0.02,
        "usdRate": 0.02,
        "baseUsdRate": 1,
        "closeStr": "0.0200"
    },
    {
        "symbol": "SCEC/ETH",
        "open": 0,
        "high": 0,
        "low": 0,
        "close": 0.0003,
        "chg": 0,
        "change": 0,
        "volume": 0,
        "turnover": 5.0132,
        "lastDayClose": 0.0003,
        "usdRate": 0.063279,
        "baseUsdRate": 210.93,
        "closeStr": "0.00030000"
    }
]
```

返回值说明   

```
symbol: 返回数据时服务器时间
open: 买一价
high: 最高价
low: 最低价
close: 收盘价
chg: 日涨幅
change: 日涨幅（美元）
volume: 数量
turnover: 24小时成交量
lastDayClose: 今日最低价
usdRate: usdt 价格
baseUsdRate: usdt比率
closeStr: 同close
```


2. Get /market/exchange-plate-full   获取1X币币市场深度

URL `http://api.1x.hk/market/exchange-plate-full` 

示例  

```
# Request
GET http://api.1x.hk/market/exchange-plate-full?symbol=SCEC/ETH

# Response
{
    "ask": {
        "minAmount": 16,
        "highestPrice": 0.0029,
        "symbol": "SCEC/ETH",
        "lowestPrice": 0.0003,
        "maxAmount": 6496,
        "items": [
            {
                "price": 0.0003,
                "amount": 2000,
                "priceStr": "0.00030000",
                "amountStr": "2000.00000000"
            },
            {
                "price": 0.00039,
                "amount": 6496,
                "priceStr": "0.00039000",
                "amountStr": "6496.00000000"
            },
            {
                "price": 0.0004,
                "amount": 555,
                "priceStr": "0.00040000",
                "amountStr": "555.00000000"
            },
            {
                "price": 0.000405,
                "amount": 3028,
                "priceStr": "0.00040500",
                "amountStr": "3028.00000000"
            }
        ],
        "direction": "SELL"
    },
    "bid": {
        "minAmount": 0,
        "highestPrice": 0,
        "symbol": "SCEC/ETH",
        "lowestPrice": 0,
        "maxAmount": 0,
        "items": [],
        "direction": "BUY"
    }
}
```

返回值说明   

```
asks :卖方深度
bids :买方深度
```

请求参数    

|参数名|   参数类型|   必填| 描述|
| :-----    | :-----   | :-----    | :-----   |
|symbol|String|是|币对如SCEC/ETH|

3. Get /market/latest-trade/   获取1X币币交易信息(最近成交)

URL `http://api.1x.hk/market/latest-trade/` 

示例  

```
# Request
GET http://api.1x.hk/market/latest-trade/?symbol=BTC/USDT&size=20
# Response
[
    {
        "symbol": "BTC/USDT",
        "price": 6590.55,
        "priceStr": "6590.5500",
        "amount": 0.2361,
        "amountStr": "0.2361",
        "buyTurnover": null,
        "sellTurnover": null,
        "direction": "BUY",
        "buyOrderId": null,
        "sellOrderId": null,
        "time": 1539173421748
    },
    {
        "symbol": "BTC/USDT",
        "price": 6590.55,
        "priceStr": "6590.5500",
        "amount": 0.0005,
        "amountStr": "0.0005",
        "buyTurnover": null,
        "sellTurnover": null,
        "direction": "BUY",
        "buyOrderId": null,
        "sellOrderId": null,
        "time": 1539173417539
    },
    ...
]
```

返回值说明   

```
symbol:交易对
price:成交价格
priceStr: 同price
amount: 交易数量
amount: 同amount
direction: BUY/SELL
time:时间戳(毫秒)
```

请求参数    

|参数名|   参数类型|   必填| 描述|
| :-----    | :-----   | :-----    | :-----   |
|symbol|String|是|币对如BTC/USDT|
|size|Int|否(默认返回最近成交20条)|

4. Get /market/history    获取1X币币K线数据(每个周期数据条数2000左右)

URL `http://api.1x.hk/market/history` 

示例  

```
# Request
GET http://api.1x.hk/market/history?symbol=BTC%2FUSDT&from=1539087024000&to=1539173425196&resolution=1
# Response
[
    [
        1539087060000,
        6644.53,
        6644.85,
        6643.19,
        6644.85,
        0.4854
    ],
    [
        1539087120000,
        6644.86,
        6644.87,
        6644.66,
        6644.8,
        0.8195
    ],
    [
        1539087180000,
        6642.85,
        6644.5,
        6642.77,
        6644.5,
        2.6666
    ],
    [
        1539087240000,
        6644.5,
        6644.76,
        6643.65,
        6643.65,
        2.1213
    ],
    [
        1539087300000,
        6643.45,
        6644.32,
        6641.56,
        6641.56,
        1.2474
    ],
]
```

返回值说明   

```
[
    1539087060000,  时间戳
    6644.53,    开
    6644.85,       高
    6643.19,       低
    6644.85,    收
    0.4854    交易量
]
```

请求参数    

|参数名|   参数类型|   必填| 描述|
| :-----    | :-----   | :-----    | :-----   |
|symbol|String|是|币对如BTC/USDT|
|resolution|String|是|1/5/15/30/60/1D/1W/1M|
|from|Long|是|1533990301000|
|to|Long|是|1539174301575|

### 币币交易 API 

用于1X币币交易  

1. POST /uc/login  用户登陆获取token

URL `http://api.1x.hk/uc/login`      

示例  

```
# Request
POST http://api.1x.hk/uc/login
# Response
{
    "data": {
        "username": "allen",
        "location": {
            "country": "中国",
            "province": null,
            "city": null,
            "district": null
        },
        "memberLevel": 2,
        "token": "xxxxxxxxx",
        "realName": "xxxxx",
        "country": {
            "zhName": "中国",
            "enName": "China",
            "areaCode": "86",
            "language": "zh_CN",
            "localCurrency": "CNY",
            "sort": 0
        },
        "avatar": "xxxx",
        "promotionCode": "U000001q7",
        "id": 1,
        "promotionPrefix": "www.1x.hk",
        "signInAbility": true,
        "signInActivity": false
    },
    "code": 0,
    "message": "SUCCESS"
}
```

返回值说明   

```
 token:个人信息、发单、撤单、吃单等需要
```

请求参数    

|参数名|   参数类型|   必填| 描述|
| :-----    | :-----   | :-----    | :-----   |
|username|String|是|用户名称|
|password|String|是|用户密码|


1. POST /uc/asset/wallet    获取用户资产数据

URL `http://api.1x.hk/uc/asset/wallet`      

示例  

```
# Request
POST http://api.1x.hk/uc/asset/wallet
# Response
{
    "data": [
        {
            "id": 175,
            "memberId": 1,
            "coin": {
                "name": "1X",
                "nameCn": "1X",
                "unit": "1X",
                "status": 0,
                "minTxFee": 0,
                "cnyRate": 1,
                "maxTxFee": 0.0005,
                "usdRate": 1,
                "sgdRate": 0,
                "enableRpc": 1,
                "sort": 11,
                "canWithdraw": 1,
                "canRecharge": 1,
                "canTransfer": 1,
                "canAutoWithdraw": 1,
                "withdrawThreshold": 100,
                "minWithdrawAmount": 5,
                "maxWithdrawAmount": 100,
                "isPlatformCoin": 1,
                "hasLegal": false,
                "allBalance": null,
                "coldWalletAddress": "0x7de593fa4375f6b41f8321f460b8ece64b749b81",
                "hotAllBalance": null,
                "minerFee": 0,
                "withdrawScale": 4,
                "minRechargeAmount": 0,
                "masterAddress": null,
                "maxDailyWithdrawRate": 0
            },
            "balance": 0,
            "frozenBalance": 0,
            "address": "0x1957c1d6d81b1647336399d771e5fee174d5c430",
            "isLock": 0
        },
        ...
    ],
    "code": 0,
    "message": "success"
}
```

返回值说明   

```
coin:币种信息
balance:账户余额
frozenBalance：账户冻结余额
```

请求参数    

|参数名|   参数类型|   必填| 描述|
| :-----    | :-----   | :-----    | :-----   |
|x-auth-token|String|是|token header 参数 |

2. POST /exchange/order/add    下单交易

URL `http://api.1x.hk/exchange/order/add`   

示例  

```
# Request
POST http://api.1x.hk/exchange/order/add
# Response
{"data":"E153917545472286","code":0,"message":"提交成功"}
```

返回值说明   

```
code:0 代表成功返回
data:订单ID
```

请求参数    

|参数名|   参数类型|   必填| 描述|
| :-----    | :-----   | :-----    | :-----   |
|x-auth-token|String|是|token header 参数 |
|symbol|String|是|币对如SCEC/ETH|
|type|String|是|交易类型：限价交易(LIMIT_PRICE) 市价交易(MARKET_PRICE)|
|price|Double|否|下单价格 市价卖单不传price|
|amount|Double|否|交易数量 市价买单不传amount,市价买单需传price作为买入总金额|
|direction|String|是|下单类型 卖（SELL） 买（BUY）|

3. POST /exchange/order/cancel/E153917558982779    撤销订单

URL `http://api.1x.hk/exchange/order/cancel/E153917558982779`   

示例  

```
# Request
POST http://api.1x.hk/exchange/order/cancel/E153917558982779
# Response
{"data":null,"code":0,"message":"提交成功"}

```

返回值说明   

```
code:0 撤单请求成功，等待系统执行撤单；false撤单失败(用于单笔订单)
```

请求参数    

|参数名|   参数类型|   必填| 描述|
| :-----    | :-----   | :-----    | :-----   |
|x-auth-token|String|是|token header 参数 |
|E153917558982779 |String|是|订单编号|



未完待续。。。
