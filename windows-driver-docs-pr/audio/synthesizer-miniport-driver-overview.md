---
title: 合成器微型端口驱动程序概述
description: 合成器微型端口驱动程序概述
ms.assetid: dbd6b95e-f8c8-49f1-ad90-b34821772391
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
ms.openlocfilehash: 8d0891c1e58b3a4bf24cd64001db781d1938b1ff
ms.sourcegitcommit: b84d760d4b45795be12e625db1d5a4167dc2c9ee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/17/2020
ms.locfileid: "90716076"
---
# <a name="synthesizer-miniport-driver-overview"></a>合成器微型端口驱动程序概述


## <span id="synthesizer_miniport_driver_overview"></span><span id="SYNTHESIZER_MINIPORT_DRIVER_OVERVIEW"></span>


DirectMusic 支持需要合成和接收器。 每个的默认实现都是通过 DirectMusic 提供的。 用户模式 Microsoft 软件合成器作为默认合成器提供，DirectSound 是默认波形接收器。 它们提供完全的硬件仿真，但通常可以通过内核模式软件或硬件实现来实现进一步的性能增强。

如果要实现硬件支持，唯一的选择是编写一个内核模式驱动程序。 在内核模式下，波形接收器由 PortCls 中的 Dmu 端口驱动程序提供，并且不需要替换为自定义实现 (因为有时在用户模式) 中完成。

对于内核模式 DirectMusic 驱动程序，最重要的标头文件为 dmusicks。 它包含实施微型端口驱动程序所需的主要内核模式接口。 这些接口包括：

[IMiniportDMus](/windows-hardware/drivers/ddi/dmusicks/nn-dmusicks-iminiportdmus)

[ISynthSinkDMus](/windows-hardware/drivers/ddi/dmusicks/nn-dmusicks-isynthsinkdmus)

[IMXF](/windows-hardware/drivers/ddi/dmusicks/nn-dmusicks-imxf)

[IAllocatorMXF](/windows-hardware/drivers/ddi/dmusicks/nn-dmusicks-iallocatormxf)

[IMasterClock](/windows-hardware/drivers/ddi/dmusicks/nn-dmusicks-imasterclock)

[IPortDMus](/windows-hardware/drivers/ddi/dmusicks/nn-dmusicks-iportdmus)

这些接口中的最后三个在 PortCls.sys 中实现。

相关的两个其他头文件是 dmusprop，其中包含 DirectMusic 属性项和 dmusbuff，其中包含主 IRP 结构 DMU \_ EVENTHEADER。

下图显示了 IHV 适配器驱动程序与 DirectMusic 系统其余部分之间的关系。

![说明适配器驱动程序与 directmusic 系统之间的关系的关系图](images/dmkmbig.png)

在最顶层，驱动程序通过 DirectMusic 端口驱动程序公开， (**IDirectMusicPort** 接口实例) 。 这就是应用程序与 DirectMusic 进行通信的方式。 此端口驱动程序通过 [**DeviceIoControl**](/windows/win32/api/ioapiset/nf-ioapiset-deviceiocontrol) 函数的标准内核流式处理调用向下传递到 pin 实例， (Microsoft Windows SDK 文档) 中所述。

请注意，在上图中，术语 "端口" 有两个冲突含义。 请避免使用内核模式 Dmu 端口驱动程序在上述用户模式下通过 DirectMusic API 使用术语端口。 这两个上下文中的术语具有相似但略有不同。 特别要注意的是，图顶部的 **IDirectMusicPort** 接口显示了 dmu 端口驱动程序在图下半部分中实现的单个 pin 实例的抽象。

每个微型端口驱动程序对象都连接到匹配的端口驱动程序对象。 端口驱动程序对象向微型端口驱动程序提供基本服务。 映射到设备的一个打开实例的每个 pin 实例都包含格式转换、排序和 "thruing" (的服务，以获取有关 thruing 的讨论，请参阅 Windows SDK 文档) 中的 **IDirectMusicThru** 接口的说明。 Pin 可以是目标或源，并且可以支持多种数据格式和范围。 每个 pin 实例指定目标或源，并指定支持的数据格式和范围。

微型端口驱动程序对象由 IHV 的适配器驱动程序创建。 尽管每个打开的驱动程序实例都有一个 pin 实例和 sequencer，但每个硬件 (或加载的内核软件合成器) 上只有一个端口-微型驱动程序对。 与微型端口驱动程序的通信是通过向下传递到微型端口驱动程序的事件流，以及微型端口驱动程序所支持的属性项。

[DirectMusic 微型端口驱动程序接口](directmusic-miniport-driver-interface.md)部分提供了 DirectMusic 微型端口驱动程序实现的详细信息。

 

