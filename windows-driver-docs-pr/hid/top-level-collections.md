---
title: 顶级集合
description: 顶级集合
keywords:
- 顶级集合 WDK HID
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 691ed7445dc07776a1092e0e79061e328ea5f3e7
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96820280"
---
# <a name="top-level-collections"></a>顶级集合




*顶层集合* 是一种面向特定软件使用者的功能分组 (或类型的使用者) 功能。 例如，可以将顶级集合描述为键盘、鼠标、使用者控件、传感器、显示器等。在 HID 规范中，这些顶级集合也称为 *应用程序集合*。 HID 设备描述了每个顶级集合的用途，以便允许 HID 功能的使用者识别它们可能感兴趣的顶级集合。 在 Windows 中，HID 设备安装程序类 (HIDClass) 为报表描述符所描述的每个顶级集合 (PDO) 生成唯一的物理设备对象。
Microsoft 将 *顶级集合* 定义为未嵌套在另一个集合中的 [HID 集合](hid-collections.md) 。 Unnested 集合始终是顶级集合，而不考虑其 HID 类型。 特别是，顶级集合不必是 **应用程序** 集合，如 USB HID 标准所定义。

一个报表描述符可包含多个顶级集合。 HID 类驱动程序枚举输入设备的顶级集合，并为每个顶级集合 (*PDO*) 创建物理设备对象。 用户模式应用程序或内核模式驱动程序可以通过打开其 PDO 并使用 [HIDClass 支持例程](/windows-hardware/drivers/ddi/_hid/#hidclass-support-routines) 和 [HID 类驱动程序 IOCTLs](/windows-hardware/drivers/ddi/_hid/#hid-class-driver-ioctls)来访问顶级集合。

顶级集合的内部结构和功能如下所述：

-   [**HIDP \_ cap**](/windows-hardware/drivers/ddi/hidpi/ns-hidpi-_hidp_caps)结构汇总了顶级 [集合的功能](collection-capability.md)。

-   [链接集合](link-collections.md) 描述包含在顶级集合内的嵌套子集合的组织。

-   [按钮功能数组](button-capability-arrays.md) 和 [值功能数组](value-capability-arrays.md) 描述由顶级集合支持的控件的功能。

