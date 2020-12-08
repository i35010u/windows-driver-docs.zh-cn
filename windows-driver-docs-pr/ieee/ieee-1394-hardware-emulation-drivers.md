---
title: IEEE 1394 硬件仿真驱动程序
description: IEEE 1394 硬件仿真驱动程序
keywords:
- IEEE 1394 WDK 总线，仿真驱动程序
- 1394 WDK 总线，仿真驱动程序
- 模拟驱动程序 WDK IEEE 1394 总线
- 硬件仿真驱动程序 WDK IEEE 1394 总线
- PDOs WDK IEEE 1394 总线
- virtual PDOs WDK IEEE 1394 总线
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 173e7c0bf73f5ce0c33d987e42a70d573df0375a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96808825"
---
# <a name="ieee-1394-hardware-emulation-drivers"></a>IEEE 1394 硬件仿真驱动程序





模拟驱动程序可以通过将单位目录添加到系统的配置 ROM 来模拟实际的 IEEE 硬件。 然后，仿真驱动程序会截获来自外部节点的请求并模拟由实际硬件设备公开的1394寄存器。

Microsoft 提供了一种虚拟设备机制，供应商可使用该机制来实现模拟驱动程序。

有关如何创建虚拟设备的信息，请参阅 [创建 IEEE 1394 虚拟设备](./creating-ieee-1394-virtual-devices.md)。

有关如何删除虚拟设备的信息，请参阅 [删除 IEEE 1394 虚拟设备](./removing-ieee-1394-virtual-devices.md)。

除了少数例外情况，仿真驱动程序可以使用完整的 1394 DDI，其方式与真实设备的函数驱动程序相同。 有关实际设备和虚拟设备使用 1394 DDI 的方式的说明，请参阅 [IEEE 1394 虚拟设备驱动程序中的支持请求](./supporting-requests-in-ieee-1394-virtual-device-drivers.md)。

 

