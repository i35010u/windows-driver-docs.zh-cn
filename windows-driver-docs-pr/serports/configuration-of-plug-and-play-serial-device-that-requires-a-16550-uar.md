---
title: 为 16550 UART 接口配置 PnP 串行设备
description: 需要 16550 UART-Compatible 接口的即插即用串行设备的配置
keywords:
- 即插即用串行设备 WDK
- 串行设备 WDK，即插即用
- 通用异步接收器-发射器 WDK 串行设备
- UART WDK 串行设备
- 16550 UART 兼容的接口 WDK 串行设备
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2572c3d018659b9d50ebb7be870263377792d12a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96812057"
---
# <a name="configuration-of-plug-and-play-serial-device-that-requires-a-16550-uart-compatible-interface"></a>需要 16550 UART-Compatible 接口的即插即用串行设备的配置





本部分介绍硬件、驱动程序和设备堆栈的典型配置，该配置用于：

-   支持即插即用。

-   需要 16550 UART 兼容接口。

-   未连接到 RS-232 端口。

例如，使用调制解调器的 PCMCIA 卡。

下图显示了一个示例 toaster 设备的典型配置，以及一个需要 16550 UART 兼容接口的示例 blender 设备。

![左图： pcmcia 卡上的即插即用 toaster 设备的硬件配置。 右图：针对 pcmcia 卡上的即插即用 toaster 设备配置驱动程序和设备堆栈](images/ser3.png)

在这些配置中，Toaster 设备是 PCMCIA 总线上的子设备。 PCMCIA 总线驱动程序在枚举 PCMCIA 卡时为 Toaster 设备创建 PDO。 Toaster 设备的 INF 文件将串行指定为较低级别的设备筛选器驱动程序。 串行为硬件设备提供 16550 UART 兼容的接口。 Toaster 驱动程序创建 FDO 并将其附加到 Toaster 设备堆栈。

 

 




