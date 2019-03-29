---
title: 处理纹理阶段
description: 处理纹理阶段
ms.assetid: e22f5e2f-f17c-4a84-941b-c38e14b28550
keywords:
- 多个纹理 WDK Direct3D，纹理阶段
- 纹理阶段 WDK Direct3D
- D3DDP2OP_TEXTURESTAGESTATE
- D3DHAL_DP2TEXTURESTAGESTATE
- 纹理管理 WDK Direct3D，阶段
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9f7c475b3ff9f177eaee02c262903b500a53b21f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56575902"
---
# <a name="processing-texture-stages"></a>处理纹理阶段


## <span id="ddk_processing_texture_stages_gg"></span><span id="DDK_PROCESSING_TEXTURE_STAGES_GG"></span>


驱动程序使用 D3DDP2OP\_TEXTURESTAGESTATE 操作代码并[ **D3DHAL\_DP2TEXTURESTAGESTATE** ](https://msdn.microsoft.com/library/windows/hardware/ff545878)按照中的命令流处理更改的结构对纹理阶段状态。 该驱动程序如何处理操作代码的信息，请参阅[命令 Stream](command-stream.md)。

例如，当在操作代码是 D3DDP2OP\_TEXTURESTAGESTATE，和的值**wStateCount**的成员[ **D3DHAL\_DP2COMMAND** ](https://msdn.microsoft.com/library/windows/hardware/ff545454)结构为 7，则七个 D3DHAL\_DP2TEXTURESTAGESTATE 结构按照，最后再下一步 D3DHAL\_达到 DP2COMMAND 指令。 每个 D3DHAL\_DP2TEXTURESTAGESTATE 结构包含**dwStage**指定纹理值混合处理管道的哪个阶段需要有纹理状态更改的成员。 **TSState**相同的结构的成员指定 D3DTEXTURESTAGESTATETYPE 枚举类型，若要设置，其状态并**dwValue** D3DHAL 成员\_DP2TEXTURESTAGESTATE结构包含指定的状态应设置为的值。

该过程是指令的相同的所有呈现器状态或任何其他类型。 如果**bCommand**的成员[ **D3DHAL\_DP2COMMAND** ](https://msdn.microsoft.com/library/windows/hardware/ff545454)结构是 D3DDP2OP\_RENDERSTATE，则结构遵循是[**D3DHAL\_DP2RENDERSTATE** ](https://msdn.microsoft.com/library/windows/hardware/ff545705)结构和在该结构中的信息用于相应地设置的呈现状态。

而不是使用不同的布尔值呈现状态来控制坐标，每个呈现的状态值是一组标志组成与 D3DWRAP\_您和 D3DWRAP\_V 标志 (中定义*d3dtypes.h*)。 此更改是与更高维纹理的兼容性。

涵盖 blend 等式，每个纹理状态、 颜色操作和 alpha 的操作的语义部分中，可以在 DirectX SDK 文档中，找到属于多个纹理实现其他有用信息。 有关启用 DirectX 6.0 和更高版本，请参阅 D3DTEXTUREOP 和 D3DTEXTUREFILTERTYPE 枚举类型的纹理阶段状态类型的详细信息。

**请注意**   DirectX 9.0 和更高版本的应用程序可以使用枚举中值 D3DSAMPLERSTATETYPE 来控制的采样器与纹理相关渲染状态特征。 在 DirectX 8.0 及更早版本，D3DTEXTURESTAGESTATETYPE 枚举中包含这些采样器状态。 在运行时映射用户模式下采样器状态 (D3DSAMP\_*Xxx*) 到内核模式 D3DTSS\_*Xxx*值，因此驱动程序不需要处理用户模式下采样器状态。 有关 D3DSAMPLERSTATETYPE 详细信息，请参阅最新的 DirectX SDK 文档。

 

 

 





