---
title: 准备 DMA 缓冲区
description: 准备 DMA 缓冲区
ms.assetid: 9231badb-7b42-46d1-95f6-34c0ec7ab3cb
keywords:
- DMA 缓冲区 WDK 显示准备
- GPU 资源不足 WDK 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 051cec0f0fd66b39e8c3306f08934528c54574fe
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63383925"
---
# <a name="preparing-dma-buffers"></a>准备 DMA 缓冲区


## <span id="ddk_preparing_dma_buffers_gg"></span><span id="DDK_PREPARING_DMA_BUFFERS_GG"></span>


显示微型端口驱动程序必须及时地准备 DMA 缓冲区。 GPU 处理 DMA 缓冲区，而显示微型端口驱动程序通常称为后准备的下一步的 DMA 缓冲区以提交到 GPU。 若要防止 GPU 资源不足，显示微型端口驱动程序必须花费更少的时间准备和提交后续 DMA 缓冲区不是 GPU 处理所需的当前 DMA 缓冲区。

 

 





