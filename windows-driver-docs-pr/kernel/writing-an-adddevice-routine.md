---
title: 编写 AddDevice 例程
description: 编写 AddDevice 例程
ms.assetid: 93a272f4-888c-4cc8-b013-c6313c10a8d8
keywords:
- 标准驱动程序例程 WDK 内核，AddDevice 例程
- 驱动程序例程 WDK 内核，AddDevice 例程
- 例程 WDK 内核，AddDevice 例程
- AddDevice 例程的 WDK 内核
- 系统空间内存分配 WDK 内核
- 系统资源存储 WDK 内核
- 存储系统资源
- 设备对象 WDK 内核，创建
- 设备初始化 WDK 内核
- 正在初始化设备
- AddDevice 例程 WDK 内核，关于 AddDevice 例程
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: c5bf2a0de1ada2faa7816a4610588a941725560f
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89190947"
---
# <a name="writing-an-adddevice-routine"></a>编写 AddDevice 例程





支持 PnP 的任何驱动程序必须具有 [*AddDevice*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device) 例程。 *AddDevice*例程创建一个或多个设备对象，表示驱动程序对其执行 i/o 请求的物理、逻辑或虚拟设备。 它还会将设备对象附加到设备堆栈，因此设备堆栈将包含与设备关联的每个驱动程序的设备对象。

PnP 管理器为驱动程序控制的每个设备调用驱动程序的 *AddDevice* 例程。 当首次) 枚举设备时，将在 (系统初始化期间调用*AddDevice*例程，并在系统运行时对新设备进行枚举。

本节包含下列主题：

[函数或筛选器驱动程序中的 AddDevice 例程](adddevice-routines-in-function-or-filter-drivers.md)

[总线驱动程序中的 AddDevice 例程](adddevice-routines-in-bus-drivers.md)

[有关编写 AddDevice 例程的指导原则](guidelines-for-writing-adddevice-routines.md)

 

