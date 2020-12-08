---
title: 命令和 DMA 缓冲区简介
description: 命令和 DMA 缓冲区简介
keywords:
- 命令缓冲区 WDK 显示，关于命令缓冲区
- DMA 缓冲区 WDK 显示，关于 DMA 缓冲区
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d9b9d71d10dc70c24beaa0e4b4c7b95cf9b3a8e5
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96792313"
---
# <a name="introduction-to-command-and-dma-buffers"></a>命令和 DMA 缓冲区简介


## <span id="ddk_introduction_to_command_and_dma_buffers_gg"></span><span id="DDK_INTRODUCTION_TO_COMMAND_AND_DMA_BUFFERS_GG"></span>


命令和 DMA 缓冲区密切类似。 但用户模式显示驱动程序使用命令缓冲区，并且显示微型端口驱动程序使用 DMA 缓冲区。

命令缓冲区具有以下特征：

-   GPU 绝不会直接访问它。

-   硬件供应商控制格式。

-   它是从呈现应用程序的专用地址空间中的常规可分页内存中为用户模式显示驱动程序分配的。

DMA 缓冲区具有以下特征：

-   它基于命令缓冲区的已验证内容。

-   它由内核可分页内存中的显示微型端口驱动程序分配。

-   在 GPU 可以读取 DMA 缓冲区之前，显示微型端口驱动程序必须对 DMA 缓冲区进行页面锁定，并通过口径映射 DMA 缓冲区。

 

 





