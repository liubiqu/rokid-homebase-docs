## 设备自动发现

[SSDP](https://zh.wikipedia.org/wiki/%E7%AE%80%E5%8D%95%E6%9C%8D%E5%8A%A1%E5%8F%91%E7%8E%B0%E5%8D%8F%E8%AE%AE) 是一个简单的基于 UDP 的网络发现协议， 广泛用于 UPNP

## 交互

- HomeBase 上线后， 会自动广播发送 SSDP SEARCH 并设置 ST 头为 homebase device
- 设备收到 SSDP Search 广播， 会向设备发送方发送UDP 单播 Response
- 设备定时向 SSDP 广播 alive 消息
- 设备下线时， 向 SSD 广播 bye 消息


## 消息示例

### SSDP SEARCH
```
M-SEARCH * HTTP/1.1
HOST: 239.255.255.250:1900
ST: homebase:device
MAN: "ssdp:discover"
MX: 3
```

### 单播 Response


```
NOTIFY * HTTP/1.1
HOST: 239.255.255.250:1900
NT: homebase:device
NTS: ssdp:alive
USN: uuid:f40c2981-7329-40b7-8b04-27f187aecfb8::homebase:bridge
LOCATION: http://10.0.0.107:10293
CACHE-CONTROL: max-age=1800
DEVICE_TYPE: BRIDGE
SERVER: node.js/6.9.1 UPnP/1.1 homebase-ssdp/1.0.0
```

### 设备根据 CACHE-CONTROL 设置的值， 定时发送 SSDP ALIVE 心跳广播

```
NOTIFY * HTTP/1.1
HOST: 239.255.255.250:1900
NT: uuid:f40c2981-7329-40b7-8b04-27f187aecfb8
NTS: ssdp:alive
USN: uuid:f40c2981-7329-40b7-8b04-27f187aecfb8
LOCATION: http://10.0.0.107:10293
CACHE-CONTROL: max-age=1800
DEVICE_TYPE: BRIDGE
SERVER: node.js/6.9.1 UPnP/1.1 homebase-ssdp/1.0.0
```

### 设备下线 向 SSDP 多播地址广播 ssdp-bye 消息

```
NOTIFY * HTTP/1.1
HOST: 239.255.255.250:1900
NT: uuid:f40c2981-7329-40b7-8b04-27f187aecfb8
NTS: ssdp:bye
USN: uuid:f40c2981-7329-40b7-8b04-27f187aecfb8
LOCATION: http://10.0.0.107:10293
CACHE-CONTROL: max-age=1800
DEVICE_TYPE: BRIDGE
SERVER: node.js/6.9.1 UPnP/1.1 homebase-ssdp/1.0.0
```

## 说明

### USN

USN 是一个服务的 Unique Number， 你可以用 UUID 为你的设备生成一个 USN； USN 代表一个独立的设备

### DEVICE_TYPE

设备在广播和单播的时候都需要包含 DEVICE_TYPE 头， DEVICE_TYPE 头标识了设备的类型， 有两种设备类型，

- BRIDGE： 设备桥， 可以返回并控制多个设备
- SINGLE： 单一设备， 具体设备类型由具体状态接口返回

### LOCATION

表示设备控制节点, 目前支持以下几种协议

- http   http 格式的驱动
- tcp   基于 json-rpc 的tcp 接口

TCP 接口实例
```
LOCATION: http://10.0.0.1:8888
```

TCP 接口实例
```
LOCATION: tcp://10.0.0.1:9999
```
