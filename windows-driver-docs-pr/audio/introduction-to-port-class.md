---
title: 端口类简介
description: 端口类简介
ms.assetid: 5f986e0c-d021-4dee-85d3-ad69a3708dd8
keywords:
- 音频的微型端口驱动程序 WDK，端口类
- 微型端口驱动程序 WDK 音频，端口类
- 端口类驱动程序 WDK 音频
- PortCls WDK 音频，微型端口驱动程序
- 端口类适配器驱动程序 WDK 音频
- 适配器驱动程序 WDK 音频，微型端口驱动程序
- 端口驱动程序 WDK 音频，微型端口驱动程序
- 端口类库 WDK 音频
- 端口驱动程序 WDK 音频，端口类
- 端口类音频适配器 WDK
- 端口驱动程序 WDK 音频
- PortCls WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 50718cd3a4f084e94a267ac30d902af04388fcd8
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63333392"
---
# <a name="introduction-to-port-class"></a>端口类简介


## <span id="introduction_to_port_class"></span><span id="INTRODUCTION_TO_PORT_CLASS"></span>


PCI 和基于 DMA 的音频设备的大多数硬件驱动程序以 Port Class 库，可通过 PortCls 系统驱动程序 (Portcls.sys) 访问。 PortCls 是 Microsoft 包括作为操作系统的一部分的音频端口类驱动程序。 PortCls 提供了一组实现大多数流式处理 (KS) 筛选器功能的一般内核的端口驱动程序。 因此，PortCls 简化了音频驱动程序开发人员的任务。 仅硬件供应商必须提供一组微型端口驱动程序来处理音频适配器的特定于硬件的函数。

尽管硬件供应商具有实现其音频设备自己 KS 筛选器的选项，但此选项将非常困难并不必要的典型的音频设备。 你可以开发一个 KS 筛选器，以符合 Stream.sys，Stream 类驱动程序或 Avstream.sys，AVStream 类驱动程序。 但基于 Stream.sys KS 筛选器不能利用 AVStream 中才有的改进。 有关 KS 筛选器和 PortCls 的详细信息，请参阅[WDM 音频驱动程序入门](getting-started-with-wdm-audio-drivers.md)。

可以改进 PortCls 的内部实现，若要利用的内核流式处理后续的 Windows 版本中的改进，虽然它保持与现有的驱动程序的兼容性。

PortCls Portcls.sys 系统文件中实现作为导出驱动程序 (内核模式 DLL)，并包含以下各项：

-   一组可由适配器驱动程序调用的帮助器函数

-   一系列*音频端口*驱动程序

将音频设备的硬件供应商提供负责*适配器驱动程序*。 适配器驱动程序包含初始化和微型端口驱动程序管理代码 (包括[ **DriverEntry** ](https://msdn.microsoft.com/library/windows/hardware/ff544113)函数) 和一系列*音频微型端口*驱动程序。

当操作系统加载适配器驱动程序时，适配器驱动程序创建一组的微型端口驱动程序对象，并提示 PortCls 系统驱动程序，以创建一组对应的端口驱动程序对象。 (中的代码示例[子创建](subdevice-creation.md)说明了此过程。)这些端口驱动程序通常是 Portcls.sys 文件中可用的子集。 每个微型端口驱动程序将绑定本身到匹配的端口驱动程序从以形成一个完整的 Portcls.sys*子*驱动程序。 组合子端口微型端口驱动程序是 KS 筛选器 (请参阅[音频筛选器](audio-filters.md))。 例如，典型的适配器驱动程序可能包含三个微型端口驱动程序：WaveRT、 DMusUART 和拓扑 (与[IMiniportWaveRT](https://msdn.microsoft.com/library/windows/hardware/ff536737)， [IMiniportDMus](https://msdn.microsoft.com/library/windows/hardware/ff536699)，并[IMiniportTopology](https://msdn.microsoft.com/library/windows/hardware/ff536712)接口)。 在初始化期间，这些微型端口驱动程序绑定到 WaveRT、 Dmu 和拓扑端口驱动程序 (与[IPortWaveRT](https://msdn.microsoft.com/library/windows/hardware/ff536920)， [IPortDMus](https://msdn.microsoft.com/library/windows/hardware/ff536879)，并[IPortTopology](https://msdn.microsoft.com/library/windows/hardware/ff536896)接口） Portcls.sys 文件中包含的。 每个这些三个子驱动程序采用 KS 筛选器的窗体。 三个筛选器一起提供的完整功能的声卡。

通常情况下，端口驱动程序提供了大多数的音频子每个类的功能。 例如，WaveRT 端口驱动程序的大部分内容是流式传输到基于 DMA 的音频设备时，音频数据所需的工作而微型端口驱动程序提供特定于设备的详细信息，例如 DMA 地址和设备名称。

音频适配器驱动程序和微型端口驱动程序通常以 Microsoft 编写C++和广泛使用的 COM 接口。 端口微型端口驱动程序体系结构将提升模块化设计。 微型端口驱动程序编写人员应实现其驱动程序，因为C++类派生自[IMiniport](https://msdn.microsoft.com/library/windows/hardware/ff536698)接口，该标头文件 Portcls.h 中定义接口。 硬件初始化发生在驱动程序加载时间--通常**Init**方法**IMiniport**-派生类 (例如， [ **IMiniportWaveRT::Init**](https://msdn.microsoft.com/library/windows/hardware/ff536759)). 有关音频微型端口驱动程序的 COM 实现的详细信息，请参阅[内核中的 COM](com-in-the-kernel.md)。

下图说明了端口和微型端口驱动程序和音频堆栈中的位置之间的关系。

![说明端口和微型端口驱动程序之间的关系的关系图](images/portcls-diag.png)

在上图中，KSEndpoint 组件是随 Windows Vista 和更高版本的 Windows 提供的系统提供的文件。 此组件是 DLL (Audiokse.dll) 的形式提供。 KSEndpoint 抽象化内核模式设备终结点，并为音频引擎提供有权访问的抽象的终结点。 有关音频引擎的详细信息，请参阅[探究 Windows Vista 音频引擎](exploring-the-windows-vista-audio-engine.md)。

在上图中的图例显示表示供应商提供的驱动程序组件的框。 请注意，每个微型端口驱动程序的上边缘接口到每个端口驱动程序的下边缘。 例如，WaveRT 端口驱动程序将公开**IPortWaveRT** WaveRT 微型端口驱动程序，它公开的接口**IMiniportWaveRT**端口驱动程序的接口。 这些接口有时称为*上边缘*并*低边缘*接口。

端口类和 AVStream 类驱动程序很相似，它们是 WDM 驱动程序和它们都支持 WDM 内核流式处理体系结构。 但是，端口类驱动程序不同于在多处理器的处理和可重入性方面的 AVStream 类驱动程序。 端口类驱动程序执行以下步骤：

-   使用三层类驱动程序、 端口驱动程序和供应商提供的微型端口驱动程序的方法。

-   必须在有限的数量的音频功能，它允许微型端口驱动程序能够更接近的音频硬件。

-   允许多个端口或微型端口驱动程序特定设备的链接。 此功能允许更好地支持多功能卡。

-   不支持外部总线 (例如，USB)。 所有端口驱动程序都支持在系统总线 （PCMCIA 和 PCI） 上驻留的设备。

在某些方面的 Windows 驱动程序的其他类使用的条款与不同的术语用于描述 WDM 音频端口和微型端口驱动程序。 中解释了这些差异[WDM 音频术语](wdm-audio-terminology.md)。

本部分讨论以下主题：

[特定于函数的接口的实现](implementation-of-function-specific-interfaces.md)

[PortCls 支持的操作系统](portcls-support-by-operating-system.md)

 

 




