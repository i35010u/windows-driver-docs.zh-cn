---
title: 顶级集合
description: 顶级集合
ms.assetid: dcbee8e3-d03a-45c8-92e4-0897b9f55177
keywords:
- WDK HID 顶级集合
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: aecf67d9b3ef2e1e242ff26dc865421935e25eb3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56547158"
---
# <a name="top-level-collections"></a>顶级集合




一个*顶部级别集合*是一组面向特定软件使用者 （或使用者的类型） 的功能的功能。 例如，顶部级别集合可能被描述为键盘、 鼠标、 使用者控件、 传感器、 显示，等等。HID 规范中，在这些顶部级别集合也称为*应用程序集合*。 HID 设备描述用途的每个顶部级别集合，以允许 HID 功能的使用者，以标识在其中他们可能感兴趣的顶部级别集合。 在 Windows，HID 设备安装程序类 (HIDClass) 生成报表描述符所描述的每个顶部级别集合的唯一物理设备对象 (PDO)。
Microsoft 定义了*顶级集合*作为[HID 集合](hid-collections.md)的不嵌套的另一集合中。 与非的集合始终是一个顶级集合，而不考虑其 HID 类型。 具体而言，顶级集合不一定要**应用程序**集合，按照 USB HID 标准的定义。

报表描述符可以包含多个顶级集合。 HID 类驱动程序枚举输入设备的顶级集合并创建一个物理设备对象 (*PDO*) 为每个顶级集合。 用户模式应用程序或内核模式驱动程序可以通过打开其 PDO 并使用访问顶级集合[HIDClass 支持例程](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_hid/#hidclass-support-routines)并[HID 类驱动程序 Ioctl](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_hid/#hid-class-driver-ioctls)。

内部结构和顶级集合的功能是由以下所述：

-   一个[ **HIDP\_CAP** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hidpi/ns-hidpi-_hidp_caps)结构总结了顶级[集合的功能](collection-capability.md)。

-   [将集合链接](link-collections.md)描述顶级集合内包含的嵌套子集合的组织。

-   [按钮功能数组](button-capability-arrays.md)并[值功能数组](value-capability-arrays.md)描述支持的顶级集合的控件的功能。

 





