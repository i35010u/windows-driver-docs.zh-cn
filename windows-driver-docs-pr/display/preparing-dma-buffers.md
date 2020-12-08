---
title: 准备 DMA 缓冲区
description: 准备 DMA 缓冲区
keywords:
- DMA 缓冲 WDK 显示，准备
- GPU 不能显示 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dca5ab8fcbf9c7e377280f00474057dc44fac73f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96833059"
---
# <a name="preparing-dma-buffers"></a>准备 DMA 缓冲区


## <span id="ddk_preparing_dma_buffers_gg"></span><span id="DDK_PREPARING_DMA_BUFFERS_GG"></span>


显示微型端口驱动程序必须及时准备 DMA 缓冲区。 当 GPU 处理 DMA 缓冲区时，通常会调用显示微型端口驱动程序来准备要提交到 GPU 的下一个 DMA 缓冲区。 为了防止 GPU 不足，显示微型端口驱动程序必须花费更少的时间来准备和提交后续 DMA 缓冲区，而不是 GPU 处理当前 DMA 缓冲区所需的时间。

 

 





