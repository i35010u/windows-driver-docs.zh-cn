---
title: 在 Direct3D 中执行浮点运算
description: 在 Direct3D 中执行浮点运算
ms.assetid: 2da736cf-d062-4c5a-b9f5-6b35f199660f
keywords:
- 浮点运算 WDK Direct3D
- Direct3D WDK Windows 2000 显示，浮点操作
- 回调函数 WDK Direct3D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: db2831bbcc0b39193a3e496b07ecdec2bd0810b4
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72829808"
---
# <a name="performing-floating-point-operations-in-direct3d"></a>在 Direct3D 中执行浮点运算


## <span id="ddk_performing_floating_point_operations_in_direct3d_gg"></span><span id="DDK_PERFORMING_FLOATING_POINT_OPERATIONS_IN_DIRECT3D_GG"></span>


DirectX 运行时在调用多个显示驱动程序的 Direct3D 回调函数时，保存并还原浮点状态。 但是，如在[DirectDraw 中执行浮点运算](performing-floating-point-operations-in-directdraw.md)中所述，某些驱动程序的 Direct3D 回调函数必须先保存浮点状态，然后才能执行浮点运算，并且必须在操作完成。

DirectX 运行时根据以下 Direct3D 回调函数的需要保存和还原浮点状态：

-   [**D3dContextCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/nc-d3dhal-lpd3dhal_contextcreatecb)

-   [**D3dContextDestroy**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/nc-d3dhal-lpd3dhal_contextdestroycb)

-   [**D3dDrawPrimitives2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/nc-d3dhal-lpd3dhal_drawprimitives2cb)

-   [**D3dGetDriverState**](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_getdriverstate)

-   [**D3dValidateTextureStageState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/nc-d3dhal-lpd3dhal_validatetexturestagestatecb)

对于以下回调函数，Direct3D 支持的显示驱动程序必须在执行浮点运算之前保存浮点状态，并在操作完成时还原它：

-   [**D3dCreateSurfaceEx**](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_createsurfaceex)

-   [**D3dDestroyDDLocal**](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_destroyddlocal)

-   [D3DBuffer 回调](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)

有关浮点运算的详细信息，请参阅[图形驱动程序函数中的浮点运算](floating-point-operations-in-graphics-driver-functions.md)。

 

 





