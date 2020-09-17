---
title: 使用 DXVA 执行 2D 操作
description: 使用 DXVA 执行 2D 操作
ms.assetid: a864941d-69ac-48a4-85a2-7e05cd3c9617
keywords:
- 二维操作 WDK DirectX 9.0，DXVA
- 2D 操作 WDK DirectX 9.0，DXVA
- DXVA WDK DirectX 9。0
- DXVA WDK DirectX 9.0，2D 操作
- DirectX 视频加速 WDK DirectX 9。0
- DirectX 视频加速 WDK DirectX 9.0，2D 操作
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f111bf3a42474ecc2d6ff7558ca3cb575786e9c3
ms.sourcegitcommit: b84d760d4b45795be12e625db1d5a4167dc2c9ee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/17/2020
ms.locfileid: "90717574"
---
# <a name="using-dxva-with-2d-operations"></a>使用 DXVA 执行 2D 操作


## <span id="ddk_using_dxva_with_2d_operations_gg"></span><span id="DDK_USING_DXVA_WITH_2D_OPERATIONS_GG"></span>


DirectX 9.0 和更高版本的驱动程序使用 D3DDP2OP \_ BLT 操作代码在 [DirectX 视频加速](directx-video-acceleration.md) (DXVA) 图面之间执行 blits。 因此，如果运行时检测到 DirectX 9.0 或更高版本的驱动程序，则运行时必须调用驱动程序的 [**D3dCreateSurfaceEx**](/windows/win32/api/ddrawint/nc-ddrawint-pdd_createsurfaceex) 函数来创建任何 DXVA (或仅 2d) 图面。

 

