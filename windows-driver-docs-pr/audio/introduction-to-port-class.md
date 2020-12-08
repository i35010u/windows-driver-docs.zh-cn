---
title: 端口类简介
description: 端口类简介
keywords:
- 音频微型端口驱动程序 WDK，端口类
- 微型端口驱动程序 WDK 音频，端口类
- 端口类驱动程序 WDK 音频
- PortCls WDK 音频，微型端口驱动程序
- 端口类适配器驱动程序 WDK 音频
- 适配器驱动程序 WDK 音频，微型端口驱动程序
- 端口驱动程序 WDK 音频、微型端口驱动程序
- 端口类库 WDK 音频
- 端口驱动程序 WDK 音频，端口类
- 端口类音频适配器 WDK
- 端口驱动程序 WDK 音频
- PortCls WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2d7bf690f763a0f04f550a4cd209d10fd6d4f389
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96784723"
---
# <a name="introduction-to-port-class"></a>端口类简介


## <span id="introduction_to_port_class"></span><span id="INTRODUCTION_TO_PORT_CLASS"></span>


适用于 PCI 和基于 DMA 的音频设备的大多数硬件驱动程序基于端口类库，可以通过 PortCls 系统驱动程序（ ( # A0) 来访问）。 PortCls 是一种音频端口类驱动程序，Microsoft 将其作为操作系统的一部分包含在其中。 PortCls 提供一组端口驱动程序，用于实现 (KS) 筛选器功能的大多数泛型内核流式处理。 因此，PortCls 简化了音频驱动程序开发人员的任务。 硬件供应商只需要提供一组微型端口驱动程序来处理音频适配器的硬件特定功能。

尽管硬件供应商可以选择为其音频设备实现自己的 KS 筛选器，但对于典型的音频设备，此选项很困难且不必要。 可以开发一个 KS 筛选器，使其符合 Stream.sys、Stream 类驱动程序或 Avstream.sys AVStream 类驱动程序。 但基于 Stream.sys 的 KS 筛选器无法利用仅在 AVStream 中提供的改进。 有关 KS 筛选器和 PortCls 的详细信息，请参阅 [与 WDM 音频驱动程序入门](getting-started-with-wdm-audio-drivers.md)。

PortCls 的内部实现可以在连续的 Windows 版本中不断地利用内核流改进功能，同时保持与现有驱动程序的兼容性。

PortCls 在 Portcls.sys 系统文件中实现为导出驱动程序 (内核模式 DLL) ，其中包含以下项：

-   适配器驱动程序可调用的一组 helper 函数

-   *音频端口* 驱动程序的集合

音频设备的硬件供应商负责提供 *适配器驱动程序*。 适配器驱动程序包括初始化和微型端口驱动程序管理代码 (包括 [**DriverEntry**](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize) 函数) 和 *音频微型端口* 驱动程序的集合。

当操作系统加载适配器驱动程序时，适配器驱动程序将创建一组微型端口驱动程序对象，并提示 PortCls 系统驱动程序创建相应的端口驱动程序对象集。  ([创建 Subdevice](subdevice-creation.md) 中的代码示例演示了此过程。 ) 这些端口驱动程序通常是 Portcls.sys 文件中可用的驱动程序的子集。 每个微型端口驱动程序将自身绑定到 Portcls.sys 的匹配端口驱动程序，以形成完整的 *subdevice* 驱动程序。 组合端口和-微型端口 subdevice 驱动程序是一个 KS 筛选器 (参阅 [音频筛选](audio-filters.md) 器) 。 例如，典型的适配器驱动程序可能包含三个微型端口驱动程序： WaveRT、DMusUART 和拓扑 (与 [IMiniportWaveRT](/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiportwavert)、 [IMiniportDMus](/windows-hardware/drivers/ddi/dmusicks/nn-dmusicks-iminiportdmus)和 [IMiniportTopology](/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiporttopology) 接口) 。 在初始化期间，这些微型端口驱动程序绑定到 WaveRT、Dmu 和拓扑端口驱动程序 (与 Portcls.sys 文件中包含的 [IPortWaveRT](/windows-hardware/drivers/ddi/portcls/nn-portcls-iportwavert)、 [IPortDMus](/windows-hardware/drivers/ddi/dmusicks/nn-dmusicks-iportdmus)和 [IPortTopology](/windows-hardware/drivers/ddi/portcls/nn-portcls-iporttopology) 接口) 。 这三个 subdevice 驱动程序都采用了一个 KS 筛选器的形式。 这三个筛选器共同公开了音频适配器的完整功能。

通常，端口驱动程序为每个音频 subdevice 类提供大部分功能。 例如，WaveRT 端口驱动程序执行将音频数据流式传输到基于 DMA 的音频设备所需的大部分工作，而微型端口驱动程序提供特定于设备的详细信息，如 DMA 地址和设备名称。

音频适配器驱动程序和微型端口驱动程序通常是使用 Microsoft c + + 编写的，广泛使用 COM 接口。 端口-微型端口驱动程序体系结构促进了模块化设计。 微型端口驱动程序编写器应将其驱动程序实现为从 [IMiniport](/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiport) 接口派生的 c + + 类，该接口是标头文件 Portcls 中定义的。 硬件初始化在驱动程序加载时执行-通常在 **IMiniport** 派生类的 **Init** 方法中 (例如， [**IMiniportWaveRT：： Init**](/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportwavert-init)) 。 有关音频微型端口驱动程序的 COM 实现的详细信息，请参阅 [内核中的 com](com-in-the-kernel.md)。

下图说明了端口和微型端口驱动程序之间的关系，以及它们在音频堆栈中的位置。

![说明端口和微型端口驱动程序之间的关系的关系图](images/portcls-diag.png)

在上图中，KSEndpoint 组件是系统提供的文件，随 Windows Vista 和 windows 的更高版本一起提供。 此组件以 DLL ( # A0) 的形式提供。 KSEndpoint 将抽象内核模式设备终结点，并向音频引擎提供对抽象终结点的访问权限。 有关音频引擎的详细信息，请参阅 [探索 Windows Vista 音频引擎](exploring-the-windows-vista-audio-engine.md)。

上图中的图例显示代表供应商提供的驱动程序组件的框。 请注意，每个微型端口驱动程序的上边缘都接口指向每个端口驱动程序的下边缘。 例如，WaveRT 端口驱动程序向 WaveRT 微型端口驱动程序公开一个 **IPortWaveRT** 接口，该接口向端口驱动程序公开一个 **IMiniportWaveRT** 接口。 这些接口有时称为 *上边缘* 和 *下边缘* 接口。

端口类和 AVStream 类驱动程序类似，因为它们都是 WDM 驱动程序，它们都支持 WDM 内核流式处理体系结构。 但是，端口类驱动程序不同于多处理器处理和重入领域中的 AVStream 类驱动程序。 端口类驱动程序执行以下操作：

-   使用三层方法，将类驱动程序、端口驱动程序和供应商提供的微型端口驱动程序组合在一起。

-   具有有限数量的音频功能，使微型端口驱动程序可以更接近音频硬件。

-   允许将多个端口或微型端口驱动程序链接到特定设备。 此功能可提供更好的多功能卡支持。

-   不支持外部总线 (例如，USB) 。 所有端口驱动程序都支持驻留在系统总线上的设备 (PCMCIA 和 PCI) 。

描述 WDM 音频端口和微型端口驱动程序的术语在某些方面不同于用于其他 Windows 驱动程序类的术语。 [WDM 音频术语](wdm-audio-terminology.md)中介绍了这些差异。

本部分介绍以下主题：

[实现特定于功能的接口](implementation-of-function-specific-interfaces.md)

[操作系统提供的 PortCls 支持](portcls-support-by-operating-system.md)

 

