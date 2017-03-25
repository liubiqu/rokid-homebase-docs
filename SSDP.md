## 设备自动发现

[SSDP](https://zh.wikipedia.org/wiki/%E7%AE%80%E5%8D%95%E6%9C%8D%E5%8A%A1%E5%8F%91%E7%8E%B0%E5%8D%8F%E8%AE%AE) 是一个简单的基于 UDP 的网络发现协议， 广泛用于 UPNP

- 设备类型
- 设备

## 设备类型


```
NOTIFY * HTTP/1.1
HOST: 239.255.255.250:1900
NT: homebase:bridge
NTS: ssdp:alive
USN: uuid:f40c2981-7329-40b7-8b04-27f187aecfb8::homebase:bridge
LOCATION: http://10.0.0.107:10293/upnp/desc.html
CACHE-CONTROL: max-age=1800
SERVER: node.js/6.9.1 UPnP/1.1 homebase-ssdp/1.0.0

```


```
NOTIFY * HTTP/1.1
HOST: 239.255.255.250:1900
NT: uuid:f40c2981-7329-40b7-8b04-27f187aecfb8
NTS: ssdp:alive
USN: uuid:f40c2981-7329-40b7-8b04-27f187aecfb8
LOCATION: http://10.0.0.107:10293/upnp/desc.html
CACHE-CONTROL: max-age=1800
SERVER: node.js/6.9.1 UPnP/1.1 homebase-ssdp/1.0.0
```

自动发现设备分成两种

1. 桥
2. 单一设备


## 通讯协议

JSON-RPC 2.0 over TCP

methods:

### method: list

- params
  - userAuth
    - userId
    - userToken
  - env

### method: get

- params
  - userAuth
    - userId
    - userToken
  - device
    - deviceId
    - deviceInfo

### method: execute

- params
  - userAuth
    - userId
    - userToken
  - action
  - device
    - deviceId
    - state
