---
title: 在 Direct3D 中执行浮点运算
description: 在 Direct3D 中执行浮点运算
ms.assetid: 2da736cf-d062-4c5a-b9f5-6b35f199660f
keywords:
- 浮点运算 WDK Direct3D
- Direct3D WDK Windows 2000 显示，浮点运算
- 回调函数 WDK Direct3D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2b03562a8985692edeee5fd8c057cf72005a7126
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385584"
---
# <a name="performing-floating-point-operations-in-direct3d"></a>在 Direct3D 中执行浮点运算


## <span id="ddk_performing_floating_point_operations_in_direct3d_gg"></span><span id="DDK_PERFORMING_FLOATING_POINT_OPERATIONS_IN_DIRECT3D_GG"></span>


DirectX 运行时保存，并调用许多显示器驱动程序的 Direct3D 回调函数时还原浮点状态。 但是，如中所述[DirectDraw 中执行浮点操作](performing-floating-point-operations-in-directdraw.md)，某些驱动程序的 Direct3D 回调函数必须保存浮点状态在执行浮点操作之前，必须还原在操作完成时的浮点状态。

DirectX 运行时将保存并还原所需的以下 Direct3D 回调函数的浮点状态：

-   [**D3dContextCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dhal/nc-d3dhal-lpd3dhal_contextcreatecb)

-   [**D3dContextDestroy**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dhal/nc-d3dhal-lpd3dhal_contextdestroycb)

-   [**D3dDrawPrimitives2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dhal/nc-d3dhal-lpd3dhal_drawprimitives2cb)

-   [**D3dGetDriverState**](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_getdriverstate)

-   [**D3dValidateTextureStageState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dhal/nc-d3dhal-lpd3dhal_validatetexturestagestatecb)

对于以下的回调函数，Direct3D 支持显示器驱动程序必须在执行浮点运算之前保存浮点状态并将其还原操作完成后：

-   [**D3dCreateSurfaceEx**](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_createsurfaceex)

-   [**D3dDestroyDDLocal**](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_destroyddlocal)

-   [D3DBuffer 回调](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)

有关浮点运算的详细信息，请参阅[图形驱动程序函数中的浮点操作](floating-point-operations-in-graphics-driver-functions.md)。

 

 





