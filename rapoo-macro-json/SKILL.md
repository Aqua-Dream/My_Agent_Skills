---
name: rapoo-macro-json
description: 记录雷柏鼠标宏 JSON 文件格式规范，包括节点类型、字段含义、延迟插入规则。用于创建、编辑或修复雷柏宏配置文件。
---

# 雷柏宏 JSON 文件格式规范

## 文件结构概览

```json
{
    "Macro": {
        "CycleNumber": 0,
        "ID": 0,
        "IgnoreDelay": false,
        "InfoList": [
            // 宏操作节点数组
        ],
        "Name": "宏名称",
        "PlayType": 3
    },
    "Platform": "AHub"
}
```

## 字段说明

### Macro 对象

| 字段 | 类型 | 说明 |
|------|------|------|
| `CycleNumber` | number | 循环次数，0 表示无限循环，1 表示单次播放 |
| `ID` | number | 宏的唯一标识符 |
| `IgnoreDelay` | boolean | 是否忽略延迟，通常为 false |
| `InfoList` | array | 宏操作节点数组，按顺序执行 |
| `Name` | string | 宏的名称 |
| `PlayType` | number | 播放类型：1=单次播放，3=按住时播放 |

### InfoList 节点

每个节点代表一个操作，包含以下字段：

| 字段 | 类型 | 说明 |
|------|------|------|
| `Action` | number | 动作类型：1=按下，0=抬起 |
| `Delay` | number | 此操作前的延迟（毫秒）|
| `KeyCode` | number | 按键码（见下方键码表）|
| `Type` | number | 节点类型：0=键盘，1=鼠标，2=延迟 |
| `X` | number | 鼠标 X 坐标（仅鼠标类型）|
| `Y` | number | 鼠标 Y 坐标（仅鼠标类型）|

## 节点类型详解

### Type 0 - 键盘按键

```json
{
    "Action": 1,
    "Delay": 0,
    "KeyCode": 8,
    "Type": 0,
    "X": 0,
    "Y": 0
}
```

- `KeyCode`: 键盘按键码（基于 USB HID 扫描码，见键码表）
- `Action`: 1=按下，0=抬起
- `Delay`: 键盘节点中通常设为 0

### Type 1 - 鼠标按键

```json
{
    "Action": 1,
    "Delay": 0,
    "KeyCode": 240,
    "Type": 1,
    "X": 0,
    "Y": 0
}
```

- `KeyCode`: 240=左键，241=右键，242=中键
- `Action`: 1=按下，0=抬起
- `Delay`: 鼠标节点中通常设为 0

### Type 2 - 延迟节点

```json
{
    "Action": 0,
    "Delay": 30,
    "KeyCode": 0,
    "Type": 2,
    "X": 0,
    "Y": 0
}
```

- `Delay`: 延迟时长（毫秒），这是唯一需要设置延迟的地方
- `Action` 和 `KeyCode` 固定为 0

## 键码映射表

雷柏使用 **USB HID 扫描码**（USB HID Usage ID），不是 Windows 虚拟键码。

### 字母键（A-Z）

| KeyCode | 按键 | KeyCode | 按键 | KeyCode | 按键 |
|---------|------|---------|------|---------|------|
| 4 | A | 13 | J | 22 | S |
| 5 | B | 14 | K | 23 | T |
| 6 | C | 15 | L | 24 | U |
| 7 | D | 16 | M | 25 | V |
| 8 | E | 17 | N | 26 | W |
| 9 | F | 18 | O | 27 | X |
| 10 | G | 19 | P | 28 | Y |
| 11 | H | 20 | Q | 29 | Z |
| 12 | I | 21 | R | | |

### 数字键（0-9）

| KeyCode | 按键 | KeyCode | 按键 |
|---------|------|---------|------|
| 39 | 0 | 34 | 5 |
| 30 | 1 | 35 | 6 |
| 31 | 2 | 36 | 7 |
| 32 | 3 | 37 | 8 |
| 33 | 4 | 38 | 9 |

### 功能键

| KeyCode | 按键 | KeyCode | 按键 |
|---------|------|---------|------|
| 58 | F1 | 64 | F7 |
| 59 | F2 | 65 | F8 |
| 60 | F3 | 66 | F9 |
| 61 | F4 | 67 | F10 |
| 62 | F5 | 68 | F11 |
| 63 | F6 | 69 | F12 |

### 控制键

| KeyCode | 按键 | KeyCode | 按键 |
|---------|------|---------|------|
| 40 | Enter | 43 | Tab |
| 41 | Esc | 44 | Space |
| 42 | Backspace | | |

### 符号键

| KeyCode | 按键 | KeyCode | 按键 |
|---------|------|---------|------|
| 45 | - | 50 | ISO # |
| 46 | = | 51 | ; |
| 47 | [ | 52 | ' |
| 48 | ] | 53 | ` |
| 49 | \ | | |

### 鼠标键

| KeyCode | 按键 |
|---------|------|
| 240 | 鼠标左键 |
| 241 | 鼠标右键 |
| 242 | 鼠标中键 |

## 正确示例

```json
// 按下 E 键 -> 延迟 -> 抬起 E 键
{
    "Action": 1,
    "Delay": 0,
    "KeyCode": 8,
    "Type": 0,
    "X": 0,
    "Y": 0
},
{
    "Action": 0,
    "Delay": 30,
    "KeyCode": 0,
    "Type": 2,
    "X": 0,
    "Y": 0
},
{
    "Action": 0,
    "Delay": 0,
    "KeyCode": 8,
    "Type": 0,
    "X": 0,
    "Y": 0
}
```

## 注意事项
- `Delay` 字段在 Type 0/1 节点中通常设为 0
- 实际延迟通过独立的 Type 2 节点实现
- 文件编码应为 UTF-8
