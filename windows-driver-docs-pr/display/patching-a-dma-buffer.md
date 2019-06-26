---
title: 修补 DMA 缓冲区
description: 修补 DMA 缓冲区
ms.assetid: 4d8a8a89-0617-4ab8-8609-37bbdb8999f0
keywords:
- DMA 缓冲区 WDK 显示修补
- 修补 WDK 显示 DMA 缓冲区
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 339587a7d528cea029b277c61a3a31b5f399b9db
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67377374"
---
# <a name="patching-a-dma-buffer"></a>修补 DMA 缓冲区


## <span id="ddk_patching_a_dma_buffer_gg"></span><span id="DDK_PATCHING_A_DMA_BUFFER_GG"></span>


后的视频内存管理器将得到通知，其中每个 DMA 缓冲区的内存资源是位于，GPU 计划程序调用显示微型端口驱动程序[ **DxgkDdiPatch** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_patch)函数修补资源与物理地址 （即，将物理地址分配到资源）。

 

 





