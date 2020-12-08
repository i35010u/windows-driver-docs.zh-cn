---
title: 显示器亮度控制
description: 允许) 的便携式计算机上 (外部或嵌入的键盘，通过 HID 控制便携式计算机或平板电脑的屏幕亮度。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 469bc0d8de11a32275a4c55a50e5aef90c54bf0e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838927"
---
# <a name="display-brightness-control"></a>显示器亮度控制


从 Windows 8 开始，已添加标准化的解决方案，以允许在便携式计算机上 (外部或嵌入) 的键盘，通过 HID 控制便携式计算机或平板电脑的屏幕亮度。

此解决方案在 HID 委员会最近批准的 [Hid 审核请求 41](https://www.usb.org/developers/hidpage#approved-usage-table-review-requests)中进行了介绍。

## <a name="architecture-and-overview"></a>体系结构和概述


Windows 8 支持屏幕亮度增加/减少，作为使用者控件顶层集合的一部分。 Windows 8 支持下表中列出的 HID 用法：

| 使用 ID | 使用名称           | 使用情况类型               |
|----------|----------------------|--------------------------|
| 0x006F   | 亮度增量 |  (RTC) 的重新触发控件 |
| 0x0070   | 亮度减量 |  (RTC) 的重新触发控件 |

 

**注意**  这些 HID 用法仅适用于移动系统 (备有电池的) 并且需要 Windows 8。

 

## <a name="sample-report-descriptor"></a>示例报表描述符


以下部分提供了 PC 制造商必须利用的示例报表描述符。 请注意，如果顶层集合是已有另一个顶级集合的报表描述符的一部分，则必须包含报表 ID (不会在下面的示例) 中显示。

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

-   当用户按下某个键时，将生成一个输入报告来标识该密钥。 释放密钥时，将发出使用情况值 = 0 的输入报告。
-   一次只能有一个使用情况处于活动状态。 使用者控件不允许同时按多个按钮。 当发送新的使用情况时，会假定释放上一个密钥的使用情况。
-   亮度向上/向下是 retriggering 键，并且其重复率由 Windows 处理。 如果用户按下了这些密钥，则硬件不应继续重新发送使用情况。 硬件只应在按下按钮时发送输入报告，并在释放钥匙时发送另一条。

## <a name="troubleshooting-common-errors"></a>排查常见错误


提示 \# 1：亮度增量/减量仅在移动系统上运行 (备有电池) 并且需要 Windows 8。

提示 \# 2：如果系统已连接到外部监视器，则亮度增量/减量将无法正常工作，因为旧监视器传输不支持向其发送消息的通道和消息。

 

 




