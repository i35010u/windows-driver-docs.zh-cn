---
title: 驱动程序管理的纹理
description: 驱动程序管理的纹理
ms.assetid: 7ec56b86-dc29-41c3-91f4-2a30e9116b61
keywords:
- 纹理管理 WDK Direct3D，驱动程序托管
- 驱动程序管理的纹理 WDK Direct3D
- 可管理的纹理 WDK Direct3D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6e5e4104ed76553500dc82999519779eaaadce6f
ms.sourcegitcommit: b84d760d4b45795be12e625db1d5a4167dc2c9ee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/17/2020
ms.locfileid: "90716500"
---
# <a name="driver-managed-textures"></a>驱动程序管理的纹理


## <span id="ddk_driver_managed_textures_gg"></span><span id="DDK_DRIVER_MANAGED_TEXTURES_GG"></span>


驱动程序可以管理已标记为可管理的纹理。 \_在**lpSurfMore- &gt; ddCapsEx**所引用的结构的**DWCAPS2**成员中，使用 DDSCAPS2 TEXTUREMANAGE 标志将这些 DirectDrawSurface 对象标记为可管理。  (**lpSurfMore** 和 **DdCapsEx** 分别是 [**DD \_ surface \_ LOCAL**](/windows/win32/api/ddrawint/ns-ddrawint-_dd_surface_local) 和 [**dd \_ surface surface \_ **](/windows/win32/api/ddrawint/ns-ddrawint-_dd_surface_more) 结构的成员。 ) 

驱动程序通过将[**DDCORECAPS**](/windows/win32/api/ddrawi/ns-ddrawi-_ddcorecaps)结构的**dwCaps2**成员设置为 DDCAPS2 CANMANAGETEXTURE 位，来支持驱动程序托管纹理 \_ 。 驱动程序在[**DD \_ HALINFO**](/windows/win32/api/ddrawint/ns-ddrawint-_dd_halinfo)结构的**ddCaps**成员中指定此 DDCORECAPS 结构。 DD \_ HALINFO 由 [**DrvGetDirectDrawInfo**](/windows/win32/api/winddi/nf-winddi-drvgetdirectdrawinfo) 返回，以响应驱动程序的 DirectDraw 组件的初始化。

然后，该驱动程序可以采用 "延迟" 方式在视频或非本地内存中创建必要的图面。 也就是说，驱动程序将纹理置于后备面中，直到它需要它们，这刚好在对使用纹理的基元进行光栅化之前。

应该首先通过其优先级分配来逐出面。 驱动程序在 \_ [**D3dDrawPrimitives2**](/windows-hardware/drivers/ddi/d3dhal/nc-d3dhal-lpd3dhal_drawprimitives2cb) 命令流中对 D3DDP2OP SETPRIORITY 操作代码做出响应。 此操作代码设置给定表面的优先级。 作为辅助度量，驱动程序应使用最近最少使用的 (LRU) 方案来收回表面。 每当在特定方案中两个或更多纹理的优先级相同时，驱动程序将使用此方案。 从逻辑上讲，所有正在使用的表面都不应被逐出。

如果驱动程序支持托管的图面，则驱动程序可能会在视频内存丢失的情况下（例如，当发生模式切换时）为托管表面接收特殊的 [*DdDestroySurface*](/windows/win32/api/ddrawint/nc-ddrawint-pdd_surfcb_destroysurface) 调用。 在这种情况下， \_ 将设置 DRAWISURF 无效标志，驱动程序只是逐出此托管表面的视频内存副本，并保持其他结构不变。 否则，驱动程序将执行常规销毁面调用。

管理纹理时，驱动程序应适当处理 [*DdBlt*](/windows/win32/api/ddrawint/nc-ddrawint-pdd_surfcb_blt) 和 [*DdLock*](/windows/win32/api/ddrawint/nc-ddrawint-pdd_surfcb_lock) 调用。 这是因为对后备面映像所做的任何更改都必须传播到表面的视频内存副本中，然后再再次使用纹理。 驱动程序应该确定是否最好只更新部分表面或全部。 例如，如果调用驱动程序的 *DdLock* 函数来仅修改某个图面的视频内存副本的部分后备 (系统内存) 映像，则在调用该驱动程序的 *DdBlt* 函数时，该驱动程序只需 blitting 从系统内存到视频内存中所需的 subsurface 即可优化该更新。

允许该驱动程序执行纹理管理，以便在纹理上执行优化转换或自行决定在内存中传输纹理的位置和时间。

 

