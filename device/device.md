# 标准化设备

## 数据类型 {Object}

- {String} [deviceId](#deviceId)
- {String} [name](#name)
- {String} [type](#type)
- {Object} [actions](#actions)
- {Object} [state](#state)
- {Boolean} [offline](#offline)
- {Object} [deviceInfo](#deviceInfo) (Option)
- {String} [parent](#parent) (Option)

### <span id = "deviceId">deviceId</span>

- {String}
- 设备唯一Id，用来标识一个设备，要具备唯一性
- example: uuid 等

```
"06d0dfe0-1123-11e7-93ae-92361f002671"
```

### <span id = "name">name</span>

- {String}
- 设备名称
- example

```
"智能灯泡"
```

### <span id = "type">type</span>

- {String}
- 设备类型
- [支持的设备类型](type.md)
- example

```
"light"
```

### <span id = "actions">actions</span>

- {Object}
- 一个智能设备具备的能力，如下面 example 所示，智能灯泡具备开关，调颜色，调亮度三个能力。
- [设备能力定义](actions-and-state.md)
- example

```JSON
{
  "switch":["on","off"],
  "color":["num"],
  "brightness":["num"]
}
```

### <span id = "state">state</span>

- {Object}
- 设备当前状态
- 与 [actions](#actions) 对应， actions 定义的设备能力对应的当前状态
- example

state:
```JSON
{
  "switch": "on",
  "color": 256,
  "brightness": 10
}
```
actions:
```JSON
{
  "switch":["on","off"],
  "color":["num"],
  "brightness":["num"]
}
```

### <span id = "offline">offline</span>

- {Boolean}
- 设备离线状态
  - true: 离线
  - false: 在线

### <span id = "deviceInfo">deviceInfo</span>

- {Object}
- Option
- 与设备有关的信息，允许自由定义和储存查询、控制设备等必需的信息
- example

```JSON
{
  "hostname":"http://127.0.0.1",
  "port":"3000"
}
```

### <span id = "parent">parent</span>

- {String}
- Option
- 母设备的 deviceId
- 例如多联开关的每一个开关都要单独转化为一个子设备，此时多联开关就是一个母设备。
