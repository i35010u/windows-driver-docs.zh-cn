---
title: 提供围栏标识符
description: 提供围栏标识符
ms.assetid: 0ec8a4eb-c441-47ae-b5de-d86e6065ffd4
keywords:
- fence 标识符 WDK 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5e9a60919c4ef9e6e3d1797c4120df0418998dcd
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67383082"
---
# <a name="supplying-fence-identifiers"></a>提供围栏标识符


Microsoft DirectX 图形内核子系统提供中的相同 fence 标识符**SubmissionFenceId**的成员[ **DXGKARG\_修补**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgkarg_patch)并[ **DXGKARG\_SUBMITCOMMAND** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgkarg_submitcommand)显示微型端口驱动程序的调用中的结构[ **DxgkDdiPatch**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_patch)并[ **DxgkDdiSubmitCommand** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_submitcommand)函数。 具体取决于图形硬件的实现方式，驱动程序仅使用需要传递到其中任何一个的 fence 标识符*DxgkDdiPatch*或*DxgkDdiSubmitCommand*函数由于以下原因：

-   驱动程序使用传递给 fence 标识符*DxgkDdiPatch*将写入直接内存访问 (DMA) 缓冲区的末尾。

-   驱动程序使用传递给 fence 标识符*DxgkDdiSubmitCommand*将环形缓冲区，即其中 DMA 缓冲区将排队等待执行的图形处理单元 (GPU) （大多数 GPU 类型使用 DMA 缓冲区的缓冲区写入队列的模型）。

 

 





