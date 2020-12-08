---
title: 提供围栏标识符
description: 提供围栏标识符
keywords:
- 围栏标识符 WDK 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b604de5dceb3520c6989af2e0a9f2310a47f3647
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96790657"
---
# <a name="supplying-fence-identifiers"></a>提供围栏标识符


Microsoft DirectX graphics 内核子系统在调用显示微型端口驱动程序的 [**DxgkDdiPatch**](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_patch)和 [**DxgkDdiSubmitCommand**](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_submitcommand)函数的 **SubmissionFenceId** 成员中提供了 [**相同的防护标识符和 \_**](/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgkarg_patch) [**DXGKARG \_ SUBMITCOMMAND**](/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgkarg_submitcommand)结构。 根据图形硬件的实现方式，驱动程序只需使用传递给 *DxgkDdiPatch* 或 *DxgkDdiSubmitCommand* 函数之一的防护标识符，原因如下：

-   驱动程序使用传递给 *DxgkDdiPatch* 的防护标识符，将 DMA) 缓冲区写入 (DMA 的直接内存访问结束。

-   驱动程序使用传递给 *DxgkDdiSubmitCommand* 的防护标识符来写入环形缓冲区，该缓冲区是 DMA 缓冲区排队等待执行的缓冲区，其中 dma 缓冲区由图形处理单元排队等候执行， (gpu)  (大多数 gpu 类型使用 DMA 缓冲区队列模型) 。

 

