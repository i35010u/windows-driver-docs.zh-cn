---
title: HID 用法
description: HID 用法标识 HID 控件的用途以及控件实际度量的内容。
keywords:
- 人体学接口设备 WDK，使用情况
- HID WDK，使用情况
- 交互式输入设备 WDK，使用情况
- 输入设备 WDK，使用情况
- 人体学接口设备 WDK，控件
- HID WDK，控件
- 交互式输入设备 WDK，控件
- 输入设备 WDK，控件
- 控制 WDK HID
- 使用情况页面 WDK HID
- 使用 Id WDK HID
- 扩展使用情况 WDK HID
- 使用范围 WDK HID
- 别名用法 WDK HID
- 使用情况 WDK HID
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c6a154a223c47da224ad0b560a2495ce2eb8432a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96820757"
---
#  <a name="hid-usages"></a>HID 用法


*Hid 用法* 标识 hid 控件的用途以及控件实际度量的内容。




在 WDK 的整个 HID 文档中使用以下概念和术语：

[使用情况页](#usage-page)

[使用 ID](#usage-id)

[扩展使用](#extended-usage)

[使用范围](#usage-range)

[使用别名](#aliased-usages)

有关 Windows 组件访问的用法的具体示例，请参阅 [Windows 打开的顶级集合以供系统使用](top-level-collections-opened-by-windows-for-system-use.md)。

有关如何确定 HIDClass 设备支持的用法的详细信息，请参阅：

[集合功能](collection-capability.md)

[按钮功能数组](button-capability-arrays.md)

[值功能数组](value-capability-arrays.md)

[解释 HID 报告](interpreting-hid-reports.md)

有关行业标准 HID 用法的详细信息，请参阅位于 [Usb 实现论坛](https://www.usb.org/hid)网站上的通用串行总线 (usb) 规范 **HID 使用情况表**。

### <a name="usage-page"></a>使用情况页

HID 使用情况组织到相关控件的 *使用情况页* 中。 特定的控件用法由其使用情况页、 [用法 ID](#usage-id)、名称和说明定义。 "使用情况" 页值为16位无符号值。

使用页面的示例包括：

| 页面 ID | 页面名称                | *hidusage* 常量  |
|:-------:|--------------------------|------------------------|
| 0x01    | 通用桌面控件 | HID_USAGE_PAGE_GENERIC |
| 0x05    | 游戏控制            | HID_USAGE_PAGE_GAME    |
| 0x08    | LED                     | HID_USAGE_PAGE_LED     |
| 0x09    | Button                   | HID_USAGE_PAGE_BUTTON  |

### <a name="usage-id"></a>使用 ID

在 "使用情况" 页的上下文中，有效的使用标识符或 *使用 ID* 指示使用情况页中的用法。 保留的用量 ID 为零。 使用 ID 值是无符号的16位值。

**一般桌面控件** 使用页上列出的控件示例：

| 使用 ID | 使用名称            | *hidusage* 常量                    |
|:--------:|-----------------------|------------------------------------------|
| 0x01     | 指针               | HID_USAGE_GENERIC_POINTER                |
| 0x02     | 鼠标                 | HID_USAGE_GENERIC_MOUSE                  |
| 0x04     | 操纵杆              | HID_USAGE_GENERIC_JOYSTICK               |
| 0x05     | 游戏板              | HID_USAGE_GENERIC_GAMEPAD                |
| 0x06     | Keyboard              | HID_USAGE_GENERIC_KEYBOARD               |
| 0x07     | 键盘                | HID_USAGE_GENERIC_KEYPAD                 |
| 0x08     | 多轴控制器 | HID_USAGE_GENERIC_MULTI_AXIS_CONTROLLER  |

### <a name="extended-usage"></a>扩展使用

*扩展用法* 是一个32位值，它在最高有效的2个字节中指定16位 [使用页](#usage-page)值，在扩展使用值的最小有效2个字节中指定16位 [使用 ID](#usage-id) 。

### <a name="usage-range"></a>使用范围

*使用范围* 是包含的连续 [使用 id](#usage-id)的范围，所有这些使用 id 都在相同的 [使用情况页](#usage-page)上。 使用范围由报表描述符中的 "使用情况最小值" 和 "使用量最多" 项指定。

### <a name="aliased-usages"></a>使用别名

可以为一个 [**链接集合**](link-collections.md) 或一个 HID 控件指定多个使用情况。 对于给定的集合或控件，此类用法的组是另一组，并且称为 *别名使用*。 分隔符项用于指定化名使用。 [使用范围](#usage-range) 不能有别名。

有关如何在顶级集合的功能数组中指定别名使用情况的信息，请参阅 [Button 功能数组](button-capability-arrays.md) 和 [值功能数组](value-capability-arrays.md)。

 

 




