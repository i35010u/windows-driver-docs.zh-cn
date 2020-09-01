---
title: 处理纹理阶段
description: 处理纹理阶段
ms.assetid: e22f5e2f-f17c-4a84-941b-c38e14b28550
keywords:
- 多纹理 WDK Direct3D，纹理阶段
- 纹理阶段 WDK Direct3D
- D3DDP2OP_TEXTURESTAGESTATE
- D3DHAL_DP2TEXTURESTAGESTATE
- 纹理管理 WDK Direct3D，阶段
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9b1f397be1a9e1bc6ca497d8397ac556a37f67d2
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89066432"
---
# <a name="processing-texture-stages"></a>处理纹理阶段


## <span id="ddk_processing_texture_stages_gg"></span><span id="DDK_PROCESSING_TEXTURE_STAGES_GG"></span>


驱动程序使用 \_ 命令流中后面的 D3DDP2OP TEXTURESTAGESTATE 操作代码和 [**D3DHAL \_ DP2TEXTURESTAGESTATE**](/windows-hardware/drivers/ddi/d3dhal/ns-d3dhal-_d3dhal_dp2texturestagestate) 结构处理纹理阶段状态的更改。 有关驱动程序如何处理操作代码的信息，请参阅 [命令流](command-stream.md)。

例如，当操作代码为 D3DDP2OP \_ TEXTURESTAGESTATE，并且[**D3DHAL \_ DP2COMMAND**](/windows-hardware/drivers/ddi/d3dhal/ns-d3dhal-_d3dhal_dp2command)结构的**wStateCount**成员的值为7时，在 \_ 到达下一个 D3DHAL DP2TEXTURESTAGESTATE 指令之前，将出现7个 D3DHAL DP2COMMAND 结构 \_ 。 每个 D3DHAL \_ DP2TEXTURESTAGESTATE 结构都包含一个 **dwStage** 成员，该成员指定纹理混合管道的哪个阶段需要更改纹理状态。 相同结构的 **TSState** 成员指定要设置的 D3DTEXTURESTAGESTATETYPE 枚举类型的状态，而 D3DHAL DP2TEXTURESTAGESTATE 结构的 **dwValue** 成员 \_ 包含应设置指定状态的值。

对于所有呈现状态或任何其他类型的指令，此过程都是相同的。 如果[**D3DHAL \_ DP2COMMAND**](/windows-hardware/drivers/ddi/d3dhal/ns-d3dhal-_d3dhal_dp2command)结构的**bCommand**成员是 D3DDP2OP \_ RENDERSTATE，则下面的结构是一个[**D3DHAL \_ DP2RENDERSTATE**](/windows-hardware/drivers/ddi/d3dhal/ns-d3dhal-_d3dhal_dp2renderstate)结构，该结构中的信息将用于相应地设置呈现状态。

每个呈现状态值是一组在 \_ \_ *d3dtypes*) 中定义 (和 D3DWRAP V 标志的标志，而不是使用不同的布尔值呈现状态来控制坐标。 此更改是为了与较三维纹理兼容。

有关多纹理实现的其他有用信息，请参阅 DirectX SDK 文档中的 "混合公式" 部分、"每纹理状态的语义"、"颜色操作" 和 "alpha 操作"。 有关为 DirectX 6.0 和更高版本启用的纹理阶段状态类型的详细信息，请参阅 D3DTEXTUREOP 和 D3DTEXTUREFILTERTYPE 枚举类型。

**注意**   DirectX 9.0 和更高版本的应用程序可以使用 D3DSAMPLERSTATETYPE 枚举中的值来控制采样器纹理相关呈现器状态的特征。 在 DirectX 8.0 及更早版本中，这些采样器状态包含在 D3DTEXTURESTAGESTATETYPE 枚举中。 运行时将用户模式采样器状态映射 (D3DSAMP \_ *Xxx*) 为内核模式 D3DTSS \_ *Xxx*值，以便驱动程序无需处理用户模式采样器状态。 有关 D3DSAMPLERSTATETYPE 的详细信息，请参阅最新的 DirectX SDK 文档。

 

 

