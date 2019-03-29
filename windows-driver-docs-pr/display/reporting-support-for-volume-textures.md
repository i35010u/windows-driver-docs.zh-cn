---
title: 报告体积纹理支持
description: 报告体积纹理支持
ms.assetid: da0c1c88-504e-4293-96ca-65cac2e0fe97
keywords:
- 纹理 WDK DirectX 8.0
- DirectX 8.0 发行说明 WDK Windows 2000 显示，体积纹理
- 体积纹理 WDK DirectX 8.0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b2c68658eb0e80da5da356bf2c073642a1f275ab
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56563443"
---
# <a name="reporting-support-for-volume-textures"></a>报告体积纹理支持


## <span id="ddk_reporting_support_for_volume_textures_gg"></span><span id="DDK_REPORTING_SUPPORT_FOR_VOLUME_TEXTURES_GG"></span>


DirectX 8.0 引入了两个新基元纹理功能标志，用于驱动程序设置来表明支持体积纹理。 这些标志才有 D3DPTEXTURECAPS\_VOLUMEMAP 和 D3DPTEXTURECAPS\_MIPVOLUMEMAP。 D3DPTEXTURECAPS\_应在设置 VOLUMEMAP **dwTextureCaps**硬件是否支持体积纹理 D3DPRIMCAPS8 结构 （D3DCAPS8 的一部分） 的字段。 D3DPTEXTURECAPS\_MIPVOLUMEMAP 指示驱动程序支持 MIP 映射体积纹理。

支持体积纹理硬件还必须在 multitexturing 方案 （在与其他体积纹理或 2D 纹理的组合） 中支持体积纹理的使用。 如果硬件不支持这种情况下，该驱动程序不能设置 D3DPTEXTURECAPS\_VOLUMEMAP。

该驱动程序可以指示它需要通过设置基元纹理功能 D3DPTEXTURECAPS 为 2 的幂的卷纹理维数\_VOLUMEMAP\_POW2。

支持体积纹理的驱动程序还需要指定它支持的最小值和最大卷纹理尺寸。 该字段**MaxVolumeExtent**应设置为卷纹理的最大支持尺寸。 相同的约束必须应用于所有三个维度的卷纹理 （宽度、 高度和深度）。

驱动程序会通知运行时的卷纹理筛选和寻址模式的硬件支持的设置的纹理**VolumeTextureFilterCaps**并**VolumeTextureAddressCaps**到适当的标志的组合。

最后，该驱动程序会通知运行时关于哪些面格式可用于通过设置 D3DFORMAT 体积纹理\_OP\_中的 VOLUMETEXTURE **dwOperations**字段的图面格式的[**DDPIXELFORMAT**](https://msdn.microsoft.com/library/windows/hardware/ff550274)。

 

 





