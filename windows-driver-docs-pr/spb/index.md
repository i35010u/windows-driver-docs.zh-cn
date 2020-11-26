---
title: 简单外设总线 (SPB) 驱动程序设计指南
description: 此部分介绍如何为简单外设总线 (SPB) 控制器设备或连接到 SPB 的外围设备编写驱动程序。
ms.assetid: 7E9F688B-F473-4343-A1E0-525273391935
ms.date: 04/20/2017
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
ms.openlocfilehash: 82e2a5f0aef3f0c610ea6654d56c817ad09142cf
ms.sourcegitcommit: 0c3cab853b0b75149b7604eef03275f997792a84
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/26/2020
ms.locfileid: "96157269"
---
# <a name="simple-peripheral-bus-spb-driver-design-guide"></a>简单外设总线 (SPB) 驱动程序设计指南

此部分介绍如何为[简单外设总线](/previous-versions/hh450903(v=vs.85)) (SPB) 控制器设备或连接到 SPB 的外围设备编写驱动程序。 SPB 类别包含总线，如 I²C 和 SPI。 SPB 控制器设备的硬件供应商会提供 SPB 控制器驱动程序来管理控制器中的硬件功能。 该驱动程序可能支持一系列类似的控制器设备。 SPB 连接的外围设备的硬件供应商会提供 SPB 外设驱动程序来管理外围设备中的硬件功能。 该驱动程序可能支持一系列的外围设备，这些设备跨各种提供兼容 SPB 的硬件平台。

在 Windows 8 之前的 Windows 版本中，操作系统从电脑主板上通过 SPB 连接的设备获取信息时，只能间接地通过平台固件进行。 从 Windows 8 开始，硬件供应商可以提供 Windows 驱动程序来直接控制器 SPB 控制器及其通过 SPB 连接的外围设备，并提供这些设备供操作系统和应用程序使用。 有关详细信息，请参阅 [SPB Controller Drivers](./spb-controller-drivers.md)（SPB 控制器驱动程序）和 [SPB Peripheral Device Drivers](./spb-peripheral-device-drivers.md)（SPB 外围设备驱动程序）。

SPB 频繁用于将低速外围设备连接到主板芯片组和系统单芯片 (SoC) 模块。 与并行总线相比，集成电路只需较少的引脚即可连接到串行总线，每个时钟周期传输多个比特的数据。 通常情况下，SPB 用在成本敏感型应用程序中。在这些应用程序中，比数据传输速度更重要的是引脚计数要低且连接要简单。 由于 SPB 以低速运行，需要的电气连接少，因此经常用于那些必须保留电池电量的应用程序中。

例如，便携式计算机中的电脑主板可以使用 I²C 总线与监视电池电量的低速设备通信。 类似地，智能手机或其他移动设备中的 SoC 模块可以使用 I²C 总线连接到传感器设备（例如加速计、GPS 设备或温度传感器）。

SPB 不是即插即用总线。 外为设备通常有到 SPB 的固定连接，不能移除。 即使可以将外围设备从 SPB 上的某个槽拔出，该槽通常也是专用于该设备的。 在系统启动期间，硬件平台中的 ACPI 固件会为即插即用管理器枚举通过 SPB 连接的外围设备，并指定专用于每个设备的硬件资源。

连接 ID（用于标识设备到 SPB 的连接）包括在这些资源中。 连接 ID 封装的信息（例如，总线地址和总线时钟频率）是 SPB 控制器建立到设备的连接所需的。 其他硬件资源可能包含一个中断，供驱动程序将其 ISR 连接到其中。 但是，设备的硬件资源不包括用于设备寄存器的存储。 通过 SPB 连接的外围设备未进行存储映射，只能通过 SPB 进行访问。 有关详细信息，请参阅 [Connection IDs for SPB-Connected Peripheral Devices](./connection-ids-for-spb-connected-peripheral-devices.md)（SPB 连接的外围设备的连接 ID）。

在将中断请求从外围设备传达至处理器时，SPB 不提供任何特定于总线的方式。 与之相反，通过 SPB 连接的外围设备通过单独的硬件路径来指示某个中断，该路径位于 SPB 和 SPB 控制器外部。 通过 SPB 连接的外围设备的中断服务例程 (ISR) 必须在 IRQL = PASSIVE\_LEVEL 的情况下运行，这样它就可以同步发送 I/O 请求，以便通过 SPB 按顺序访问设备的硬件寄存器。 有关详细信息，请参阅 [Interrupts from SPB-Connected Peripheral Devices](./interrupts-from-spb-connected-peripheral-devices.md)（来自通过 SPB 连接的外围设备的中断）。
