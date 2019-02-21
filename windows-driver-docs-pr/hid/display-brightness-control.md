---
title: 显示的亮度控制
description: 允许键盘 （外部或嵌入在便携式计算机上），来控制通过 HID 的便携式计算机或平板电脑的屏幕亮度。
ms.assetid: B22BA244-C5C6-4A50-AFE6-4E773194F18C
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b9f4277b52857efe36a1c17c484521cc95be19d7
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56520775"
---
# <a name="display-brightness-control"></a>显示的亮度控制


从 Windows 8 开始，已对标准化的解决方案已添加为允许键盘 （外部或嵌入在便携式计算机上），来控制通过 HID 的便携式计算机或平板电脑的屏幕亮度。

此解决方案中描述的 hid 标准委员会最近批准[HID 评审请求 41](http://www.usb.org/developers/hidpage#approved-usage-table-review-requests)。

## <a name="architecture-and-overview"></a>体系结构和概述


Windows 8 为屏幕亮度增大/减少为使用者控件顶级集合的一部分提供支持。 Windows 8 支持下表中列出的 HID 用法：

| 使用 ID | 用法的名称           | 使用类型               |
|----------|----------------------|--------------------------|
| 0x006F   | 亮度增量 | 重新触发控件 (RTC) |
| 0x0070   | 亮度递减 | 重新触发控件 (RTC) |

 

**请注意**  这些 HID 用法仅在移动系统 （由电池供电） 上运行并且需要 Windows 8。

 

## <a name="sample-report-descriptor"></a>示例报告描述符


以下部分提供了 PC 制造商必须利用的示例报告描述符。 请注意，是否顶部级别集合是已具有另一个顶部级别集合的报告描述符的一部分，报表 ID 必须包含 （在下面的示例中未显示）。

``` syntax
Usage Page (Consumer)
Usage (Consumer Control)
Collection (Application)
   Logical Minimum (0x00)
   Logical Maximum (0x3FF)
   Usage Minimum (0x00)
   Usage Maximum (0x3FF)
   Report Size (16)
   Report Count (1)
   Input (Data, Array, Absolute)
End Collection
```

*重要说明*

-   当用户按下某个键时，输入的报表生成来标识该项。 当释放键用法值了输入的报表 = 0 颁发。
-   只能使用一次处于活动状态且已发送。 使用者控件不允许多个按钮，同时按下。 当发送新的用途时，假定释放以前的密钥的使用情况。
-   亮度向上/向下的 retriggering 密钥并由 Windows 处理重复的其速率。 硬件应不保留重新发送使用情况时这些密钥保持由用户按下。 释放键时，硬件应该只会发送一个输入的报告按钮被按下时，另一个。

## <a name="troubleshooting-common-errors"></a>故障排除的常见错误


提示\#1:亮度递增/递减 HID 用法仅只能对移动系统 （由电池供电） 进行操作，需要 Windows 8。

提示\#2:如果系统已附加到外部监视器，因为 （旧） 监视传输不支持通道 HID 消息向其或从它们的功能将无法正常亮度递增/递减。

 

 




