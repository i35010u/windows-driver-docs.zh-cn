---
title: 报告非本地显示内存的 Direct3D 功能
description: DMA 模型驱动程序必须导出非本地显示内存曲面的 Direct3D 功能。
ms.assetid: aa1b08c0-b212-48b6-a450-78d36951db80
keywords:
- DMA 样式 AGP WDK DirectDraw
- 显示内存 WDK DirectDraw DMA 样式 AGP
- 非本地显示内存 WDK DirectDraw DMA 样式 AGP
- AGP WDK DirectDraw，DMA 样式 AGP
- 绘制 AGP 支持 WDK DirectDraw DMA 样式 AGP
- DirectDraw AGP 支持 WDK Windows 2000 显示，DMA 样式 AGP
- 内存 WDK DirectDraw AGP DMA 样式 AGP
- Direct3D 的报告功能
ms.date: 12/06/2018
ms.localizationpriority: medium
ms.custom: seodec18
ms.openlocfilehash: 0b10858642009f8fd724675e786a09a82f968c83
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56577346"
---
# <a name="reporting-direct3d-capabilities-for-nonlocal-display-memory"></a>报告非本地显示内存的 Direct3D 功能

DMA 模型驱动程序还将导出的 Direct3D 功能对于非本地显示内存图面。 这是比报告 DirectDraw 功能极大地简化。 受影响的唯一功能是 D3DDEVCAPS\_TEXTURENONLOCALVIDEOMEMORY。 如果显示卡导出 DMA 模型可以直接从非本地显示内存纹理，它应在其 Direct3D 设备描述设置此功能。 如果不能和应用程序必须显式加载或 blt 非本地内存面向显示本地显示内存图面执行纹理之前，它不应设置此功能。 出于完整性的考虑，execute 模型驱动程序应始终设置此功能位。

 

 





