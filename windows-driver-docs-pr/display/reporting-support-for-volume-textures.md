---
title: 报告体积纹理支持
description: 报告体积纹理支持
keywords:
- 纹理 WDK DirectX 8。0
- DirectX 8.0 发行说明 WDK Windows 2000 显示，音量纹理
- 卷纹理 WDK DirectX 8。0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b4fd189b36e9a6d33f8406788bd3e72b21e35f18
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96808443"
---
# <a name="reporting-support-for-volume-textures"></a>报告体积纹理支持


## <span id="ddk_reporting_support_for_volume_textures_gg"></span><span id="DDK_REPORTING_SUPPORT_FOR_VOLUME_TEXTURES_GG"></span>


DirectX 8.0 引入了两个新的基元纹理功能标志，驱动程序设置这些标志以指示支持卷纹理。 这些标志是 D3DPTEXTURECAPS \_ VOLUMEMAP 和 D3DPTEXTURECAPS \_ MIPVOLUMEMAP。 \_如果硬件支持批量纹理，则应在 D3DCAPS8) 的 **dwTextureCaps** 字段中设置 D3DPTEXTURECAPS VOLUMEMAP (部分。 D3DPTEXTURECAPS \_ MIPVOLUMEMAP 指示驱动程序支持 MIP 映射的卷纹理。

支持卷纹理的硬件还必须支持在 multitexturing 方案中使用音量纹理 (与其他音量纹理或2D 纹理) 结合使用。 如果硬件不支持此方案，驱动程序将无法设置 D3DPTEXTURECAPS \_ VOLUMEMAP。

驱动程序可以通过设置基元纹理功能 D3DPTEXTURECAPS VOLUMEMAP POW2，来指示它要求卷纹理的尺寸为2的幂 \_ \_ 。

还需要支持卷纹理的驱动程序来指定它支持的最小和最大卷纹理维度。 应将字段 **MaxVolumeExtent** 设置为卷纹理支持的最大尺寸。 相同的约束必须应用于卷纹理的所有三个维度 (宽度、高度和深度) 。

驱动程序通过将 " **VolumeTextureFilterCaps** " 和 " **VolumeTextureAddressCaps** " 设置为适当的标志组合来通知运行时硬件支持的卷纹理筛选和纹理寻址模式。

最后，驱动程序通过 \_ \_ 在表面格式的 [**DDPIXELFORMAT**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ddpixelformat)的 **dwOperations** 字段中设置 D3DFORMAT OP VOLUMETEXTURE，通知运行时可以将哪些表面格式与卷纹理一起使用。

 

