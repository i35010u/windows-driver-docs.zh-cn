---
title: 指定 DMA 缓冲区的段
description: 指定 DMA 缓冲区的段
ms.assetid: 7cd51f22-bf9b-4c45-98f0-e9e0d41dab96
keywords:
- 内存段 WDK 显示，DMA 缓冲区
- DMA 缓冲 WDK 显示，内存段
- 缓冲 WDK 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ac518fe8cf2c9a09de7165469598a33dc638bf3c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72825714"
---
# <a name="specifying-segments-for-dma-buffers"></a>指定 DMA 缓冲区的段


## <span id="ddk_specifying_segments_for_dma_buffers_gg"></span><span id="DDK_SPECIFYING_SEGMENTS_FOR_DMA_BUFFERS_GG"></span>


显示微型端口驱动程序可以指定可从中分配 DMA 缓冲区的口径段。 DMA 缓冲区还可以作为连续的锁定系统内存分配。

当应用程序需要 DMA 缓冲区时，视频内存管理器会分配并销毁它们。 因此，视频内存管理器需要一组可以从中分配 DMA 缓冲区的段。 请注意，段集可能只包含一个段。

当 Microsoft DirectX 图形内核子系统调用显示微型端口驱动程序的[**DxgkDdiCreateDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_createdevice)函数来创建图形上下文设备时，显示微型端口驱动程序可以指定一个段集，视频内存管理器可以从中分配 DMA 缓冲区。 如果显示微型端口驱动程序将[**DXGK\_DEVICEINFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_deviceinfo)结构的**DmaBufferSegmentSet**成员设置为0，则视频内存管理器将为 DMA 缓冲区分配连续的非分页内存;在这种情况下，显示微型端口驱动程序必须通过使用 PCI 周期和 DMA 来访问内存，必须直接从内存的物理地址发送数据。 如果显示微型端口驱动程序将**DmaBufferSegmentSet**设置为非零值，则视频内存管理器将分配可分页内存，并将页映射到指定的口径段。 在对[**DxgkDdiSubmitCommand**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_submitcommand)函数的调用中，将在显示微型端口驱动程序中显示口径段内的页。

请注意，基本的视频内存管理器模型不支持本地视频内存中的 DMA 缓冲区。

 

 





