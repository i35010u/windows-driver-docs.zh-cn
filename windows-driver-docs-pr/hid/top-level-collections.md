---
title: 顶级集合
description: 顶级集合
ms.assetid: dcbee8e3-d03a-45c8-92e4-0897b9f55177
keywords:
- 顶级集合 WDK HID
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4615d9099b1d66b6199f96ceda341997f9164145
ms.sourcegitcommit: 9145bffd4cc3b990a9ebff43b588db6ef2001f5d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/09/2020
ms.locfileid: "89592449"
---
# <a name="top-level-collections"></a>顶级集合




*顶层集合*是一种面向特定软件使用者的功能分组 (或类型的使用者) 功能。 例如，可以将顶级集合描述为键盘、鼠标、使用者控件、传感器、显示器等。在 HID 规范中，这些顶级集合也称为 *应用程序集合*。 HID 设备描述了每个顶级集合的用途，以便允许 HID 功能的使用者识别它们可能感兴趣的顶级集合。 在 Windows 中，HID 设备安装程序类 (HIDClass) 为报表描述符所描述的每个顶级集合 (PDO) 生成唯一的物理设备对象。
Microsoft 将 *顶级集合* 定义为未嵌套在另一个集合中的 [HID 集合](hid-collections.md) 。 Unnested 集合始终是顶级集合，而不考虑其 HID 类型。 特别是，顶级集合不必是 **应用程序** 集合，如 USB HID 标准所定义。

一个报表描述符可包含多个顶级集合。 HID 类驱动程序枚举输入设备的顶级集合，并为每个顶级集合 (*PDO*) 创建物理设备对象。 用户模式应用程序或内核模式驱动程序可以通过打开其 PDO 并使用 [HIDClass 支持例程](/windows-hardware/drivers/ddi/_hid/#hidclass-support-routines) 和 [HID 类驱动程序 IOCTLs](/windows-hardware/drivers/ddi/_hid/#hid-class-driver-ioctls)来访问顶级集合。

顶级集合的内部结构和功能如下所述：

-   [**HIDP \_ cap**](/windows-hardware/drivers/ddi/hidpi/ns-hidpi-_hidp_caps)结构汇总了顶级[集合的功能](collection-capability.md)。

-   [链接集合](link-collections.md) 描述包含在顶级集合内的嵌套子集合的组织。

-   [按钮功能数组](button-capability-arrays.md) 和 [值功能数组](value-capability-arrays.md) 描述由顶级集合支持的控件的功能。

