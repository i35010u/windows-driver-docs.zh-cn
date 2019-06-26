---
title: 使用 DXVA 执行 2D 操作
description: 使用 DXVA 执行 2D 操作
ms.assetid: a864941d-69ac-48a4-85a2-7e05cd3c9617
keywords:
- 二维操作 WDK DirectX 9.0 DXVA
- 2D 操作 WDK DirectX 9.0 DXVA
- DXVA WDK DirectX 9.0
- DXVA WDK DirectX 9.0，2D 操作
- DirectX 视频加速 WDK DirectX 9.0
- DirectX 视频加速 WDK DirectX 9.0，2D 操作
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 384adf9817d63bc3ea9f8529cdff6a83c858337a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67370632"
---
# <a name="using-dxva-with-2d-operations"></a>使用 DXVA 执行 2D 操作


## <span id="ddk_using_dxva_with_2d_operations_gg"></span><span id="DDK_USING_DXVA_WITH_2D_OPERATIONS_GG"></span>


DirectX 9.0 和更高版本的驱动程序使用 D3DDP2OP\_BLT 操作代码来执行之间 blits [DirectX 视频加速](directx-video-acceleration.md)(DXVA) 图面。 因此，如果在运行时检测到 DirectX 9.0 或更高版本的驱动程序，运行时必须调用的驱动程序[ **D3dCreateSurfaceEx** ](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_createsurfaceex)函数来创建任何 DXVA （或仅限 2D） 图面。

 

 





