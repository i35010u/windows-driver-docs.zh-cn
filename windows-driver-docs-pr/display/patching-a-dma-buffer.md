---
title: 修补 DMA 缓冲区
description: 修补 DMA 缓冲区
ms.assetid: 4d8a8a89-0617-4ab8-8609-37bbdb8999f0
keywords:
- DMA 缓冲 WDK 显示，修补
- 修补 DMA 缓冲区 WDK 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2666a5700bc755075c90c383d070b56903e6de16
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89064682"
---
# <a name="patching-a-dma-buffer"></a>修补 DMA 缓冲区


## <span id="ddk_patching_a_dma_buffer_gg"></span><span id="DDK_PATCHING_A_DMA_BUFFER_GG"></span>


在显示 DMA 缓冲区的每个内存资源的位置通知视频内存管理器后，GPU 计划程序将调用显示微型端口驱动程序的 [**DxgkDdiPatch**](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_patch) 函数，以使用物理地址来修补资源 (即，为资源) 分配物理地址。

 

