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
ms.openlocfilehash: a0d901d240db82930f88d2ee2f9692d407338a82
ms.sourcegitcommit: 3040b84a9cc5d5594cb829f15c2bb114a28d5120
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/05/2020
ms.locfileid: "93365427"
---
# <a name="bus-drivers"></a>总线驱动程序





*总线驱动程序* 服务总线控制器、适配器或桥 (参阅 [可能的驱动程序层](types-of-wdm-drivers.md#possible-driver-layers)) 。 Microsoft 为大多数常见总线（如 PCI、PnpISA、SCSI 和 USB）提供总线驱动程序。 其他总线驱动程序可由 Ihv 或 Oem 提供。 总线驱动程序是必需的驱动程序;计算机上的每个总线类型都有一个总线驱动程序。 如果计算机上有多个相同类型的总线，则总线驱动程序可以为多个总线提供服务。

总线驱动程序的主要职责是：

-   枚举其总线上的设备。

-   响应即插即用 Irp 和电源管理 Irp。

-   对某些总线) 的总线 (执行多路复用。

-   一般在其总线上管理设备。

总线驱动程序本质上是 [函数驱动程序](function-drivers.md) ，也会枚举子级。

在枚举过程中，总线驱动程序标识其总线上的设备，并为它们创建设备对象。  (有关设备对象的信息，请参阅 [设备对象和设备堆栈](introduction-to-device-objects.md)。 ) 总线驱动程序用于识别连接的设备的方法取决于特定总线。

总线驱动程序代表其总线上的设备执行某些操作，包括访问设备寄存器以物理方式更改设备的电源状态。 例如，当设备进入睡眠状态时，总线驱动程序会将设备寄存器设置为使设备进入正确的设备电源状态。

但请注意，总线驱动程序不会处理连接到其总线的子设备的读取和写入请求。 对子设备的读取和写入请求由子设备的 [函数驱动程序](function-drivers.md)处理。 仅当子设备在 *raw 模式下* 使用时，父总线驱动程序才会处理设备的读取和写入操作。

由于总线驱动程序充当控制器、适配器或网桥的函数驱动程序，因此它还管理这些组件的设备电源策略。

总线驱动程序可以实现为驱动程序/微型驱动程序对，SCSI 端口/微型端口驱动程序对驱动 SCSI 主机总线适配器 (HBA) 的方式。 在此类驱动程序对中，微型驱动程序链接到第二个驱动程序，该驱动程序是一个 DLL。

 

 




