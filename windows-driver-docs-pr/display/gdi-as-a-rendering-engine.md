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
ms.openlocfilehash: e6fc967c97d4018a11659f407e487ba0711d9974
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89065850"
---
# <a name="gdi-as-a-rendering-engine"></a>用作渲染引擎的 GDI


## <span id="ddk_gdi_as_a_rendering_engine_gg"></span><span id="DDK_GDI_AS_A_RENDERING_ENGINE_GG"></span>


对于呈现操作，驱动程序必须首先为启用的每个*PDEV*结构启用一个*表面*。 PDEV 是物理设备的逻辑表示形式。 如果可以将硬件设置为 GDI 标准格式的位图，则可以使用 GDI 将部分或全部绘图用于位图图面。 GDI 还可以处理高级 [半色调](gdi-halftoning-capabilities.md)。

有关启用 *PDEVs* 和表面的信息，请参阅 [**DrvEnablePDEV**](/windows/desktop/api/winddi/nf-winddi-drvenablepdev) 和 [**DrvEnableSurface**](/windows/desktop/api/winddi/nf-winddi-drvenablesurface) 函数。

 

