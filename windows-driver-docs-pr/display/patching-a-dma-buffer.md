---
title: 修补 DMA 缓冲区
description: 修补 DMA 缓冲区
ms.assetid: 4d8a8a89-0617-4ab8-8609-37bbdb8999f0
keywords:
- DMA 缓冲 WDK 显示，修补
- 修补 DMA 缓冲区 WDK 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0f71ff78483e7221df2230c3849b9cf36cd52253
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72829866"
---
# <a name="patching-a-dma-buffer"></a>修补 DMA 缓冲区


## <span id="ddk_patching_a_dma_buffer_gg"></span><span id="DDK_PATCHING_A_DMA_BUFFER_GG"></span>


在显示 DMA 缓冲区的每个内存资源的位置通知视频内存管理器后，GPU 计划程序将调用显示微型端口驱动程序的[**DxgkDdiPatch**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_patch)函数，以使用物理地址修补资源（即分配物理资源的地址）。

 

 





