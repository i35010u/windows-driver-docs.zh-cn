---
title: D3dCreateSurfaceEx 句柄和 DirectDraw DDIs
description: D3dCreateSurfaceEx 句柄和 DirectDraw DDIs
ms.assetid: 626b04a2-3c50-425a-bbdf-3fb24fc95215
keywords:
- 上下文 WDK Direct3D D3dCreateSurfaceEx
- D3dCreateSurfaceEx
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8351408c2feac317228a713fc1085bf418a37f0a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56547266"
---
# <a name="d3dcreatesurfaceex-handles-and-directdraw-ddis"></a>D3dCreateSurfaceEx 句柄和 DirectDraw DDIs


## <span id="ddk_d3dcreatesurfaceex_handles_and_directdraw_ddis_gg"></span><span id="DDK_D3DCREATESURFACEEX_HANDLES_AND_DIRECTDRAW_DDIS_GG"></span>


句柄不完全隔离的 DirectX 7.0 驱动程序由 DirectDraw 托管 DDRAWI\_DDSURFACE\_更和 DDRAWI\_DDSURFACE\_LCL 结构。 这些结构名称是实质上是结构的别名[ **DD\_面\_详细**](https://msdn.microsoft.com/library/windows/hardware/ff551737)并[ **DD\_面\_本地**](https://msdn.microsoft.com/library/windows/hardware/ff551733)。 在如 DirectDraw DDIs [ *DdBlt* ](https://msdn.microsoft.com/library/windows/hardware/ff549205)并[ *DdFlip*](https://msdn.microsoft.com/library/windows/hardware/ff549306)，驱动程序将图面上结构指针传递，并且必须能够使用这些而不是其私有表示形式的结构。

 

 





