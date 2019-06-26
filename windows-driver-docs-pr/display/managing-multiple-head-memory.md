---
title: 管理多头内存
description: 管理多头内存
ms.assetid: 37cda124-0c3b-4af4-92b8-329440dd3221
keywords:
- 多个头硬件 WDK DirectX 9.0 中，内存管理
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e2e661604f114cd062731329072f1e720cac96c9
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67383438"
---
# <a name="managing-multiple-head-memory"></a>管理多头内存


## <span id="ddk_managing_multiple_head_memory_gg"></span><span id="DDK_MANAGING_MULTIPLE_HEAD_MEMORY_GG"></span>


设置 DDSCAPS2\_ADDITIONALPRIMARY 功能位**dwCaps2**的成员[ **DDSCAPS2** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff550292(v=vs.85))的每个表面上从属结构head 通知这些图面是从分配给该头的视频内存分配的最后一个曲面该头。 从属头然后应释放控件到主头其视频内存的分配，因为从属头保证它不会接收后续[ *DdCreateSurface* ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff549263(v=vs.85))调用的应用程序生存期内。

该驱动程序必须确保 master 头能够分配与从属头相关联的内存。

当运行时调用的驱动程序[ *DdDestroySurface* ](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_surfcb_destroysurface)函数来销毁从属头中的图面 DDSCAPS2\_ADDITIONALPRIMARY 功能设置位，则该驱动程序通知从属头将再次其视频内存管理的控件。

大多数情况下，所选择的哪头拥有的视频内存是固有现有 DirectDraw 进程中。 特别是：

-   运行时可保证任何后续分配请求都是在从属后的 heads *DdCreateSurface*调用都是使用 DDSCAPS2\_ADDITIONALPRIMARY 位。 因此，该驱动程序不需要在任何时间限制从其自己的视频内存池分配。

-   当应用程序是终止或最小化时，所有表面会被都销毁。 因此，所创建的主头从属头池中的所有纹理进行都清理。

-   如果 DDSCAPS2\_ADDITIONALPRIMARY 位未设置对于图面上从属头，则这些头继续分配视频内存，就像独立的头。 实际上，这种从属头是功能上等同于多个监视器的任何其他适配器。

-   该驱动程序时需要提供的主头从从属 head 的池，其中包括有关何时从从属 head 的池分配特定资源确定分配内存的实现。 请注意，master 头没有任何相关信息本身是否参与多个头方案中。 在主头用尽了其自己的视频内存，它必须遍历中其组，以确定是否所有这些头具有可以由主机使用的应用程序池的所有从属头 (即，以确定任何从属头是否收到*DdCreateSurface* DDSCAPS2 调用\_ADDITIONALPRIMARY 位集)。

-   最后，请注意，在运行时可保证在组中的所有头都参与多个头方案。 因此，该驱动程序必须保持的状态，指示其是否当前在多个头模式下的一位。

 

 





