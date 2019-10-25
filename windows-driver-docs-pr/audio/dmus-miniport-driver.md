---
title: DMus 微型端口驱动程序
description: DMus 微型端口驱动程序
ms.assetid: a0ce6545-2050-49fb-88b5-a75dcd4c7ebc
keywords:
- 音频微型端口驱动程序 WDK，Dmu
- 微型端口驱动程序 WDK 音频，Dmu
- DirectMusic WDK 音频，微型端口驱动程序
- Dmu 微型端口驱动程序 WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 05604d5e7e738ea44de9ff4acb7f4f55b7f7f1bd
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72833452"
---
# <a name="dmus-miniport-driver"></a>DMus 微型端口驱动程序


## <span id="dmus_miniport_driver"></span><span id="DMUS_MINIPORT_DRIVER"></span>


Dmu 微型端口驱动程序管理高级 MIDI 设备的硬件相关功能。 这些设备支持 DirectMusic 功能，如精度 sequencer 计时、可下载的声音（DLS）和通道组。 Dmu 微型端口驱动程序可在 MPU-401 等设备上实现高性能。 根据硬件的功能，可以通过微型端口驱动程序或端口驱动程序来处理计时。 Dmu 微型端口驱动程序还可以支持生成波形输出流的软件合成器。

MIDI 硬件设备的 Dmu 微型端口驱动程序应支持两个接口：

-   微型端口接口初始化微型端口对象并创建 MIDI 流。

-   流接口管理 MIDI 流并公开大多数微型端口驱动程序的功能。

微型端口接口[IMiniportDMus](https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusicks/nn-dmusicks-iminiportdmus)继承了[IMiniport](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiport)接口中的方法。 **IMiniportDMus**提供了以下附加方法：

[**IMiniportDMus：： Init**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusicks/nf-dmusicks-iminiportdmus-init)

初始化微型端口对象。

[**IMiniportDMus：： Newstream.ischecked**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusicks/nf-dmusicks-iminiportdmus-newstream)

创建新的流对象。

[**IMiniportDMus：： Service**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusicks/nf-dmusicks-iminiportdmus-service)

通知服务请求的微型端口驱动程序。

流接口[IMXF](https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusicks/nn-dmusicks-imxf)继承**IUnknown**接口中的方法。 **IMXF**提供了以下附加方法：

[**IMXF::ConnectOutput**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusicks/nf-dmusicks-imxf-connectoutput)

将此流对象（数据源）连接到另一个流对象（数据接收器）的**IMXF**接口。

[**IMXF：:D isconnectOutput**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusicks/nf-dmusicks-imxf-disconnectoutput)

断开此流对象与作为数据接收器的另一个流对象的**IMXF**接口的连接。

[**IMXF：:P utMessage**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusicks/nf-dmusicks-imxf-putmessage)

将[**dmu\_内核\_事件**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusicks/ns-dmusicks-_dmus_kernel_event)结构传递到数据接收器。

[**IMXF：： SetState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusicks/nf-dmusicks-imxf-setstate)

设置流的状态。

此外，Dmu 微型端口驱动程序的[ISynthSinkDMus](https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusicks/nn-dmusicks-isynthsinkdmus)接口提供软件合成程序的 DLS 功能。 **ISynthSinkDMus**继承基接口**IMXF**中的方法。 **ISynthSinkDMus**提供了以下附加方法：

[**ISynthSinkDMus::RefTimeToSample**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusicks/nf-dmusicks-isynthsinkdmus-reftimetosample)

将引用时间转换为采样时间。

[**ISynthSinkDMus：： Render**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusicks/nf-dmusicks-isynthsinkdmus-render)

将波形数据呈现到波形接收器的缓冲区中。

[**ISynthSinkDMus::SampleToRefTime**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusicks/nf-dmusicks-isynthsinkdmus-sampletoreftime)

将采样时间转换为引用时间。

[**ISynthSinkDMus::SyncToMaster**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusicks/nf-dmusicks-isynthsinkdmus-synctomaster)

将示例时钟同步到主时钟。

端口驱动程序的波形接收器调用**ISynthSinkDMus：： Render**来读取合成器从其 MIDI 输入流生成的波形 PCM 数据。 有关波形接收器的详细信息，请参阅[内核模式软件合成程序的波形接收器](a-wave-sink-for-kernel-mode-software-synthesizers.md)。

微型端口驱动程序在 Dmu 端口驱动程序上调用以下接口：

[IPortDMus](https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusicks/nn-dmusicks-iportdmus)

[IAllocatorMXF](https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusicks/nn-dmusicks-iallocatormxf)

[IMasterClock](https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusicks/nn-dmusicks-imasterclock)

PortCls 包含一个内置的 Dmu 微型端口驱动程序。 有关详细信息，请参阅[**PcNewMiniport**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcnewminiport)。

 

 




