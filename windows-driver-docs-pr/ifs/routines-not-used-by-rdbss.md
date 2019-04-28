---
title: 不是由 RDBSS 使用的例程
description: 不是由 RDBSS 使用的例程
ms.assetid: bf3e2936-05c9-4012-a55b-40022844f5db
keywords:
- 最小-重定向程序 WDK RDBSS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ccdc6dc02d32e4916320c15136b250dcfa4009e9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63344524"
---
# <a name="routines-not-used-by-rdbss"></a>不是由 RDBSS 使用的例程


数量的例程中 MINIRDR 列出\_未调用或使用 RDBSS 调度结构。 不需要为网络微型-重定向程序以实现任何这些例程的因为它们将永远不会调用。 应设置网络微型重定向**NULL** MINIRDR 中的所有这些例程的指针\_调度结构传递给[ **RxRegisterMinirdr** ](https://msdn.microsoft.com/library/windows/hardware/ff554693)从其[ **DriverEntry** ](https://msdn.microsoft.com/library/windows/hardware/ff544113)例程。

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

 

 




