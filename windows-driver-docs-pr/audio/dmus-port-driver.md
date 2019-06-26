---
title: Dmu 端口驱动程序
description: Dmu 端口驱动程序
ms.assetid: 19828364-1b0d-4fc0-b142-9d776cbf1ada
keywords:
- DirectMusic WDK 音频，端口驱动程序
- Dmu 端口驱动程序 WDK 音频
- PortCls WDK 音频，端口驱动程序
- 音频的微型端口驱动程序 WDK，端口驱动程序
- 微型端口驱动程序 WDK 音频，端口驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8953a0132ad1c8acd0e20002d6b9623731798c3e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67360114"
---
# <a name="dmus-port-driver"></a>Dmu 端口驱动程序


## <span id="dmus_port_driver"></span><span id="DMUS_PORT_DRIVER"></span>


Dmu 端口驱动程序管理 Microsoft DirectMusic 合成器或捕获设备。 与 MIDI 端口驱动程序，它仅支持简单 MIDI 的设备，相比 Dmu 端口驱动程序支持具有高级 MIDI 功能，如精度 sequencer 计时、 可下载的声音 (DL) 和通道组的设备。 适配器驱动程序实现相应[Dmu 微型端口驱动程序](dmus-miniport-driver.md)绑定到 Dmu 端口驱动程序以形成 DirectMusic 筛选器 (请参阅[MIDI 和 DirectMusic 筛选器](midi-and-directmusic-filters.md))，可以呈现或捕获 MIDI流。

Dmu 端口驱动程序公开[IPortDMus](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dmusicks/nn-dmusicks-iportdmus)微型端口驱动程序的接口。 **IPortDMus**继承基接口中的方法[IPort](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iport)。 **IPortDMus**提供了以下其他方法：

[**IPortDMus::Notify**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dmusicks/nf-dmusicks-iportdmus-notify)

通知的 MIDI 合成器或捕获设备具有高级到 MIDI 流中的新位置的端口驱动程序。

[**IPortDMus::RegisterServiceGroup**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dmusicks/nf-dmusicks-iportdmus-registerservicegroup)

注册端口驱动程序的服务组对象。
已注册的服务组包含一系列由端口驱动程序微型端口驱动程序调用时调用的一个或多个服务例程**通知**; 有关详细信息，请参阅[服务接收器对象和服务组对象](service-sink-and-service-group-objects.md).

Dmu 端口驱动程序还会创建一个内存[allocator](allocator.md)对每个流并公开的分配器[IAllocatorMXF](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dmusicks/nn-dmusicks-iallocatormxf)微型端口驱动程序的流对象的接口。 **IAllocatorMXF**继承基接口中的方法[IMXF](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dmusicks/nn-dmusicks-imxf)。 **IAllocatorMXF**提供了以下其他方法：

[**IAllocatorMXF::GetBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dmusicks/nf-dmusicks-iallocatormxf-getbuffer)

获取 MIDI 事件或太大中容纳不下的事件列表的缓冲区[ **DMU\_内核\_事件**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dmusicks/ns-dmusicks-_dmus_kernel_event)结构。

[**IAllocatorMXF::GetBufferSize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dmusicks/nf-dmusicks-iallocatormxf-getbuffersize)

获取以字节为单位来检索缓冲区的大小**GetBuffer**方法。

[**IAllocatorMXF::GetMessage**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dmusicks/nf-dmusicks-iallocatormxf-getmessage)

获取包含单个类型 DMU 的结构存储的消息缓冲区\_内核\_事件。

[**IAllocatorMXF::PutBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dmusicks/nf-dmusicks-iallocatormxf-putbuffer)

不使用。
Dmu 端口和微型端口驱动程序对象与彼此通信通过其各自**IPortDMus**并[IMiniportMidi](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iminiportmidi)接口。 微型端口驱动程序的流对象，通过与通信端口驱动程序，此外，其[IMXF](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dmusicks/nn-dmusicks-imxf)接口，以及的微型端口驱动程序的流对象进行通信使用端口驱动程序的分配器通过其**IAllocatorMXF**接口。

对 DirectMusic 驱动程序支持的详细信息，请参阅[合成器微型端口驱动程序概述](synthesizer-miniport-driver-overview.md)。

在 Windows XP 及更高版本， **IPortDMus**并[IPortMidi](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iportmidi)接口都实现在单个内部驱动程序的模块中。 这种整合得益于这两个接口的相似性。 例如，对于这两个接口定义的相同方法。 对于以前版本的 Windows，应看到的行为方面没有变化编写的应用程序**IPortMidi**并**IPortDMus**所得合并的 MIDI 和 Dmu 端口驱动程序的接口。

 

 




