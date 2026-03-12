---
name: xmouse-macro-syntax
description: X-Mouse Button Control 宏语法参考指南。帮助用户理解和编写 XMBC 的模拟按键序列宏，包括标记语法、辅助键、鼠标操作、延迟控制、程序控制等。当用户询问 XMBC 宏写法、模拟按键序列、鼠标宏语法时使用。
---

# X-Mouse Button Control 宏语法指南

## 概述

X-Mouse Button Control (XMBC) 的「模拟按键序列」功能允许通过特定标记(tag)来模拟键盘按键、鼠标操作、系统命令等。

标记格式为 `{TAGNAME}` 或带参数的 `{TAGNAME:参数}`。

---

## 基础语法规则

### 1. 普通字符
直接输入字母数字会被当作按键发送：
```
hello world    # 依次按下 h,e,l,l,o,空格,w,o,r,l,d
```

### 2. 标记格式
- 无参数标记：`{TAG}`
- 单参数标记：`{TAG:value}`
- 多参数标记：`{TAG:x,y}` 或 `{TAG:x-y}`

### 3. 大小写敏感
- 普通字母区分大小写：`a` ≠ `A`
- 标记名不区分大小写：`{LMB}` = `{lmb}`

---

## 辅助按键标记

用于模拟 Ctrl、Alt、Shift 等修饰键。**仅应用到下一个普通按键**。

| 标记 | 说明 |
|------|------|
| `{CTRL}` / `{RCTRL}` | 左/右 Ctrl |
| `{ALT}` / `{RALT}` | 左/右 Alt |
| `{SHIFT}` / `{RSHIFT}` | 左/右 Shift |
| `{LWIN}` / `{RWIN}` | 左/右 Windows 键 |
| `{APPS}` | 应用程序键(右键菜单) |

**组合使用示例：**
```
{CTRL}A              # Ctrl+A (全选)
{CTRL}{ALT}DEL       # Ctrl+Alt+Del
{CTRL}Btext{CTRL}B   # 在Word中加粗"text"
```

---

## 扩展按键标记

| 标记 | 说明 | 标记 | 说明 |
|------|------|------|------|
| `{DEL}` | 删除键 | `{INS}` | 插入键 |
| `{PGUP}` | 上翻页 | `{PGDN}` | 下翻页 |
| `{HOME}` | 行首 | `{END}` | 行尾 |
| `{RETURN}` | 回车 | `{ESCAPE}` | Esc |
| `{BACKSPACE}` | 退格 | `{TAB}` | 制表 |
| `{PRTSCN}` | 截图 | `{PAUSE}` | 暂停 |
| `{SPACE}` | 空格 | `{CAPSLOCK}` | 大小写锁定 |
| `{NUMLOCK}` | 数字锁定 | `{SCROLLLOCK}` | 滚动锁定 |
| `{BREAK}` | 中断 | `{CTRLBREAK}` | Ctrl+Break |

---

## 方向键与功能键

| 类型 | 标记 |
|------|------|
| 方向键 | `{UP}` `{DOWN}` `{LEFT}` `{RIGHT}` |
| 功能键 | `{F1}` 到 `{F24}` |

---

## 鼠标按键标记

### 基本点击

| 标记 | 说明 |
|------|------|
| `{LMB}` | 左键点击 |
| `{RMB}` | 右键点击 |
| `{MMB}` | 中键点击 |
| `{MB4}` / `{XMB1}` | 鼠标侧键4/扩展键1 |
| `{MB5}` / `{XMB2}` | 鼠标侧键5/扩展键2 |

### 按下/释放标记

在鼠标标记后加 `D` (Down) 或 `U` (Up)：

| 标记 | 说明 |
|------|------|
| `{LMBD}` | 左键按下 |
| `{LMBU}` | 左键释放 |
| `{RMBD}` / `{RMBU}` | 右键按下/释放 |
| `{MMBD}` / `{MMBU}` | 中键按下/释放 |

**示例：**
```
{LMBD}{WAITMS:500}{LMBU}    # 按住左键500ms后释放
```

---

## 鼠标滚轮标记

| 标记 | 说明 |
|------|------|
| `{MWUP}` | 滚轮向上 |
| `{MWDN}` | 滚轮向下 |
| `{TILTL}` | 滚轮左倾 |
| `{TILTR}` | 滚轮右倾 |

---

## 延迟标记

| 标记 | 说明 | 示例 |
|------|------|------|
| `{WAIT:n}` | 延迟 n 秒 | `{WAIT:2}` 延迟2秒 |
| `{WAITMS:n}` | 延迟 n 毫秒 | `{WAITMS:500}` 延迟500ms |
| `{WAITMS:x-y}` | 随机延迟 x 到 y 毫秒 | `{WAITMS:50-150}` |

---

## 按键按住标记

| 标记 | 说明 | 示例 |
|------|------|------|
| `{HOLD:n}` | 按住下一个键 n 秒 | `{HOLD:2}A` 按住A键2秒 |
| `{HOLDMS:n}` | 按住下一个键 n 毫秒 | `{HOLDMS:50}r` |

---

## 数字键盘标记

| 标记 | 说明 |
|------|------|
| `{NUM0}` ~ `{NUM9}` | 数字键0-9 |
| `{NUM+}` `{NUM-}` | 加减 |
| `{NUM.}` | 小数点 |
| `{NUM/}` `{NUM*}` | 除乘 |
| `{NUMENTER}` | 小键盘回车 |

---

## 浏览器按键标记

| 标记 | 说明 |
|------|------|
| `{BACK}` | 后退 |
| `{FORWARD}` | 前进 |
| `{STOP}` | 停止 |
| `{REFRESH}` | 刷新 |
| `{WEBHOME}` | 主页 |
| `{SEARCH}` | 搜索 |
| `{FAVORITES}` | 收藏夹 |

---

## 音量与多媒体标记

| 标记 | 说明 |
|------|------|
| `{VOL+}` / `{VOL-}` | 音量增减 |
| `{MUTE}` | 静音 |
| `{MEDIAPLAY}` / `{MEDIASTOP}` | 播放/停止 |
| `{MEDIANEXT}` / `{MEDIAPREV}` | 下一首/上一首 |

---

## 切换锁定键标记

| 标记 | 说明 |
|------|------|
| `{NUMLOCKON}` / `{NUMLOCKOFF}` | 开启/关闭数字锁定 |
| `{CAPSLOCKON}` / `{CAPSLOCKOFF}` | 开启/关闭大写锁定 |
| `{SCROLLLOCKON}` / `{SCROLLLOCKOFF}` | 开启/关闭滚动锁定 |

---

## 鼠标移动标记

| 标记 | 说明 | 示例 |
|------|------|------|
| `{MADD:x,y}` | 相对移动 x,y 像素 | `{MADD:100,0}` 右移100像素 |
| `{MSET:x,y}` | 绝对定位到 x,y | `{MSET:500,300}` |
| `{PSET:x,y}` | 相对于配置文件窗口定位 | `{PSET:100,100}` |
| `{ASET:x,y}` | 相对于活动窗口定位 | `{ASET:50,50}` |
| `{MSAVE:n}` | 保存当前位置到记忆 n (1-10) | `{MSAVE:1}` |
| `{MREST:n}` | 从记忆 n 恢复位置 | `{MREST:1}` |

---

## 程序控制标记

| 标记 | 说明 | 示例 |
|------|------|------|
| `{RUN:程序}` | 运行程序 | `{RUN:C:\Windows\notepad.exe}` |
| `{RUNHID:程序}` | 隐藏窗口运行 | - |
| `{RUNMAX:程序}` | 最大化运行 | - |
| `{RUNMIN:程序}` | 最小化运行 | - |
| `{RUNADM:程序}` | 管理员模式运行 | - |
| `{KILL:程序}` | 结束进程 | `{KILL:notepad.exe}` |

---

## 特殊功能标记

| 标记 | 说明 | 示例 |
|------|------|------|
| `{VKC:n}` | 发送虚拟键码 | `{VKC:65}` 发送A键 |
| `{EXT:n}` | 发送扩展虚拟键码 | - |
| `{SC:n}` | 发送扫描码 | - |
| `{SCE:n}` | 发送扩展扫描码 | - |
| `{CLEAR}` | 清除所有辅助键状态 | - |
| `{CB:文本}` | 复制文本到剪贴板 | `{CB:Hello World}` |

---

## 动作标记

| 标记 | 说明 |
|------|------|
| `{ACTIVATE}` | 激活鼠标下的窗口 |
| `{ACTIVATEPARENT}` | 激活父窗口 |
| `{ACTIVATETOP}` | 激活顶级窗口 |
| `{CURSORBUSY}` | 显示忙碌光标 |
| `{CURSORDEFAULT}` | 恢复默认光标 |
| `{INVERTXY}` / `{INVERTX}` / `{INVERTY}` | 反转坐标轴 |
| `{LOCKXY}` / `{LOCKX}` / `{LOCKY}` | 锁定坐标轴 |
| `{LOCKC}` | 循环锁定 X→Y→解锁 |
| `{UNLOCKXY}` / `{UNLOCKX}` / `{UNLOCKY}` | 解锁坐标轴 |

---

## 方案层标记

| 标记 | 说明 |
|------|------|
| `{LAYER:x}` | 切换到方案 x |
| `{LAYER:next}` | 切换到下一方案 |
| `{LAYER:back}` | 切换到上一方案 |
| `{LAYER:last}` | 撤销方案切换 |

---

## 触发条件标记

用于控制宏在何时执行：

| 标记 | 说明 |
|------|------|
| `{OD}` | 仅在按键按下时发送 (On Down) |
| `{OU}` | 仅在按键释放时发送 (On Up) |
| `{OR}` | 仅在按键重复时发送 (On Repeat) |

**示例：**
```
{OD}{LMB}{OU}{RMB}    # 按下时发左键，释放时发右键
```

---

## 发送方法 1,2,4,5,6,7,9 的特殊标记

某些发送方法支持精细控制按键按下和释放：

| 标记 | 说明 |
|------|------|
| `{PRESS}` | 按下后续按键（不释放） |
| `{RELEASE}` | 释放之前按下的键 |

**重要：** 必须在同一序列中释放所有按下的键！

**示例：**
```
{PRESS}abc{WAITMS:100}{RELEASE}cba
# 按下a,b,c，等待100ms，然后按c,b,a的顺序释放
```

---

## 实用示例

### 游戏连点宏
```
{LMBD}{WAITMS:180}{RMB}{WAITMS:120}{LMBU}{WAITMS:50}
{LMBD}{WAITMS:180}{RMB}{WAITMS:120}{LMBU}
```
按住左键同时点击右键的组合技。

### FPS压枪+移动宏
```
{LMB}{WAITMS:131}{LMB}{WAITMS:231}{RMB}{WAITMS:20}
w{WAITMS:30}a{WAITMS:30}s{WAITMS:30}d{WAITMS:30}w
```
连点左键、开镜，配合WASD移动。

### 窗口操作
```
{ALT}{F4}              # 关闭窗口
{CTRL}W                # 关闭标签页
{LWIN}D                # 显示桌面
```

### 文本输入
```
{CTRL}BHello{CTRL}B    # 在Word中加粗"Hello"
{CB:预设文本}          # 复制文本到剪贴板
```

### 程序启动
```
{RUN:C:\Windows\System32\calc.exe}    # 打开计算器
{KILL:notepad.exe}                    # 关闭记事本
```

---

## 注意事项

1. **辅助键仅作用于下一个按键**：`{CTRL}AB` = Ctrl+A, 然后普通B
2. **延迟单位**：`{WAIT}`是秒，`{WAITMS}`是毫秒
3. **鼠标按下释放必须配对**：每个`{LMBD}`应有对应的`{LMBU}`