---
title: 支持内核模式命令缓冲区
description: 支持内核模式命令缓冲区
ms.assetid: c61a39b3-6fd6-461f-a68f-450ccd705f6f
keywords:
- 命令缓冲区 WDK 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f7f37252c5cfc51bd6d728f1858bc6f2a988f1a7
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67375788"
---
# <a name="supporting-kernel-mode-command-buffers"></a>支持内核模式命令缓冲区


## <span id="ddk_introduction_to_command_and_dma_buffers_gg"></span><span id="DDK_INTRODUCTION_TO_COMMAND_AND_DMA_BUFFERS_GG"></span>


显示微型端口驱动程序应在提交中的调用的响应的命令缓冲区[ **DxgkDdiRenderKm** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_renderkm)函数中所述[提交命令缓冲区](submitting-a-command-buffer.md)。

可以使用该驱动程序**MultipassOffset**的成员[ **DXGKARG\_呈现**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgkarg_render)结构来跟踪输入的命令缓冲区处理的进度。 例如，显示微型端口驱动程序可以使用高 16 位为最后一个处理的命令和低 16 位的偏移量来跟踪命令的处理。

 

 





