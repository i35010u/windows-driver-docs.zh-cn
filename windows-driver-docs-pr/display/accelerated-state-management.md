---
title: 加速状态管理
description: 加速状态管理
ms.assetid: 276d3cdb-34bf-49e8-aae5-94315746c5ff
keywords:
- 加速的状态管理 WDK Direct3D
- 指出 WDK Direct3D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 60bbd56a4f0ba43041f95a4e0dc1508ba3ab2756
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63323802"
---
# <a name="accelerated-state-management"></a>加速状态管理


## <span id="ddk_accelerated_state_management_gg"></span><span id="DDK_ACCELERATED_STATE_MANAGEMENT_GG"></span>


加速的状态管理是一种机制用于在单个调用跨 API 和 DDI 通信大型状态更改。 此方案允许应用程序定义的状态集调用集合作为状态块定义的一个整数。 将此整数作为呈现状态发送一次调用中执行所有状态更改。

这可减少 API 开销减少的数量**IDirect3DDevice7::SetRenderState**方法调用必需的并允许用户"预编译"阶段到其自己的更改，从而可以提高效率的驱动程序在状态块时特定于硬件的格式定义，而不是在执行每个状态更改。 **IDirect3DDevice7::SetRenderState** Direct3D SDK 文档中所述

大多数应用程序呈现中只有少量的状态，因此具有细粒度的状态转换很少很重要。 更重要的用于定义块可以互换的状态为常见的呈现方案之间的驱动程序开关。 这是整个点加速的状态管理。

状态集令牌用于驱动程序中记录了状态。 一个句柄是指状态的集合。 [ **D3DHAL\_DP2STATESET** ](https://msdn.microsoft.com/library/windows/hardware/ff545844)结构通知有关要执行何种状态集操作的驱动程序。

如果**dwOperation** D3DHAL 成员\_DP2STATESET 结构设置为 D3DHAL\_STATESETBEGIN，驱动程序将开始录制中包含的句柄的状态**dwParam**成员。 当驱动程序收到**dwOperation** D3DHAL 的\_STATESETEND，它将停止录制状态。

如果**dwOperation**成员是 D3DHAL\_STATESETDELETE，引用该状态集中**dwParam**应删除句柄。

如果**dwOperation**成员是 D3DHAL\_STATESETEXECUTE，由引用状态块**dwParam**句柄应该应用到设备中。

如果**dwOperation**成员是 D3DHAL\_STATESETCAPTURE，驱动程序中的当前状态中应捕获特定的方式提供状态块中定义的当前状态的快照。 即，捕获已在状态块中的状态。 因此，状态块是用作一种的掩码，仅记录在其中定义的状态。 例如，如果没有 D3DRENDERSTATE\_ZENABLE 呈现状态块中的状态然后的当前状态 D3DRENDERSTATE\_捕获 ZENABLE 并将其放入状态块。 如果没有 D3DRENDERSTATE\_ZENABLE 处于状态阻止，则不会捕获该状态。

状态分组用于使可针对不同的呈现方案对略有修改的一般状态块。 这些预定义的分组 （D3DSTATEBLOCKTYPE 中枚举 DirectX SDK 文档中） 定义可以随后修改状态更改以容纳预期定期呈现方案的一般状态块。 例如，驱动程序可能会创建 100 泛型预定义的状态块，然后修改每个位置以适应不同的呈现方案。 状态的块类型传入**sbType** D3DHAL 成员\_DP2STATESET 结构。

**SbType**成员时才有效 D3DHAL\_STATESETBEGIN 和 D3DHAL\_STATESETEND 并具有以下 D3DSTATEBLOCKTYPE 枚举类型之一的指定预定义的状态的块类型：**NULL**对于无状态，D3DSBT\_D3DSBT 的所有状态的所有\_像素状态和 D3DSBT PIXELSTATE\_VERTEXSTATE 顶点状态。

该驱动程序应忽略**sbType**成员，除非它实现了呈现状态扩展。 如果扩展该驱动程序实现呈现状态，即，运行时会提供的 Direct3D 呈现之外的状态，它可以使用**sbType**以确定哪种类型的预定义的呈现状态正在使用。 中的信息可以确定如何适当地追加状态块，以支持其扩展。

 

 





