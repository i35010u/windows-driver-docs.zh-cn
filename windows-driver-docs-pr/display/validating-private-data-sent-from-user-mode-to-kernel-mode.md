---
title: 验证从用户模式发送到内核模式的专用数据
description: 验证从用户模式发送到内核模式的专用数据
ms.assetid: 7022af7b-80e7-41a5-bd53-32d7eafc4062
keywords:
- 验证专用数据 WDK 显示
- 专用数据验证 WDK 显示
- 专用数据 WDK 显示无效
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 358c78073b9debafad01fb867c2fdfbf47cd0424
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72829225"
---
# <a name="validating-private-data-sent-from-user-mode-to-kernel-mode"></a>验证从用户模式发送到内核模式的专用数据


显示微型端口驱动程序必须验证所有从用户模式显示驱动程序发送的专用数据，以防微型端口驱动程序崩溃、无响应（挂起）、断言或在专用数据无效时损坏内存。 但是，因为操作系统重置了 "挂起" 的硬件，所以显示微型端口驱动程序可以将指令发送到导致 GPU "挂起" 的图形处理单元（GPU）。 专用数据可以包含以下任何项：

-   发送给微型端口驱动程序的[**DxgkDdiRender**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_render)或[**DxgkDdiRenderKm**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_renderkm)函数的命令缓冲区内容在[**DXGKARG\_呈现**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgkarg_render)结构的**pCommand**缓冲区成员中。

-   发送到以下微型端口驱动程序函数的数据：
    -   [**DXGKARG\_CREATEALLOCATION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgkarg_createallocation)和[**DXGK\_ALLOCATIONINFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_allocationinfo)结构的**PPrivateDriverData**缓冲区成员中的[**DxgkDdiCreateAllocation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_createallocation)函数。
    -   [**DXGKARG\_转义**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgkarg_escape)结构的**pPrivateDriverData**缓冲区成员中的[**DxgkDdiEscape**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_escape)函数。
    -   [**DXGKARG\_ACQUIRESWIZZLINGRANGE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgkarg_acquireswizzlingrange)结构的**PrivateDriverData** 32 位成员中的[**DxgkDdiAcquireSwizzlingRange**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_acquireswizzlingrange)函数。
    -   [**DXGKARG\_RELEASESWIZZLINGRANGE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgkarg_releaseswizzlingrange)结构的**PrivateDriverData** 32 位成员中的[**DxgkDdiReleaseSwizzlingRange**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_releaseswizzlingrange)函数。
    -   当在**类型**成员中指定 DXGKQAITYPE\_UMDRIVERPRIVATE 值时， [**DXGKARG\_QUERYADAPTERINFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgkarg_queryadapterinfo)结构的**PInputData**缓冲区成员中的[**DxgkDdiQueryAdapterInfo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_queryadapterinfo)函数。

 

 





