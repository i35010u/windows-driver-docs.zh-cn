---
title: 修补 DMA 缓冲区
description: 修补 DMA 缓冲区
keywords:
- DMA 缓冲 WDK 显示，修补
- 修补 DMA 缓冲区 WDK 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1bc14f7c33affb6e2bc1892c006744a54c4a5a6e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96798271"
---
# <a name="patching-a-dma-buffer"></a>修补 DMA 缓冲区


## <span id="ddk_patching_a_dma_buffer_gg"></span><span id="DDK_PATCHING_A_DMA_BUFFER_GG"></span>


在显示 DMA 缓冲区的每个内存资源的位置通知视频内存管理器后，GPU 计划程序将调用显示微型端口驱动程序的 [**DxgkDdiPatch**](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_patch) 函数，以使用物理地址来修补资源 (即，为资源) 分配物理地址。

 

