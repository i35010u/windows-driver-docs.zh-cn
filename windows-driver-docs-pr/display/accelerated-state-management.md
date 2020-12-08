---
title: 加速状态管理
description: 加速状态管理
keywords:
- 加速状态管理 WDK Direct3D
- 状态 WDK Direct3D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 95da2ebc9a966e835ff2cb521954a84ee1045b63
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96810581"
---
# <a name="accelerated-state-management"></a>加速状态管理


## <span id="ddk_accelerated_state_management_gg"></span><span id="DDK_ACCELERATED_STATE_MANAGEMENT_GG"></span>


加速状态管理是一种机制，用于在单个调用中跨 API 和 DDI 传递大状态更改。 此方案允许应用程序将状态集调用的集合定义为单个整数定义的状态块。 作为渲染状态发送此整数将在一次调用中执行所有状态更改。

这会减少 API 开销，因为它减少了所需的 **IDirect3DDevice7：： SetRenderState** 方法调用的数目，并且可以通过在状态块定义时允许它们将更改为其自己的特定于硬件的格式，而不是每次状态更改的执行来改善驱动程序的效率。 Direct3D SDK 文档中介绍了 **IDirect3DDevice7：： SetRenderState**

大多数应用程序只会在少数几种状态下进行呈现，因此不太重要。 更为重要的是，能够定义可在常见呈现方案间进行交换的状态块。 这是加速状态管理的要点。

状态集令牌用于记录驱动程序中的状态。 句柄是指状态的集合。 [**D3DHAL \_ DP2STATESET**](/windows-hardware/drivers/ddi/d3dhal/ns-d3dhal-_d3dhal_dp2stateset)结构通知驱动程序要执行的状态集操作。

如果 D3DHAL DP2STATESET 结构的 **dwOperation** 成员 \_ 设置为 D3DHAL \_ STATESETBEGIN，则驱动程序将开始记录 **dwParam** 成员中包含的句柄的状态。 当驱动程序接收到 D3DHAL STATESETEND 的 **dwOperation** 时 \_ ，它将停止记录状态。

如果 **dwOperation** 成员是 D3DHAL \_ STATESETDELETE，则应删除 **dwParam** 句柄所引用的状态集。

如果 **dwOperation** 成员是 D3DHAL \_ STATESETEXECUTE，则应在设备中应用 **dwParam** 句柄所引用的状态块。

如果 **dwOperation** 成员是 D3DHAL \_ STATESETCAPTURE，则应以特定方式捕获驱动程序中的当前状态，从而提供状态块中定义的当前状态的快照。 也就是说，只捕获状态块中已经存在的状态。 因此，状态块充当一种掩码，只记录其中定义的记录状态。 例如，如果 \_ 状态块中有一个 D3DRENDERSTATE ZENABLE 呈现状态，则将捕获 D3DRENDERSTATE ZENABLE 的当前状态 \_ 并将其放入状态块。 如果 \_ 状态块中没有 D3DRENDERSTATE ZENABLE，则不会捕获该状态。

状态分组用于生成可对不同呈现方案进行略微修改的通用状态块。  (在 DirectX SDK 文档的 D3DSTATEBLOCKTYPE 中枚举这些预定义分组) 定义一般状态块，随后可以用状态更改进行修改以适应预期的重复呈现方案。 例如，驱动程序可能会创建100一般预定义状态块，然后略微修改它们以适应不同的呈现方案。 在 D3DHAL DP2STATESET 结构的 **sbType** 成员中传递状态块类型 \_ 。

**SbType** 成员仅适用于 D3DHAL \_ STATESETBEGIN 和 D3DHAL \_ STATESETEND，并指定预定义的状态块类型和以下 D3DSTATEBLOCKTYPE 枚举类型之一： **NULL** 表示无状态，D3DSBT 所有 \_ 状态的所有状态，D3DSBT PIXELSTATE 用于 \_ 像素状态，D3DSBT VERTEXSTATE \_ 用于顶点状态。

驱动程序应忽略 **sbType** 成员，除非它实现呈现状态扩展。 如果驱动程序实现扩展呈现状态（即，呈现 Direct3D 运行时提供的状态除外），则它可以使用 **sbType** 来确定所使用的预定义呈现状态的类型。 通过此信息，可以确定如何适当地附加状态块以支持其扩展。

 

