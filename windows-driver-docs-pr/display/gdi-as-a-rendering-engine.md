---
title: 用作渲染引擎的 GDI
description: 用作渲染引擎的 GDI
ms.assetid: 3aae0c71-fc98-452c-a7a3-f20a790a466b
keywords:
- GDI WDK Windows 2000 显示，呈现引擎
- 图形驱动程序 WDK Windows 2000 显示，呈现引擎
- 绘制 WDK GDI，呈现引擎
- 渲染引擎 WDK GDI
- PDEV WDK GDI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5d065cce0a8e18cb0fea3115b39ecf3bc2b0cfaa
ms.sourcegitcommit: b84d760d4b45795be12e625db1d5a4167dc2c9ee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/17/2020
ms.locfileid: "90714752"
---
# <a name="gdi-as-a-rendering-engine"></a>用作渲染引擎的 GDI


## <span id="ddk_gdi_as_a_rendering_engine_gg"></span><span id="DDK_GDI_AS_A_RENDERING_ENGINE_GG"></span>


对于呈现操作，驱动程序必须首先为启用的每个*PDEV*结构启用一个*表面*。 PDEV 是物理设备的逻辑表示形式。 如果可以将硬件设置为 GDI 标准格式的位图，则可以使用 GDI 将部分或全部绘图用于位图图面。 GDI 还可以处理高级 [半色调](gdi-halftoning-capabilities.md)。

有关启用 *PDEVs* 和表面的信息，请参阅 [**DrvEnablePDEV**](/windows/win32/api/winddi/nf-winddi-drvenablepdev) 和 [**DrvEnableSurface**](/windows/win32/api/winddi/nf-winddi-drvenablesurface) 函数。

 

