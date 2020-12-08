---
title: 通过 16550 UART 接口配置 PnP 多功能串行设备
description: 在需要 16550 UART-Compatible 接口的多功能设备上配置即插即用串行设备
keywords:
- 即插即用串行设备 WDK
- 串行设备 WDK，即插即用
- 通用异步接收器-发射器 WDK 串行设备
- UART WDK 串行设备
- 16550 UART 兼容的接口 WDK 串行设备
- 多功能设备
- 多功能设备 WDK 串行设备
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f09aacc8c44e13687a3d5ba42a3ed9ae0d0322a1
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96812063"
---
# <a name="configuration-of-plug-and-play-serial-device-on-a-multifunction-device-that-requires-a-16550-uart-compatible-interface"></a>在需要 16550 UART-Compatible 接口的多功能设备上配置即插即用串行设备





本部分介绍适用于多功能串行设备的硬件、驱动程序和设备堆栈的配置：

-   支持即插即用。

-   需要 16550 UART 兼容接口。

-   未连接到 RS-232 端口。

具体的例子是具有调制解调器和 LAN 适配器的 PCMCIA 卡。

下图显示了一个示例 toaster 设备的典型配置，以及一个需要 16550 UART 兼容接口的示例 blender 设备

![说明多功能 pcmcia 卡上 toaster 的硬件和驱动程序和设备堆栈配置，以及 toaster 和 blender 的示意图](images/ser4.png)

在这些配置中，Toaster 设备是多功能设备上的子设备，而多功能设备是 PCMCIA 总线上的子设备。

INF 文件和 Toaster 设备的安装程序将串行驱动程序安装为较低级别的设备筛选器驱动程序，以便为 Toaster 设备提供 16550 UART 兼容的接口。 Toaster 驱动程序创建 FDO 并将其附加到串行驱动程序筛选器。

 

 




