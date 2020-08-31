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
ms.openlocfilehash: a91637d51c90ff47d2d6040e139a0da7af086e1d
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89066600"
---
# <a name="specifying-memory-type-for-a-resource"></a>为资源指定内存类型


用户模式显示驱动程序接收有关在收到 [用于创建资源的请求](requesting-and-using-surface-memory.md)时应使用的内存类型的信息。 内存类型通过分别通过 D3DDDIPOOL \_ SYSTEMMEM 或 D3DDDIPOOL VIDEOMEMORY 枚举器指定为 \_ [**D3DDDIARG \_ CREATERESOURCE**](/windows-hardware/drivers/ddi/d3dukmdt/ns-d3dukmdt-_d3dddiarg_createresource)结构的**池**成员的系统或视频内存。 此外，Microsoft Direct3D 运行时通过在 **池中** 成员中指定以下枚举器之一，为驱动程序提供有关要使用的视频内存类型的提示：

-   D3DDDIPOOL \_ LOCALVIDMEM

    运行时建议驱动程序使用本地视频内存。

-   D3DDDIPOOL \_ NONLOCALVIDMEM

    运行时建议驱动程序使用非本地的视频内存 (例如，AGP 内存) 。

运行时向用户模式显示驱动程序提供提示以提高性能。 例如， \_ 如果 CPU 写入图面，则运行时可以指定 D3DDDIPOOL NONLOCALVIDMEM，这将使用非本地视频内存执行速度更快。

用户模式显示驱动程序通过特定于供应商的方式，通过[**D3DDDI \_ ALLOCATIONINFO**](/windows-hardware/drivers/ddi/d3dukmdt/ns-d3dukmdt-_d3dddi_allocationinfo)和[**DXGK \_ ALLOCATIONINFO**](/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_allocationinfo)结构的**pPrivateDriverData**成员将提示传递到显示微型端口驱动程序。 显示微型端口驱动程序通过从对**HintedSegmentId** \_ 驱动程序的[**DxgkDdiCreateAllocation**](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_createallocation)函数的调用返回 DXGK ALLOCATIONINFO 结构的 HintedSegmentId 成员中的段的标识符，向视频内存管理器指示要使用的适当内存段。

无论用于创建资源的视频内存的类型如何，用户模式显示驱动程序都不能向运行时公开任何语义差异。 也就是说，对于每个视频内存类型，驱动程序必须以相同的方式呈现信息，并且必须返回相同的返回值。

 

