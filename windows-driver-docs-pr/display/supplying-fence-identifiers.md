---
title: 提供围栏标识符
description: 提供围栏标识符
ms.assetid: 0ec8a4eb-c441-47ae-b5de-d86e6065ffd4
keywords:
- 围栏标识符 WDK 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 66e618d1a263af6ca22683625ea1fe4662d77fe8
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72829416"
---
# <a name="supplying-fence-identifiers"></a>提供围栏标识符


Microsoft DirectX graphics 内核子系统在[**DXGKARG\_PATCH**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgkarg_patch)和[**DXGKARG\_SUBMITCOMMAND**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgkarg_submitcommand)结构的**SubmissionFenceId**成员中提供了一个相同的防护标识符，以便调用显示微型端口驱动程序的[**DxgkDdiPatch**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_patch)和[**DxgkDdiSubmitCommand**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_submitcommand)函数。 根据图形硬件的实现方式，驱动程序只需使用传递给*DxgkDdiPatch*或*DxgkDdiSubmitCommand*函数之一的防护标识符，原因如下：

-   驱动程序使用传递给*DxgkDdiPatch*的隔离标识符来写入直接内存访问（DMA）缓冲区的末尾。

-   驱动程序使用传递给*DxgkDdiSubmitCommand*的防护标识符来写入环形缓冲区，该缓冲区是 DMA 缓冲区排队等候以供图形处理单元（gpu）执行（大多数 GPU 类型使用 DMA 缓冲区队列模型）的缓冲区。

 

 





