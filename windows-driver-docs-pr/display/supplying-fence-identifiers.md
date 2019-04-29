---
title: 提供围栏标识符
description: 提供围栏标识符
ms.assetid: 0ec8a4eb-c441-47ae-b5de-d86e6065ffd4
keywords:
- fence 标识符 WDK 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 715ace0caaad49ceca450485fc5f40819fcabe3a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63375948"
---
# <a name="supplying-fence-identifiers"></a>提供围栏标识符


Microsoft DirectX 图形内核子系统提供中的相同 fence 标识符**SubmissionFenceId**的成员[ **DXGKARG\_修补**](https://msdn.microsoft.com/library/windows/hardware/ff557610)并[ **DXGKARG\_SUBMITCOMMAND** ](https://msdn.microsoft.com/library/windows/hardware/ff559490)显示微型端口驱动程序的调用中的结构[ **DxgkDdiPatch**](https://msdn.microsoft.com/library/windows/hardware/ff559737)并[ **DxgkDdiSubmitCommand** ](https://msdn.microsoft.com/library/windows/hardware/ff560790)函数。 具体取决于图形硬件的实现方式，驱动程序仅使用需要传递到其中任何一个的 fence 标识符*DxgkDdiPatch*或*DxgkDdiSubmitCommand*函数由于以下原因：

-   驱动程序使用传递给 fence 标识符*DxgkDdiPatch*将写入直接内存访问 (DMA) 缓冲区的末尾。

-   驱动程序使用传递给 fence 标识符*DxgkDdiSubmitCommand*将环形缓冲区，即其中 DMA 缓冲区将排队等待执行的图形处理单元 (GPU) （大多数 GPU 类型使用 DMA 缓冲区的缓冲区写入队列的模型）。

 

 





