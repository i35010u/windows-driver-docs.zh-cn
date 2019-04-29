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
ms.openlocfilehash: dbf083f8908300663aa77e6ee4f5804229437812
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63389079"
---
# <a name="using-dxva-with-2d-operations"></a>使用 DXVA 执行 2D 操作


## <span id="ddk_using_dxva_with_2d_operations_gg"></span><span id="DDK_USING_DXVA_WITH_2D_OPERATIONS_GG"></span>


DirectX 9.0 和更高版本的驱动程序使用 D3DDP2OP\_BLT 操作代码来执行之间 blits [DirectX 视频加速](directx-video-acceleration.md)(DXVA) 图面。 因此，如果在运行时检测到 DirectX 9.0 或更高版本的驱动程序，运行时必须调用的驱动程序[ **D3dCreateSurfaceEx** ](https://msdn.microsoft.com/library/windows/hardware/ff542840)函数来创建任何 DXVA （或仅限 2D） 图面。

 

 





