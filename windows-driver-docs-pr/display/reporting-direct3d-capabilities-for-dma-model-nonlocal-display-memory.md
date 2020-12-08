---
title: 报告非本地显示内存的 Direct3D 功能
description: DMA 模型驱动程序必须为非本地显示内存图面导出 Direct3D 功能。
keywords:
- DMA 样式 AGP WDK DirectDraw
- 显示内存 WDK DirectDraw，DMA 样式 AGP
- 非本地显示内存 WDK DirectDraw，DMA 样式 AGP
- AGP WDK DirectDraw，DMA 样式 AGP
- 绘制 AGP 支持 WDK DirectDraw，DMA 样式 AGP
- DirectDraw AGP 支持 WDK Windows 2000 显示，DMA 样式 AGP
- 内存 WDK DirectDraw AGP、DMA 样式 AGP
- 报表 Direct3D 功能
ms.date: 12/06/2018
ms.localizationpriority: medium
ms.custom: seodec18
ms.openlocfilehash: bd2bd9a153cf3c2f574e8f01b179d9e53c4f3932
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96783965"
---
# <a name="reporting-direct3d-capabilities-for-nonlocal-display-memory"></a>报告非本地显示内存的 Direct3D 功能

DMA 模型驱动程序还必须为非本地显示内存图面导出 Direct3D 功能。 这比报告 DirectDraw 功能要简单得多。 受影响的唯一功能是 D3DDEVCAPS \_ TEXTURENONLOCALVIDEOMEMORY。 如果导出 DMA 模型的显示卡可以直接从非本地显示内存中纹理，则应在其 Direct3D 设备说明中设置此功能。 如果不能，并且应用程序必须在执行纹理前将非本地显示内存图面显式加载或 blt 到本地显示内存表面，则不应设置此功能。 为了完整起见，执行模型驱动程序应始终设置此功能位。

 

 





