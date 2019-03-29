---
title: HID 集合
description: HID 集合是 HID 控件和其各自的 HID 用法的有意义分组。
ms.assetid: 2d3efb38-4eba-43db-8cff-9fac30209952
keywords:
- 人机接口设备 WDK 集合
- HID WDK 集合
- 交互式输入的设备 WDK，集合
- 输入设备 WDK，集合
- WDK HID 集合
- 有关 HID 集合集合 WDK HID，
- WDK HID 的子集合
- 人机接口设备 WDK 控件
- HID WDK 控件
- 交互式输入的设备 WDK，控件
- 输入设备 WDK，控件
- WDK HID 的控件
- HID 的集合 WDK
- HID 的集合 WDK，关于 HID 集合
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6ce277d5ec85cadb9ebfe59c1ef40e01c4daf0af
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56577439"
---
# <a name="hid-collections"></a>HID 集合


一个*HID 集合*是有意义的 HID 控件和其各自分组[HID 用法](hid-usages.md)。

如果逻辑上相关或在功能上依赖于另一个应一起分组控件。 例如，SHIFT 键和键盘上的字母键应不属于单独的集合。 集合可以具有嵌套*子集合*，也称为[将集合链接](link-collections.md)。 报告描述符定义一个或多个[顶级集合](top-level-collections.md)，并与每个集合关联的报表项定义一个或多个 HID 报表。




Windows 扩展 HID 集合，包括以下的概念：

[顶级集合](top-level-collections.md)

[打开 Windows 系统的顶级集合使用](top-level-collections-opened-by-windows-for-system-use.md)

[Preparsed 的数据](preparsed-data.md)

[链接集合](link-collections.md)

[集合功能](collection-capability.md)

[按钮功能数组](button-capability-arrays.md)

[值功能数组](value-capability-arrays.md)

[数据索引](data-indices.md)

 

 




