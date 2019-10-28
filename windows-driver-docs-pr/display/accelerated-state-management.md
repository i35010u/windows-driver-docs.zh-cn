---
title: 加速状态管理
description: 加速状态管理
ms.assetid: 276d3cdb-34bf-49e8-aae5-94315746c5ff
keywords:
- 加速状态管理 WDK Direct3D
- 状态 WDK Direct3D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c2107b9227b56fe29389241990e5ea69991b6c34
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839836"
---
# <a name="accelerated-state-management"></a>加速状态管理


## <span id="ddk_accelerated_state_management_gg"></span><span id="DDK_ACCELERATED_STATE_MANAGEMENT_GG"></span>


加速状态管理是一种机制，用于在单个调用中跨 API 和 DDI 传递大状态更改。 此方案允许应用程序将状态集调用的集合定义为单个整数定义的状态块。 作为渲染状态发送此整数将在一次调用中执行所有状态更改。

这会减少 API 开销，因为它减少了所需的**IDirect3DDevice7：： SetRenderState**方法调用的数目，并且可以通过允许它们将状态更改为其自己的特定于硬件的格式来 "预编译"，从而提高驱动程序的效率块定义，而不是在每次状态更改时执行。 Direct3D SDK 文档中介绍了**IDirect3DDevice7：： SetRenderState**

大多数应用程序只会在少数几种状态下进行呈现，因此不太重要。 更为重要的是，能够定义可在常见呈现方案间进行交换的状态块。 这是加速状态管理的要点。

状态集令牌用于记录驱动程序中的状态。 句柄是指状态的集合。 [**D3DHAL\_DP2STATESET**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/ns-d3dhal-_d3dhal_dp2stateset)结构通知驱动程序要执行哪些状态集操作。

如果 D3DHAL\_DP2STATESET 结构的**dwOperation**成员设置为 D3DHAL\_STATESETBEGIN，则驱动程序将开始记录**dwParam**成员中包含的句柄的状态。 当驱动程序收到 D3DHAL\_STATESETEND 的**dwOperation**时，它将停止记录状态。

如果**dwOperation**成员为 D3DHAL\_STATESETDELETE，则应删除**dwParam**句柄所引用的状态集。

如果**dwOperation**成员为 D3DHAL\_STATESETEXECUTE，则应在设备中应用**dwParam**句柄所引用的状态块。

如果**dwOperation**成员为 D3DHAL\_STATESETCAPTURE，则应以特定方式捕获驱动程序中的当前状态，从而提供状态块中定义的当前状态的快照。 也就是说，只捕获状态块中已经存在的状态。 因此，状态块充当一种掩码，只记录其中定义的记录状态。 例如，如果状态块中有一个 D3DRENDERSTATE\_ZENABLE render 状态，则捕获 D3DRENDERSTATE\_ZENABLE 的当前状态，并将其放入状态块。 如果状态块中没有 D3DRENDERSTATE\_ZENABLE，则不会捕获该状态。

状态分组用于生成可对不同呈现方案进行略微修改的通用状态块。 这些预定义的分组（在 DirectX SDK 文档的 D3DSTATEBLOCKTYPE 中枚举）定义一般状态块，随后可以用状态更改进行修改以适应预期的重复呈现方案。 例如，驱动程序可能会创建100一般预定义状态块，然后略微修改它们以适应不同的呈现方案。 在 D3DHAL\_DP2STATESET 结构的**sbType**成员中传递状态块类型。

**SbType**成员仅对 D3DHAL\_STATESETBEGIN 和 D3DHAL\_STATESETEND 有效，并指定具有以下 D3DSTATEBLOCKTYPE 枚举类型之一的预定义状态块类型： **NULL**表示无状态，D3DSBT @no__t_所有状态均为4_、D3DSBT\_PIXELSTATE for 象素 state 和 D3DSBT\_VERTEXSTATE for 顶点状态。

驱动程序应忽略**sbType**成员，除非它实现呈现状态扩展。 如果驱动程序实现扩展呈现状态（即，呈现 Direct3D 运行时提供的状态除外），则它可以使用**sbType**来确定所使用的预定义呈现状态的类型。 通过此信息，可以确定如何适当地附加状态块以支持其扩展。

 

 





