---
title: 在 Direct3D 中执行浮点运算
description: 在 Direct3D 中执行浮点运算
keywords:
- 浮点运算 WDK Direct3D
- Direct3D WDK Windows 2000 显示，浮点操作
- 回调函数 WDK Direct3D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7692d7d5afb80d20a1e05d262ba2be3d3492f6f8
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96834593"
---
# <a name="performing-floating-point-operations-in-direct3d"></a>在 Direct3D 中执行浮点运算


## <span id="ddk_performing_floating_point_operations_in_direct3d_gg"></span><span id="DDK_PERFORMING_FLOATING_POINT_OPERATIONS_IN_DIRECT3D_GG"></span>


DirectX 运行时在调用多个显示驱动程序的 Direct3D 回调函数时，保存并还原浮点状态。 但是，如在 [DirectDraw 中执行浮点运算](performing-floating-point-operations-in-directdraw.md)中所述，某些驱动程序的 Direct3D 回调函数必须在执行浮点运算之前保存浮点状态，并且在操作完成时必须还原浮点状态。

DirectX 运行时根据以下 Direct3D 回调函数的需要保存和还原浮点状态：

-   [**D3dContextCreate**](/windows-hardware/drivers/ddi/d3dhal/nc-d3dhal-lpd3dhal_contextcreatecb)

-   [**D3dContextDestroy**](/windows-hardware/drivers/ddi/d3dhal/nc-d3dhal-lpd3dhal_contextdestroycb)

-   [**D3dDrawPrimitives2**](/windows-hardware/drivers/ddi/d3dhal/nc-d3dhal-lpd3dhal_drawprimitives2cb)

-   [**D3dGetDriverState**](/windows/win32/api/ddrawint/nc-ddrawint-pdd_getdriverstate)

-   [**D3dValidateTextureStageState**](/windows-hardware/drivers/ddi/d3dhal/nc-d3dhal-lpd3dhal_validatetexturestagestatecb)

对于以下回调函数，Direct3D 支持的显示驱动程序必须在执行浮点运算之前保存浮点状态，并在操作完成时还原它：

-   [**D3dCreateSurfaceEx**](/windows/win32/api/ddrawint/nc-ddrawint-pdd_createsurfaceex)

-   [**D3dDestroyDDLocal**](/windows/win32/api/ddrawint/nc-ddrawint-pdd_destroyddlocal)

-   [D3DBuffer 回调](/windows-hardware/drivers/ddi/index)

有关浮点运算的详细信息，请参阅 [图形驱动程序函数中的浮点运算](floating-point-operations-in-graphics-driver-functions.md)。

 

