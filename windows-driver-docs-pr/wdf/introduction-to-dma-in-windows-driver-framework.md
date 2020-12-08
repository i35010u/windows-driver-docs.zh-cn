---
title: Windows 驱动程序框架中的 DMA 简介
description: Windows 驱动程序框架中的 DMA 简介
keywords:
- DMA 操作 WDK KMDF，关于 DMA 操作
- 总线主控 DMA WDK KMDF，关于 DMA 操作
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1dd7a1c3ff99f062a76a5e226d1ba37a32650468
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96821739"
---
# <a name="introduction-to-dma-in-windows-driver-framework"></a>Windows 驱动程序框架中的 DMA 简介


\[仅适用于 KMDF\]




在 Windows 7 和更早版本中，Kernel-Mode Driver Framework (KMDF) 仅支持 (DMA) 设备的总线主直接内存访问。 此类设备包含它们自己的 DMA 控制器。

在运行 Windows 8 和更高版本的基于芯片 (SoC) 平台上的系统上，该框架还支持系统模式 DMA，其中多个设备共享单个多通道 DMA 控制器。

框架的 DMA 支持包括：

-   一组框架 DMA 对象和方法，驱动程序使用这些对象和方法将 i/o 请求转换为 DMA 操作。

-   一组驱动程序提供的事件回调函数，这些函数将设备的 DMA 行为配置为不同的事件发生。

此框架支持单数据包和散播/聚集 DMA 传输。 它还支持使用公用缓冲区。

在运行 Windows 8 和更高版本的基于 SoC 的平台上，该框架支持单数据包系统模式 DMA 传输。 有关详细信息，请参阅 [支持 System-Mode DMA](supporting-system-mode-dma.md)。

此框架不支持基于 PC 的平台上的系统模式 DMA 传输。

 ## <a name="related-topics"></a>相关主题
 
 [为设备驱动程序启用 DMA 重新映射](../pci/enabling-dma-remapping-for-device-drivers.md)

