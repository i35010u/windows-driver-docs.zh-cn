---
title: 修补 DMA 缓冲区
description: 修补 DMA 缓冲区
ms.assetid: 4d8a8a89-0617-4ab8-8609-37bbdb8999f0
keywords:
- DMA 缓冲区 WDK 显示修补
- 修补 WDK 显示 DMA 缓冲区
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dc4a5196bf04475a8f03795e0b7379f8f6d333e4
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63352398"
---
# <a name="patching-a-dma-buffer"></a>修补 DMA 缓冲区


## <span id="ddk_patching_a_dma_buffer_gg"></span><span id="DDK_PATCHING_A_DMA_BUFFER_GG"></span>


后的视频内存管理器将得到通知，其中每个 DMA 缓冲区的内存资源是位于，GPU 计划程序调用显示微型端口驱动程序[ **DxgkDdiPatch** ](https://msdn.microsoft.com/library/windows/hardware/ff559737)函数修补资源与物理地址 （即，将物理地址分配到资源）。

 

 





