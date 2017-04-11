## Homebase TCP 通讯协议

基于 JSON-RPC 2.0

## 连接过程

- Homebase 获取到 TCP 驱动服务 ip 与 端口
- Homebase 建立与该端口的连接
- Homebase 发送 TCP json-rpc call
- TCP 驱动返回结果
- 链接

## 指令

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
    - type
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
