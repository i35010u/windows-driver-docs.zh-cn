---
title: 顶级集合的 HIDClass 硬件 ID
description: 此部分指定 HID 类驱动程序为顶级集合生成的硬件 Id。
ms.assetid: a90eea17-0a63-4786-a31f-740bcc670c2a
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
ms.openlocfilehash: f8e1000cfa7e1d111dadf415af2428edd6e1f2ae
ms.sourcegitcommit: f8c3585ec7b1bdfcd65f7f2cc9aa688655de4d20
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/15/2020
ms.locfileid: "81396309"
---
# <a name="hidclass-hardware-ids-for-top-level-collections"></a>顶级集合的 HIDClass 硬件 ID


此部分指定 HID 类驱动程序为顶级集合生成的硬件 Id。

供应商必须使用指定为*供应商硬件 ID 格式*的格式来识别顶级集合。 所有其他*设备 ID*格式仅保留供内部使用。

HID 类驱动程序为 devnode 生成的硬件 Id 取决于以下各项：

1.  基础传输支持的函数数
2.  报表描述符中的顶级集合数

根据这些因素，有4个类别的硬件 Id

|                 | 单个 TLC | 多个 TLC |
|-----------------|------------|--------------|
| 单函数 | 案例1     | 案例2       |
| 多功能  | 情况3     | 情况4       |

 

## <a name="case-1-single-function-device-with-single-tlc"></a>情况1：具有单一 TLC 的单功能设备


使用此硬件 ID 格式的条件：

1.  基础传输支持的函数数 = 1 & &
2.  TLC 数 = 1

硬件 ID 格式：

-   HID\\Vid\_v （4） & Pid\_d （4） & Rev\_r （4）
-   HID\\Vid\_v （4） & Pid\_d （4）
-   \_设备\_HID： p （4）\_U:u （4）
-   HID\_设备

## <a name="case-2-single-function-device-with-multiple-tlc"></a>案例2：具有多个 TLC 的单功能设备


使用此硬件 ID 格式的条件：

1.  基础传输支持的函数数 = 1 & &
2.  TLC > 1 的数目

硬件 ID 格式：

-   HID\\Vid\_v （4） & Pid\_d （4） & Rev\_r （4） & Colb （2）
-   HID\\Vid\_v （4） & Pid\_d （4） & Colb （2）
-   HID\_设备\_UP： p （4）\_U:u （4） \[仅为 WINDOWS Inf 保留\]
-   仅 \[为 WINDOWS Inf 保留\_设备的 HID\]

## <a name="case-3-multi-function-device-with-single-tlc"></a>情况3：多功能设备与单个 TLC


使用此硬件 ID 格式的条件：

1.  基础传输 > 1 & 支持的函数数 &
2.  TLC 数 = 1

硬件 ID 格式：

-   HID\\Vid\_v （4） & Pid\_d （4） & Rev\_r （4） & MI\_z （2）
-   HID\\Vid\_v （4） & Pid\_d （4） & MI\_z （2）
-   HID\_设备\_UP： p （4）\_U:u （4） \[仅为 WINDOWS Inf 保留\]
-   仅 \[为 WINDOWS Inf 保留\_设备的 HID\]

## <a name="case-4-multi-function-device-with-multiple-tlc"></a>情况4：包含多个 TLC 的多功能设备


使用此硬件 ID 格式的条件：

1.  基础传输 > 1 & 支持的函数数 &
2.  TLC > 1 的数目

硬件 ID 格式：

-   HID\\Vid\_v （4） & Pid\_d （4） & Rev\_r （4） & MI\_z （2） & Colb （2）
-   HID\\Vid\_v （4） & Pid\_d （4） & 英里\_z （2） & Colb （2）
-   HID\_设备\_UP： p （4）\_U:u （4） \[仅为 WINDOWS Inf 保留\]
-   仅 \[为 WINDOWS Inf 保留\_设备的 HID\]

## <a name="special-purpose-hardware-id"></a>特殊用途的硬件 ID


下面是 Windows 用于提供默认系统功能的硬件 Id （仅供内部使用）。

| 设备类型            | 使用情况页 | 用法 | 硬件 ID                   |
|------------------------|:----------:|:-----:|-------------------------------|
| 指针                | 0x01       | 0x01  | \_系统\_的 HID\_设备    |
| 鼠标                  | 0x01       | 0x02  | \_系统\_的 HID\_设备    |
| 操纵杆               | 0x01       | 0x04  | \_设备\_系统\_的 HID     |
| 游戏板               | 0x01       | 0x05  | \_设备\_系统\_的 HID     |
| 键盘               | 0x01       | 0x06  | \_设备\_系统\_的 HID |
| 键盘                 | 0x01       | 0x07  | \_设备\_系统\_的 HID |
| 系统控件         | 0x01       | 0x80  | \_设备\_系统\_的 HID  |
| 消费者音频控制 | 0x0C       | 0x01  | HID\_设备\_系统\_使用者 |

重要说明：

-   HIDClass 未生成兼容 Id
-   供应商第三方 Inf 必须仅与硬件 Id 匹配
-   包含 HID\_设备\_系统\_\* 的硬件 Id 是操作系统为其使用而打开的 "特殊" 设备。 供应商提供的 INF 不得与这些特殊硬件 Id 匹配。
-   供应商提供的第三方 HID 传输微型驱动程序必须提供以下列出的字段，以确保 HIDClass 可以生成相应的硬件 Id。

图例：

| 字段 | 包含        | 十六进制值 | 含义                                                  |
|:-----:|-----------------|-------------------|----------------------------------------------------------|
| v （4）  | 四个十六进制数字 | 0x0000-0xFFFF     | 供应商 ID                                                |
| d （4）  | 四个十六进制数字 | 0x0000-0xFFFF     | Product ID                                               |
| r （4）  | 四个十六进制数字 | 0x0000-0xFFFF     | 修订号                                          |
| z （2）  | 两个十六进制数字  | 0x00-0xFF         | 接口编号（仅适用于复合 USB 设备。） |
| b （2）  | 两个十六进制数字  | 0x00-0xFF         | 收集号（仅适用于多 TLC 设备。） |
| p （4）  | 四个十六进制数字 | 0x0000-0xFFFF     | TLC 的使用页码                                |
| u （4）  | 四个十六进制数字 | 0x0000-0xFFFF     | TLC 的使用数量                                      |
