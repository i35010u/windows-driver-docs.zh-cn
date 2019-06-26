---
title: 验证从用户模式发送到内核模式的专用数据
description: 验证从用户模式发送到内核模式的专用数据
ms.assetid: 7022af7b-80e7-41a5-bd53-32d7eafc4062
keywords:
- 验证显示 WDK 的专用数据
- 私有数据验证 WDK 显示
- 无效的专用数据 WDK 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: df699cc66135a029553fe0c0fd690fecbdd40157
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67374360"
---
# <a name="validating-private-data-sent-from-user-mode-to-kernel-mode"></a>验证从用户模式发送到内核模式的专用数据


显示微型端口驱动程序必须验证发送的所有专用数据从用户模式显示驱动程序以防止发生故障，微型端口驱动程序未响应 （挂起） 断言，或如果是无效的私有数据损坏内存。 但是，因为操作系统将重置"挂起"的硬件，显示微型端口驱动程序可以将指令发送到图形处理单元 (GPU)，导致 GPU"挂起"。 私有数据可以包括任何以下各项：

-   命令发送到微型端口驱动程序的缓冲区内容[ **DxgkDdiRender** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_render)或[ **DxgkDdiRenderKm** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_renderkm)中函数**pCommand**缓冲区隶属[ **DXGKARG\_呈现**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgkarg_render)结构。

-   数据发送到以下的微型端口驱动程序函数：
    -   [ **DxgkDdiCreateAllocation** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_createallocation)函数，在**pPrivateDriverData**缓冲的成员[ **DXGKARG\_CREATEALLOCATION** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgkarg_createallocation)并[ **DXGK\_ALLOCATIONINFO** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_allocationinfo)结构。
    -   [ **DxgkDdiEscape** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_escape)函数，在**pPrivateDriverData**缓冲区隶属[ **DXGKARG\_转义**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgkarg_escape)结构。
    -   [ **DxgkDdiAcquireSwizzlingRange** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_acquireswizzlingrange)函数，在**PrivateDriverData**的 32 位成员[ **DXGKARG\_ACQUIRESWIZZLINGRANGE** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgkarg_acquireswizzlingrange)结构。
    -   [ **DxgkDdiReleaseSwizzlingRange** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_releaseswizzlingrange)函数，在**PrivateDriverData**的 32 位成员[ **DXGKARG\_RELEASESWIZZLINGRANGE** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgkarg_releaseswizzlingrange)结构。
    -   [ **DxgkDdiQueryAdapterInfo** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_queryadapterinfo)函数，在**pInputData**缓冲区隶属[ **DXGKARG\_QUERYADAPTERINFO** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgkarg_queryadapterinfo)结构时 DXGKQAITYPE\_中指定 UMDRIVERPRIVATE 值**类型**成员。

 

 





