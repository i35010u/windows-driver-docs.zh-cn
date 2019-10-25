---
title: 报告使用图面格式执行 2D 操作的支持
description: 报告使用图面格式执行 2D 操作的支持
ms.assetid: c7737daf-3342-48dc-a365-f789b7203013
keywords:
- 二维操作 WDK DirectX 9.0，表面格式
- 2D 操作 WDK DirectX 9.0，表面格式
- 表面格式 WDK DirectX 9。0
- surface 格式化 WDK DirectX 9.0，报告支持2D 操作
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a1728a140c98029b8e3d12a8de9e2b0353dee2e6
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72829596"
---
# <a name="reporting-support-for-2d-operations-using-surface-formats"></a>报告使用图面格式执行 2D 操作的支持


## <span id="ddk_reporting_support_for_2d_operations_using_surface_formats_gg"></span><span id="DDK_REPORTING_SUPPORT_FOR_2D_OPERATIONS_USING_SURFACE_FORMATS_GG"></span>


驱动程序在[**DDPIXELFORMAT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ddpixelformat)结构的**dwOperations**成员中指定了图面的格式标志，以指示它可以使用该格式执行2d 操作。

例如，驱动程序可以通过设置 D3DFORMAT\_OP\_OFFSCREENPLAIN 标志，指示它可以复制到图面上或从颜色填充到图面。

当驱动程序使用供应商提供的代码或 D3DFORMAT 枚举类型的代码设置 DDPIXELFORMAT 的**dwFourCC**成员并为图面分配格式时，驱动程序还可以使用 D3DFORMAT\_OP\_将\_转换为\_ARGB 和 D3DFORMAT\_MEMBEROFGROUP\_ARGB 标志，用于指示是否可以在源和目标曲面之间执行颜色转换。 也就是说，具有 D3DFORMAT\_MEMBEROFGROUP\_ARGB 标志集的目标图面指示其颜色格式可转换为具有 D3DFORMAT\_OP\_将\_转换为\_ARGB 标志集的任何源图面。

驱动程序只能为每个通道至少具有5位颜色信息的目标表面格式指定 D3DFORMAT\_MEMBEROFGROUP\_ARGB 标志。 也就是说，DDPIXELFORMAT 的**dwFourCC**成员中设置的 D3DFMT\_A1R5G5B5 格式有效。 但是，D3DFMT\_A4R4G4B4 格式无效。 指定\_D3DFORMAT 时，驱动程序也将被限制为特定的源表面格式，\_将\_转换为\_ARGB 标志。 源格式可以是任何对 D3DFORMAT\_MEMBEROFGROUP\_ARGB 标志或*FOURCC* surface 格式有效的格式。

请注意，尽管 D3DFORMAT\_OP\_将\_转换为\_ARGB 和 D3DFORMAT\_MEMBEROFGROUP\_ARGB 表示 ARGB 格式，但运行时还允许驱动程序指定带有 XRGB 格式的表面（例如，D3DFMT\_X1R5G5B5）。 如果驱动程序指定 D3DFORMAT\_MEMBEROFGROUP\_ARGB 或 D3DFORMAT\_OP\_将\_转换为具有无效格式的\_ARGB，则运行时将阻止 Direct3D HAL 加载。

 

 





