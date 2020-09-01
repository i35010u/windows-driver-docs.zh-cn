---
title: DirectMusic 微型端口驱动程序接口
description: DirectMusic 微型端口驱动程序接口
ms.assetid: a3532993-732a-4a7e-82bc-fc4199ec23dd
keywords:
- 微型端口驱动程序 WDK 音频，合成程序
- 合成 WDK 音频，微型端口驱动程序
- 波形接收器音频、微型端口驱动程序
- DirectMusic 内核模式 WDK 音频、微型端口驱动程序
- 内核模式 synths WDK 音频，微型端口驱动程序
- 端口驱动程序 WDK 音频，合成程序
- 硬件加速 WDK 音频
- 微型端口驱动程序 WDK 音频、内核模式硬件加速
- 合成 WDK 音频，内核模式硬件加速
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f19927272e263ab7087419f35c5599a076969c27
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89208131"
---
# <a name="directmusic-miniport-driver-interface"></a>DirectMusic 微型端口驱动程序接口


## <span id="directmusic_miniport_driver_interface"></span><span id="DIRECTMUSIC_MINIPORT_DRIVER_INTERFACE"></span>


Dmu 微型端口驱动程序接口基于 MIDI 微型端口驱动程序接口，但它添加了以下扩展插件来支持高级合成程序：

-   对于每个实例，DLS 下载超过16个通道

-   硬件中的附注事件的排序

Dmu 微型端口驱动程序接口有几种不同的方式。 Dmu 微型端口驱动程序实现接口 [IMiniportDMus](/windows-hardware/drivers/ddi/dmusicks/nn-dmusicks-iminiportdmus) ，而不是 [IMiniportMidi](/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiportmidi)。 此接口类似于 **IMiniportMidi**，但 [**IMiniportDMus：： newstream.ischecked**](/windows-hardware/drivers/ddi/dmusicks/nf-dmusicks-iminiportdmus-newstream) 方法) 接口创建 [IMXF](/windows-hardware/drivers/ddi/dmusicks/nn-dmusicks-imxf) (MIDI 转换筛选器，并连接到 IAllocatorMXF 端口驱动程序中的 [Dmu](/windows-hardware/drivers/ddi/dmusicks/nn-dmusicks-iallocatormxf) 接口，而不是实现 [IMiniportMidiStream](/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiportmidistream) 接口。 **IAllocatorMXF** 和 **IMXF** 包装标准 **GetMessage** 和 **PutMessage** 调用 (参阅 [**IAllocatorMXF：： GetMessage**](/windows-hardware/drivers/ddi/dmusicks/nf-dmusicks-iallocatormxf-getmessage) 和 [**IMXF：:P utmessage**](/windows-hardware/drivers/ddi/dmusicks/nf-dmusicks-imxf-putmessage)) 。 这些调用处理打包事件，而不是原始 MIDI 字节。

合成器的 Dmu 微型端口驱动程序可以实现部分或全部 DirectMusic 属性。 这些属性允许系统管理设备的 DLS 下载和通道分配。 Dmusprop 头文件定义特定于 DirectMusic 的属性项。 有关这些属性的列表，请参阅 [KSPROPSETID \_ 合成](./kspropsetid-synth.md) 和 [KSPROPSETID \_ 合成 \_ dl](./kspropsetid-synth-dls.md)。

Dmu 微型端口驱动程序应允许创建多个 pin 实例。 每个 pin 实例都作为一个虚拟合成器，包含一组与其他 pin 实例无关的通道和 DL 下载。

[音频驱动程序属性集](./audio-drivers-property-sets.md)中所述的某些合成属性在 pin 实例上起作用，其他是全局的。 若要处理全局属性，合成器必须在其拓扑中包含合成器节点。 每个属性项的说明指示该项是发送到合成器节点还是发送到 pin 实例。 对于支持合成的每个硬件，都存在一个端口驱动程序对象和一个微型端口驱动程序对象，如下图所示。

![说明 directmusic 合成器的端口和微型端口驱动程序的示意图](images/dmkmport.png)

端口驱动程序对象公开 [IPortDMus](/windows-hardware/drivers/ddi/dmusicks/nn-dmusicks-iportdmus) 接口的一个实例，该实例由微型端口驱动程序对象保存。 微型端口驱动程序会导出端口驱动程序所持有的 **IMiniportDMus** 接口的一个实例。 对于每个实例化的 pin，端口驱动程序请求匹配的 **IMXF** 接口。 系统与此实例之间的通信是对寻址到 pin 的属性请求的组合以及流向或来自 **IMXF** 流接口的事件的组合。

创建两个对象时，必须将其传递到微型端口驱动程序：

-   Clock

-   分配器对象

时钟对于呈现和捕获操作非常重要。 微型端口驱动程序需要在指定的时间呈现说明;当微型端口驱动程序读取 MIDI 数据时，它需要知道时间，以便对内核事件进行时间戳。 有关详细信息，请参阅 [延迟时钟](latency-clocks.md)。

具有**IAllocatorMXF**接口的[分配](allocator.md)器对象将用作用于回收内存的内存池。 系统中的所有 MIDI 消息都从此公共池分配。 分配器对象应用于创建或销毁单个消息。

本节包括：

[MIDI 传输](midi-transport.md)

[延迟时钟](latency-clocks.md)

[微型端口驱动程序属性项请求](miniport-driver-property-item-requests.md)

[将 PortDMus 设置为默认的 DirectMusic 端口驱动程序](making-portdmus-the-default-directmusic-port-driver.md)

[将合成器作为旧设备公开](exposing-your-synthesizer-as-a-legacy-device.md)

 

