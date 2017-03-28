# 设备能力与状态

- 设备能力 `actions`: 指的是智能设备具备的能力，比如智能灯泡具有开关、调颜色、调亮度的能力。
- 设备状态 `state`: 指的是设备当前的状态，与定义的设备能力对应。
- 设备能力接受值与状态值详见 [设备能力](#actions)
- example

actions:
```JSON
{
  "switch":["on","off"],
  "color":["num"],
  "brightness":["num"]
}
```

state:
```JSON
{
  "switch": "on",
  "color": 256,
  "brightness": 10
}
```

## <span id = "actions">设备能力 actions</span>

- 开关 [switch](#switch)
- 颜色 [color](#color)
- 亮度 [brightness](#brightness)
- 模式 [mode](#mode)
- 位置量 [position](#position)
- 风速 [fanspeed](#fanspeed)
- 转向模式 [swing_mode](#swing_mode)
- 音量 [volume](#volume)
- 频道 [channel](#channel)
- 湿度 [humidity](#humidity)
- 温度 [temperature](#temperature)
- Ping [ping](#ping)

### <span id = "switch">开关 switch</span>

- actions 接受值 [ "on", "off", "stop"]
  - "on" : 开
  - "off" : 关
  - "stop" : 暂停，停止

```JSON
{ "switch": ["on", "off"] }
```

- state 值
  - {string}
  - actions 定义设备能力对应的状态

```JSON
{ "switch":"on" }
```

### <span id = "color">颜色 color</span>

- actions 接受值 [ "random", "num" ]
  - "random": 颜色随机值
  - "num": 指定颜色RGB值，例如蓝色RGB值为 0x00FF00

```JSON
{ "color": ["num"] }
```

- state 值
  - {number}
  - RGB 十六进制数值
  - 0x000000 - 0xFFFFFF

```JSON
{ "color": 65280 }
```

### <span id = "brightness">亮度 brightness</span>

- actions 接受值 [ "up", "down", "max", "min", "num" ]
  - "up": 调亮
  - "down": 调暗
  - "max": 调到最亮
  - "min": 调到最暗
  - "num": 调到 0 到 100 之间指定数值，若设备亮度范围更大，则需要自行转换。

```JSON
{ "brightness": ["up", "down", "num"] }
```

- state 值
  - {number}
  - 0 到 100 之间十进制数值

```JSON
{ "brightness": 68 }
```

### <span id = "mode">模式 mode</span>

- actions 接受值 [ "auto", "manual", "cool", "heat", "dry", "fan", "silent", "energy", "sleep" ]
  - "auto": 自动模式
  - "manual": 手动模式
  - "cool": 制冷模式
  - "heat": 制热模式
  - "dry": 除湿模式
  - "fan": 送风模式
  - "silent": 静音模式
  - "energy": 省电模式
  - "sleep": 睡眠模式

```JSON
{ "mode": ["auto", "cool", "heat", "fan"] }
```

- state 值
  - {string}
  - actions 定义能力对应的状态

```JSON
{ "mode": "auto" }
```

### <span id = "position">位置量 position</span>
- actions 接受值
  - [ 'up'， 'down'， 'num' ]
- state 值
  - {number}
  - 0 - 100

### <span id = "fanspeed">风速 fanspeed</span>
- actions 接受值
  - [ 'up', 'down', 'max', 'min', 'num' ]
- state 值
  - {number}
  - 0 - 100

### <span id = "swing_mode">转向模式 swing_mode</span>
- actions 接受值
  - [ 'auto', 'on', 'off', 'horizon', 'horizon.off','vertical', 'vertical.off' ]
- state 值
  - {string}
  - [ 'auto', 'on', 'off', 'horizon', 'horizon.off','vertical', 'vertical.off' ]

### <span id = "volume">音量 volume</span>
- actions 接受值
  - [ 'up', 'down', 'max', 'min', 'num' ]
- state 值
  - {number}
  - 0 - 100

### <span id = "channel">频道 channel</span>
- actions 接受值
  - [ 'next', 'prev', 'random', 'num' ]
- state 值
  - {number}
  - 正整数
  - 如果不能明确获取到具体数值，可以为空

### <span id = "humidity">湿度 humidity</span>
- actions 接受值
  - [ 'up', 'down', 'max', 'min', 'num' ]
- state 值
  - {number}
  - 0 - 100

### <span id = "temperature">温度 temperature</span>
- actions 接受值
  - [ 'up', 'down', 'max', 'min', 'num' ]
- state 值
  - {number}
  - 0 - 100

### <span id = "ping">ping</span>
- actions 接受值
  - [ 'trigger' ]
- state 值
  - {Boolean}
  - 为空，不需要提供state
