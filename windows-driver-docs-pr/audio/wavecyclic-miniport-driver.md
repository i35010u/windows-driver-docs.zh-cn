---
title: WaveCyclic 微型端口驱动程序
description: WaveCyclic 微型端口驱动程序
ms.assetid: 8a4811e9-e52b-4183-8d11-482883500f82
keywords:
- 音频的微型端口驱动程序 WDK WaveCyclic
- 微型端口驱动程序 WDK 音频 WaveCyclic
- WaveCyclic 微型端口驱动程序 WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 43000886805d646dcfebf29ef074525f74c50ee7
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67354109"
---
# <a name="wavecyclic-miniport-driver"></a>WaveCyclic 微型端口驱动程序


## <span id="wavecyclic_miniport_driver"></span><span id="WAVECYCLIC_MINIPORT_DRIVER"></span>


**重要**  不再建议使用 WavePci，而是改用 WaverRT。

 

WaveCyclic 微型端口驱动程序管理批呈现或的音频数据使用循环缓冲区的批捕获设备的硬件相关的函数。 循环缓冲区通常是一个独立的连续的物理内存块，并且可以位于驱动程序的选择的内存区域。 具有任何以下限制的设备应提供 WaveCyclic 微型端口驱动程序而非[WavePci 微型端口驱动程序](wavepci-miniport-driver.md):

-   设备缺少 DMA 硬件。

-   设备的 DMA 硬件可以访问仅在占用一个独立的连续的物理内存块的缓冲区中的数据。

-   设备的 DMA 硬件不能访问的物理内存的所有区域中的数据。

WaveCyclic 微型端口驱动程序应实现两个接口：

-   **微型端口接口**支持微型端口驱动程序初始化和流创建。

-   **流接口**管理批流，并会公开大部分的微型端口驱动程序的功能。

微型端口接口[IMiniportWaveCyclic](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iminiportwavecyclic)，继承中的方法[IMiniport](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iminiport)接口。 IMiniportWaveCyclic 提供了以下其他方法：

[**IMiniportWaveCyclic::Init**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iminiportwavecyclic-init)

初始化微型端口对象。

[**IMiniportWaveCyclic::NewStream**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iminiportwavecyclic-newstream)

创建新的流对象。

流接口[IMiniportWaveCyclicStream](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iminiportwavecyclicstream)，继承中的方法[ **IUnknown** ](https://docs.microsoft.com/windows/desktop/api/unknwn/nn-unknwn-iunknown)接口。 IMiniportWaveCyclicStream 提供了以下其他方法：

[**IMiniportWaveCyclicStream::GetPosition**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iminiportwavecyclicstream-getposition)

获取批流中的设备的当前位置。

[**IMiniportWaveCyclicStream::NormalizePhysicalPosition**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iminiportwavecyclicstream-normalizephysicalposition)

将基于时间的值转换为物理缓冲区位置值。

[**IMiniportWaveCyclicStream::SetFormat**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iminiportwavecyclicstream-setformat)

设置批流的数据格式。

[**IMiniportWaveCyclicStream::SetNotificationFreq**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iminiportwavecyclicstream-setnotificationfreq)

设置在通知中会发生中断的频率。

[**IMiniportWaveCyclicStream::SetState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iminiportwavecyclicstream-setstate)

设置批流的状态。

[**IMiniportWaveCyclicStream::Silence**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iminiportwavecyclicstream-silence)

复制到缓冲区中的无声段。
 

 




