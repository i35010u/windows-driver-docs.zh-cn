---
title: 使用有保证的协定 DMA 缓冲区模型
description: 使用有保证的协定 DMA 缓冲区模型
ms.assetid: fee6f7eb-157b-466d-b482-110a48045283
keywords:
- DMA 缓冲区 WDK 显示，保证协定模式
- 保证 WDK 显示协定 DMA 缓冲区
- 修补程序位置列出 WDK 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d554145854979b80ac46425dd138998daa42d1dd
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67381071"
---
# <a name="using-the-guaranteed-contract-dma-buffer-model"></a>使用有保证的协定 DMA 缓冲区模型


Windows Vista 显示器驱动程序模型可保证 DMA 缓冲区的大小和修补程序位置用于渲染设备列表。

在保证的协定模式下，用户模式显示驱动程序是了解当用户模式显示驱动程序填充命令缓冲区并调用才可用于转换的 DMA 缓冲区和修补程序位置列表的确切大小[ **pfnRenderCb** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_rendercb)以将其提交到显示微型端口驱动程序。 每次调用后**pfnRenderCb**，用户模式显示驱动程序将收到适用于以下转换 DMA 缓冲区和修补程序位置列表的大小 (即，以下调用**pfnRenderCb**).

视频内存管理器保证不剪裁 DMA 缓冲区和修补程序位置列出了该设备，直到下一步转换完毕。 显示微型端口驱动程序必须能够转换为一个 DMA 缓冲区和一个修补程序位置列表中的一个命令缓冲区。 如果此转换不可能，用户模式命令缓冲区，根据定义，无效。 显示微型端口驱动程序不能返回指示 DMA 缓冲区空间不足和修补程序位置列出了转换; 过程状态因为这会导致视频内存管理器 bug 检查系统，因为内存管理器无法满足的有保证的 DMA 合同要求。

 

 





