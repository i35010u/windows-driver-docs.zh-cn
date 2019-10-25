---
title: 支持内核模式命令缓冲区
description: 支持内核模式命令缓冲区
ms.assetid: c61a39b3-6fd6-461f-a68f-450ccd705f6f
keywords:
- 命令缓冲区 WDK 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fb0bfd9ac620280c54475d1f0f4091996f3b8d78
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72825612"
---
# <a name="supporting-kernel-mode-command-buffers"></a>支持内核模式命令缓冲区


## <span id="ddk_introduction_to_command_and_dma_buffers_gg"></span><span id="DDK_INTRODUCTION_TO_COMMAND_AND_DMA_BUFFERS_GG"></span>


如[提交命令缓冲区](submitting-a-command-buffer.md)中所述，显示微型端口驱动程序应提交一个命令缓冲区来响应对[**DxgkDdiRenderKm**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_renderkm)函数的调用。

驱动程序可以使用[**DXGKARG\_呈现**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgkarg_render)结构的**MultipassOffset**成员跟踪输入命令缓冲区处理的进度。 例如，显示微型端口驱动程序可以使用高16位作为上次处理的命令的偏移量，使用低16位来跟踪命令的处理。

 

 





