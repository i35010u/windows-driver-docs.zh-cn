---
title: D3dCreateSurfaceEx 句柄和 DirectDraw DDI
description: D3dCreateSurfaceEx 句柄和 DirectDraw DDI
ms.assetid: 626b04a2-3c50-425a-bbdf-3fb24fc95215
keywords:
- 上下文 WDK Direct3D D3dCreateSurfaceEx
- D3dCreateSurfaceEx
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 627b62b1e523f869c19471ddb74291ed878c0279
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67370158"
---
# <a name="d3dcreatesurfaceex-handles-and-directdraw-ddis"></a>D3dCreateSurfaceEx 句柄和 DirectDraw DDI


## <span id="ddk_d3dcreatesurfaceex_handles_and_directdraw_ddis_gg"></span><span id="DDK_D3DCREATESURFACEEX_HANDLES_AND_DIRECTDRAW_DDIS_GG"></span>


句柄不完全隔离的 DirectX 7.0 驱动程序由 DirectDraw 托管 DDRAWI\_DDSURFACE\_更和 DDRAWI\_DDSURFACE\_LCL 结构。 这些结构名称是实质上是结构的别名[ **DD\_面\_详细**](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_surface_more)并[ **DD\_面\_本地**](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_surface_local)。 在如 DirectDraw DDIs [ *DdBlt* ](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_surfcb_blt)并[ *DdFlip*](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_surfcb_flip)，驱动程序将图面上结构指针传递，并且必须能够使用这些而不是其私有表示形式的结构。

 

 





