---
title: 功能拓扑
description: 功能拓扑
ms.assetid: f25b3581-5561-4668-8549-65506b03815d
keywords:
- 功能拓扑 WDK BDA
- 控制节点 WDK BDA
- 模板拓扑 WDK BDA
- pin 类型 WDK AVStream
- 节点 WDK AVStream
- 节点说明 Guid WDK BDA
- 实际拓扑-WDK BDA
- Guid WDK BDA
- 解调器控制节点 WDK BDA
- 调谐器控制节点 WDK BDA
- 广播驱动程序体系结构 WDK AVStream，控制节点
- BDA WDK AVStream，控制节点
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 668f8ae70e9499478c4a2abe7966f61af515b01a
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89186356"
---
# <a name="functional-topology"></a>功能拓扑





为了能够以一种适用于所有类型的网络类型以及硬件和软件实现的方式（例如，调谐器和解码器）来构建广播接收器筛选器图形，广播体系结构采用了来自 DirectShow 的筛选器图的熟悉概念，并在 *功能拓扑*的概念中对其进行了抽象。 功能拓扑（例如筛选器图）描述了传入信号发生的一系列转换。 但是，与筛选器关系图不同的是，功能拓扑不描述任何实际筛选器或软件模块;或如何在软件或硬件中实现操作。 相反，它描述了抽象 *控制节点*的配置，其中每个节点都表示一个常见的离散操作。

根据计算机上安装的硬件和软件组件的类型，相同的功能拓扑可能会导致不同的筛选器图形配置或 *实际拓扑*。 例如，如果硬件供应商选择在同一张卡上实现一个调谐器和一个解调器，则 [内核流式处理 (KS) 代理模块](/windows-hardware/drivers/ddi/_stream/index) 将筛选器图中的此硬件设备表示为一个具有两个内部控制节点的筛选器。 BDA 设备筛选器可将自身与传统的 DirectShow 过滤器区分开来，因为单个 BDA 设备过滤器可以封装任意多个硬件功能 (控制节点实现) 内置于单个功能模块 (例如，电路卡或芯片) 。

控制节点提供的函数由 GUID 唯一标识。 有关节点说明 GUID 的定义，请参阅 [BDA 节点类别 guid](./bda-node-category-guids.md)。 在图形构建过程中，网络提供程序筛选器使用这些 Guid 来确定哪些节点可用于支持特定网络类型或优化空间。 广播接收方筛选器图中的筛选器通过 COM 接口（节点类型和它们支持的 pin 类型）指示。 用于筛选器的 BDA 驱动程序通过 KS 属性集指出此相同的信息。 筛选器包含描述其节点类型、固定类型和 pin 和节点连接方式的数据结构。 此信息称为筛选器的 *模板拓扑*。 下图说明了模板拓扑。

![阐释模板拓扑的关系图](images/bapinnod.png)

上图中的模板拓扑包含五种不同的节点类型和四种不同的 pin 类型。 Pin 和节点类型的数目是由筛选器分配的任意标识符。 然而，每个节点类型都与网络提供商可以检查的节点说明 GUID 相关联。 每个节点类型在拓扑中只能出现一次，但由于筛选器会将标识符随意分配给节点类型，因此同一个控制节点 GUID 可能与多个节点类型相关联。 例如，用数字1和3标识的节点类型可以表示具有两个不同输出路径的相同控制节点 GUID。 模板拓扑必须使用两个不同的节点类型来表示此方案。 在模板拓扑中连接这些 pin 和节点类型的行显示了筛选器支持的路径。

网络提供程序必须检查此拓扑，并确定筛选器对任何特定图形中的信号执行的转换。 有关描述模板拓扑的数据结构的详细信息，请参阅 [广播驱动程序体系结构微型驱动程序](broadcast-driver-architecture-minidrivers.md)。

 

