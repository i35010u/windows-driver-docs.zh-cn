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
ms.openlocfilehash: 6ba445fc94bab92226137cc6da200d6eec4bbee0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56555938"
---
# <a name="specifying-memory-type-for-a-resource"></a>为资源指定内存类型


用户模式显示驱动程序将收到在接收时应使用的内存类型有关的信息[创建资源的请求](requesting-and-using-surface-memory.md)。 内存类型指定为系统或视频内存通过 D3DDDIPOOL\_SYSTEMMEM 或 D3DDDIPOOL\_VIDEOMEMORY 枚举器，分别**池**的成员[ **D3DDDIARG\_CREATERESOURCE** ](https://msdn.microsoft.com/library/windows/hardware/ff542963)结构。 此外，Microsoft Direct3D 运行时提供对有关类型的视频内存，以通过指定一个以下枚举器中使用的驱动程序的提示**池**成员：

-   D3DDDIPOOL\_LOCALVIDMEM

    在运行时建议的驱动程序使用本地视频内存。

-   D3DDDIPOOL\_NONLOCALVIDMEM

    在运行时建议的驱动程序使用非本地视频内存 （例如，AGP 内存）。

运行时提供对用户模式下的提示，显示驱动程序以提高性能。 例如，运行时可能会指定 D3DDDIPOOL\_NONLOCALVIDMEM 如果 CPU 写入面上，使用非本地的视频内存更快地执行。

用户模式显示驱动程序将提示传递给显示微型端口驱动程序通过**pPrivateDriverData**的成员[ **D3DDDI\_ALLOCATIONINFO** ](https://msdn.microsoft.com/library/windows/hardware/ff544364)并[ **DXGK\_ALLOCATIONINFO** ](https://msdn.microsoft.com/library/windows/hardware/ff560960)特定于供应商的方式。 显示微型端口驱动程序的视频内存管理器指示要通过返回中的段的标识符使用的适当的内存段**HintedSegmentId** DXGK 成员\_ALLOCATIONINFO 结构从驱动程序的调用[ **DxgkDdiCreateAllocation** ](https://msdn.microsoft.com/library/windows/hardware/ff559606)函数。

而不考虑用于创建该资源的视频内存的类型，用户模式显示驱动程序必须公开给运行时任何语义差异。 也就是说，对于每个视频内存类型，驱动程序必须具有相同呈现的信息，必须返回相同的返回值。

 

 





