---
title: 不是由 RDBSS 使用的例程
description: 不是由 RDBSS 使用的例程
ms.assetid: bf3e2936-05c9-4012-a55b-40022844f5db
keywords:
- 最小-重定向程序 WDK RDBSS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 114552f3848f9da5b0b440436681dcd58e6f9356
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67371931"
---
# <a name="routines-not-used-by-rdbss"></a>不是由 RDBSS 使用的例程


数量的例程中 MINIRDR 列出\_未调用或使用 RDBSS 调度结构。 不需要为网络微型-重定向程序以实现任何这些例程的因为它们将永远不会调用。 应设置网络微型重定向**NULL** MINIRDR 中的所有这些例程的指针\_调度结构传递给[ **RxRegisterMinirdr** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nf-mrx-rxregisterminirdr)从其[ **DriverEntry** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_initialize)例程。

下面是不由 RDBSS 的例程的完整列表：

-   **MRxCancel**

-   **MRxCancelCreateSrvCall**

-   **MRxClosedFcbTimeOut**

-   **MRxClosedSrvOpenTimeOut**

-   **MRxClosePrintFile**

-   **MRxEnumeratePrintQueue**

-   **MRxLowIOSubmit\[LOWIO\_OP\_CLEAROUT\]**

-   **MRxOpenPrintFile**

-   **MRxUpdateNetRootState**

-   **MRxWritePrintFile**

 

 




