---
title: 报告使用图面格式执行 2D 操作的支持
description: 报告使用图面格式执行 2D 操作的支持
ms.assetid: c7737daf-3342-48dc-a365-f789b7203013
keywords:
- 二维操作 WDK DirectX 9.0，图面上的格式
- 2D 操作 WDK DirectX 9.0，图面上的格式
- 图面格式 WDK DirectX 9.0
- 图面格式 WDK DirectX 9.0 中，报告对 2D 操作的支持
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: db0a10a650dc04096325e111f47b9420ccf19887
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67359307"
---
# <a name="reporting-support-for-2d-operations-using-surface-formats"></a>报告使用图面格式执行 2D 操作的支持


## <span id="ddk_reporting_support_for_2d_operations_using_surface_formats_gg"></span><span id="DDK_REPORTING_SUPPORT_FOR_2D_OPERATIONS_USING_SURFACE_FORMATS_GG"></span>


该驱动程序指定中使用的标志**dwOperations**的成员[ **DDPIXELFORMAT** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-_ddpixelformat)表面的格式，以指示它可以执行使用二维操作的结构该格式。

例如，可以指示驱动程序，它可以复制面向或源自并通过设置 D3DFORMAT 颜色填充到图面\_OP\_OFFSCREENPLAIN 标志。

枚举类型设置的驱动程序时使用供应商提供的代码或代码从 D3DFORMAT **dwFourCC** DDPIXELFORMAT 并将图面，该驱动程序的格式指定的成员还可以使用 D3DFORMAT\_OP\_转换\_TO\_ARGB 和 D3DFORMAT\_MEMBEROFGROUP\_ARGB 标志以指示是否可以源和目标的图面之间执行颜色转换。 即，具有 D3DFORMAT 的目标曲面\_MEMBEROFGROUP\_ARGB 标志设置指示，可从任何源面具有 D3DFORMAT 转换其颜色格式\_OP\_转换\_TO\_ARGB 标志设置。

该驱动程序可以仅指定 D3DFORMAT\_MEMBEROFGROUP\_目标图面上格式，并至少为 5 位的每个通道的颜色信息的 ARGB 标志。 也就是说，D3DFMT\_A1R5G5B5 格式中设置**dwFourCC** DDPIXELFORMAT 成员是否有效。 但是，D3DFMT\_A4R4G4B4 格式无效。 驱动程序还受限于特定源的图面上格式时指定 D3DFORMAT\_OP\_转换\_TO\_ARGB 标志。 源格式可以是任何格式有效 D3DFORMAT\_MEMBEROFGROUP\_ARGB 标志或*FOURCC*图面上的格式。

请注意，虽然 D3DFORMAT\_OP\_转换\_TO\_ARGB 和 D3DFORMAT\_MEMBEROFGROUP\_ARGB 指示 ARGB 格式，则运行时还允许指定具有曲面的驱动程序XRGB 格式 (例如，D3DFMT\_X1R5G5B5)。 如果该驱动程序指定 D3DFORMAT\_MEMBEROFGROUP\_ARGB 或 D3DFORMAT\_OP\_转换\_TO\_ARGB 格式无效，运行时使用 Direct3D HAL 导致无法加载。

 

 





