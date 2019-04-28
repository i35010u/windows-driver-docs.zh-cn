---
title: 合成器微型端口驱动程序概述
description: 合成器微型端口驱动程序概述
ms.assetid: dbd6b95e-f8c8-49f1-ad90-b34821772391
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
ms.openlocfilehash: 53db733ab39d953b78b2787ec29193e631eadf8d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63335399"
---
# <a name="synthesizer-miniport-driver-overview"></a>合成器微型端口驱动程序概述


## <span id="synthesizer_miniport_driver_overview"></span><span id="SYNTHESIZER_MINIPORT_DRIVER_OVERVIEW"></span>


合成器和接收器是必需的 DirectMusic 支持。 DirectMusic 提供的每个默认实现。 作为默认合成器提供用户模式下的 Microsoft 软件合成器，DirectSound 是默认批接收器。 这提供了完整的硬件仿真，但是，进一步性能增强功能通常都可以使用内核模式软件或硬件实现满足。

如果要实现对硬件的支持，唯一的选择是编写一个内核模式驱动程序。 在内核模式下，批接收器中 PortCls Dmu 端口驱动程序提供，无需替换为自定义实现 （如有时在用户模式下完成）。

内核模式 DirectMusic 驱动程序，最重要的标头文件是 dmusicks.h。 它包含您需要实现微型端口驱动程序的内核模式的主要接口。 这些接口是：

[IMiniportDMus](https://msdn.microsoft.com/library/windows/hardware/ff536699)

[ISynthSinkDMus](https://msdn.microsoft.com/library/windows/hardware/ff537011)

[IMXF](https://msdn.microsoft.com/library/windows/hardware/ff536782)

[IAllocatorMXF](https://msdn.microsoft.com/library/windows/hardware/ff536491)

[IMasterClock](https://msdn.microsoft.com/library/windows/hardware/ff536696)

[IPortDMus](https://msdn.microsoft.com/library/windows/hardware/ff536879)

PortCls.sys 中实现这些接口的最后三个。

两个感兴趣的其他标头文件是 dmusprop.h，其中包含 DirectMusic 属性项和 dmusbuff.h，其中包含主 IRP 结构 DMU\_EVENTHEADER。

下图显示了 IHV 适配器驱动程序和 DirectMusic 系统的其余部分之间的关系。

![说明到 directmusic 系统的适配器驱动程序的关系的关系图](images/dmkmbig.png)

在最顶层级别，该驱动程序通过公开 DirectMusic 端口驱动程序 ( **IDirectMusicPort**接口实例)。 这是应用程序如何与 DirectMusic。 此端口驱动程序与通过流式处理通过调用的标准内核的 pin 实例向下进行通信[ **DeviceIoControl** ](https://msdn.microsoft.com/library/windows/desktop/aa363216)函数 （Microsoft Windows SDK 文档中所述）。

请注意，术语"端口"在上图中有两个冲突的含义。 避免混淆字词端口 DirectMusic api 的使用情况，在上面的用户模式下使用内核模式 Dmu 端口驱动程序。 条款在两个上下文中具有类似但略有不同含义。 具体而言，请注意， **IDirectMusicPort**图顶部的界面提供 Dmu 端口驱动程序实现的下半部分图中的单个插针实例的抽象。

微型端口驱动程序的每个对象连接到匹配的端口驱动程序对象。 端口驱动程序对象提供给微型端口驱动程序的基本服务。 每个 pin 实例映射到一个打开的设备实例有格式转换、 序列化和"thruing"等服务 (thruing 的讨论，请参阅的说明**IDirectMusicThru** Windows SDK 中的接口文档）。 Pin 可以是目标或源，并且可以支持多种数据格式和范围。 每个 pin 实例指定目标或源，并指定哪些数据格式和支持范围。

由 IHV 的适配器驱动程序创建微型端口驱动程序对象。 虽然没有一个插针实例和每个的驱动程序打开实例的排序器，但没有只有一个端口微型端口驱动程序对每种硬件 （或加载的内核软件合成器）。 与微型端口驱动程序的通信是通过向下传递，微型端口驱动程序且由微型端口驱动程序支持的属性项的事件流。

部分[DirectMusic 微型端口驱动程序接口](directmusic-miniport-driver-interface.md)显示 DirectMusic 微型端口驱动程序实现的详细信息。

 

 




