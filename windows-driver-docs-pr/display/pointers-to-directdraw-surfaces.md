---
title: 指向 DirectDraw 图面的指针
description: 指向 DirectDraw 图面的指针
keywords:
- 上下文 WDK Direct3D，DirectDraw surface 指针
- DirectDraw 图面指针 WDK Direct3D
- DirectDraw WDK Direct3D 的表面指针
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c83439e56494b7567251572fd85be0840a3a71b8
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96795575"
---
# <a name="pointers-to-directdraw-surfaces"></a>指向 DirectDraw 图面的指针


## <span id="ddk_pointers_to_directdraw_surfaces_gg"></span><span id="DDK_POINTERS_TO_DIRECTDRAW_SURFACES_GG"></span>


驱动程序编写者可能会尝试将指向 DirectDrawSurface 数据结构的指针保存到其专用驱动程序端表面结构内。 但是，这种做法在 Microsoft Windows 2000 和更高版本中不会成功，因为对 DirectDraw 内核端数据结构的访问是通过管理方案经过调谐的，该方案将这些结构从用户模式和驱动程序中隔离开来。 [**EngLockDirectDrawSurface**](/windows/win32/api/winddi/nf-winddi-englockdirectdrawsurface) 提供指向结构的指针，该结构在调用 [**EngUnlockDirectDrawSurface**](/windows/win32/api/winddi/nf-winddi-engunlockdirectdrawsurface) 例程之前有效。

在此锁定/取消锁定对外，该结构不能保证驻留在同一位置，甚至不存在。 此外，这些锁定/取消锁定对会影响性能。 如果驱动程序保留自己的 surface 结构副本，则不需要锁。 在低频率调用（如 [**D3dCreateSurfaceEx**](/windows/win32/api/ddrawint/nc-ddrawint-pdd_createsurfaceex)）期间，对驱动程序端表面结构内的数据进行更新。 结果就是，在 [**D3dDrawPrimitives2**](/windows-hardware/drivers/ddi/d3dhal/nc-d3dhal-lpd3dhal_drawprimitives2cb)等高频率调用期间必须执行较少的代码。

 

