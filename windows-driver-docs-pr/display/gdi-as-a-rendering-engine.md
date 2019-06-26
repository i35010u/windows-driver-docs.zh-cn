---
title: 用作渲染引擎的 GDI
description: 用作渲染引擎的 GDI
ms.assetid: 3aae0c71-fc98-452c-a7a3-f20a790a466b
keywords:
- GDI WDK Windows 2000 显示，呈现引擎
- 图形驱动程序 WDK Windows 2000 显示，呈现引擎
- 绘制 WDK GDI，呈现引擎
- 呈现引擎 WDK GDI
- PDEV WDK GDI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 507c77f87ddd0e2852d1647ba0b1d0355b550ea6
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67375799"
---
# <a name="gdi-as-a-rendering-engine"></a>用作渲染引擎的 GDI


## <span id="ddk_gdi_as_a_rendering_engine_gg"></span><span id="DDK_GDI_AS_A_RENDERING_ENGINE_GG"></span>


对于呈现操作，该驱动程序必须首先启用*面*每个*PDEV*已启用的结构。 PDEV 是物理设备的逻辑表示形式。 如果硬件可设置为标准格式 GDI 位图，GDI 可以用于执行部分或全部绘制到的位图图面。 此外可以处理 GDI 高级[半色调](gdi-halftoning-capabilities.md)。

有关启用信息*PDEVs*和图面，是指[ **DrvEnablePDEV** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvenablepdev)并[ **DrvEnableSurface**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvenablesurface)函数。

 

 





