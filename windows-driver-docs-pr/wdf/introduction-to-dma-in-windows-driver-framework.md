---
title: Windows 驱动程序框架中的 DMA 简介
description: Windows 驱动程序框架中的 DMA 简介
ms.assetid: 9bcd8ac1-f3dd-4bb3-a671-51c9465f8efa
keywords:
- DMA 操作 WDK KMDF 有关 DMA 操作
- 主总线 DMA WDK KMDF，有关 DMA 操作
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4a862b13160c7f079c6b82584d01d60b30e6c075
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63378109"
---
# <a name="introduction-to-dma-in-windows-driver-framework"></a>Windows 驱动程序框架中的 DMA 简介


\[仅适用于 KMDF\]




在 Windows 7 及更早版本，内核模式驱动程序框架 (KMDF) 支持仅总线 master 直接内存访问 (DMA) 设备。 此类设备包含其自己 DMA 控制器。

系统上的芯片 (SoC) – 基于平台运行 Windows 8 和更高版本，该框架还支持系统模式 DMA，其中多个设备共享单个的多渠道 DMA 控制器。

框架的 DMA 支持包括：

-   Framework DMA 对象和驱动程序用于将输入/输出请求转换成 DMA 操作方法的一组。

-   一组配置设备的 DMA 行为，不同的事件发生时的驱动程序所提供事件回调函数。

该框架支持这两种单一的数据包和散播-聚集 DMA 传输。 它还支持常见的缓冲区的使用。

SoC 基于在平台上运行 Windows 8 及更高版本，该框架支持单个数据包系统模式 DMA 传输。 有关详细信息，请参阅[支持系统模式 DMA](supporting-system-mode-dma.md)。

框架执行的操作不支持系统模式基于 PC 的平台上的 DMA 传输。

 

 





