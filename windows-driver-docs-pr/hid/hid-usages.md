---
title: HID 的用法
description: HID 的用法确定 HID 控件和控件的实际测量的预期的用途。
ms.assetid: 84fed314-3554-4291-b51c-734d874a4bab
keywords:
- 人机接口设备 WDK 用法
- HID WDK 用法
- 交互式输入的设备 WDK，用法
- 输入设备 WDK，用法
- 人机接口设备 WDK 控件
- HID WDK 控件
- 交互式输入的设备 WDK，控件
- 输入设备 WDK，控件
- WDK HID 的控件
- 使用情况页面 WDK HID
- Id WDK HID 的使用情况
- WDK HID 扩展的用法
- 使用范围是 WDK HID
- 使用别名用法 WDK HID
- WDK HID 的使用情况
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 43f88332071171ce90e145e9abfacb36d4c26e61
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56554642"
---
#  <a name="hid-usages"></a>HID 的用法


*HID 的用法*标识 HID 控件和控件的实际测量的预期的用途。




以下概念和术语在整个 WDK 中的 HID 文档：

[使用情况页面](#usage-page)

[使用 ID](#usage-id)

[扩展的使用情况](#extended-usage)

[使用范围](#usage-range)

[使用别名用法](#aliased-usages)

Windows 组件访问的使用情况的具体示例，请参阅[顶级集合打开供系统使用的 Windows](top-level-collections-opened-by-windows-for-system-use.md)。

有关如何确定 HIDClass 设备支持的使用情况的详细信息，请参阅：

[集合功能](collection-capability.md)

[按钮功能数组](button-capability-arrays.md)

[值功能数组](value-capability-arrays.md)

[解释 HID 报表](interpreting-hid-reports.md)

行业标准的 HID 用法的详细信息，请参阅通用串行总线 (USB) 规范*HID 用法表*位于处[USB 实现论坛](https://go.microsoft.com/fwlink/?linkid=830142)网站。 （此资源可能不会在某些语言和国家/地区中可用。）

### <a name="usage-page"></a>使用情况页面

HID 的用法分为*使用情况页面*相关的控件。 由其使用情况页上，定义特定的控件使用情况[用法 ID](#usage-id)、 名称和说明。 使用情况页面的示例包括泛型桌面控件、 游戏控件、 Led、 按钮和等等。 泛型桌面控件使用情况页面列出的控件的示例包括指针、 鼠标和键盘的设备、 游戏杆，等等。 使用情况页值为 16 位无符号的值。

### <a name="usage-id"></a>使用 ID

使用情况页面，使用是有效标识符的上下文中或*用法 ID*，指示在使用情况页面中的用法。 保留使用情况 ID 为 0。 使用 ID 值是一个无符号的 16 位值。

### <a name="extended-usage"></a>扩展的使用情况

*扩展的使用情况*是一个 32 位值，指定 16 位[使用情况页面](#usage-page)中最有效的两个字节和 16 位值[用法 ID](#usage-id)中最不重要的两个字节扩展的用法值。

### <a name="usage-range"></a>使用范围

一个*用法范围*是连续的非独占范围[Id 使用情况](#usage-id)，则所有的是同一个[使用情况页面](#usage-page)。 使用范围由最小的使用情况和使用情况报告描述符中的最大项指定。

### <a name="aliased-usages"></a>使用别名用法

可以为指定多个使用情况[**集合链接**](link-collections.md)或 HID 控件。 对于给定的集合或控件，此类使用情况的一组是、 别名和称为*别名用法*。 分隔符项用来指定别名用法。 [使用范围](#usage-range)不能有别名。

有关如何在顶级集合的功能数组中指定别名用法的信息，请参阅[按钮功能数组](button-capability-arrays.md)并[值功能数组](value-capability-arrays.md)。

 

 




