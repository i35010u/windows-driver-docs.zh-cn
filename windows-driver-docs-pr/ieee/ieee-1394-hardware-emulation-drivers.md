---
title: IEEE 1394 硬件仿真驱动程序
description: IEEE 1394 硬件仿真驱动程序
ms.assetid: 44141072-e425-4983-9234-3ad79daa2017
keywords:
- IEEE 1394 WDK 总线，仿真驱动程序
- 1394 WDK 总线，仿真驱动程序
- 仿真驱动程序 WDK IEEE 1394 总线
- 硬件仿真驱动程序 WDK IEEE 1394 总线
- PDOs WDK IEEE 1394 总线
- 虚拟 PDOs WDK IEEE 1394 总线
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e5e00227bc9cc9b2252f19b55bbd39f989974bd2
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63376666"
---
# <a name="ieee-1394-hardware-emulation-drivers"></a>IEEE 1394 硬件仿真驱动程序





仿真驱动程序可以模拟实际 IEEE 硬件，通过将一个单元目录添加到系统的配置 rom。 仿真驱动程序然后截获来自外部节点请求并模拟实际的硬件设备公开的 1394年寄存器。

Microsoft 提供可用于实现仿真驱动程序供应商的虚拟设备机制。

有关如何创建虚拟设备的信息，请参阅[创建 IEEE 1394 虚拟设备](https://msdn.microsoft.com/library/windows/hardware/ff537065)。

有关如何删除虚拟设备的信息，请参阅[删除 IEEE 1394 虚拟设备](https://msdn.microsoft.com/library/windows/hardware/ff537630)。

只需几个例外情况之外，仿真驱动程序可以使用完整的 1394 DDI 方式将实际设备功能驱动程序将完全相同。 实部和虚拟设备使用 1394 DDI 方式的差异说明，请参阅[IEEE 1394 虚拟设备驱动程序中支持请求](https://msdn.microsoft.com/library/windows/hardware/ff538825)。

 

 




