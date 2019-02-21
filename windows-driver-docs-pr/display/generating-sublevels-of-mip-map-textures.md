---
title: 生成 MIP 映射纹理的子级别
description: 生成 MIP 映射纹理的子级别
ms.assetid: fbfb0d1b-468d-4e7f-865e-bdc7d19f5516
keywords:
- MIP 映射纹理 WDK DirectX 9.0 中，生成子级别
- MIP 贴图纹理 WDK DirectX 9.0 的子级别
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0d51be4c4595834d7d458c3ec9ca57f8735b0988
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56519265"
---
# <a name="generating-sublevels-of-mip-map-textures"></a>生成 MIP 映射纹理的子级别


## <span id="ddk_generating_sublevels_of_mip_map_textures_gg"></span><span id="DDK_GENERATING_SUBLEVELS_OF_MIP_MAP_TEXTURES_GG"></span>


显示驱动程序指示支持自动生成 MIP 贴图纹理的子级别通过设置 DDCAPS2\_CANAUTOGENMIPMAP 位**dwCaps2**的成员[ **DDCORECAPS** ](https://msdn.microsoft.com/library/windows/hardware/ff549248)结构。 该驱动程序指定在此 DDCORECAPS 结构**ddCaps**的成员[ **DD\_HALINFO** ](https://msdn.microsoft.com/library/windows/hardware/ff551627)结构。 DD\_驱动程序的返回 HALINFO [ **DrvGetDirectDrawInfo** ](https://msdn.microsoft.com/library/windows/hardware/ff556229)函数。 显示驱动程序还指示是否以特定的面格式支持自动生成的子级别通过设置 D3DFORMAT\_OP\_AUTOGENMIPMAP 标志**dwOperations**的成员[ **DDPIXELFORMAT** ](https://msdn.microsoft.com/library/windows/hardware/ff550274)格式的结构。

Direct3D 运行时创建纹理图面时，设置 DDSCAPS3\_AUTOGENMIPMAP 位**dwCaps3** DDSCAPSEX 的成员 ([**DDSCAPS2**](https://msdn.microsoft.com/library/windows/hardware/ff550292))若要指示此纹理 MIP 贴图子级别可以自动生成的结构。 如果 Direct3D 指示某些纹理自动生成其 MIP 贴图子级别和一些纹理不会自动生成，该驱动程序只能执行位块操作 (D3DDP2OP\_TEXBLT) 对这些纹理中以下所述方案：

-   该驱动程序不能从 MIP 映射到目标纹理不会自动生成的源纹理的位块。

-   如果不会不自动生成 MIP 源纹理从驱动程序 blits 映射到的目标纹理，驱动程序仅 blits 最顶层的匹配级别。 从源纹理子级别将被忽略。 可以生成目标子级别。

-   同样，如果映射到目标纹理，同时自动生成 MIP 驱动程序 blits 源中的，驱动程序仅 blits 的最顶层级别匹配。 从源纹理子级别将被忽略。 可以生成目标子级别。

若要生成 MIP 贴图纹理的子级别，该驱动程序收到 D3DDP2OP\_GENERATEMIPSUBLEVELS 命令连同[ **D3DHAL\_DP2GENERATEMIPSUBLEVELS** ](https://msdn.microsoft.com/library/windows/hardware/ff545570)结构。 若要接收此命令，纹理的图面格式必须公开 D3DFORMAT\_OP\_AUTOGENMIPMAP 标志。

有关[驱动程序管理资源](driver-managed-resources.md)，驱动程序逐出和替换的视频内存中的资源，该驱动程序必须使用的最后一个组筛选器类型自动生成子级别时。 因为 Direct3D 不控制逐出和资源的替换，Direct3D 不会发送 D3DDP2OP\_GENERATEMIPSUBLEVELS 命令向驱动程序。

Direct3D 运行时不能调用的驱动程序[ *DdLock* ](https://msdn.microsoft.com/library/windows/hardware/ff549599)函数或使用任何其他[DDI](direct3d-driver-ddi.md)访问自动生成 MIP 贴图纹理的子级别。 这意味着对于自动生成 MIP 贴图纹理，与轻型 MIP 贴图纹理相同，子级别是"隐式"，并可以通过适当的驱动程序指定。 该驱动程序不需要指定"已完成"的图面上的数据结构。 但请注意，必须能够调用驱动程序的 Direct3D *DdLock*或[ *DdBlt* ](https://msdn.microsoft.com/library/windows/hardware/ff549205)函数，发送 D3DDP2OP\_BLT 命令，或使用任何其他 DDI （适用于[驱动程序管理纹理](driver-managed-textures.md)，动态纹理或特定于供应商仅格式) 来访问自动生成 MIP 贴图纹理的最高级别。

 

 





