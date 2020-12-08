---
title: 顶级集合的 HIDClass 硬件 ID
description: 此部分指定 HID 类驱动程序为顶级集合生成的硬件 Id。
keywords:
- 人体学接口设备 WDK，硬件 Id
- HID WDK，硬件 Id
- 交互式输入设备 WDK，硬件 Id
- 输入设备 WDK，硬件 Id
- 供应商硬件 Id WDK HID
- 硬件 Id WDK HID
- ID 格式 WDK HID
- 人体学接口设备 WDK、集合
- HID WDK，集合
- 交互式输入设备 WDK，集合
- 输入设备 WDK，集合
- 集合 WDK HID，硬件 Id
- 顶级集合 WDK HID
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9c4ddedb5dcfe8e7f5e1680aa0981595796d6ff3
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96820755"
---
# <a name="hidclass-hardware-ids-for-top-level-collections"></a>顶级集合的 HIDClass 硬件 ID


此部分指定 HID 类驱动程序为[顶级集合](top-level-collections.md)生成的[硬件 id](../install/hardware-ids.md) 。

供应商必须使用指定为 *供应商硬件 ID 格式* 的格式来识别顶级集合。 所有其他 *设备 ID* 格式仅保留供内部使用。

HID 类驱动程序为 devnode 生成的硬件 Id 取决于以下各项：

1.  基础传输支持的函数数
2.  报表描述符中的顶级集合数

根据这些因素，有4个类别的硬件 Id

|     类型        | 单个 TLC | 多个 TLC |
|-----------------|------------|--------------|
| Single-Function | Case 1     | Case 2       |
| 多功能  | 情况3     | 情况4       |

 

## <a name="case-1-single-function-device-with-single-tlc"></a>情况1：具有单一 TLC 的单功能设备


使用此硬件 ID 格式的条件：

1.  基础传输支持的函数数 = 1 &&
2.  TLC 数 = 1

硬件 ID 格式：

-   HID \\ Vid \_ v (4) # B0 Pid \_ d (4) # B1 Rev \_ r (4) 
-   HID \\ Vid \_ v (4) # B0 Pid \_ d (4) 
-   HID \_ 设备 \_ 启动： p (4) \_ U:u (4) 
-   HID \_ 设备

## <a name="case-2-single-function-device-with-multiple-tlc"></a>案例2：具有多个 TLC 的单功能设备


使用此硬件 ID 格式的条件：

1.  基础传输支持的函数数 = 1 &&
2.  TLC > 1 的数目

硬件 ID 格式：

-   HID \\ Vid \_ v (4) # B0 Pid \_ d (4) # B1 Rev \_ r (4) # B2 Colb (2) 
-   HID \\ Vid \_ v (4) # B0 Pid \_ d (4) # B1 Colb (2) 
-   HID \_ 设备 \_ UP： p (4) \_ U:u (4) \[ 仅为 WINDOWS inf 保留\]
-   \_ \[ 仅为 WINDOWS inf 保留的 HID 设备\]

## <a name="case-3-multi-function-device-with-single-tlc"></a>情况3：多功能设备与单个 TLC


使用此硬件 ID 格式的条件：

1.  基础传输 > 1 && 支持的函数数
2.  TLC 数 = 1

硬件 ID 格式：

-   HID \\ Vid \_ v (4) # B0 Pid \_ d (4) # B1 Rev \_ r (4) # B2 MI \_ z (2) 
-   HID \\ Vid \_ v (4) # B0 Pid \_ d (4) # B1 MI \_ z (2) 
-   HID \_ 设备 \_ UP： p (4) \_ U:u (4) \[ 仅为 WINDOWS inf 保留\]
-   \_ \[ 仅为 WINDOWS inf 保留的 HID 设备\]

## <a name="case-4-multi-function-device-with-multiple-tlc"></a>情况4：包含多个 TLC 的多功能设备


使用此硬件 ID 格式的条件：

1.  基础传输 > 1 && 支持的函数数
2.  TLC > 1 的数目

硬件 ID 格式：

-   HID \\ Vid \_ v (4) # B0 Pid \_ d (4) # B1 Rev \_ r (4) # B2 MI \_ z (2) # B3 Colb (2) 
-   HID \\ Vid \_ v (4) # B0 Pid \_ d (4) # B1 MI \_ z (2) # B2 Colb (2) 
-   HID \_ 设备 \_ UP： p (4) \_ U:u (4) \[ 仅为 WINDOWS inf 保留\]
-   \_ \[ 仅为 WINDOWS inf 保留的 HID 设备\]

## <a name="special-purpose-hardware-id"></a>特殊用途的硬件 ID


下面是仅供 Windows 用于提供默认系统功能) 使用的硬件 Id (。

| 设备类型            | 使用情况页 | 使用情况 | 硬件 ID                   |
|------------------------|:----------:|:-----:|-------------------------------|
| 指针                | 0x01       | 0x01  | HID \_ 设备 \_ 系统 \_ 鼠标    |
| 鼠标                  | 0x01       | 0x02  | HID \_ 设备 \_ 系统 \_ 鼠标    |
| 操纵杆               | 0x01       | 0x04  | HID \_ 设备 \_ 系统 \_ 游戏     |
| 游戏板               | 0x01       | 0x05  | HID \_ 设备 \_ 系统 \_ 游戏     |
| Keyboard               | 0x01       | 0x06  | HID \_ 设备 \_ 系统 \_ 键盘 |
| 键盘                 | 0x01       | 0x07  | HID \_ 设备 \_ 系统 \_ 键盘 |
| 系统控件         | 0x01       | 0x80  | HID \_ 设备 \_ 系统 \_ 控件  |
| 消费者音频控制 | 0x0C       | 0x01  | HID \_ 设备 \_ 系统 \_ 使用者 |

重要说明：

-   HIDClass 未生成兼容 Id
-   供应商第三方 Inf 必须仅与硬件 Id 匹配
-   包含 HID \_ 设备系统的硬件 \_ id \_ \* 是操作系统为其使用而打开的 "特殊" 设备。 供应商提供的 INF 不得与这些特殊硬件 Id 匹配。
-   供应商提供的第三方 HID 传输微型驱动程序必须提供以下列出的字段，以确保 HIDClass 可以生成相应的硬件 Id。

图例：

| 字段 | 包含        | 十六进制值 | 含义                                                  |
|:-----:|-----------------|-------------------|----------------------------------------------------------|
|  (4)   | 四个十六进制数字 | 0x0000-0xFFFF     | 供应商 ID                                                |
| d (4)   | 四个十六进制数字 | 0x0000-0xFFFF     | 产品 ID                                               |
| r (4)   | 四个十六进制数字 | 0x0000-0xFFFF     | 修订号                                          |
| z (2)   | 两个十六进制数字  | 0x00-0xFF         | 接口编号 (仅用于复合 USB 设备。 )  |
| b (2)   | 两个十六进制数字  | 0x00-0xFF         | 集合编号 (仅用于 TLC 设备。 )  |
| p (4)   | 四个十六进制数字 | 0x0000-0xFFFF     | TLC 的使用页码                                |
| u (4)   | 四个十六进制数字 | 0x0000-0xFFFF     | TLC 的使用数量                                      |
