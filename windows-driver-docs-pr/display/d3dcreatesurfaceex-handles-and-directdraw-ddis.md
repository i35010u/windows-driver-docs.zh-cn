---
title: D3dCreateSurfaceEx 句柄和 DirectDraw DDI
description: D3dCreateSurfaceEx 句柄和 DirectDraw DDI
ms.assetid: 626b04a2-3c50-425a-bbdf-3fb24fc95215
keywords:
- 上下文 WDK Direct3D，D3dCreateSurfaceEx
- D3dCreateSurfaceEx
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 204849eedfbb44a188b43f1c4cb1e90739377007
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89063138"
---
# <a name="d3dcreatesurfaceex-handles-and-directdraw-ddis"></a>D3dCreateSurfaceEx 句柄和 DirectDraw DDI


## <span id="ddk_d3dcreatesurfaceex_handles_and_directdraw_ddis_gg"></span><span id="DDK_D3DCREATESURFACEEX_HANDLES_AND_DIRECTDRAW_DDIS_GG"></span>


句柄并不完全将 DirectX 7.0 驱动程序与 DirectDraw 托管的 DDRAWI \_ DDSURFACE \_ 更多和 DDRAWI \_ DDSURFACE \_ LCL 结构隔离。 这些结构名称本质上是用于结构 [**DD \_ Surface \_ **](/windows/desktop/api/ddrawint/ns-ddrawint-_dd_surface_more) 和 [**dd \_ surface \_ LOCAL**](/windows/desktop/api/ddrawint/ns-ddrawint-_dd_surface_local)的别名。 在 DirectDraw DDIs （如 [*DdBlt*](/windows/desktop/api/ddrawint/nc-ddrawint-pdd_surfcb_blt) 和 [*DdFlip*](/windows/desktop/api/ddrawint/nc-ddrawint-pdd_surfcb_flip)）中，驱动程序传递 surface structure 指针，并且必须能够使用这些结构而不是其专用表示形式。

 

