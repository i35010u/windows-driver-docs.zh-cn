---
title: 设备对象简介
description: 设备对象简介
ms.assetid: 310a2344-f3bc-4a7a-8e1e-63232ecd4cbe
keywords:
- 设备对象 WDK 内核，有关设备对象
- 多个设备对象 WDK 内核
- 设备堆栈 WDK 内核，有关设备堆栈
- 设备扩展 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8fcde47110d5d072391ecfa09294903e546c2319
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56569446"
---
# <a name="introduction-to-device-objects"></a>设备对象简介





操作系统表示设备*设备对象*。 一个或多个设备对象都与每个设备关联。 设备对象作为目标的设备上的所有操作。

内核模式驱动程序必须创建至少一个设备对象的每个设备，但存在以下例外：

-   有一个关联的类或端口驱动程序的微型驱动程序不需要创建自己的设备对象。 包含类或端口驱动程序创建设备对象，并将调度到微型驱动程序的操作。

-   驱动程序属于的设备特定于类型的子系统，例如 NDIS 微型端口驱动程序，必须创建由子系统及其设备对象。

请参阅你的特定设备类型以确定您的驱动程序创建其自己的设备对象的文档。

某些设备对象不表示物理设备。 仅限软件的驱动程序，它处理 I/O 请求，但不将这些请求传递到硬件，仍必须创建一个设备对象来表示其操作的目标。

有关您的驱动程序如何创建设备对象的详细信息，请参阅[创建一个设备对象](creating-a-device-object.md)。

设备由多个设备对象，一个用于处理 I/O 请求的设备驱动程序堆栈中每个驱动程序通常表示。 设备的设备对象分为*设备堆栈*。 在设备上执行操作时，系统将传递[ **IRP** ](https://msdn.microsoft.com/library/windows/hardware/ff550694)数据结构中设备堆栈的顶部的设备对象的驱动程序。 每个驱动程序处理 IRP，或将其传递给设备堆栈中的下一步下一个设备对象与关联的驱动程序。 有关设备堆栈的详细信息，请参阅[WDM 设备对象和设备堆栈](wdm-device-objects-and-device-stacks.md)。 有关 Irp 的详细信息，请参阅[处理 Irp](handling-irps.md)。

设备对象表示由[**设备\_对象**](https://msdn.microsoft.com/library/windows/hardware/ff543147)结构，由对象管理器管理。 对象管理器提供的其他系统对象的设备对象相同的功能。 具体而言，可以命名的设备对象，并指定的设备对象可以在其上打开的句柄。 有关指定的设备对象的详细信息，请参阅[名为设备对象](named-device-objects.md)。

系统提供的每个设备对象，调用该驱动程序可用于特定于设备的存储的设备扩展的专用的存储。 创建并由系统和设备对象释放设备扩展。 有关详细信息，请参阅[设备扩展](device-extensions.md)。

下图说明了设备对象与 I/O 管理器之间的关系。

![说明一个设备对象的关系图](images/3devobj.png)

该图显示的成员**设备\_对象**感兴趣的驱动程序编写器的结构。 有关这些成员的详细信息，请参阅[创建一个设备对象](creating-a-device-object.md)，[初始化设备对象](initializing-a-device-object.md)，并[属性的设备对象](properties-of-device-objects.md)。

 

 




