---
title: WavePci 微型端口驱动程序
description: WavePci 微型端口驱动程序
ms.assetid: 8a166087-d158-4d49-a917-2a5a78b43cb4
keywords:
- 音频微型端口驱动程序 WDK，WavePci
- 微型端口驱动程序 WDK 音频，WavePci
- WavePci 微型端口驱动程序 WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ac464be6fea3c7245f50be4053aa45916ebebfd7
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72829964"
---
# <a name="wavepci-miniport-driver"></a>WavePci 微型端口驱动程序


## <span id="wavepci_miniport_driver"></span><span id="WAVEPCI_MINIPORT_DRIVER"></span>


**重要**  不再建议使用 WavePci，改用 WaverRT。

 

WavePci 微型端口驱动程序管理带有散点/集合 DMA 硬件的波形渲染或波形捕获设备的硬件相关功能，这些功能可以将音频数据传入或传出物理内存中的任何位置。 如果 wave 设备不能执行散点/收集传输或只能访问物理内存中的受限制区域，则应改用[WaveCyclic 微型端口驱动程序](wavecyclic-miniport-driver.md)。

WavePci 微型端口驱动程序应实现两个接口：

-   **微型端口接口**执行微型端口驱动程序初始化、通道枚举和流创建。

-   **流接口**管理波形流并公开大多数微型端口驱动程序的功能。

微型端口接口[IMiniportWavePci](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiportwavepci)继承了[IMiniport](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiport)接口中的方法。 IMiniportWavePci 提供了以下附加方法：

[**IMiniportWavePci：： Init**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportwavepci-init)

初始化微型端口对象。

[**IMiniportWavePci：： Newstream.ischecked**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportwavepci-newstream)

创建新的流对象。

[**IMiniportWavePci：： Service**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportwavepci-service)

通知服务请求的微型端口驱动程序。

流接口[IMiniportWavePciStream](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiportwavepcistream)继承[**IUnknown**](https://docs.microsoft.com/windows/desktop/api/unknwn/nn-unknwn-iunknown)接口中的方法。 IMiniportWavePciStream 提供了以下附加方法：

[**IMiniportWavePciStream::GetAllocatorFraming**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportwavepcistream-getallocatorframing)

获取波形流的微型端口驱动程序的首选分配器框架参数。

[**IMiniportWavePciStream::GetPosition**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportwavepcistream-getposition)

获取设备在 wave 流中的当前位置。

[**IMiniportWavePciStream::MappingAvailable**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportwavepcistream-mappingavailable)

指示新的映射可从端口驱动程序获得。

[**IMiniportWavePciStream::NormalizePhysicalPosition**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportwavepcistream-normalizephysicalposition)

将物理缓冲区位置值转换为基于时间的值。

[**IMiniportWavePciStream::RevokeMappings**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportwavepcistream-revokemappings)

撤消以前颁发的映射。

[**IMiniportWavePciStream：： Service**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportwavepcistream-service)

通知请求服务的流对象。

[**IMiniportWavePciStream::SetFormat**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportwavepcistream-setformat)

设置波形流的数据格式。

[**IMiniportWavePciStream：： SetState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportwavepcistream-setstate)

设置波形流的状态。
 

 




