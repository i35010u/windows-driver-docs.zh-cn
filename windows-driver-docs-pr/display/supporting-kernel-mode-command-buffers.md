---
title: 支持的内核模式命令缓冲区
description: 支持的内核模式命令缓冲区
ms.assetid: c61a39b3-6fd6-461f-a68f-450ccd705f6f
keywords:
- 命令缓冲区 WDK 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c2c29abcb6910e02ac507bf8bc07b540a3b9d330
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56544297"
---
# <a name="supporting-kernel-mode-command-buffers"></a>支持的内核模式命令缓冲区


## <span id="ddk_introduction_to_command_and_dma_buffers_gg"></span><span id="DDK_INTRODUCTION_TO_COMMAND_AND_DMA_BUFFERS_GG"></span>


显示微型端口驱动程序应在提交中的调用的响应的命令缓冲区[ **DxgkDdiRenderKm** ](https://msdn.microsoft.com/library/windows/hardware/ff559800)函数中所述[提交命令缓冲区](submitting-a-command-buffer.md)。

可以使用该驱动程序**MultipassOffset**的成员[ **DXGKARG\_呈现**](https://msdn.microsoft.com/library/windows/hardware/ff557648)结构来跟踪输入的命令缓冲区处理的进度。 例如，显示微型端口驱动程序可以使用高 16 位为最后一个处理的命令和低 16 位的偏移量来跟踪命令的处理。

 

 





