## 通讯协议

基于 JSON-RPC 2.0

## 连接过程

- Homebase 获取到 ip 与 端口
- Homebase 建立与该端口的连接
- Homebase 发送 connect 指令
- 设备端返回 连接状态， 如果连接失败 1s后 断开连接
- 通过 JSON RPC 与设备进行数据交互

## 指令

### 建立连接 connect， 明文传输， 建立连接

method:  `connect`

paramsg

  - deviceId
  - sereverName
  - time

result

  - deviceId 设备 GUID
  - appId app 在 Rokid 的注册 id

实例

```
--> {"jsonrpc": "2.0", "method": "connect", "params": { "deviceId": "device:aaa-bbb-ccc-ddd", "appId": "homebase.rokid.com"}}, "id": 1 }
<-- {"jsonrpc": "2.0", "result": {"deviceId": "", "appId": ""}, "id": 1}
```

### method: list

- params
  - userAuth
    - userId
    - userToken

```
--> {"jsonrpc": "2.0", "method": "list", "params": {"userAuth":{ "userId": "hello1234" }}, "id": 1}
<-- {"jsonrpc": "2.0", "result": 200, "id": 1}
```

### method: get

- params
  - userAuth
    - userId
    - userToken
  - device
    - deviceId
    - deviceInfo
  - env

```
--> {"jsonrpc": "2.0", "method": "get", "params": {"userAuth":{ "userId": "hello1234", "userToken": "" }, "device": {"deviceId": "", deviceInfo: {}}}, "id": 1}
<-- {"jsonrpc": "2.0", "result": 200, "id": 1}
```

### method: execute

- params
  - userAuth
    - userId
    - userToken
  - action
  - device
    - deviceId  
    - state

```
--> { "jsonrpc": "2.0", "method": "list", "params": {"userAuth":{ "userId": "hello1234" }}, "id": 1 }
<-- { "jsonrpc": "2.0", "result": 200, "id": 1}
```

### method: command

- params
  - method {String}
  - params {Object}
