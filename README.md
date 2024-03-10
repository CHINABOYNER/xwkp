# 接口文档

变动说明：梁靖松

- 修改了获取聊天大厅接口的返回值：增添url属性，规范返回格式
- 修改了通过用户id和指定用户的聊天记录接口：规范返回值格式

**baseURL发生变动**

## 登录接口

https://xwkp.bitstone14.xyz/xwkp/login

参数：

key: username  value: string

key: password   value: string

## 登录者查看发布订单接口

先登录后才能查看，无需参数

快递：https://xwkp.bitstone14.xyz/xwkp/orderexpress

外卖：https://xwkp.bitstone14.xyz/xwkp/ordersendfood

其他：https://xwkp.bitstone14.xyz/xwkp/orderother

## 通过接单者学号查看订单接口

参数：

key：ACusername

value：学号（string）

快递：https://xwkp.bitstone14.xyz/xwkp/orderexpressac

外卖：https://xwkp.bitstone14.xyz/xwkp/ordersendfac

其他：https://xwkp.bitstone14.xyz/xwkp/orderotherac





## 修改订单完成状态接口

先登录后才能有效访问该接口

参数：

| key     | value type | 说明     |
| ------- | ---------- | -------- |
| orderId | string     | 订单号   |
| status  | int        | 订单状态 |

规定：status 1表示已发布    2表示已接单    3表示配送中    4表示已完成

快递：https://xwkp.bitstone14.xyz/xwkp/setorderexpress

外卖：https://xwkp.bitstone14.xyz/xwkp/setordersendfood

其他：https://xwkp.bitstone14.xyz/xwkp/setorderother



## 获取未完成订单接口（处于已发布状态的订单）

先登录后才能有效访问该接口，无需参数

快递：https://xwkp.bitstone14.xyz/xwkp/getnotfinishede

外卖：https://xwkp.bitstone14.xyz/xwkp/getnotfinisheds

其他：https://xwkp.bitstone14.xyz/xwkp/getnotfinishedo



## 用户修改信息接口

先登录后才能有效访问该接口

https://xwkp.bitstone14.xyz/xwkp/setuserinformation

参数：

| key             | value type | 说明     |
| --------------- | ---------- | -------- |
| name            | string     | 姓名     |
| gender          | int        | 1男，2女 |
| telephoneNumber | string     | 电话号码 |

## 获取用户信息接口

先登录后才能有效访问该接口，无需参数，返回的是当前登录者的信息

https://xwkp.bitstone14.xyz/xwkp/getuserinformation

返回值

| key             | value type | 说明                                |
| --------------- | ---------- | ----------------------------------- |
| name            | string     | 姓名                                |
| gender          | stting     | 男或女(默认未知)                    |
| telephoneNumber | string     | 电话号码                            |
| url             | string     | 头像的url，如果没有设置，则获取不到 |

## 设置用户头像接口

https://xwkp.bitstone14.xyz/xwkp/upload

参数：

| key  | value type | 说明       |
| ---- | ---------- | ---------- |
| file | file       | 上传的图片 |

返回值：

{"status":"0/1"} //0代表上传失败，1代表上传成功

## 发布订单接口

**发布快递接口**

先登录后才能有效访问该接口

https://xwkp.bitstone14.xyz/xwkp/releaseorderexpress

参数

| key             | value type | explanation |
| --------------- | ---------- | ----------- |
| receiverName    | string     | 收货人姓名  |
| address         | string     | 收货地址    |
| telephoneNumber | string     | 收货人电话  |
| site            | string     | 快递站点    |
| pickUpCode      | string     | 取件码      |
| money           | double     | 悬赏金额    |
| remarks         | string     | 备注        |

**发布外卖接口**

先登录后才能有效访问该接口

https://xwkp.bitstone14.xyz/xwkp/releaseordersf

参数

| key             | value type | explanation |
| --------------- | ---------- | ----------- |
| receiverName    | string     | 收货人姓名  |
| address         | string     | 收货地址    |
| telephoneNumber | string     | 收货人电话  |
| site            | string     | 取餐站点    |
| money           | double     | 悬赏金额    |
| remarks         | string     | 备注        |

**发布其他需求的接口**

先登录后才能有效访问该接口

https://xwkp.bitstone14.xyz/xwkp/releaseorderother

| key             | value type | explanation |
| --------------- | ---------- | ----------- |
| receiverName    | string     | 收货人姓名  |
| address         | string     | 收货地址    |
| telephoneNumber | string     | 收货人电话  |
| money           | double     | 悬赏金额    |
| need            | string     | 需求        |
| remarks         | string     | 备注        |



## 通过订单号查询订单信息的接口

https://xwkp.bitstone14.xyz/xwkp/allorder

说明：传入一个参数（订单号），会返回订单的信息，3种类型的订单返回数据会不一样，但是都会有一个一样的键值对用于区分订单类型

​			**区分类型的key为flag，value规定 1为快递订单，2为外卖订单，3为其他类型订单**



## 删除订单接口

先登录后才能有效访问该接口

https://xwkp.bitstone14.xyz/xwkp/deleteorder

通过订单号删除订单

**注意：当且仅当订单的状态码为1时可以删除**

参数：

key：orderId                   value type：string                          explanation：订单号

# WebSocket

wss://chat.bitstone14.xyz/websocket

第一次连接成功时，需要给服务端发送消息

```json
{
    "username":"username",
	"flag":"1"
}
```

| key      | value type | explanation  |
| -------- | ---------- | ------------ |
| username | string     | 当前用户的id |
| flag     | string     | 字符1        |



每一条消息的格式

```json
{
	"fromname":"user1",
    "toname":"user2",
    "message":"你好啊user2，我是user1",
    "flag":"2"
}
```

| key      | value type | explanation                                                |
| -------- | ---------- | ---------------------------------------------------------- |
| fromname | string     | 发送者的id                                                 |
| toname   | string     | 接收者的id                                                 |
| message  | string     | 发送的内容                                                 |
| flag     | string     | 数据包的标识，2表示该数据包是用户发送的文本消息，3表示图片 |



聊天记录

```json
{
	"ordernum":"信息编号（数字）",
    "sender":"发送者id",
    "receiver":"接收者id",
    "message":"聊天信息",
    "flag":"标志（数字）",
    "time":"消息产生时间"
}
```

| key      | value type | explanation                                  |
| -------- | ---------- | -------------------------------------------- |
| ordernum | int        | 聊天信息编号，按时间顺序递增                 |
| sender   | string     | 发送者id                                     |
| receiver | string     | 接收者id                                     |
| message  | string     | 发送的消息内容                               |
| flag     | int        | 2表示该数据包是用户发送的文本消息，3表示图片 |
| time     | string     | 消息发送的时间                               |



### 通过当前用户id查找与当前用户有聊天记录的人(聊天大厅)

注意：我给出来的顺序都是按照时间排好序的，按时间的降序（最近一次聊天的放前面）

这个接口只能在正常建立websocket连接后的账号才能使用，否则可能会因为查询不到这个人聊天表而报错

usl:  https://chat.bitstone14.xyz/getChatHall

交互格式：application/json

请求参数说明：

```json
{
    "username":"admin2"
}
//username   String类型   表示当前用户的账号
```

返回值说明：

```json
{
    "code": 21200,
    "msg": "请求成功",
    "data": [
        {
            "ordernum": 1,
            "connector": "admin",
            "time": "2023-08-14 16:32:54.0",
            "connectorURL": "http://139.9.188.179/imgs/2023/08/7653777259b78de6.jpg"
        }
    ]
}
```



### 通过用户id查找和指定用户的聊天记录

注意：我给出来的顺序都是按照时间排好序的，按时间的升序（最近的聊天记录放后面）

* 当前用户可能作为发送者出现，也有可能作为接收者出现；
* 同样，指定用户可能作为发送者出现，也有可能作为接收者出现；

usl:  https://chat.bitstone14.xyz/getChatRecords

交互格式：application/json

请求参数说明：

```json
{
    "username":"202121132185",
    "otherid":"202121132186"
}
/**
username  String类型  表示当前用户的账号
otherid   String类型  表示和他聊天的人的账号
*/
```

返回值说明：

```json
{
    "code": 21200,
    "msg": "请求成功",
    "data": [
        {
            "ordernum": 1,
            "sender": "admin",
            "receiver": "admin2",
            "message": {
                "fromname": "admin",
                "toname": "admin2",
                "message": "你好",
                "flag": "2"
            },
            "flag": 2,
            "time": "2023-08-14 16:32:13"
        }
    ]
}
```

