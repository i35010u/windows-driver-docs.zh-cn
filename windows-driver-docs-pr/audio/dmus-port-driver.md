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
ms.openlocfilehash: cf97f4a8156344aff6d0175c0613f3772b20a5e9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63333842"
---
# <a name="dmus-port-driver"></a>Dmu 端口驱动程序


## <span id="dmus_port_driver"></span><span id="DMUS_PORT_DRIVER"></span>


Dmu 端口驱动程序管理 Microsoft DirectMusic 合成器或捕获设备。 与 MIDI 端口驱动程序，它仅支持简单 MIDI 的设备，相比 Dmu 端口驱动程序支持具有高级 MIDI 功能，如精度 sequencer 计时、 可下载的声音 (DL) 和通道组的设备。 适配器驱动程序实现相应[Dmu 微型端口驱动程序](dmus-miniport-driver.md)绑定到 Dmu 端口驱动程序以形成 DirectMusic 筛选器 (请参阅[MIDI 和 DirectMusic 筛选器](midi-and-directmusic-filters.md))，可以呈现或捕获 MIDI流。

Dmu 端口驱动程序公开[IPortDMus](https://msdn.microsoft.com/library/windows/hardware/ff536879)微型端口驱动程序的接口。 **IPortDMus**继承基接口中的方法[IPort](https://msdn.microsoft.com/library/windows/hardware/ff536842)。 **IPortDMus**提供了以下其他方法：

[**IPortDMus::Notify**](https://msdn.microsoft.com/library/windows/hardware/ff536880)

通知的 MIDI 合成器或捕获设备具有高级到 MIDI 流中的新位置的端口驱动程序。

[**IPortDMus::RegisterServiceGroup**](https://msdn.microsoft.com/library/windows/hardware/ff536882)

注册端口驱动程序的服务组对象。
已注册的服务组包含一系列由端口驱动程序微型端口驱动程序调用时调用的一个或多个服务例程**通知**; 有关详细信息，请参阅[服务接收器对象和服务组对象](service-sink-and-service-group-objects.md).

Dmu 端口驱动程序还会创建一个内存[allocator](allocator.md)对每个流并公开的分配器[IAllocatorMXF](https://msdn.microsoft.com/library/windows/hardware/ff536491)微型端口驱动程序的流对象的接口。 **IAllocatorMXF**继承基接口中的方法[IMXF](https://msdn.microsoft.com/library/windows/hardware/ff536782)。 **IAllocatorMXF**提供了以下其他方法：

[**IAllocatorMXF::GetBuffer**](https://msdn.microsoft.com/library/windows/hardware/ff536492)

获取 MIDI 事件或太大中容纳不下的事件列表的缓冲区[ **DMU\_内核\_事件**](https://msdn.microsoft.com/library/windows/hardware/ff536340)结构。

[**IAllocatorMXF::GetBufferSize**](https://msdn.microsoft.com/library/windows/hardware/ff536493)

获取以字节为单位来检索缓冲区的大小**GetBuffer**方法。

[**IAllocatorMXF::GetMessage**](https://msdn.microsoft.com/library/windows/hardware/ff536494)

获取包含单个类型 DMU 的结构存储的消息缓冲区\_内核\_事件。

[**IAllocatorMXF::PutBuffer**](https://msdn.microsoft.com/library/windows/hardware/ff536495)

不使用。
Dmu 端口和微型端口驱动程序对象与彼此通信通过其各自**IPortDMus**并[IMiniportMidi](https://msdn.microsoft.com/library/windows/hardware/ff536703)接口。 微型端口驱动程序的流对象，通过与通信端口驱动程序，此外，其[IMXF](https://msdn.microsoft.com/library/windows/hardware/ff536782)接口，以及的微型端口驱动程序的流对象进行通信使用端口驱动程序的分配器通过其**IAllocatorMXF**接口。

对 DirectMusic 驱动程序支持的详细信息，请参阅[合成器微型端口驱动程序概述](synthesizer-miniport-driver-overview.md)。

在 Windows XP 及更高版本， **IPortDMus**并[IPortMidi](https://msdn.microsoft.com/library/windows/hardware/ff536891)接口都实现在单个内部驱动程序的模块中。 这种整合得益于这两个接口的相似性。 例如，对于这两个接口定义的相同方法。 对于以前版本的 Windows，应看到的行为方面没有变化编写的应用程序**IPortMidi**并**IPortDMus**所得合并的 MIDI 和 Dmu 端口驱动程序的接口。

 

 




