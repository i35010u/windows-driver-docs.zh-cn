---
title: 系统提供的并行驱动程序的功能
description: 系统提供的并行驱动程序的功能
ms.assetid: 6d579a88-4608-4333-9789-e10c562fc644
keywords:
- 系统提供并行的驱动程序 WDK，有关系统提供并行的驱动程序
- Parclass 驱动程序
- Parport 驱动程序
- 功能的设备对象 WDK 端口
- FDOs WDK 端口
- IEEE 1284 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7a3069fb56abe1b79b2817f593c7fcd56f154dc6
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382078"
---
# <a name="features-of-system-supplied-parallel-drivers"></a>系统提供的并行驱动程序的功能





本部分介绍系统提供并行和驱动程序的并行端口连接到并行端口的设备的功能。

除了 64 位版本的 Microsoft Windows 中，Windows 2000 及更高版本为插到并行端口连接的设备提供并行端口功能驱动程序和并行端口总线驱动程序。 对于 64 位版本的 Windows，Microsoft 不提供并行的驱动程序。

Windows 2000 包括以下驱动程序：

-   *Parclass*是连接到并行端口的设备的并行端口总线驱动程序。 是可执行映像的 Parclass *parallel.sys*。

-   *Parport*是并行端口功能驱动程序。 是可执行映像的 Parport *parport.sys*。

通过紧密连接模拟 Parclass 和 Parport[内部设备控制请求的并行端口](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)和[并行端口回调例程](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)。

在 Windows XP 及更高版本，Parclass 被删除，并且 Parport 提供并行端口功能驱动程序和并行端口总线驱动程序的函数。 是可执行映像的 Windows XP 中 Parport *parport.sys*。

并行端口的系统提供的函数驱动程序创建一个表示系统中的每个并行端口的功能的设备对象 (FDO)。 并行端口的系统提供的总线驱动程序创建一个表示端口的总线驱动程序枚举每个并行设备的物理设备对象 (PDO)。 客户端，例如[供应商提供并行的驱动程序](vendor-supplied-parallel-drivers.md)，运行并行设备通过并行设备的 PDO 和设备的父端口的 FDO 提供的接口。

除了介绍在并行的文档中，次要操作区别之外[系统提供并行的驱动程序的客户端接口](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)与 Windows XP 及更高版本的 Windows 2000 中相同。

系统提供的并行驱动程序支持：

-   旧的并行端口、 标准的并行端口设备、 IEEE 1284 兼容的设备、 IEEE 1284 合规的设备和 IEEE 1284.3 菊花链设备

-   包括 Centronics 模式下，IEEE 1284 模式，扩展的功能端口 (ECP) 模式和增强的并行端口 (EPP) 模式的大多数通信模式

-   Plug and Play、 电源管理和 Windows Management Instrumentation (WMI)

-   共享访问系统上安装的所有并行端口

-   原始访问所有并行设备

-   Ioctl 和回调来操作的并行端口和设备-请参阅[IOCTL 和并行端口和设备的回调支持](ioctl-and-callback-support-for-parallel-ports-and-devices.md)

系统提供的并行驱动程序提供以下*分部*支持 IEEE 1284.3 设备：

- 设备控制请求和回调例程的组合，它在功能上等效于*服务提供程序接口*。 请参阅*服务提供程序接口 (SPI)* IEEE P1284.3 规范中。

- 所选内容和操作的多个 IEEE 1284.3 菊花链设备和最终的链设备<em>，作为</em>中定义*菊花链*IEEE P1284.3 规范的子句。

- 若要支持的数据的基本服务链接层中的规定*数据链路层*子句的 IEEE P1284.3 规范中-请参阅[连接到 IEEE 1284.3 数据链接设备](connecting-to-an-ieee-1284-3-data-link-device.md)。

系统提供的并行驱动程序*不支持*以下 IEEE 1284.3 规范：

-   Multiplexors 中的规定*多路传送器*IEEE P1284.3 规范的子句。

    没有计划为在 Windows 的未来版本中支持此功能。

-   IEEE 1284.3 菊花链设备的中断。

创建的系统提供的并行驱动程序：

-   设备对象、 接口和未受保护的符号链接，如中所述[并行端口和设备的设备堆栈](device-stacks-for-parallel-ports-and-devices.md)。

-   每个并行端口工作队列。

    若要分配的并行端口并选择附加到并行端口的 IEEE 1284.3 设备的并行端口 I/O 队列请求系统提供的函数驱动程序。

-   工作线程和工作队列的每个并行的设备。

    并行端口的系统提供的总线驱动程序以下的 I/O 请求排队，如果它不能立即完成这些： 读取、 写入、 设备控制和内部设备控制。

有关如何运行的并行端口和设备连接到并行端口的详细信息，请参阅：

[并行端口和设备简介](introduction-to-parallel-ports-and-devices.md)

[供应商提供的并行驱动程序](vendor-supplied-parallel-drivers.md)

[系统提供并行的驱动程序的客户端接口](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)

有关并行端口和标准设备信息，请参阅以下规范：

-   IEEE Std 1284 1994 年 IEEE 标准为个人计算机为双向并行外围接口信号方法

-   IEEE P1284.3、 接口和协议 IEEE 1284 1994年符合外围设备和主机适配器扩展标准草案 D6.00，1998 年 12 月 3 日

 

 




