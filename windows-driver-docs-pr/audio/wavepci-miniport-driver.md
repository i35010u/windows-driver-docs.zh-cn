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
ms.openlocfilehash: 54e5dbf183d7bfe6adb67cfe980dc985f992714f
ms.sourcegitcommit: b84d760d4b45795be12e625db1d5a4167dc2c9ee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/17/2020
ms.locfileid: "90716624"
---
# <a name="wavepci-miniport-driver"></a>WavePci 微型端口驱动程序


## <span id="wavepci_miniport_driver"></span><span id="WAVEPCI_MINIPORT_DRIVER"></span>


**重要提示**   不再建议使用 WavePci，而是改用 WaverRT。

 

WavePci 微型端口驱动程序管理带有散点/集合 DMA 硬件的波形渲染或波形捕获设备的硬件相关功能，这些功能可以将音频数据传入或传出物理内存中的任何位置。 如果 wave 设备不能执行散点/收集传输或只能访问物理内存中的受限制区域，则应改用 [WaveCyclic 微型端口驱动程序](wavecyclic-miniport-driver.md) 。

WavePci 微型端口驱动程序应实现两个接口：

-   **微型端口接口** 执行微型端口驱动程序初始化、通道枚举和流创建。

-   **流接口** 管理波形流并公开大多数微型端口驱动程序的功能。

微型端口接口 [IMiniportWavePci](/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiportwavepci)继承了 [IMiniport](/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiport) 接口中的方法。 IMiniportWavePci 提供了以下附加方法：

[**IMiniportWavePci：： Init**](/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportwavepci-init)

初始化微型端口对象。

[**IMiniportWavePci：： Newstream.ischecked**](/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportwavepci-newstream)

创建新的流对象。

[**IMiniportWavePci：： Service**](/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportwavepci-service)

通知服务请求的微型端口驱动程序。

流接口 [IMiniportWavePciStream](/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiportwavepcistream)继承 [**IUnknown**](/windows/win32/api/unknwn/nn-unknwn-iunknown) 接口中的方法。 IMiniportWavePciStream 提供了以下附加方法：

[**IMiniportWavePciStream::GetAllocatorFraming**](/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportwavepcistream-getallocatorframing)

获取波形流的微型端口驱动程序的首选分配器框架参数。

[**IMiniportWavePciStream::GetPosition**](/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportwavepcistream-getposition)

获取设备在 wave 流中的当前位置。

[**IMiniportWavePciStream::MappingAvailable**](/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportwavepcistream-mappingavailable)

指示新的映射可从端口驱动程序获得。

[**IMiniportWavePciStream::NormalizePhysicalPosition**](/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportwavepcistream-normalizephysicalposition)

将物理缓冲区位置值转换为基于时间的值。

[**IMiniportWavePciStream::RevokeMappings**](/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportwavepcistream-revokemappings)

撤消以前颁发的映射。

[**IMiniportWavePciStream：： Service**](/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportwavepcistream-service)

通知请求服务的流对象。

[**IMiniportWavePciStream::SetFormat**](/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportwavepcistream-setformat)

设置波形流的数据格式。

[**IMiniportWavePciStream：： SetState**](/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportwavepcistream-setstate)

设置波形流的状态。
 

