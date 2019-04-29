---
title: 顶级集合的 HIDClass 硬件 ID
description: 本部分中指定的硬件的 HID 类驱动程序生成为顶级集合的 Id。
ms.assetid: a90eea17-0a63-4786-a31f-740bcc670c2a
keywords:
- 人机接口设备 WDK，硬件 Id
- HID WDK，硬件 Id
- 交互式输入的设备 WDK，硬件 Id
- 输入设备 WDK，硬件 Id
- 供应商的硬件 Id WDK HID
- 硬件 Id WDK HID
- ID 格式 WDK HID
- 人机接口设备 WDK 集合
- HID WDK 集合
- 交互式输入的设备 WDK，集合
- 输入设备 WDK，集合
- WDK HID，硬件 Id 的集合
- WDK HID 顶级集合
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 697277bf4f3e3de70e04242c87fb22c7d545d718
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63388785"
---
# <a name="hidclass-hardware-ids-for-top-level-collections"></a>顶级集合的 HIDClass 硬件 ID


本部分中指定的硬件的 HID 类驱动程序生成为顶级集合的 Id。

供应商必须使用指定为的格式*供应商的硬件 ID 格式*来标识顶级集合。 所有其他*设备 ID*格式保留仅供内部使用。




硬件 Id 的 HID 类驱动程序生成 devnode 取决于以下因素：

1.  支持的基础传输的函数数目
2.  报表描述符中的顶部级别集合数

根据这些因素，有 4 个类别的硬件 Id

|                 | 单个 TLC | 多个 TLC |
|-----------------|------------|--------------|
| 单函数 | 案例 1     | 情况 2       |
| 多函数  | 案例 3     | 用例 4       |

 

## <a name="case-1-single-function-device-with-single-tlc"></a>案例 1：单个 TLC 使用单函数设备


在其下使用此硬件 ID 格式的条件：

1.  支持的基础传输的函数数目 = 1 （& a) （& a)
2.  TLC 数 = 1

硬件 ID 格式：

-   HID\\Vid\_v(4)&Pid\_d(4)&Rev\_r(4)
-   HID\\Vid\_v(4)&Pid\_d(4)
-   HID\_设备\_UP:p(4)\_U:u(4)
-   HID\_设备

## <a name="case-2-single-function-device-with-multiple-tlc"></a>情况 2：使用多个 TLC 单函数设备


在其下使用此硬件 ID 格式的条件：

1.  支持的基础传输的函数数目 = 1 （& a) （& a)
2.  数 TLC &gt; 1

硬件 ID 格式：

-   HID\\Vid\_v(4)&Pid\_d(4)&Rev\_r(4)&Colb(2)
-   HID\\Vid\_v(4)&Pid\_d(4)&Colb(2)
-   HID\_设备\_UP:p(4)\_U:u(4)\[留待仅 WINDOWS Inf\]
-   HID\_设备\[留待仅 WINDOWS Inf\]

## <a name="case-3-multi-function-device-with-single-tlc"></a>情况 3：使用单个 TLC 多功能设备


在其下使用此硬件 ID 格式的条件：

1.  支持的基础传输的函数数目&gt;1 & &
2.  TLC 数 = 1

硬件 ID 格式：

-   HID\\Vid\_v(4)&Pid\_d(4)&Rev\_r(4)&MI\_z(2)
-   HID\\Vid\_v(4)&Pid\_d(4)&MI\_z(2)
-   HID\_设备\_UP:p(4)\_U:u(4)\[留待仅 WINDOWS Inf\]
-   HID\_设备\[留待仅 WINDOWS Inf\]

## <a name="case-4-multi-function-device-with-multiple-tlc"></a>情形 4:使用多个 TLC 多功能设备


在其下使用此硬件 ID 格式的条件：

1.  支持的基础传输的函数数目&gt;1 & &
2.  数 TLC &gt; 1

硬件 ID 格式：

-   HID\\Vid\_v(4)&Pid\_d(4)&Rev\_r(4)&MI\_z(2)&Colb(2)
-   HID\\Vid\_v(4)&Pid\_d(4)&MI\_z(2)&Colb(2)
-   HID\_设备\_UP:p(4)\_U:u(4)\[留待仅 WINDOWS Inf\]
-   HID\_设备\[留待仅 WINDOWS Inf\]

## <a name="special-purpose-hardware-id"></a>特殊用途的硬件 ID


以下是硬件 Id （仅供内部使用），Windows 使用提供的默认系统功能。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th>设备类型</th>
<th>使用情况页面</th>
<th>用法</th>
<th>硬件 ID</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>指针</p></td>
<td><p>0x01</p></td>
<td><p>0x01</p></td>
<td><p>HID_DEVICE_SYSTEM_MOUSE</p></td>
</tr>
<tr class="even">
<td><p>鼠标</p></td>
<td><p>0x01</p></td>
<td><p>0x02</p></td>
<td><p>HID_DEVICE_SYSTEM_MOUSE</p></td>
</tr>
<tr class="odd">
<td><p>游戏杆</p></td>
<td><p>0x01</p></td>
<td><p>0x04</p></td>
<td><p>HID_DEVICE_SYSTEM_GAME</p></td>
</tr>
<tr class="even">
<td><p>游戏板</p></td>
<td><p>0x01</p></td>
<td><p>0x05</p></td>
<td><p>HID_DEVICE_SYSTEM_GAME</p></td>
</tr>
<tr class="odd">
<td><p>键盘</p></td>
<td><p>0x01</p></td>
<td><p>0x06</p></td>
<td><p>HID_DEVICE_SYSTEM_KEYBOARD</p></td>
</tr>
<tr class="even">
<td><p>键盘</p></td>
<td><p>0x01</p></td>
<td><p>0x07</p></td>
<td><p>HID_DEVICE_SYSTEM_KEYBOARD</p></td>
</tr>
<tr class="odd">
<td><p>系统控制</p></td>
<td><p>0x01</p></td>
<td><p>0x80</p></td>
<td><p>HID_DEVICE_SYSTEM_CONTROL</p></td>
</tr>
<tr class="even">
<td><p>使用者音频控件</p></td>
<td><p>0x0C</p></td>
<td><p>0x01</p></td>
<td><p>HID_DEVICE_SYSTEM_CONSUMER</p></td>
</tr>
</tbody>
</table>

 

重要说明：

-   有由 HIDClass 生成任何兼容 Id
-   供应商的硬件 Id 必须仅匹配第三方 Inf
-   硬件 Id 包含 HID\_设备\_系统\_\*是"特殊"操作系统打开其使用的设备。 供应商提供 INF 必须不匹配这些特殊的硬件 Id。
-   供应商提供第三方 HID 传输微型驱动程序必须提供字段下面列出以确保 HIDClass 可以生成相应的硬件 Id。

图例：

|       |                 |                   |                                                          |
|-------|-----------------|-------------------|----------------------------------------------------------|
| 字段 | 包含        | 十六进制值 | 含义                                                  |
| v(4)  | 四个十六进制数字 | 0x0000-0xFFFF     | 供应商 ID                                                |
| d(4)  | 四个十六进制数字 | 0x0000-0xFFFF     | 产品 ID                                               |
| r(4)  | 四个十六进制数字 | 0x0000-0xFFFF     | 修订号                                          |
| z(2)  | 两个十六进制数字  | 0x00-0xFF         | 接口号 （仅用于复合的 USB 设备。） |
| b(2)  | 两个十六进制数字  | 0x00-0xFF         | 集合数 （仅用于多个 TLC 设备。） |
| p(4)  | 四个十六进制数字 | 0x0000-0xFFFF     | 使用情况 TLC 页的页码                                |
| u(4)  | 四个十六进制数字 | 0x0000-0xFFFF     | TLC 的使用情况数量                                      |

 

 

 




