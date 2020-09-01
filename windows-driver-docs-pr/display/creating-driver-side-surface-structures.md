---
title: 创建驱动程序端图面结构
description: 创建驱动程序端图面结构
ms.assetid: d5e2e6ee-8853-4a17-b1c6-48c75474b2b7
keywords:
- 上下文 WDK Direct3D，驱动程序端表面结构
- 驱动程序端表面结构 WDK Direct3D
- D3dCreateSurfaceEx
- 表面 WDK DirectDraw，驱动程序端结构
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: af957acb08c4d8f6f9097e3f1fa5f21e0c90c647
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89067334"
---
# <a name="creating-driver-side-surface-structures"></a>创建驱动程序端图面结构


## <span id="ddk_creating_driver_side_surface_structures_gg"></span><span id="DDK_CREATING_DRIVER_SIDE_SURFACE_STRUCTURES_GG"></span>


DirectDraw 运行时在调用了[*DdCreateSurface*](/previous-versions/windows/hardware/drivers/ff549263(v=vs.85))入口点并为其分配的内存后调用驱动程序的[**D3dCreateSurfaceEx**](/windows/desktop/api/ddrawint/nc-ddrawint-pdd_createsurfaceex)入口点。 运行时仅*D3dCreateSurfaceEx*对用 DDSCAPS \_ 纹理、DDSCAPS \_ EXECUTEBUFFER、DDSCAPS \_ 3DDEVICE 或 DDSCAPS \_ ZBUFFER 标志标记的图面调用 D3dCreateSurfaceEx。

在调用 [**D3dCreateSurfaceEx**](/windows/desktop/api/ddrawint/nc-ddrawint-pdd_createsurfaceex)之前，运行时会将整数值指定为图面的句柄。 此值存储在 DDRAWI DDSURFACE 结构 (的**dwSurfaceHandle**成员中， \_ \_ 由 DDRAWI **lpSurfMore** \_ DDSURFACE LCL 结构) 的 lpSurfMore 成员指向 \_ 。 请参阅 [**dd \_ surface \_ 更多**](/windows/desktop/api/ddrawint/ns-ddrawint-_dd_surface_more) 和 [**dd \_ surface \_ LOCAL**](/windows/desktop/api/ddrawint/ns-ddrawint-_dd_surface_local)，这是 DDRAWI DDSURFACE 的别名 \_ \_ 和 DDRAWI \_ DDSURFACE \_ LCL 结构。

这些整数值从1开始，并尽可能小。  (零是为表面控点保证的无效值。 ) 目的在于驱动程序可以将指针数组保存到其自身的结构中。 当 *D3dCreateSurfaceEx* 被称为数组末尾) 之外时，它会 (立即重新分配数组，然后继续。 Direct3D 运行时通过 *D3dCreateSurfaceEx*将句柄显示给驱动程序之前，不会将句柄值传递给驱动程序。 但是，驱动程序应足够强大，以便处理超出范围的值，或引用句柄表中已被释放的 DdDestroySurface 的槽， (是已为其) 调用了[*DdDestroySurface*](/windows/desktop/api/ddrawint/nc-ddrawint-pdd_surfcb_destroysurface)的句柄。 请注意，由于零是一个保证无效的值，因此句柄表中的零项可重复用于其他目的。 *Perm3*示例驱动程序使用零项来存储数组的当前长度。

**注意**   Microsoft Windows 驱动程序工具包 (WDK) 不包含*Perm3*)  (的 3Dlabs Permedia3 示例显示驱动程序。 你可以从 Windows Server 2003 SP1 驱动程序开发工具包获取此示例驱动程序 (DDK) ，你可以从 WDHC 网站的 "Windows 驱动程序开发工具包" 页下载该驱动程序。

 

 

