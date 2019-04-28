---
title: 总线驱动程序
description: 总线驱动程序
ms.assetid: d1a92c06-882d-49dc-befa-5b9a9e8aecd7
keywords:
- 总线驱动程序 WDK WDM
- 枚举总线设备 WDK WDM
- 总线控制器 WDK WDM
- 适配器 WDK WDM
- 桥接 WDK WDM
- WDM 总线驱动程序 WDK
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: f9618484d66ecfeeea4834673a80023cbc996f63
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63338633"
---
# <a name="bus-drivers"></a>总线驱动程序





一个*总线驱动程序*服务总线控制器、 适配器或桥 (请参阅[可能驱动程序层](types-of-wdm-drivers.md#possible-driver-layers)图)。 Microsoft 提供了最常见的总线，例如 PCI、 PnpISA、 SCSI、 和 USB 总线驱动程序。 可以由 Ihv 或 Oem 提供其他总线驱动程序。 总线驱动程序是必需的驱动程序;没有为每种类型的计算机上的总线的一个总线驱动程序。 如果没有在计算机上的相同类型的多个总线，总线驱动程序可服务多个总线。

总线驱动程序的主要职责是：

-   枚举其总线上的设备。

-   响应插 Irp 和 Irp 的电源管理。

-   进行多路复用到总线 （适用于某些总线） 的访问权限。

-   以一般方式管理其总线上的设备。

总线驱动程序实质上是[函数的驱动程序](function-drivers.md)说明还枚举子项。

在枚举，总线驱动程序标识其总线上的设备，并为它们创建设备对象。 (有关设备对象的信息，请参阅[设备对象和设备堆栈](device-objects-and-device-stacks.md)。)总线驱动程序用于标识连接的设备的方法取决于特定的总线。

总线驱动程序对其总线，包括访问设备寄存器，若要更改设备的电源状态，以物理方式执行某些操作代表设备。 例如，当设备进入睡眠状态，总线驱动程序设置设备注册将设备放在正确的设备电源状态。

但请注意，总线驱动程序不会处理读取和写入请求的子设备连接到其总线。 读取和写入到子设备的请求都将处理由子设备的功能驱动程序 does 父总线驱动程序句柄读取和写入设备。

因为总线驱动程序充当其控制器、 适配器或桥的函数驱动程序，它还管理设备的电源策略为这些组件。

总线驱动程序可作为一个驱动程序/微型驱动程序对 SCSI 端口/微型端口驱动程序对驱动器的 SCSI 主机总线适配器 (HBA) 的方式。 在此类驱动程序对，微型驱动程序链接到第二个驱动程序，这是一个 DLL。

 

 




