---
title: DMA 模型非本地显示内存的标志支持
description: DMA 模型非本地显示内存的标志支持
keywords:
- DMA 样式 AGP WDK DirectDraw
- 显示内存 WDK DirectDraw，DMA 样式 AGP
- 非本地显示内存 WDK DirectDraw，DMA 样式 AGP
- AGP WDK DirectDraw，DMA 样式 AGP
- 绘制 AGP 支持 WDK DirectDraw，DMA 样式 AGP
- DirectDraw AGP 支持 WDK Windows 2000 显示，DMA 样式 AGP
- 内存 WDK DirectDraw AGP、DMA 样式 AGP
- 标志 WDK DirectDraw 非本地内存
- DDCAPS2_NONLOCALVIDMEM
- DDCAPS2_NONLOCALVIDMEMCAPS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4251feb58043c864ac77381f3b8d99afb8fe206e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838077"
---
# <a name="flagging-support-for-dma-model-nonlocal-display-memory"></a>DMA 模型非本地显示内存的标志支持


## <span id="ddk_flagging_support_for_dma_model_nonlocal_display_memory_gg"></span><span id="DDK_FLAGGING_SUPPORT_FOR_DMA_MODEL_NONLOCAL_DISPLAY_MEMORY_GG"></span>


除了指定 DDCAPS2 \_ NONLOCALVIDMEM 标志来报告 AGP 支持外，DMA 模型驱动程序还必须导出功能标志 DDCAPS2 \_ NONLOCALVIDMEMCAPS。 此标志指示非本地 (AGP) 内存的功能与本地显示内存不同。

 

 





