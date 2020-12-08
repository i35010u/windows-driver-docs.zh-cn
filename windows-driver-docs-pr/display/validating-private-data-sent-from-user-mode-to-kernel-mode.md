---
title: 验证从用户模式发送到内核模式的专用数据
description: 验证从用户模式发送到内核模式的专用数据
keywords:
- 验证专用数据 WDK 显示
- 专用数据验证 WDK 显示
- 专用数据 WDK 显示无效
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a77024d0a4b1a6b035160ba34b9afca50a3bb7ac
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96830065"
---
# <a name="validating-private-data-sent-from-user-mode-to-kernel-mode"></a>验证从用户模式发送到内核模式的专用数据


显示微型端口驱动程序必须验证所有从用户模式显示驱动程序发送的专用数据，以防微型端口驱动程序崩溃，无需响应 (挂起) 、断言或在专用数据无效时损坏内存。 但是，因为操作系统重置了 "挂起" 的硬件，所以显示微型端口驱动程序可以将指令发送到图形处理单元 (GPU) 导致 GPU "挂起"。 专用数据可以包含以下任何项：

-   发送给微型端口驱动程序的 [**DxgkDdiRender**](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_render)或 [**DxgkDdiRenderKm**](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_renderkm)函数的命令缓冲区内容 [**DXGKARG \_ 呈现**](/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgkarg_render)结构的 **pCommand** 缓冲区成员。

-   发送到以下微型端口驱动程序函数的数据：
    -   [**DXGKARG \_ CREATEALLOCATION**](/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgkarg_createallocation)和 [**DXGK \_ ALLOCATIONINFO**](/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_allocationinfo)结构的 **pPrivateDriverData** 缓冲区成员中的 [**DxgkDdiCreateAllocation**](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_createallocation)函数。
    -   [**DXGKARG \_ 转义**](/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgkarg_escape)结构的 **pPrivateDriverData** 缓冲区成员中的 [**DxgkDdiEscape**](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_escape)函数。
    -   [**DXGKARG \_ ACQUIRESWIZZLINGRANGE**](/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgkarg_acquireswizzlingrange)结构的 **PrivateDriverData** 32 位成员中的 [**DxgkDdiAcquireSwizzlingRange**](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_acquireswizzlingrange)函数。
    -   [**DXGKARG \_ RELEASESWIZZLINGRANGE**](/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgkarg_releaseswizzlingrange)结构的 **PrivateDriverData** 32 位成员中的 [**DxgkDdiReleaseSwizzlingRange**](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_releaseswizzlingrange)函数。
    -   当 [**DxgkDdiQueryAdapterInfo**](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_queryadapterinfo)在类型成员中指定 DXGKQAITYPE UMDRIVERPRIVATE 值时， [**DXGKARG \_ QUERYADAPTERINFO**](/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgkarg_queryadapterinfo)结构的 **pInputData** 缓冲区成员中的 DxgkDdiQueryAdapterInfo 函数 \_ 。 **Type**

 

