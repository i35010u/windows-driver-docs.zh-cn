---
title: 不是由 RDBSS 使用的例程
description: 不是由 RDBSS 使用的例程
keywords:
- 小型重定向程序 WDK，RDBSS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cfb4eb39769515611d51241208f9f617e7f42930
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96839545"
---
# <a name="routines-not-used-by-rdbss"></a>不是由 RDBSS 使用的例程


MINIRDR 调度结构中列出的许多例程 \_ 不会被调用或由 RDBSS 使用。 网络小型重定向程序无需实现其中的任何例程，因为它们永远不会被调用。 网络小型重定向程序应为 MINIRDR **NULL** \_ 调度结构中从其 [**DriverEntry**](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)例程传入 [**RxRegisterMinirdr**](/windows-hardware/drivers/ddi/mrx/nf-mrx-rxregisterminirdr)的所有例程设置一个 NULL 指针。

下面是 RDBSS 未使用的例程的完整列表：

-   **MRxCancel**

-   **MRxCancelCreateSrvCall**

-   **MRxClosedFcbTimeOut**

-   **MRxClosedSrvOpenTimeOut**

-   **MRxClosePrintFile**

-   **MRxEnumeratePrintQueue**

-   **MRxLowIOSubmit \[ LOWIO \_ OP \_ CLEAROUT\]**

-   **MRxOpenPrintFile**

-   **MRxUpdateNetRootState**

-   **MRxWritePrintFile**

 

