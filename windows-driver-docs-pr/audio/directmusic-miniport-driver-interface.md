---
title: DirectMusic 微型端口驱动程序接口
description: DirectMusic 微型端口驱动程序接口
ms.assetid: a3532993-732a-4a7e-82bc-fc4199ec23dd
keywords:
- 微型端口驱动程序 WDK 音频，合成器
- 合成器 WDK 音频，微型端口驱动程序
- 批接收器 WDK 音频，微型端口驱动程序
- DirectMusic 内核模式 WDK 音频，微型端口驱动程序
- 内核模式 synths WDK 音频，微型端口驱动程序
- 端口驱动程序 WDK 音频，合成器
- 硬件加速 WDK 音频
- 微型端口驱动程序 WDK 音频，内核模式硬件加速
- 合成器 WDK 音频，内核模式硬件加速
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 54820cce4e34f0419b7e0985b9cda5faa920bdb9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56563163"
---
# <a name="directmusic-miniport-driver-interface"></a>DirectMusic 微型端口驱动程序接口


## <span id="directmusic_miniport_driver_interface"></span><span id="DIRECTMUSIC_MINIPORT_DRIVER_INTERFACE"></span>


Dmu 微型端口驱动程序接口基于 MIDI 微型端口驱动程序接口，但它添加了支持高级合成器的以下扩展：

-   DLS 下载大于 16 个通道，每个实例

-   请注意事件在硬件中的序列化

Dmu 微型端口驱动程序接口方面不同于几种方法中的 MIDI 微型端口驱动程序接口。 Dmu 微型端口驱动程序实现接口[IMiniportDMus](https://msdn.microsoft.com/library/windows/hardware/ff536699)而不是[IMiniportMidi](https://msdn.microsoft.com/library/windows/hardware/ff536703)。 此接口是类似于**IMiniportMidi**，但[ **IMiniportDMus::NewStream** ](https://msdn.microsoft.com/library/windows/hardware/ff536701)方法将创建[IMXF](https://msdn.microsoft.com/library/windows/hardware/ff536782) （MIDI 转换筛选器） 界面，并连接到[IAllocatorMXF](https://msdn.microsoft.com/library/windows/hardware/ff536491) Dmu 端口驱动程序，而不是实现中的接口[IMiniportMidiStream](https://msdn.microsoft.com/library/windows/hardware/ff536704)接口。 **IAllocatorMXF**并**IMXF**包装标准**GetMessage**并**PutMessage**调用 (请参阅[ **IAllocatorMXF::GetMessage** ](https://msdn.microsoft.com/library/windows/hardware/ff536494)并[ **IMXF::PutMessage**](https://msdn.microsoft.com/library/windows/hardware/ff536791))。 这些调用处理打包事件而不是与原始 MIDI 字节。

合成器 Dmu 微型端口驱动程序可以实现部分或全部 DirectMusic 属性。 这些属性允许系统在管理 DLS 下载和通道分配的设备。 Dmusprop.h 标头文件定义特定于 DirectMusic 的属性项。 有关这些属性的列表，请参阅[KSPROPSETID\_合成](https://msdn.microsoft.com/library/windows/hardware/ff537486)并[KSPROPSETID\_合成器\_Dls](https://msdn.microsoft.com/library/windows/hardware/ff537488)。

Dmu 微型端口驱动程序需要允许多个 pin 实例创建。 每个 pin 实例充当一个虚拟合成器，并包含一组通道和 DLS 下载独立于其他 pin 实例。

某些合成器属性中所述[音频驱动程序的属性集](https://msdn.microsoft.com/library/windows/hardware/ff536197)作用于一个 pin 的实例，而有些全局任务。 若要处理的全局属性，合成器必须其网络拓扑中有一个合成器节点。 每个属性项的说明指示该项是否发送到合成器节点或 pin 实例。 对于支持合成硬件的每个片段，存在端口驱动程序对象和微型端口驱动程序对象，如下图中所示。

![说明用于 directmusic 合成器端口和微型端口驱动程序的关系图](images/dmkmport.png)

端口驱动程序对象公开的一个实例[IPortDMus](https://msdn.microsoft.com/library/windows/hardware/ff536879)接口，它持有的微型端口驱动程序对象。 微型端口驱动程序将导出的一个实例**IMiniportDMus**接口，这由端口驱动程序。 对于每个实例化的插针，端口驱动程序请求匹配**IMXF**接口。 系统与此实例之间的通信是组合属性请求发送到的 pin 和事件流动面向或源自**IMXF**流接口。

在创建时，必须将两个对象传递给微型端口驱动程序：

-   时钟

-   分配器对象

时钟是非常重要的呈现和捕获操作。 微型端口驱动程序需要呈现说明它们的指定时间;当微型端口驱动程序读取 MIDI 数据中时，它需要知道时间，使其可时间戳内核事件。 有关详细信息，请参阅[延迟时钟](latency-clocks.md)。

[Allocator](allocator.md)对象，它具有**IAllocatorMXF**接口中，为内存池中用于回收内存。 在系统中的所有 MIDI 消息是从此公共池都分配。 应使用的分配器对象来创建或销毁各个消息。

本部分包括：

[MIDI 传输](midi-transport.md)

[延迟时钟](latency-clocks.md)

[微型端口驱动程序属性项请求](miniport-driver-property-item-requests.md)

[使 PortDMus 默认 DirectMusic 端口驱动程序](making-portdmus-the-default-directmusic-port-driver.md)

[将你合成器公开为旧设备](exposing-your-synthesizer-as-a-legacy-device.md)

 

 




