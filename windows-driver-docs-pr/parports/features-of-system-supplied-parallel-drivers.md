---
title: 系统提供的并行驱动程序的功能
description: 系统提供的并行驱动程序的功能
ms.assetid: 6d579a88-4608-4333-9789-e10c562fc644
keywords:
- 系统提供的并行驱动程序 WDK，关于系统提供的并行驱动程序
- Parclass 驱动程序
- Parport 驱动程序
- 功能设备对象 WDK 端口
- FDOs WDK 端口
- IEEE 1284 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f8b7d9be6ebaa7e400fab3ff127e0a4ee0eac336
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72831478"
---
# <a name="features-of-system-supplied-parallel-drivers"></a>系统提供的并行驱动程序的功能





本部分介绍系统提供的并行端口和设备连接到并行端口的并行驱动程序的功能。

除64位版本的 Microsoft Windows 以外，Windows 2000 和更高版本为附加到并行端口的即插即用设备提供并行端口功能驱动程序和并行端口总线驱动程序。 Microsoft 不提供适用于64位版本 Windows 的并行驱动程序。

Windows 2000 包括下列驱动程序：

-   *Parclass*是连接到并行端口的设备的并行端口总线驱动程序。 Parclass 的可执行映像是*parallel*。

-   *Parport*是并行端口功能驱动程序。 Parport 的可执行映像为*Parport*。

Parclass 和 Parport 的操作通过[内部设备控制对并行端口](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)和[并行端口回调例程](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)的请求密切连接起来。

在 Windows XP 和更高版本中，Parclass 已删除，Parport 提供并行端口功能驱动程序和并行端口总线驱动程序的功能。 Windows XP 中的 Parport 的可执行映像为*Parport*。

系统提供的并行端口函数驱动程序创建一个功能设备对象（FDO），用于表示系统中枚举的每个并行端口。 系统提供的并行端口总线驱动程序创建一个物理设备对象（PDO），该对象表示总线驱动程序在端口上枚举的每个并行设备。 客户端（例如[供应商提供的并行驱动程序](vendor-supplied-parallel-drivers.md)）通过并行设备的 PDO 提供的接口和设备的父端口的 FDO 操作并行设备。

除并行文档中所述的轻微操作差异外，[客户端接口到系统提供的并行驱动程序](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)在 windows 2000 与 windows XP 和更高版本中相同。

系统提供的并行驱动程序支持：

-   传统的并行端口、标准的并行端口设备、与 IEEE 1284 兼容的设备、符合 IEEE 1284 的设备和 IEEE 1284.3 菊花链设备

-   大多数通信模式，包括 Centronics 模式、IEEE 1284 模式、扩展功能端口（ECP）模式和增强型并行端口（EPP）模式

-   即插即用、电源管理和 Windows Management Instrumentation （WMI）

-   共享访问系统上安装的所有并行端口

-   对所有并行设备的原始访问

-   操作并行端口和设备的 IOCTLs 和回调--请参阅[IOCTL 和对并行端口和设备的回调支持](ioctl-and-callback-support-for-parallel-ports-and-devices.md)

系统提供的并行驱动程序提供对 IEEE 1284.3 设备的以下*部分*支持：

- 在功能上等效于*服务提供程序接口*的设备控制请求和回调例程的组合。 请参阅 IEEE P 1284.3 规范中的*服务提供程序接口（SPI）* 。

- 在 IEEE P 1284.3 规范的*菊花链式*子句中定义的多个 ieee 1284.3 菊花<em>链设备和</em>链端设备的选择和操作。

- 支持数据链路层的基本服务（如 IEEE P 1284.3 规范的*数据链路层*子句中所指定）--请参阅[连接到 Ieee 1284.3 数据链接设备](connecting-to-an-ieee-1284-3-data-link-device.md)。

系统提供的并行驱动程序*不支持*以下 IEEE 1284.3 规范：

-   Multiplexors，正如 IEEE P 1284.3 规范的*多重多重*子句中所指定。

    在将来的 Windows 版本中，无计划支持此功能。

-   IEEE 1284.3 菊花链设备的中断。

系统提供的并行驱动程序创建：

-   设备对象、接口和未受保护的符号链接，如[并行端口和设备的设备堆栈](device-stacks-for-parallel-ports-and-devices.md)中所述。

-   每个并行端口的工作队列。

    系统提供的并行端口函数驱动程序对分配并行端口的 i/o 请求进行排队，并选择连接到并行端口的 IEEE 1284.3 设备。

-   每个并行设备的工作线程和工作队列。

    系统提供的并行端口总线驱动程序在无法立即完成以下 i/o 请求的情况下将队列排队：读取、写入、设备控制和内部设备控制。

有关如何操作连接到并行端口的并行端口和设备的详细信息，请参阅：

[并行端口和设备简介](introduction-to-parallel-ports-and-devices.md)

[供应商提供的并行驱动程序](vendor-supplied-parallel-drivers.md)

[系统提供的并行驱动程序的客户端接口](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)

有关并行端口和设备标准的信息，请参阅以下规范：

-   IEEE Std 1284-1994，适用于个人计算机的双向并行外围设备的 IEEE 标准信号方法

-   IEEE P 1284.3，适用于符合 IEEE 1284-1994 标准的外围设备和主机适配器的接口和协议扩展标准，草稿 D 6.00，1998

 

 




