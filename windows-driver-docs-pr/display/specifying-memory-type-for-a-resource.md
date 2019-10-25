---
title: 为资源指定内存类型
description: 为资源指定内存类型
ms.assetid: b4691de0-d3c9-4a6f-a9f4-aafb22ea3e97
keywords:
- 视频内存类型 WDK 显示
- 内存类型 WDK 显示
- 资源内存类型 WDK 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4e2fe99adf82eb1cea8fe4bb24bcc00f60297f65
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72825719"
---
# <a name="specifying-memory-type-for-a-resource"></a>为资源指定内存类型


用户模式显示驱动程序接收有关在收到[用于创建资源的请求](requesting-and-using-surface-memory.md)时应使用的内存类型的信息。 内存类型通过 D3DDDIPOOL\_SYSTEMMEM 或 D3DDDIPOOL\_VIDEOMEMORY 枚举器分别指定为[**D3DDDIARG\_CREATERESOURCE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dukmdt/ns-d3dukmdt-_d3dddiarg_createresource)结构的**池**成员的系统或视频内存. 此外，Microsoft Direct3D 运行时通过在**池中**成员中指定以下枚举器之一，为驱动程序提供有关要使用的视频内存类型的提示：

-   D3DDDIPOOL\_LOCALVIDMEM

    运行时建议驱动程序使用本地视频内存。

-   D3DDDIPOOL\_NONLOCALVIDMEM

    运行时建议驱动程序使用非本地视频内存（例如，AGP 内存）。

运行时向用户模式显示驱动程序提供提示以提高性能。 例如，如果 CPU 写入图面，则运行时可以指定 D3DDDIPOOL\_NONLOCALVIDMEM，这将使用非本地视频内存执行速度更快。

用户模式显示驱动程序通过特定于供应商的方式，通过[**D3DDDI\_ALLOCATIONINFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dukmdt/ns-d3dukmdt-_d3dddi_allocationinfo)和[**DXGK\_ALLOCATIONINFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_allocationinfo)结构的**pPrivateDriverData**成员将提示传递到显示微型端口驱动程序。 显示微型端口驱动程序通过从对驱动程序的调用返回 DXGK\_ALLOCATIONINFO 结构的**HintedSegmentId**成员中的段的标识符，向视频内存管理器指示要使用的适当内存段[**DxgkDdiCreateAllocation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_createallocation)函数。

无论用于创建资源的视频内存的类型如何，用户模式显示驱动程序都不能向运行时公开任何语义差异。 也就是说，对于每个视频内存类型，驱动程序必须以相同的方式呈现信息，并且必须返回相同的返回值。

 

 





