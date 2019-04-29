---
title: 命令和 DMA 缓冲区简介
description: 命令和 DMA 缓冲区简介
ms.assetid: e9fa38a2-3243-4578-83c3-4559ec3480a7
keywords:
- 命令缓冲区 WDK 显示有关命令缓冲区
- DMA 缓冲区 WDK 显示，DMA 缓冲区
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6b6eece19903448d2f59e43222c5fe3ee77359cb
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63362147"
---
# <a name="introduction-to-command-and-dma-buffers"></a>命令和 DMA 缓冲区简介


## <span id="ddk_introduction_to_command_and_dma_buffers_gg"></span><span id="DDK_INTRODUCTION_TO_COMMAND_AND_DMA_BUFFERS_GG"></span>


命令和 DMA 缓冲区非常类似于彼此。 但是，命令缓冲区可供用户模式显示驱动程序，并且显示微型端口驱动程序使用 DMA 缓冲区。

命令缓冲区具有以下特征：

-   通过 GPU 永远不会直接访问它。

-   硬件供应商控制的格式。

-   它被分配给用户模式显示驱动程序从呈现应用程序的专用地址空间中的正则可分页内存。

DMA 缓冲区具有以下特征：

-   它基于经过验证的命令缓冲区内容。

-   它会显示微型端口驱动程序从内核可分页内存分配。

-   GPU 可以读取从 DMA 缓冲区之前，显示微型端口驱动程序必须页锁 DMA 缓冲区，并将映射通过 aperture DMA 缓冲区。

 

 





