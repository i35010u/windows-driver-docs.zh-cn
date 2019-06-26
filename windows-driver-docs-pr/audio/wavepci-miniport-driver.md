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
ms.openlocfilehash: c029b906e58a8cb612e81161152f00ed1644a9d2
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67364787"
---
# <a name="wavepci-miniport-driver"></a>WavePci 微型端口驱动程序


## <span id="wavepci_miniport_driver"></span><span id="WAVEPCI_MINIPORT_DRIVER"></span>


**重要**  不再建议使用 WavePci，而是改用 WaverRT。

 

WavePci 微型端口驱动程序管理的物理内存中的任何位置从批呈现或具有可将音频数据到或传输的分散/聚拢 DMA 硬件的批捕获设备的硬件相关的函数。 应使用不具备的功能来执行散播-聚集传输或能够访问受限制的区域仅在物理内存中的波形设备[WaveCyclic 微型端口驱动程序](wavecyclic-miniport-driver.md)相反。

WavePci 微型端口驱动程序应实现两个接口：

-   **微型端口接口**执行微型端口驱动程序初始化、 通道枚举和流创建。

-   **流接口**管理批流，并会公开大部分的微型端口驱动程序的功能。

微型端口接口[IMiniportWavePci](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iminiportwavepci)，继承中的方法[IMiniport](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iminiport)接口。 IMiniportWavePci 提供了以下其他方法：

[**IMiniportWavePci::Init**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iminiportwavepci-init)

初始化微型端口对象。

[**IMiniportWavePci::NewStream**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iminiportwavepci-newstream)

创建新的流对象。

[**IMiniportWavePci::Service**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iminiportwavepci-service)

通知服务的请求的微型端口驱动程序。

流接口[IMiniportWavePciStream](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iminiportwavepcistream)，继承从方法[ **IUnknown** ](https://docs.microsoft.com/windows/desktop/api/unknwn/nn-unknwn-iunknown)接口。 IMiniportWavePciStream 提供了以下其他方法：

[**IMiniportWavePciStream::GetAllocatorFraming**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iminiportwavepcistream-getallocatorframing)

获取批流微型端口驱动程序的首选分配器组帧参数。

[**IMiniportWavePciStream::GetPosition**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iminiportwavepcistream-getposition)

获取批流中的设备的当前位置。

[**IMiniportWavePciStream::MappingAvailable**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iminiportwavepcistream-mappingavailable)

指示新的映射是可从端口驱动程序。

[**IMiniportWavePciStream::NormalizePhysicalPosition**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iminiportwavepcistream-normalizephysicalposition)

将基于时间的值转换为物理缓冲区位置值。

[**IMiniportWavePciStream::RevokeMappings**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iminiportwavepcistream-revokemappings)

撤消以前颁发的映射。

[**IMiniportWavePciStream::Service**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iminiportwavepcistream-service)

通知服务的请求的流对象。

[**IMiniportWavePciStream::SetFormat**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iminiportwavepcistream-setformat)

设置批流的数据格式。

[**IMiniportWavePciStream::SetState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iminiportwavepcistream-setstate)

设置批流的状态。
 

 




