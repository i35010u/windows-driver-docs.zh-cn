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
ms.openlocfilehash: e06de0746a89551f61f37c65f9b4eef882c9d308
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838298"
---
# <a name="writing-an-adddevice-routine"></a>编写 AddDevice 例程





支持 PnP 的任何驱动程序必须具有[*AddDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device)例程。 *AddDevice*例程创建一个或多个设备对象，表示驱动程序对其执行 i/o 请求的物理、逻辑或虚拟设备。 它还会将设备对象附加到设备堆栈，因此设备堆栈将包含与设备关联的每个驱动程序的设备对象。

PnP 管理器为驱动程序控制的每个设备调用驱动程序的*AddDevice*例程。 *AddDevice*例程在系统初始化期间调用（当首次枚举设备时），并在系统运行时枚举新设备。

本部分包含以下主题：

[函数或筛选器驱动程序中的 AddDevice 例程](adddevice-routines-in-function-or-filter-drivers.md)

[总线驱动程序中的 AddDevice 例程](adddevice-routines-in-bus-drivers.md)

[AddDevice 例程编写准则](guidelines-for-writing-adddevice-routines.md)

 

 




