---
title: Dmu 端口驱动程序
description: Dmu 端口驱动程序
ms.assetid: 19828364-1b0d-4fc0-b142-9d776cbf1ada
keywords:
- DirectMusic WDK 音频，端口驱动程序
- Dmu 端口驱动程序 WDK 音频
- PortCls WDK 音频，端口驱动程序
- 音频微型端口驱动程序 WDK，端口驱动程序
- 微型端口驱动程序 WDK 音频、端口驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 40ec3ee54d3bf7c80013f7f25d7e60000411f9c2
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72833443"
---
# <a name="dmus-port-driver"></a>Dmu 端口驱动程序


## <span id="dmus_port_driver"></span><span id="DMUS_PORT_DRIVER"></span>


Dmu 端口驱动程序管理 Microsoft DirectMusic 合成器或捕获设备。 与仅支持简单 MIDI 设备的 MIDI 端口驱动程序相比，Dmu 端口驱动程序支持具有高级 MIDI 功能的设备，如精度 sequencer 计时、可下载声音（DLS）和通道组。 适配器驱动程序实现相应的[dmu 微型端口驱动程序，该驱动程序](dmus-miniport-driver.md)绑定到 dmu 端口驱动程序以形成 DirectMusic 筛选器（请参阅[Midi 和 DirectMusic 筛选器](midi-and-directmusic-filters.md)），该筛选器可以呈现或捕获 MIDI 流。

Dmu 端口驱动程序向微型端口驱动程序公开[IPortDMus](https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusicks/nn-dmusicks-iportdmus)接口。 **IPortDMus**继承基接口[IPort](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iport)中的方法。 **IPortDMus**提供了以下附加方法：

[**IPortDMus：： Notify**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusicks/nf-dmusicks-iportdmus-notify)

通知端口驱动程序： MIDI 合成器或捕获设备已前进到 MIDI 流中的新位置。

[**IPortDMus::RegisterServiceGroup**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusicks/nf-dmusicks-iportdmus-registerservicegroup)

使用端口驱动程序注册服务组对象。
已注册的服务组包含一个或多个由端口驱动程序调用**Notify**时由端口驱动程序调用的服务例程的列表;有关详细信息，请参阅[服务接收器和服务组对象](service-sink-and-service-group-objects.md)。

Dmu 端口驱动程序还会为每个流创建一个内存[分配](allocator.md)器，并向微型端口驱动程序的流对象公开分配器的[IAllocatorMXF](https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusicks/nn-dmusicks-iallocatormxf)接口。 **IAllocatorMXF**继承基接口[IMXF](https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusicks/nn-dmusicks-imxf)中的方法。 **IAllocatorMXF**提供了以下附加方法：

[**IAllocatorMXF：： GetBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusicks/nf-dmusicks-iallocatormxf-getbuffer)

获取 MIDI 事件或事件列表的缓冲区，这些事件太大，无法在[**dmu\_内核\_事件**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusicks/ns-dmusicks-_dmus_kernel_event)结构中容纳。

[**IAllocatorMXF::GetBufferSize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusicks/nf-dmusicks-iallocatormxf-getbuffersize)

获取**GetBuffer**方法检索到的缓冲区的大小（以字节为单位）。

[**IAllocatorMXF：： GetMessage**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusicks/nf-dmusicks-iallocatormxf-getmessage)

获取包含 DMU\_内核\_事件的单个结构的存储的消息缓冲区。

[**IAllocatorMXF：:P utBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusicks/nf-dmusicks-iallocatormxf-putbuffer)

不使用。
Dmu 端口和微型端口驱动程序对象通过其各自的**IPortDMus**和[IMiniportMidi](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiportmidi)接口相互通信。 此外，端口驱动程序通过其[IMXF](https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusicks/nn-dmusicks-imxf)接口与微型端口驱动程序的流对象通信，微型端口驱动程序的流对象通过其**IAllocatorMXF**接口与端口驱动程序的分配器进行通信。

有关 DirectMusic 的驱动程序支持的详细信息，请参阅[合成器微型端口驱动程序概述](synthesizer-miniport-driver-overview.md)。

在 Windows XP 和更高版本中， **IPortDMus**和[IPortMidi](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iportmidi)接口都是在单个内部驱动程序模块中实现的。 此合并可通过这两个接口的相似性来实现。 例如，为这两个接口定义了相同的方法。 对于为以前版本的 Windows 编写的应用程序，应在**IPortMidi**和**IPortDMus**接口的行为上不发生任何变化，因为这会导致 MIDI 和 dmu 端口驱动程序的合并。

 

 




