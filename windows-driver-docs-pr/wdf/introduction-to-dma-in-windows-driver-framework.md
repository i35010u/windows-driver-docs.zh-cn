---
title: Windows 驱动程序框架中的 DMA 简介
description: Windows 驱动程序框架中的 DMA 简介
ms.assetid: 9bcd8ac1-f3dd-4bb3-a671-51c9465f8efa
keywords:
- DMA 操作 WDK KMDF，关于 DMA 操作
- 总线主控 DMA WDK KMDF，关于 DMA 操作
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c8a50cb13e6778122d13df46a4c62ca80cddd4ff
ms.sourcegitcommit: 2d999dcf63d3b67bf74777d6fae29d96b98141ec
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/11/2020
ms.locfileid: "84714826"
---
# <a name="introduction-to-dma-in-windows-driver-framework"></a>Windows 驱动程序框架中的 DMA 简介


\[仅适用于 KMDF\]




在 Windows 7 和更早版本中，内核模式驱动程序框架（KMDF）仅支持总线主机直接内存访问（DMA）设备。 此类设备包含它们自己的 DMA 控制器。

在运行 Windows 8 和更高版本的基于芯片（SoC）的平台上，该框架还支持系统模式 DMA，在这种情况下，多个设备共享单个多通道 DMA 控制器。

框架的 DMA 支持包括：

-   一组框架 DMA 对象和方法，驱动程序使用这些对象和方法将 i/o 请求转换为 DMA 操作。

-   一组驱动程序提供的事件回调函数，这些函数将设备的 DMA 行为配置为不同的事件发生。

此框架支持单数据包和散播/聚集 DMA 传输。 它还支持使用公用缓冲区。

在运行 Windows 8 和更高版本的基于 SoC 的平台上，该框架支持单数据包系统模式 DMA 传输。 有关详细信息，请参阅[支持系统模式 DMA](supporting-system-mode-dma.md)。

此框架不支持基于 PC 的平台上的系统模式 DMA 传输。

 ## <a name="related-topics"></a>相关主题
 
 [为设备驱动程序启用 DMA 重新映射](https://docs.microsoft.com/windows-hardware/drivers/pci/enabling-dma-remapping-for-device-drivers)

 





