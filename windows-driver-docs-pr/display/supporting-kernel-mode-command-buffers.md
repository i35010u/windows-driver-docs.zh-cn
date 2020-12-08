---
title: 支持内核模式命令缓冲区
description: 支持内核模式命令缓冲区
keywords:
- 命令缓冲区 WDK 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3b108931dc671aaaea7fd873c4bf1d70e343b813
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96793846"
---
# <a name="supporting-kernel-mode-command-buffers"></a>支持内核模式命令缓冲区


## <span id="ddk_introduction_to_command_and_dma_buffers_gg"></span><span id="DDK_INTRODUCTION_TO_COMMAND_AND_DMA_BUFFERS_GG"></span>


如 [提交命令缓冲区](submitting-a-command-buffer.md)中所述，显示微型端口驱动程序应提交一个命令缓冲区来响应对 [**DxgkDdiRenderKm**](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_renderkm)函数的调用。

驱动程序可以使用 [**DXGKARG \_ 呈现**](/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgkarg_render)结构的 **MultipassOffset** 成员跟踪输入命令缓冲区处理的进度。 例如，显示微型端口驱动程序可以使用高16位作为上次处理的命令的偏移量，使用低16位来跟踪命令的处理。

 

