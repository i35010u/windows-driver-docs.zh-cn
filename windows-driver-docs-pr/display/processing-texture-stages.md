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
ms.openlocfilehash: 03ff3d64f62f635257131e949c6e90de9006c175
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72826052"
---
# <a name="processing-texture-stages"></a>处理纹理阶段


## <span id="ddk_processing_texture_stages_gg"></span><span id="DDK_PROCESSING_TEXTURE_STAGES_GG"></span>


驱动程序使用命令流中的 D3DDP2OP\_TEXTURESTAGESTATE 操作代码和[**D3DHAL\_DP2TEXTURESTAGESTATE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/ns-d3dhal-_d3dhal_dp2texturestagestate)结构处理纹理阶段状态的更改。 有关驱动程序如何处理操作代码的信息，请参阅[命令流](command-stream.md)。

例如，当操作代码为 D3DDP2OP\_TEXTURESTAGESTATE，而[ **\_D3DHAL**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/ns-d3dhal-_d3dhal_dp2command)的 wStateCount 成员的值为7时，结构的成员的值为7，然后在到达下一个 DP2COMMAND\_D3DHAL 指令之前，七个 DP2TEXTURESTAGESTATE\_D3DHAL 结构。 每个 D3DHAL\_DP2TEXTURESTAGESTATE 结构都包含一个**dwStage**成员，该成员指定纹理混合管道的哪个阶段需要纹理状态更改。 同一结构的**TSState**成员指定要设置的 D3DTEXTURESTAGESTATETYPE 枚举类型的状态，而 D3DHAL\_DP2TEXTURESTAGESTATE 结构的**dwValue**成员包含指定状态应设置为的值。

对于所有呈现状态或任何其他类型的指令，此过程都是相同的。 如果[**D3DHAL\_DP2COMMAND**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/ns-d3dhal-_d3dhal_dp2command)结构的**BCOMMAND**成员为 D3DDP2OP\_RENDERSTATE，则以下结构为[**D3DHAL\_DP2RENDERSTATE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/ns-d3dhal-_d3dhal_dp2renderstate)结构，该结构中的信息将用于相应地设置渲染状态。

每个呈现状态值是一组由 D3DWRAP\_您和\_D3DWRAP 的标志（在*d3dtypes*中定义），而不是使用不同的布尔值呈现状态来控制坐标。 此更改是为了与较三维纹理兼容。

有关多纹理实现的其他有用信息，请参阅 DirectX SDK 文档中的 "混合公式" 部分、"每纹理状态的语义"、"颜色操作" 和 "alpha 操作"。 有关为 DirectX 6.0 和更高版本启用的纹理阶段状态类型的详细信息，请参阅 D3DTEXTUREOP 和 D3DTEXTUREFILTERTYPE 枚举类型。

**请注意**   DirectX 9.0 和更高版本的应用程序可以使用 D3DSAMPLERSTATETYPE 枚举中的值来控制采样器纹理相关呈现器状态的特征。 在 DirectX 8.0 及更早版本中，这些采样器状态包含在 D3DTEXTURESTAGESTATETYPE 枚举中。 运行时将用户模式采样器状态（D3DSAMP\_*xxx*）映射到内核模式 D3DTSS\_*Xxx*值，以便驱动程序无需处理用户模式采样器状态。 有关 D3DSAMPLERSTATETYPE 的详细信息，请参阅最新的 DirectX SDK 文档。

 

 

 





