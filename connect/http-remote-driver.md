# HTTP Remote Driver

HTTP 远程驱动是接入 Homebase 推荐的方式， 本地 Android Native Driver， Rokid Skill 接入都使用 HTTP 的驱动协议，也是 SSDP 局域网发现的设备除了 TCP 控制协议之外的另外一种支持的协议。

你可以通过 开发者驱动， 或 [rhome 命令][rhome] 来开发和调试 HTTP Driver


## 通用格式

HTTP 远程驱动使用 JSON 作为数据交换格式， 执行成功会返回如下字段：

**成功返回**

- `status` {int} 成功返回必须为 0
- `data` {any} 执行结果, 根据接口类型返回不同的结果


```json
{
  "status": 0,
  "data": {
    "some": "data"
  }
}
```

**错误返回**

- `status` {Int} 必须 大于0 的正整数
- `message` {String} status > 0 时必选，错误描述
- `errorName` {String} 可选， Homebase 标准错误名，

```json
{
  "status": 1,
  "message": "time out",
  "errorName": null
}
```

## 标准接口

### 1. `POST /list` 设备搜索

搜索给定用户账号下的所有设备， 包括虚拟设备， 子设备

参数：

- userAuth {Object} 用户授权信息

```json
{
  "userAuth": {
    "userId": "",
    "userToken": ""
  }
}
```


**返回值**

标准化后的 [Device][device] 列表 { Array }：

示例

```json
{
  "status": 0,
    "data": [
      {
        "type": "light",
        "deviceId": "123123",
        "name": "灯灯灯灯",
        "actions": {
          "switch": ["on", "off"]
        },
        "state": {
          "switch": "off"
        }
      }
    ]
}
```

### 2. `POST /get` 获取单个设备状态

获取单个设备最新状态和信息

**参数**

- deviceId  {String} 厂商设备ID， 可以包含不可变数据， 与厂商ID一起，可以唯一确认一台设备
- userAuth {Object} 设备关联的用户授权信息

```json
{
  "deviceId": "xxx",
  "userAuth": {
    "userId": "",
    "userToken": ""
  }
}
```

**返回**

get 接口返回一个 [Device][device]

```json

{
  "status": 0,
  "data": {
     "deviceId": "xxx",
     "state": {
       "switch": "on"
     },
     "userAUth": {
       "userId": "",
       "userToken": ""
     }
  }
}

```

**返回值**

Object 设备最新状态对象：

- `name` 设备名称
- `actions` 设备支持的 action
- `state` 设备运行状态

**注意事项**

- 有些设备如果无法返回状态，返回一个空的对象


### `POST /execute` 执行操作指令， 并返回可确定的最新状态

设备执行操作， 将返回最新状态

**参数**

- device `{Object}`
- device.deviceId  `{String}`, 厂商设备ID， 可以包含不可变数据， 与厂商ID一起，可以唯一确认一台设备
- device.state  `{Object}`, 获取设备当前状态
- device.userAuth `{Object}`, 用户授权信息
- action `{Object}` 需要执行的操作， 参考文档 homebase.devices.v4.pdf



request

```json
{
  "device": {
     "deviceId": "xxx",
     "state": {
        "switch": "on"
     },
     "userAUth": {
        "userId": "",
        "userToken": ""
     }
  },
  "action": {
    "switch": "on"
  }
}
```

response

```json

{
  "status": 0,
  "data": {
    "switch": "on"
  }
}

```




actions 一个系列操作， 示例 "打开灯并设置成红色"
```
{
  "switch": "on",
  "color": "red"
}
```


**返回值**

Object 设备最新状态， 如果无法确定设备的状态， 返回字段可以置空， 返回的设备状态将被缓存到虚拟设备中去


### `POST /command` 执行特定指令

执行自定义指令

说明：

- 如果是用户名，密码登录的 Driver 必须提供 `login` command，返回 userId,userToken
- 如果是 OAuth 登录的， 必须提供 `OAuth` command, 返回 OAuth loginUrl

**参数**

- command `{String}`
- params  `{Object}`

request sample

```json
{
  "command": "login",
  "params": {
    "username": "superman",
    "password": "xxxxxx"
  }
}
```

request sample

```json

{
  "status": 0,
  "data": {
    "userId": "superman",
    "userToken": "DFGHJKLCVBNMFGHJKL"
  }
}

```


#### 常用指令 Command

command **OAuth**

params:

- authCallbackUrl 登录后回调页面

request
```json
{
  "authCallbackUrl": "http://foo/bar"
}

```

returns { String } 登录跳转 URL

response
```json
{
  "status": 0,
  "data": "http://oauthurl"
}
```

command **OAuthRefresh**

params:

- userId 用户Id
- userToken 用户Token

```json
{
    "userId": "superman",
    "userToken": "fjfjfjfjfjfj"
}
```

returns result <Object>

- result.userToken
- result.expireTime

```json
{
  "status": 0,
  "data": {
    "userToken": "",
    "expireTime": ""
  }
}
```

command **login**

params:

- username 用户Id
- password 密码

```json
{
    "username": "superman",
    "password": "fjfjfjfjfjfj"
}
```

returns result <Object>

- result.userToken

```json
{
  "status": 0,
  "data": {
    "userToken": "userToken"
  }
}
```

### 关于 deviceId

关于 deviceId， deviceId 用户存储一些在设备执行需要用到的设备识别参数， 我们建议将需要的参数序列化成字符串（比如， 通过 JSON ）， 在获取的时候反序列化，并拿到其中的参数

deviceId 需要保持灵活性和可扩展性， 以便后续设备需要更多的信息。


### 如何描述你的设备？

请参考： [设备定义][device] 


[device]: ../device/device.md
[rhome]: ../develop/rhome.md
