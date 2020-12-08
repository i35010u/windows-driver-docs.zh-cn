---
title: HID 集合概述
description: HID 集合是有意义的 HID 控件和它们各自的 HID 用法的分组。
keywords:
- 人体学接口设备 WDK、集合
- HID WDK，集合
- 交互式输入设备 WDK，集合
- 输入设备 WDK，集合
- 集合 WDK HID
- 集合 WDK HID，关于 HID 集合
- 子集合 WDK HID
- 人体学接口设备 WDK，控件
- HID WDK，控件
- 交互式输入设备 WDK，控件
- 输入设备 WDK，控件
- 控制 WDK HID
- HID 集合 WDK
- HID 集合 WDK，关于 HID 集合
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c51c13f29c866f903b98491d17dc4f247557e0c7
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838915"
---
# <a name="hid-collections-overview"></a>HID 集合概述


*Hid 集合* 是有意义的 hid 控件和它们各自的 [hid 用法](hid-usages.md)的分组。

如果控件以逻辑方式相关或在功能上依赖于其他控件，则应将它们组合在一起。 例如，键盘上的 SHIFT 键和字母键不应属于单独的集合。 集合可以 *具有嵌套子集合，* 也称为 [链接集合](link-collections.md)。 报表描述符定义了一个或多个 [顶级集合](top-level-collections.md)，以及与每个集合关联的报表项定义了一个或多个 HID 报表。




Windows 扩展了 HID 集合的概念，包括以下内容：

[顶级集合](top-level-collections.md)

[Windows 为系统使用打开的顶级集合](top-level-collections-opened-by-windows-for-system-use.md)

[Preparsed 数据](preparsed-data.md)

[链接集合](link-collections.md)

[集合功能](collection-capability.md)

[Button 功能数组](button-capability-arrays.md)

[值功能阵列](value-capability-arrays.md)

[数据索引](data-indices.md)

 

 




