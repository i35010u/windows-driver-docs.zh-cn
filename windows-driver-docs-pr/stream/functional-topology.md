---
title: 功能拓扑
description: 功能拓扑
ms.assetid: f25b3581-5561-4668-8549-65506b03815d
keywords:
- 功能拓扑 WDK BDA
- 控制节点 WDK BDA
- 模板拓扑 WDK BDA
- 将固定类型 WDK AVStream
- 节点 WDK AVStream
- 节点说明 Guid WDK BDA
- 实际拓扑 WDK BDA
- Guid WDK BDA
- 解调器控制节点 WDK BDA
- 调谐器控制节点 WDK BDA
- 广播驱动程序体系结构 WDK AVStream，控制节点
- BDA WDK AVStream，控制节点
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 223e090fcbed413dc60cd871b602ff52a8d8a377
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56562770"
---
# <a name="functional-topology"></a>功能拓扑





若要启用的适用于所有类型的网络类型，采用了广播的接收器筛选器关系图生成和硬件和软件实现的例如，调谐器和解码器，广播体系结构采用筛选器关系图的熟悉的概念从 DirectShow 和中的概念抽象化*功能拓扑*。 功能的拓扑，像是一个筛选器图形，描述发生的转换的一系列上传入的信号。 但是，与筛选器图形，不同的功能的拓扑不描述任何实际筛选器或软件模块;或操作中的软件或硬件的实现方式。 相反，它描述了抽象的配置*控制节点*，其中每个表示某些常用的离散操作。

根据计算机中安装的硬件和软件组件的类型，相同的功能拓扑可能会导致不同的筛选器图形配置或*实际拓扑*。 例如，如果硬件供应商选择实现调谐器和解调器上同一线路张卡，然后[内核流式处理 (KS) 代理模块](https://msdn.microsoft.com/library/windows/hardware/ff560877)这个硬件设备筛选器关系图中的表示为具有两个有单个筛选器内部控制节点。 BDA 设备筛选器区分开来本身更传统的 DirectShow 筛选器因为单个 BDA 设备筛选器可以封装为多硬件的函数 （控制节点实现） 内置于单个功能模块 （例如，一条线路卡或芯片）。

由 GUID 唯一地标识控制节点提供的函数。 节点说明的 GUID 的定义，请参阅[BDA 节点类别 Guid](https://msdn.microsoft.com/library/windows/hardware/ff556529)。 在关系图构建过程中，网络提供程序筛选器使用这些 Guid 来确定哪些节点可支持特定的网络类型或优化空间中。 指示广播的接收器筛选器关系图中的筛选器，通过 COM 接口、 节点类型和它们支持的 pin 类型。 BDA 驱动程序的筛选器指示 KS 属性集通过此相同信息。 筛选器包含数据结构，用于描述其节点类型、 固定类型和 pin 和节点可以连接的方式。 此信息的筛选器称为*模板拓扑*。 下图演示了模板拓扑。

![说明模板拓扑关系图](images/bapinnod.png)

在上图中的模板拓扑包含五个不同的节点类型和四种不同的 pin 类型。 Pin 和节点类型的数字是由筛选器分配的任意标示符。 每个节点类型，但是，是节点说明可以检查网络提供商的 GUID 与相关联。 每个节点类型可以只出现一次在拓扑中，但因为任意方法筛选器将标识符分配到节点类型，相同的控制节点 GUID 可以与多个节点类型关联。 例如，带有数字 1 和 3 的节点类型可以表示具有两个不同的输出路径的相同控制节点 GUID。 模板拓扑必须代表两个单独的节点类型与此方案。 连接这些 pin 和节点类型模板拓扑中的行显示的路径筛选器支持。

网络提供商必须检查此拓扑，并确定对任何特定关系图中的信号的筛选器执行的转换。 有关描述模板拓扑的数据结构的详细信息，请参阅[广播驱动程序体系结构微型驱动程序](broadcast-driver-architecture-minidrivers.md)。

 

 




