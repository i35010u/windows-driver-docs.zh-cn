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
ms.openlocfilehash: 6c663cd0793db3060895807fbdea2945e9ecfdb0
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89067114"
---
# <a name="using-dxva-with-2d-operations"></a>使用 DXVA 执行 2D 操作


## <span id="ddk_using_dxva_with_2d_operations_gg"></span><span id="DDK_USING_DXVA_WITH_2D_OPERATIONS_GG"></span>


DirectX 9.0 和更高版本的驱动程序使用 D3DDP2OP \_ BLT 操作代码在 [DirectX 视频加速](directx-video-acceleration.md) (DXVA) 图面之间执行 blits。 因此，如果运行时检测到 DirectX 9.0 或更高版本的驱动程序，则运行时必须调用驱动程序的 [**D3dCreateSurfaceEx**](/windows/desktop/api/ddrawint/nc-ddrawint-pdd_createsurfaceex) 函数来创建任何 DXVA (或仅 2d) 图面。

 

