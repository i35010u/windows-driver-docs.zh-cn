---
title: 报告体积纹理支持
description: 报告体积纹理支持
ms.assetid: da0c1c88-504e-4293-96ca-65cac2e0fe97
keywords:
- 纹理 WDK DirectX 8。0
- DirectX 8.0 发行说明 WDK Windows 2000 显示，音量纹理
- 卷纹理 WDK DirectX 8。0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 941c0f411d56f1159a682bc6c3478ac3d704d41b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72829577"
---
# <a name="reporting-support-for-volume-textures"></a>报告体积纹理支持


## <span id="ddk_reporting_support_for_volume_textures_gg"></span><span id="DDK_REPORTING_SUPPORT_FOR_VOLUME_TEXTURES_GG"></span>


DirectX 8.0 引入了两个新的基元纹理功能标志，驱动程序设置这些标志以指示支持卷纹理。 这些标志是 D3DPTEXTURECAPS\_VOLUMEMAP 和 D3DPTEXTURECAPS\_MIPVOLUMEMAP。 如果硬件支持卷纹理，则应在 D3DPRIMCAPS8 结构的**dwTextureCaps**字段中设置 D3DPTEXTURECAPS\_VOLUMEMAP （D3DCAPS8 的一部分）。 D3DPTEXTURECAPS\_MIPVOLUMEMAP 指示驱动程序支持 MIP 映射的卷纹理。

支持卷纹理的硬件还必须支持在 multitexturing 方案中使用音量纹理（与其他音量纹理或2D 纹理相结合）。 如果硬件不支持此方案，则驱动程序无法将 D3DPTEXTURECAPS 设置为 "\_VOLUMEMAP"。

该驱动程序可以通过将基元纹理功能\_D3DPTEXTURECAPS 设置为 "VOLUMEMAP\_POW2" 来指示它要求卷纹理的尺寸为2的幂。

还需要支持卷纹理的驱动程序来指定它支持的最小和最大卷纹理维度。 应将字段**MaxVolumeExtent**设置为卷纹理支持的最大尺寸。 相同的约束必须适用于所有三种尺寸的纹理（宽度、高度和深度）。

驱动程序通过将 " **VolumeTextureFilterCaps** " 和 " **VolumeTextureAddressCaps** " 设置为适当的标志组合来通知运行时硬件支持的卷纹理筛选和纹理寻址模式。

最后，驱动程序通过在表面格式的[**DDPIXELFORMAT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ddpixelformat)的**dwOperations**字段中设置 D3DFORMAT\_OP\_VOLUMETEXTURE，来通知运行时可以将哪些表面格式与卷纹理一起使用。

 

 





