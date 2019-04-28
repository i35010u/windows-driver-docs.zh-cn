---
title: WavePci 微型端口驱动程序
description: WavePci 微型端口驱动程序
ms.assetid: 8a166087-d158-4d49-a917-2a5a78b43cb4
keywords:
- 音频的微型端口驱动程序 WDK WavePci
- 微型端口驱动程序 WDK 音频 WavePci
- WavePci 微型端口驱动程序 WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a4c3f964af84e1da63b41271cd89c905e1626eaa
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63335230"
---
# <a name="wavepci-miniport-driver"></a>WavePci 微型端口驱动程序


## <span id="wavepci_miniport_driver"></span><span id="WAVEPCI_MINIPORT_DRIVER"></span>


**重要**  不再建议使用 WavePci，而是改用 WaverRT。

 

WavePci 微型端口驱动程序管理的物理内存中的任何位置从批呈现或具有可将音频数据到或传输的分散/聚拢 DMA 硬件的批捕获设备的硬件相关的函数。 应使用不具备的功能来执行散播-聚集传输或能够访问受限制的区域仅在物理内存中的波形设备[WaveCyclic 微型端口驱动程序](wavecyclic-miniport-driver.md)相反。

WavePci 微型端口驱动程序应实现两个接口：

-   **微型端口接口**执行微型端口驱动程序初始化、 通道枚举和流创建。

-   **流接口**管理批流，并会公开大部分的微型端口驱动程序的功能。

微型端口接口[IMiniportWavePci](https://msdn.microsoft.com/library/windows/hardware/ff536724)，继承中的方法[IMiniport](https://msdn.microsoft.com/library/windows/hardware/ff536698)接口。 IMiniportWavePci 提供了以下其他方法：

[**IMiniportWavePci::Init**](https://msdn.microsoft.com/library/windows/hardware/ff536734)

初始化微型端口对象。

[**IMiniportWavePci::NewStream**](https://msdn.microsoft.com/library/windows/hardware/ff536735)

创建新的流对象。

[**IMiniportWavePci::Service**](https://msdn.microsoft.com/library/windows/hardware/ff536736)

通知服务的请求的微型端口驱动程序。

流接口[IMiniportWavePciStream](https://msdn.microsoft.com/library/windows/hardware/ff536725)，继承从方法[ **IUnknown** ](https://msdn.microsoft.com/library/windows/desktop/ms680509)接口。 IMiniportWavePciStream 提供了以下其他方法：

[**IMiniportWavePciStream::GetAllocatorFraming**](https://msdn.microsoft.com/library/windows/hardware/ff536726)

获取批流微型端口驱动程序的首选分配器组帧参数。

[**IMiniportWavePciStream::GetPosition**](https://msdn.microsoft.com/library/windows/hardware/ff536727)

获取批流中的设备的当前位置。

[**IMiniportWavePciStream::MappingAvailable**](https://msdn.microsoft.com/library/windows/hardware/ff536728)

指示新的映射是可从端口驱动程序。

[**IMiniportWavePciStream::NormalizePhysicalPosition**](https://msdn.microsoft.com/library/windows/hardware/ff536729)

将基于时间的值转换为物理缓冲区位置值。

[**IMiniportWavePciStream::RevokeMappings**](https://msdn.microsoft.com/library/windows/hardware/ff536730)

撤消以前颁发的映射。

[**IMiniportWavePciStream::Service**](https://msdn.microsoft.com/library/windows/hardware/ff536731)

通知服务的请求的流对象。

[**IMiniportWavePciStream::SetFormat**](https://msdn.microsoft.com/library/windows/hardware/ff536732)

设置批流的数据格式。

[**IMiniportWavePciStream::SetState**](https://msdn.microsoft.com/library/windows/hardware/ff536733)

设置批流的状态。
 

 




