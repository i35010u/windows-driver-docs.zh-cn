---
title: WaveCyclic 微型端口驱动程序
description: WaveCyclic 微型端口驱动程序
ms.assetid: 8a4811e9-e52b-4183-8d11-482883500f82
keywords:
- 音频微型端口驱动程序 WDK，WaveCyclic
- 微型端口驱动程序 WDK 音频，WaveCyclic
- WaveCyclic 微型端口驱动程序 WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 72e1702067d788cb8048be3634fd56f4839d7e60
ms.sourcegitcommit: b84d760d4b45795be12e625db1d5a4167dc2c9ee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/17/2020
ms.locfileid: "90716632"
---
# <a name="wavecyclic-miniport-driver"></a>WaveCyclic 微型端口驱动程序


## <span id="wavecyclic_miniport_driver"></span><span id="WAVECYCLIC_MINIPORT_DRIVER"></span>


**重要提示**   不再建议使用 WavePci，而是改用 WaverRT。

 

WaveCyclic 微型端口驱动程序管理用于音频数据的循环缓冲的波形渲染或波形捕获设备的硬件相关功能。 循环缓冲区通常是连续物理内存的单个块，可以位于驱动程序选择的内存区域中。 具有以下任何限制的设备应提供 WaveCyclic 微型端口驱动程序，而不是 [WavePci 微型端口驱动程序](wavepci-miniport-driver.md)：

-   设备缺少 DMA 硬件。

-   设备的 DMA 硬件只能在占用单个连续物理内存块的缓冲区中访问数据。

-   设备的 DMA 硬件无法访问物理内存所有区域中的数据。

WaveCyclic 微型端口驱动程序应实现两个接口：

-   **微型端口接口** 支持微型端口驱动程序初始化和流创建。

-   **流接口** 管理波形流并公开大多数微型端口驱动程序的功能。

微型端口接口 [IMiniportWaveCyclic](/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiportwavecyclic)继承了 [IMiniport](/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiport) 接口中的方法。 IMiniportWaveCyclic 提供了以下附加方法：

[**IMiniportWaveCyclic：： Init**](/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportwavecyclic-init)

初始化微型端口对象。

[**IMiniportWaveCyclic：： Newstream.ischecked**](/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportwavecyclic-newstream)

创建新的流对象。

流接口 [IMiniportWaveCyclicStream](/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiportwavecyclicstream)继承 [**IUnknown**](/windows/win32/api/unknwn/nn-unknwn-iunknown) 接口中的方法。 IMiniportWaveCyclicStream 提供了以下附加方法：

[**IMiniportWaveCyclicStream::GetPosition**](/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportwavecyclicstream-getposition)

获取设备在 wave 流中的当前位置。

[**IMiniportWaveCyclicStream::NormalizePhysicalPosition**](/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportwavecyclicstream-normalizephysicalposition)

将物理缓冲区位置值转换为基于时间的值。

[**IMiniportWaveCyclicStream::SetFormat**](/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportwavecyclicstream-setformat)

设置波形流的数据格式。

[**IMiniportWaveCyclicStream::SetNotificationFreq**](/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportwavecyclicstream-setnotificationfreq)

设置发生通知中断的频率。

[**IMiniportWaveCyclicStream：： SetState**](/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportwavecyclicstream-setstate)

设置波形流的状态。

[**IMiniportWaveCyclicStream：：无声**](/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportwavecyclicstream-silence)

将无声复制到缓冲区中。
 

