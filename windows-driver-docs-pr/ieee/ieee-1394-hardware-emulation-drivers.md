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
ms.openlocfilehash: 4b9b58a1cb0bbe88a21a239ed77c028e0e2056fe
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385772"
---
# <a name="ieee-1394-hardware-emulation-drivers"></a>IEEE 1394 硬件仿真驱动程序





仿真驱动程序可以模拟实际 IEEE 硬件，通过将一个单元目录添加到系统的配置 rom。 仿真驱动程序然后截获来自外部节点请求并模拟实际的硬件设备公开的 1394年寄存器。

Microsoft 提供可用于实现仿真驱动程序供应商的虚拟设备机制。

有关如何创建虚拟设备的信息，请参阅[创建 IEEE 1394 虚拟设备](https://docs.microsoft.com/windows-hardware/drivers/ieee/creating-ieee-1394-virtual-devices)。

有关如何删除虚拟设备的信息，请参阅[删除 IEEE 1394 虚拟设备](https://docs.microsoft.com/windows-hardware/drivers/ieee/removing-ieee-1394-virtual-devices)。

只需几个例外情况之外，仿真驱动程序可以使用完整的 1394 DDI 方式将实际设备功能驱动程序将完全相同。 实部和虚拟设备使用 1394 DDI 方式的差异说明，请参阅[IEEE 1394 虚拟设备驱动程序中支持请求](https://docs.microsoft.com/windows-hardware/drivers/ieee/supporting-requests-in-ieee-1394-virtual-device-drivers)。

 

 




