---
title: DMA 模型非本地显示内存的标志支持
description: DMA 模型非本地显示内存的标志支持
ms.assetid: 7310bf92-a1bb-4a72-8e1a-bae7e656a499
keywords:
- DMA 样式 AGP WDK DirectDraw
- 显示内存 WDK DirectDraw DMA 样式 AGP
- 非本地显示内存 WDK DirectDraw DMA 样式 AGP
- AGP WDK DirectDraw，DMA 样式 AGP
- 绘制 AGP 支持 WDK DirectDraw DMA 样式 AGP
- DirectDraw AGP 支持 WDK Windows 2000 显示，DMA 样式 AGP
- 内存 WDK DirectDraw AGP DMA 样式 AGP
- 标志 WDK DirectDraw 非本地内存
- DDCAPS2_NONLOCALVIDMEM
- DDCAPS2_NONLOCALVIDMEMCAPS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 014f96f31bff351ab66ba6e6464362c47f6d9474
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56567321"
---
# <a name="flagging-support-for-dma-model-nonlocal-display-memory"></a>DMA 模型非本地显示内存的标志支持


## <span id="ddk_flagging_support_for_dma_model_nonlocal_display_memory_gg"></span><span id="DDK_FLAGGING_SUPPORT_FOR_DMA_MODEL_NONLOCAL_DISPLAY_MEMORY_GG"></span>


除了指定 DDCAPS2\_NONLOCALVIDMEM 标志来报告 AGP 支持，DMA 模型驱动程序必须导出功能标志 DDCAPS2\_NONLOCALVIDMEMCAPS。 此标志指示非本地 (AGP) 内存具有不同的功能比本地显示内存。

 

 





